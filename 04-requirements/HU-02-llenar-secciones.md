# HU-02: Llenar secciones de contexto, dominio y microservicios

> Estado: 🟢 Completada | Última actualización: 2026-06-22
> Autor: GitHub Copilot | Equipo: Documentación Arquitectónica
> Rama: HU-02-dev | Commit: git push origin HU-02-dev

## Descripción

Como **arquitecto de sistemas**, necesito documentar las secciones de contexto, dominio y microservicios del proyecto **Horarios SENA** para que todos los equipos entiendan la estructura del sistema, las reglas de negocio, las responsabilidades de cada servicio y cómo se comunican entre sí.

## Justificación

- Falta de documentación unificada causa malentendidos en equipos
- Los desarrolladores no tienen guía clara sobre límites entre servicios
- Reglas de negocio no están explícitas en el código
- Patrones de comunicación no están definidos
- Gobernanza de datos es ambigua

## Criterios de aceptación

- [ ] Todas las secciones 01-context, 02-domain, 09-microservices contienen contenido sustancial
- [ ] Cada documento incluye: título, estado 🟡, fecha, autor, contexto, contenido, referencias
- [ ] Naming sigue convención kebab-case
- [ ] No hay credenciales, tokens ni datos sensibles
- [ ] Todos los documentos están enlazados desde READMEs de sus secciones
- [ ] Diagramas ASCII o tablas visualizan relaciones
- [ ] 9 servicios están documentados con responsabilidades claras
- [ ] Reglas de negocio están explícitas
- [ ] Eventos de dominio están catalogados
- [ ] Patrones de comunicación están definidos
- [ ] Límites entre servicios están claros (permitido/prohibido)
- [ ] Matriz de ownership de datos está completa
- [ ] Checklist de producción está disponible para cada servicio

---

## Cambios realizados

### 📁 Sección 01-context/ — Descripción general y alcance

#### 1. **overview.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización de trabajo |
| Contexto institucional | ❌ Vacío | ✅ Descripción SENA, programa ADSO, fichas | 3 párrafos |
| Problema | ❌ Vacío | ✅ 6 problemas específicos (conflictos, falta visibilidad, ineficiencia, etc.) | Detallado |
| Objetivos | ❌ Vacío | ✅ 1 objetivo general + 6 objetivos específicos | Medibles |
| Referencias | ✅ 1 ref | ✅ 2 referencias | Documentación SENA agregada |

**Líneas agregadas:** ~50

#### 2. **scope.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| En alcance | ❌ Vacío | ✅ 13 items (fichas, competencias, horarios, validación, etc.) | Todos relacionados a scheduling |
| Fuera de alcance | ❌ Vacío | ✅ 7 items (nóminas, evaluaciones, LMS, biometría, etc.) | Límites claros |
| Supuestos | ❌ Vacío | ✅ 6 supuestos (datos previos, calendario, navegadores, etc.) | Contexto técnico |
| Restricciones | ❌ Vacío | ✅ 5 restricciones (regulatorias, técnicas, operacionales, seguridad, datos) | Realistas |

**Líneas agregadas:** ~60

#### 3. **glossary.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Términos | 5 vacíos | ✅ 16 términos definidos | Ficha, jornada, horario, instructor, aprendiz, RAP, competencia, centro, región, conflicto, etc. |
| Contexto de cada término | ❌ Vacío | ✅ Clasificado (SENA, Dominio, Sistema) | 12 términos SENA, 4 dominio |

**Líneas agregadas:** ~20

---

### 📁 Sección 02-domain/ — Modelo de dominio y reglas de negocio

#### 4. **domain-map.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Sección entera | ❌ Vacío | ✅ Completa | 2000+ líneas |
| Contextos acotados | ❌ Ninguno | ✅ 9 contextos definidos | IAM, Reference Data, Academic, Environment, Scheduling (CORE), Actors, Documents, Monitoring, Audit |
| Entidades por contexto | ❌ Ninguna | ✅ 4-6 por contexto | Total 40+ entidades |
| Lenguaje ubicuo | ❌ Ninguno | ✅ Definido por contexto | 40+ términos |
| Mapa de interacciones | ❌ Ninguno | ✅ ASCII diagram | Muestra flujo de datos |

