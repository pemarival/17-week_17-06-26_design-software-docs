# Requisitos funcionales

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Requisitos

## Estructura

Requisitos agrupados por contexto de dominio, mapeados a servicios microservicios.

---

## 1. Contexto: Identity & Access Management (IAM)

### RF-IAM-001: Autenticación con correo
- **Descripción:** Usuario ingresa correo y contraseña para acceder
- **Actor:** Director, Coordinador, Instructor, Aprendiz
- **Flujo:**
  1. Usuario ingresa correo
  2. Usuario ingresa contraseña
  3. Sistema valida credenciales
  4. Si correctas, emite JWT token
  5. Si incorrectas, muestra error
- **Restricciones:** Intento 5 fallos = bloqueo 15 minutos
- **Servicio:** iam-service

### RF-IAM-002: Control de roles
- **Descripción:** Sistema asigna permisos según rol del usuario
- **Roles:**
  - DIRECTOR: ver todo, crear alertas
  - COORDINADOR: crear fichas, asignar horarios
  - INSTRUCTOR: ver mis horarios, ver mis sesiones
  - APRENDIZ: ver mi ficha, descargar certificados
- **Servicio:** iam-service

### RF-IAM-003: Cierre de sesión
- **Descripción:** Usuario puede cerrar sesión y token expira
- **Flujo:** Click en "Cerrar sesión" → Token invalidado → Redirige a login
- **Servicio:** iam-service

---

## 2. Contexto: Academic Management

### RF-ACAD-001: Crear ficha de formación
- **Descripción:** Coordinador crea nueva ficha (agrupación de aprendices + instructor + ambientes)
- **Actor:** Coordinador
- **Entrada:** Programa, Centro, Jornada, Coordinador
- **Flujo:**
  1. Coordinador accede a "Crear ficha"
  2. Selecciona programa (ej: ADSO)
  3. Selecciona centro
  4. Selecciona jornada (mañana/tarde/noche)
  5. Sistema asigna ID ficha
  6. Guarda en BD
  7. Publica evento "FichaCreada"
- **Salida:** Ficha ID, estado PLANEACION
- **Servicio:** academic-management-service

### RF-ACAD-002: Listar competencias del programa
- **Descripción:** Ver todas las competencias que debe cubrir un programa
- **Entrada:** Programa ID
- **Salida:** Lista de competencias con RAPs
- **Servicio:** academic-management-service

### RF-ACAD-003: Registrar RAP (Resultado de Aprendizaje)
- **Descripción:** Arquitecto registra nuevos RAPs en competencia
- **Actor:** Administrador
- **Entrada:** Competencia ID, nombre RAP, criterios
- **Servicio:** academic-management-service

---

## 3. Contexto: Training Environment (Ambientes)

### RF-ENV-001: Crear ambiente
- **Descripción:** Administrador registra nuevo ambiente (aula, laboratorio, taller)
- **Actor:** Administrador
- **Entrada:** Nombre, Centro, Capacidad, Tipo (aula/lab/taller), Recursos
- **Flujo:**
  1. Accede a "Crear ambiente"
  2. Ingresa datos
  3. Sistema valida capacidad > 0
  4. Guarda en BD
  5. Disponible para asignaciones
- **Servicio:** training-environment-service

### RF-ENV-002: Marcar ambiente no disponible
- **Descripción:** Administrador marca ambiente en mantenimiento
- **Actor:** Administrador
- **Entrada:** Ambiente ID, Fecha inicio, Fecha fin, Razón
- **Flujo:**
  1. Sistema crea registro de no disponibilidad
  2. Publica evento "AmbienteNoDisponible"
  3. Motor de scheduling invalida horarios solapados
- **Servicio:** training-environment-service

### RF-ENV-003: Consultar disponibilidad de ambiente
- **Descripción:** Ver calendario de ocupación de ambiente
- **Entrada:** Ambiente ID, Fecha inicio, Fecha fin
- **Salida:** Tabla horario x ocupación (ocupado/disponible)
- **Servicio:** training-environment-service

---

## 4. Contexto: Scheduling (CORE - Motor de asignación)

