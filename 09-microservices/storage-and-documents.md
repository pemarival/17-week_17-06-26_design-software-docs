# Almacenamiento y gestión de documentos

> Estado: 🟡 En progreso
> Última actualización: 2026-06-22
> Autor: Por definir
> Equipo: Por definir

---

## Estrategia de almacenamiento

### Database per Service

Cada servicio tiene su propia base de datos independiente:

| Servicio                     | BD            | Motor                    | Propósito                             |
| ---------------------------- | ------------- | ------------------------ | ------------------------------------- |
| iam-service                  | iam_db        | PostgreSQL               | Usuarios, roles, sesiones             |
| reference-data-service       | ref_db        | PostgreSQL               | Centros, regiones, parámetros         |
| academic-management-service  | academic_db   | PostgreSQL               | Programas, competencias, RAPs, fichas |
| training-environment-service | env_db        | PostgreSQL               | Ambientes, inventario, disponibilidad |
| scheduling-service           | scheduling_db | PostgreSQL               | Horarios, sesiones, conflictos        |
| actors-service               | actors_db     | PostgreSQL               | Instructores, aprendices, empresas    |
| document-service             | document_db   | PostgreSQL               | Documentos, plantillas, versiones     |
| monitoring-service           | monitoring_db | PostgreSQL               | KPIs, alertas, métricas históricas    |
| audit-service                | audit_db      | PostgreSQL (append-only) | Auditoría inmutable                   |

---

## Replicación de datos

Cuando un servicio necesita datos de otro:

### Opción 1: Consulta síncrona (REST o gRPC)

* Uso: Validaciones en tiempo real
* Ejemplo: scheduling valida instructor disponible en actors-service

### Opción 2: Replicación eventual (mediante eventos)

* Uso: Datos frecuentemente consultados
* Ejemplo: scheduling replica lista de RAPs activos desde academic-management
* Garantía: Consistencia eventual (< 5 segundos)

### Opción 3: Caché compartido (Redis)

* Uso: Datos de referencia que cambian poco
* Ejemplo: centros, parámetros
* TTL: 24 horas

---

## Documentos y archivos

### Estructura en Cloud Storage

```text
cloud-storage/
├── certificados/
│   ├── {fichaId}/{aprendizId}/
│   │   ├── {ano}-{mes}-{dia}_certificado.pdf
│   │   └── {ano}-{mes}-{dia}_certificado_v2.pdf
│
├── diplomas/
│   ├── {fichaId}/{aprendizId}/
│   │   └── {ano}-{mes}-{dia}_diploma.pdf
│
├── reportes/
│   ├── {ano}/
│   │   ├── {mes}/
│   │   │   ├── reporte_ocupacion_{dia}.pdf
│   │   │   └── reporte_kpi_{dia}.xlsx
│
├── plantillas/
│   ├── certificado_base.docx
│   ├── diploma_base.docx
│   └── reporte_horarios_base.docx
│
└── temporales/
    ├── {sessionId}/
    │   └── archivos_generacion
```

*(Los archivos temporales se eliminan automáticamente después de 24 horas.)*

---

## Servicio de documentos

`document-service` gestiona:

* Generación de PDFs a partir de plantillas
* Versionado de documentos
* Almacenamiento en cloud storage
* Ciclo de vida: borrador → generado → archivado
* Descarga y acceso controlado por permisos

---

## Plantillas

### Certificado

**Entrada**

* Ficha ID
* Aprendiz ID
* RAPs completados

**Salida**

* PDF con logo SENA
* Datos personales
* Competencias

**Variables**

* `{nombreAprendiz}`
* `{documentoAprendiz}`
* `{competencias}`
* `{fecha}`

---

### Diploma

**Entrada**

* Ficha ID
* Aprendiz ID

**Salida**

* PDF de egresado

**Variables**

* Similares al certificado

---

### Reporte de horarios

**Entrada**

* Ficha ID
* Rango de fechas

**Salida**

* PDF con tabla horarios × instructor × ambiente

---

### Reporte KPI

**Entrada**

* Centro ID
* Fecha

**Salida**

* XLSX con:

  * Ocupación
  * Carga instructores
  * Eficiencia

---

## Retención de datos

### Datos transaccionales

| Entidad              | Retención | Motivo             |
| -------------------- | --------- | ------------------ |
| Horarios completados | 7 años    | Legal              |
| Auditoría            | 7 años    | Legal              |
| Documentos generados | 3 años    | Consulta histórica |
| Sesiones de usuario  | 90 días   | Compliance         |
| Logs de aplicación   | 30 días   | Troubleshooting    |
| Alertas vistas       | 1 año     | Histórico          |

---

## Limpieza automática

Jobs programados:

* Diariamente (01:00): eliminar archivos temporales > 24h
* Semanalmente (domingo 02:00): archivar auditoría > 7 años
* Mensualmente (primer día 03:00): comprimir logs > 30 días

---

## Seguridad de datos

### Encriptación

* En tránsito: TLS 1.3 para REST, mTLS para gRPC
* En reposo: AES-256 para datos sensibles (documentos, auditoría)
* Llaves: rotación trimestral, gestión en Key Vault

### Backup

* Frecuencia: diaria para BDs transaccionales
* RPO: < 1 hora
* RTO: < 4 horas
* Retención:

  * 30 días en storage primario
  * 1 año en archivo
* Redundancia: multi-región (activa–pasiva)

### Compliance

* Cumplimiento SGPL (seguridad de la información)
* Cumplimiento normativa SENA sobre datos de aprendices
* Anonimización de PII en reportes analíticos