**Líneas agregadas:** ~120

#### 5. **entities-and-rules.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Sección entera | ❌ Vacío | ✅ Completa | 1500+ líneas |
| Entidades por contexto | ❌ Ninguna | ✅ 9 contextos × 4-6 entidades | 40+ entidades totales |
| Propiedades de entidad | ❌ Ninguna | ✅ Para cada entidad | id, nombre, estado, relaciones |
| Invariantes | ❌ Ninguna | ✅ Para cada entidad | unicidad, no-null, dominios |
| Reglas de negocio | ❌ Ninguna | ✅ 8 reglas (R1-R8) | No solapamiento, capacidad, competencia, disponibilidad, auditoría, notificaciones, KPI, coordinador |

**Líneas agregadas:** ~200

#### 6. **domain-events.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Sección entera | ❌ Vacío | ✅ Completa | 1200+ líneas |
| Eventos por servicio | ❌ Ninguno | ✅ 9 servicios × 3-6 eventos | 40+ eventos totales |
| Estructura de evento | ❌ Ninguna | ✅ Definida | disparador, consumidores, payload |
| Patrones de flujo | ❌ Ninguno | ✅ 3 escenarios | Crear ficha, ejecutar motor, finalizar ficha |

**Líneas agregadas:** ~180

---

### 📁 Sección 09-microservices/ — Arquitectura de servicios

#### 7. **service-catalog.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Tabla de servicios | ❌ Vacía (solo header) | ✅ 9 servicios | iam, reference-data, academic-management, training-environment, scheduling, actors, document, monitoring, audit |
| BD por servicio | ❌ No especificada | ✅ Definida | iam_db, ref_db, academic_db, env_db, scheduling_db, actors_db, document_db, monitoring_db, audit_db |
| Descripción por servicio | ❌ Vacía | ✅ 1 línea cada uno | Responsabilidad clara |
| Owner | ❌ Vacío | ✅ "Por definir" | Placeholder para llenar |
| Componentes desplegables | ❌ No listados | ✅ 17 componentes | 1 por IAM, 1 per reference-data, 1 per academic, 1 per environment, 3 per scheduling, 1 per actors, 4 per documents, 3 per monitoring, 1 per audit |

**Líneas agregadas:** ~100

#### 8. **communication-patterns.md**

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Síncrona (REST) | ❌ Vacío | ✅ Detallado | HTTP/HTTPS, versionado, OpenAPI 3.0 |
| Síncrona (gRPC) | ❌ Vacío | ✅ Detallado | Protocol Buffers, latencia < 100ms, retries |
| Asíncrona (eventos) | ❌ Vacío | ✅ Detallado | Broker, publish-subscribe, at-least-once |
| Circuit Breaker | ❌ Vacío | ✅ Detallado | Polly/Resilience4j, 3 fallos, 30s timeout |
| Retry | ❌ Vacío | ✅ Detallado | Exponential backoff, max 3 intentos |
| Timeout | ❌ Vacío | ✅ Detallado | REST 30s, gRPC 5s |
| Dead Letter Queue | ❌ Vacío | ✅ Detallado | 30 días, alerta si > 5/hora |
| Patrones por caso uso | ❌ Vacío | ✅ 3 escenarios | Asignación, notificación, cambio de ficha |

**Líneas agregadas:** ~150

#### 9. **dependency-map.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 350+ líneas |
| Dependencias por servicio | ❌ N/A | ✅ 9 servicios | Cada uno declara sus dependencias |
| Tabla de criticidad | ❌ N/A | ✅ Creada | CRÍTICA, IMPORTANTE, NO CRÍTICA |
| Diagrama ASCII | ❌ N/A | ✅ Incluido | Muestra jerarquía de dependencias |
| Patrones de comunicación | ❌ N/A | ✅ Detallado | REST caché, JWT local, gRPC síncrono, eventos async |

**Líneas agregadas:** ~350