### RF-SCHED-001: Ejecutar motor de asignación
- **Descripción:** Sistema sugiere horarios automáticamente para una ficha
- **Actor:** Coordinador
- **Entrada:** Ficha ID, Opción: "Autoasignar"
- **Flujo:**
  1. Sistema obtiene:
     - Competencias/RAPs de ficha
     - Instructores con esas competencias
     - Ambientes disponibles
     - Restricciones de tiempo
  2. Ejecuta algoritmo de optimización
  3. Genera matriz de sugerencias
  4. Valida contra 8 reglas (sin solapamiento, capacidad, competencia, etc.)
  5. Devuelve horarios sin conflictos O conflictos detectados
- **Salida:** Lista de horarios sugeridos OR lista de conflictos
- **Servicio:** scheduling-service

### RF-SCHED-002: Guardar horario
- **Descripción:** Coordinador aprueba y guarda horario asignado
- **Actor:** Coordinador
- **Entrada:** Ficha ID, Instructor ID, Ambiente ID, Franja horaria
- **Validaciones:**
  - Instructor no ocupado en esa franja
  - Ambiente no ocupado en esa franja
  - Instructor tiene competencia requerida
  - Ambiente tiene capacidad suficiente
  - Ambiente disponible (no en mantenimiento)
- **Resultado:** Horario guardado, evento publicado, notificaciones enviadas
- **Servicio:** scheduling-service

### RF-SCHED-003: Detectar conflictos
- **Descripción:** Sistema identifica solapamientos o violaciones de reglas
- **Tipo conflicto:**
  - Instructor asignado a 2 fichas simultáneamente
  - Ambiente asignado a 2 sesiones simultáneamente
  - Capacidad ambiente excedida
  - Instructor sin competencia requerida
- **Resultado:** Crea registro Conflicto, notifica director
- **Servicio:** scheduling-service

### RF-SCHED-004: Cancelar horario
- **Descripción:** Coordinador puede eliminar un horario existente
- **Actor:** Coordinador, Director
- **Entrada:** Horario ID, Razón (opcional)
- **Flujo:**
  1. Valida que coordinador tenga permiso
  2. Marca horario como CANCELADO
  3. Publica evento "HorarioCancelado"
  4. Notifica instructor, coordinador, director
  5. Registra en auditoría
- **Servicio:** scheduling-service

---

## 5. Contexto: Actors (Instructores, Aprendices, Empresas)

### RF-ACT-001: Registrar instructor
- **Descripción:** Administrador crea registro de instructor
- **Actor:** Administrador
- **Entrada:** Nombre, Documento, Centro, Especialidades (competencias)
- **Flujo:**
  1. Crea usuario en IAM
  2. Asigna rol INSTRUCTOR
  3. Crea registro en actors-service
  4. Vincula competencias
  5. Disponible para asignaciones
- **Servicio:** actors-service

### RF-ACT-002: Registrar aprendiz
- **Descripción:** Administrador inscribe aprendiz en ficha
- **Actor:** Administrador
- **Entrada:** Nombre, Documento, Ficha ID
- **Flujo:**
  1. Crea usuario en IAM (opcional)
  2. Asigna rol APRENDIZ
  3. Crea registro en actors-service
  4. Vincula a ficha
  5. Publica evento "AprendizAsignado"
- **Servicio:** actors-service

### RF-ACT-003: Consultar disponibilidad de instructor
- **Descripción:** Ver calendario de ocupación de instructor
- **Entrada:** Instructor ID, Fecha inicio, Fecha fin
- **Salida:** Horas disponibles, horas ocupadas, carga total (h/semana)
- **Servicio:** actors-service

---

## 6. Contexto: Documents (Documentos y Plantillas)

### RF-DOC-001: Generar certificado
- **Descripción:** Sistema genera PDF certificado para aprendiz
- **Disparador:** Ficha finalizada
- **Entrada:** Ficha ID, Aprendiz ID
- **Flujo:**
  1. Obtiene plantilla de certificado
  2. Obtiene datos: nombre aprendiz, RAPs completados, fecha
  3. Renderiza PDF con datos
  4. Almacena en cloud storage
  5. Publica evento "DocumentoGenerado"
  6. Notifica aprendiz
