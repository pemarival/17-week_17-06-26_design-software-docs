# Catálogo de servicios

> Estado: 🟡 En progreso | Última actualización: 2026-06-22
> Autor: Por definir | Equipo: Por definir

Registro centralizado de los 9 microservicios del sistema **Horarios SENA**. Alineados con módulos funcionales M1-M9.

## Servicios de dominio

| Servicio | BD | Descripción | Owner | Repo | Estado |
|----------|----|----|-------|------|--------|
| [iam-service](./services/01-iam-service/) | iam_db | Autenticación, autorización y sesiones de usuario | Por definir | — | 🔴 |
| [reference-data-service](./services/02-reference-data-service/) | ref_db | Estructura institucional: centros, regiones, catálogos y parámetros | Por definir | — | 🔴 |
| [academic-management-service](./services/03-academic-management-service/) | academic_db | Programas, competencias, RAPs y fichas de formación | Por definir | — | 🔴 |
| [training-environment-service](./services/04-training-environment-service/) | env_db | Ambientes, inventario, mantenimiento y disponibilidad | Por definir | — | 🔴 |
| [scheduling-service](./services/05-scheduling-service/) | scheduling_db | Motor de asignación, horarios, sesiones y detección de conflictos | Por definir | — | 🔴 |
| [actors-service](./services/06-actors-service/) | actors_db | Instructores, aprendices, empresas y etapa productiva | Por definir | — | 🔴 |
| [document-service](./services/07-document-service/) | document_db | Documentos, plantillas, generación de PDF y ciclo de vida | Por definir | — | 🔴 |
| [monitoring-service](./services/08-monitoring-service/) | monitoring_db | KPIs, alertas, notificaciones y seguimiento | Por definir | — | 🔴 |
| [audit-service](./services/09-audit-service/) | audit_db | Auditoría append-only: registro inmutable de operaciones | Por definir | — | 🔴 |

## Total

**9 servicios** — Base de datos independiente por servicio (Database per Service Pattern)

## Componentes desplegables

Cada servicio incluye componentes específicos según su responsabilidad:

### iam-service
- `iam-api` — API de autenticación y autorización

### reference-data-service
- `reference-data-api` — API de datos de referencia

### academic-management-service
- `academic-management-api` — API de gestión académica

### training-environment-service
- `training-environment-api` — API de ambientes de formación

### scheduling-service
- `schedules-api` — API REST de horarios
- `scheduling-engine-workflow` — Motor de asignación (procesamiento heavy)
- `conflict-validator-worker` — Validación de conflictos (async)

### actors-service
- `actors-api` — API de actores (instructores, aprendices, empresas)

### document-service
- `document-api` — API de documentos
- `template-api` — API de plantillas
- `pdf-renderer-worker` — Generación de PDF (async)
- `document-lifecycle-worker` — Gestión de ciclo de vida (async)

### monitoring-service
- `monitoring-api` — API de KPIs y alertas
- `alert-worker` — Generación de alertas (async)
- `notification-worker` — Envío de notificaciones (async)

### audit-service
- `audit-worker` — Registro de auditoría (append-only)

**Total: 17 componentes desplegables**

## Notas

1. Cada servicio tiene su propio repositorio de código (monorepo o polyrepo)
2. Las dependencias entre servicios se establecen mediante eventos asincrónicos (cuando sea posible)
3. Los datos de cada contexto de dominio están bajo la responsabilidad de su servicio
4. Ver [09-microservices/communication-patterns.md](./communication-patterns.md) para patrones de comunicación
5. Ver [09-microservices/service-boundary-rules.md](./service-boundary-rules.md) para límites de servicio