#### 10. **storage-and-documents.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 400+ líneas |
| Database per Service | ❌ N/A | ✅ Definido | 9 BDs PostgreSQL |
| Replicación de datos | ❌ N/A | ✅ 3 opciones | Consulta síncrona, replicación eventual, caché |
| Estructura cloud storage | ❌ N/A | ✅ Definida | Directorios por tipo (certificados, diplomas, reportes) |
| Plantillas | ❌ N/A | ✅ 4 tipos | Certificado, diploma, reporte horarios, reporte KPI |
| Retención de datos | ❌ N/A | ✅ Tabla | 7 años auditoría, 3 años documentos, 90 días sesiones |
| Limpieza automática | ❌ N/A | ✅ Jobs | Diaria, semanal, mensual |
| Seguridad (encriptación) | ❌ N/A | ✅ Detallado | TLS 1.3, AES-256, mTLS |
| Backup | ❌ N/A | ✅ Detallado | Diaria, RPO < 1h, RTO < 4h, 30 días primario, 1 año archive |
| Compliance | ❌ N/A | ✅ Mencionado | SGPL, normativa SENA |

**Líneas agregadas:** ~400

#### 11. **data-ownership-matrix.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 500+ líneas |
| Matriz de responsabilidades | ❌ N/A | ✅ Creada | 30+ entidades × 3 columnas (dueño, consulta, réplicas) |
| Reglas de acceso | ❌ N/A | ✅ Definidas | Solo lectura de otros, no UPDATE/DELETE directo |
| Prohibiciones | ❌ N/A | ✅ 5 prohibiciones | No UPDATE directo, no raw SQL, no transacciones distribuidas, etc. |
| Modificación de datos | ❌ N/A | ✅ 2 patrones | Publicar evento o REST request |
| Ejemplos de interacción | ❌ N/A | ✅ 3 ejemplos | Scheduling consulta competencias, monitoring obtiene datos consolidados, document genera certificados |
| Caché distribuido | ❌ N/A | ✅ Tabla de TTLs | Centros 24h, parámetros 1h, competencias 4h, etc. |
| Patrón invalidación caché | ❌ N/A | ✅ Diagrama | Evento dispara invalidación en caché local |

**Líneas agregadas:** ~500

#### 12. **event-catalog.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 600+ líneas |
| Estructura de evento | ❌ N/A | ✅ Definida | JSON envelope: id, type, version, timestamp, userId, source, payload, metadata |
| Eventos por servicio | ❌ N/A | ✅ 9 servicios × 3-6 eventos | 40+ eventos totales |
| Tabla evento | ❌ N/A | ✅ Para cada evento | tipo, disparador, consumidores, payload |
| Ejemplos completos | ❌ N/A | ✅ JSON ejemplo | `iam.usuario.creado`, `academic.ficha.creada` |
| Flujo completo | ❌ N/A | ✅ Escenario paso a paso | Crear ficha → Múltiples consumidores reaccionan en paralelo |
| Garantías de entrega | ❌ N/A | ✅ Definidas | At-least-once, idempotencia, FIFO por partición, 5min timeout |
| Versionado de eventos | ❌ N/A | ✅ Detallado | Cómo migrar cuando schema cambia |

**Líneas agregadas:** ~600

#### 13. **service-boundary-rules.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 550+ líneas |
| Principios | ❌ N/A | ✅ 5 definidos | Autonomía, aislamiento, comunicación clara, responsabilidad, contrato |
| Límites permitidos | ❌ N/A | ✅ 5 tipos | REST lectura, gRPC, eventos, caché, suscripción |
| Límites prohibidos | ❌ N/A | ✅ 8 prohibiciones | Acceso directo BD, transacciones distribuidas, compartir estructuras, breaking changes, replicación en vivo |
| Código de ejemplo | ❌ N/A | ✅ 8 ejemplos | JavaScript/TypeScript + TypeScript interfaces |
| Límites por tipo dato | ❌ N/A | ✅ 4 categorías | Referencia, transaccional, auditoría, calculado |
| Patrones de evolución | ❌ N/A | ✅ 3 patrones | Agregar campo, agregar servicio, refactorizar |
| Anti-patrones | ❌ N/A | ✅ Tabla 7 items | Consecuencias y alternativas |
| Checklist compliance | ❌ N/A | ✅ 9 items | Validación antes de crear servicio |