- **Salida:** PDF descargable
- **Servicio:** document-service

### RF-DOC-002: Generar reporte de horarios
- **Descripción:** Exportar horarios de ficha como PDF
- **Actor:** Coordinador, Director
- **Entrada:** Ficha ID
- **Salida:** PDF con tabla de horarios (instructor, ambiente, franja horaria)
- **Servicio:** document-service

### RF-DOC-003: Descargar documento
- **Descripción:** Usuario descarga PDF de documento generado
- **Actor:** Aprendiz, Coordinador, Director
- **Entrada:** Documento ID
- **Flujo:**
  1. Valida permisos (propietario del documento o admin)
  2. Obtiene URL del cloud storage
  3. Envía archivo al cliente
  4. Publica evento "DocumentoDescargado"
- **Servicio:** document-service

---

## 7. Contexto: Monitoring (KPIs, Alertas, Notificaciones)

### RF-MON-001: Calcular KPIs
- **Descripción:** Sistema calcula métricas de eficiencia diariamente
- **KPIs:**
  - Ocupación de ambiente (% horas ocupadas / disponibles)
  - Carga de instructor (horas/semana)
  - Eficiencia de centro (promedio ocupación)
- **Frecuencia:** Diariamente a las 23:59
- **Flujo:**
  1. Obtiene horarios del día
  2. Calcula métricas
  3. Guarda en BD
  4. Compara con umbrales
  5. Si sobrepasa, publica evento "AlertaGenerada"
- **Servicio:** monitoring-service

### RF-MON-002: Generar alerta por sobrecarga
- **Descripción:** Sistema notifica si instructor está sobrecargado
- **Criterio:** Carga > 30 horas/semana
- **Destinatario:** Director, Coordinador, Instructor
- **Flujo:**
  1. Monitoring detecta umbral cruzado
  2. Publica evento "AlertaGenerada"
  3. notification-worker envía email
- **Servicio:** monitoring-service

### RF-MON-003: Ver dashboard de KPIs
- **Descripción:** Director ve gráficos de KPIs del centro
- **Actor:** Director
- **Entrada:** Centro ID
- **Salida:** 5+ gráficos (ocupación, carga, eficiencia, alertas, tendencias)
- **Actualización:** Cada 1 hora
- **Servicio:** monitoring-service

---

## 8. Contexto: Audit (Auditoría)

### RF-AUD-001: Registrar operación
- **Descripción:** Sistema registra toda operación en log append-only
- **Disparador:** Cualquier cambio en otros contextos
- **Registro contiene:**
  - Timestamp
  - Usuario ID
  - Acción (CREATE, UPDATE, DELETE)
  - Entidad afectada
  - Datos antes/después
  - IP, User-Agent
- **Propiedad:** Append-only, nunca modificable
- **Servicio:** audit-service

### RF-AUD-002: Consultar auditoría
- **Descripción:** Ver log de operaciones filtrado
- **Actor:** Director, Auditor
- **Filtros:** Usuario, Rango de fechas, Tipo de acción, Entidad
- **Salida:** Tabla de eventos registrados
- **Servicio:** audit-service

---

## Mapeo a servicios

| Contexto | Servicio | RFs |
|----------|----------|-----|
| IAM | iam-service | RF-IAM-001 a 003 |
| Academic | academic-management-service | RF-ACAD-001 a 003 |
| Environment | training-environment-service | RF-ENV-001 a 003 |
| **Scheduling (CORE)** | **scheduling-service** | **RF-SCHED-001 a 004** |
| Actors | actors-service | RF-ACT-001 a 003 |
| Documents | document-service | RF-DOC-001 a 003 |
| Monitoring | monitoring-service | RF-MON-001 a 003 |
| Audit | audit-service | RF-AUD-001 a 002 |

**Total: 26 requisitos funcionales**

---

## Referencias

- [03-product/product-backlog.md](../03-product/product-backlog.md) — 50 RFs en backlog
- [02-domain/domain-map.md](../02-domain/domain-map.md) — 9 contextos de dominio
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — 9 servicios