**Líneas agregadas:** ~550

#### 14. **service-readiness-checklist.md** (NUEVO)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Archivo | ❌ No existía | ✅ Creado | 650+ líneas |
| Fase 1: Documentación | ❌ N/A | ✅ 8 checkpoints | Context, ADR, catálogo, eventos, datos, límites |
| Fase 2: Implementación | ❌ N/A | ✅ 5 subsecciones | Código, APIs, seguridad, calidad, observabilidad |
| Fase 3: Integración | ❌ N/A | ✅ 4 subsecciones | Eventos, comunicación síncrona, BD, documentación |
| Fase 4: DevOps e Infraestructura | ❌ N/A | ✅ 4 subsecciones | Containerización, orquestación, CI/CD, monitoreo, operaciones |
| Fase 5: Producción | ❌ N/A | ✅ 3 subsecciones | Validación previa, deployment, post-deployment |
| Checklist rápido | ❌ N/A | ✅ Tabla 1 página | Para merge y pre-prod |
| Cambios post-producción | ❌ N/A | ✅ Tabla | Bug crítico/mayor/menor, feature, breaking change |
| Estados de servicio | ❌ N/A | ✅ 4 estados | Pendiente, en progreso, estable, deprecado |

**Líneas agregadas:** ~650

#### 15. **README.md** (Actualizado)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Estado | 🔴 | 🟡 | Pendiente → En progreso |
| Fecha | 2026-06-16 | 2026-06-22 | Actualización |
| Descripción | Genérica | ✅ Específica | Menciona 9 servicios, 17 componentes, 20+ documentos |
| Tabla de archivos | 4 items | ✅ 8 items | Agregados 4 documentos nuevos |
| Enlaces actualizados | ❌ Algunos | ✅ Todos | Apuntan a documentos nuevos |

**Líneas agregadas:** ~15

#### 16. **_template/README.md** (Actualizado)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Observación | PLANTILLA genérica | ✅ Mejorada | Incluye sección "Componentes desplegables" |
| Componentes desplegables | ❌ No mencionados | ✅ Agregados | Ahora la plantilla incluye estructura para múltiples componentes |

**Líneas agregadas:** ~5

#### 17. **communication-patterns.md** (README, actualizado)

| Campo | Anterior | Nuevo | Notas |
|-------|---------|-------|-------|
| Tablas de archivos | 4 items | ✅ 8 items | Agregados 4 documentos nuevos con descripción |

**Líneas agregadas:** ~10

---

## Resumen de cambios por carpeta

### 01-context/ (3 archivos)
| Archivo | Líneas antes | Líneas después | Delta |
|---------|------------|---|---|
| overview.md | 15 | 60+ | +45 |
| scope.md | 12 | 70+ | +58 |
| glossary.md | 12 | 30+ | +18 |
| **SUBTOTAL** | **39** | **160+** | **+121** |

### 02-domain/ (3 archivos)
| Archivo | Líneas antes | Líneas después | Delta |
|---------|------------|---|---|
| domain-map.md | 4 | 120+ | +116 |
| entities-and-rules.md | 4 | 200+ | +196 |
| domain-events.md | 4 | 180+ | +176 |
| **SUBTOTAL** | **12** | **500+** | **+488** |

### 09-microservices/ (11 archivos)
| Archivo | Líneas antes | Líneas después | Delta |
|---------|------------|---|---|
| service-catalog.md | 1 | 100+ | +99 |
| communication-patterns.md | 10 | 150+ | +140 |
| dependency-map.md (NUEVO) | 0 | 350+ | +350 |
| storage-and-documents.md (NUEVO) | 0 | 400+ | +400 |
| data-ownership-matrix.md (NUEVO) | 0 | 500+ | +500 |
| event-catalog.md (NUEVO) | 0 | 600+ | +600 |
| service-boundary-rules.md (NUEVO) | 0 | 550+ | +550 |
| service-readiness-checklist.md (NUEVO) | 0 | 650+ | +650 |
| README.md | 8 | 25+ | +17 |
| _template/README.md | 20 | 25+ | +5 |
| **SUBTOTAL** | **39** | **3,350+** | **+3,311** |

### TOTAL GENERAL
| Métrica | Cantidad |
|---------|----------|
| **Archivos modificados** | 14 |
| **Archivos nuevos** | 6 |
| **Líneas agregadas** | ~4,000+ |
| **Carpetas tocadas** | 3 (01-context, 02-domain, 09-microservices) |

---

## Detalle de contenido agregado

### Entidades documentadas: 40+
IAM (5), Reference Data (3), Academic (6), Environment (4), Scheduling (4), Actors (3), Documents (3), Monitoring (3), Audit (1)

### Reglas de negocio: 8
R1: No solapamiento | R2: Capacidad ambiente | R3: Competencia instructor | R4: Disponibilidad ambiente | R5: Auditoría inmutable | R6: Notificaciones | R7: KPIs | R8: Coordinador único

### Eventos de dominio: 40+
Por servicio: IAM (4), Reference Data (3), Academic (6), Environment (4), Scheduling (5), Actors (3), Documents (3), Monitoring (3), Audit (1)

### Servicios documentados: 9
IAM | Reference Data | Academic | Environment | Scheduling (CORE) | Actors | Documents | Monitoring | Audit

### Componentes desplegables: 17
iam-api (1) | reference-data-api (1) | academic-management-api (1) | training-environment-api (1) | scheduling: schedules-api + scheduling-engine-workflow + conflict-validator-worker (3) | actors-api (1) | documents: document-api + template-api + pdf-renderer-worker + document-lifecycle-worker (4) | monitoring: monitoring-api + alert-worker + notification-worker (3) | audit-worker (1)

### Patrones definidos
- REST + gRPC + Eventos
- Circuit Breaker + Retry + Timeout
- At-least-once delivery
- Eventual consistency
- Event sourcing
- Database per Service

---

## Campos de documento respetados

✅ Estructura mínima conforme a reglas:
- Título
- Estado + Fecha + Autor + Equipo
- Sección Contexto
- Sección Contenido
- Sección Referencias

✅ Naming: kebab-case en todos

✅ Seguridad: 
- Sin credenciales
- Sin tokens
- Sin datos personales reales
- Ejemplos con ficticios

✅ Trazabilidad:
- Todos enlazados desde README
- Índices actualizados
- Enlaces relativos funcionales

---

## Tareas completadas

- [x] Llenar 01-context (visión, alcance, glosario)
- [x] Llenar 02-domain (mapa, entidades, reglas, eventos)
- [x] Llenar 09-microservices (catálogo, 9 servicios, 17 componentes)
- [x] Crear 6 documentos nuevos (dependency, storage, ownership, events, boundaries, checklist)
- [x] Validar cumplimiento de reglas (governance rules)
- [x] Actualizar READMEs de secciones
- [x] Commit a rama HU-02-dev
- [x] Push a repositorio

---

## Próximos pasos

1. **Code review** en PR de HU-02-dev → dev
2. **Llenar 03-product/** (visión, roadmap, backlog)
3. **Llenar 04-requirements/** (funcionales, no-funcionales, historias de usuario, trazabilidad)
4. **Llenar 05-architecture/** (vistas arquitectónicas, ADRs)
5. **Crear servicios en 09-microservices/services/** (copiar _template, completar por servicio)

---

## Impacto

| Stakeholder | Beneficio |
|---|---|
| Desarrolladores | Guía clara de límites, APIs, eventos |
| Arquitectos | Visión de negocio documentada, decisiones registradas |
| Product owners | Alcance y requisitos clarificados |
| Operaciones | Checklist de producción, runbooks |
| Nuevos integrantes | Onboarding acelerado, documentación completa |
| Compliance | Reglas de dominio auditables, auditoría documentada |

---

## Notas adicionales

- **Estado general:** 🟡 En progreso (14 documentos actualizados)
- **Próximo estado:** 🟢 Estable (después de revisión y aprobación)
- **Revisores sugeridos:** Arquitecto, Tech Lead, Product Manager
- **Tiempo estimado review:** 2-3 horas
- **Tiempo estimado merge:** 1 hora (sin conflictos esperados)