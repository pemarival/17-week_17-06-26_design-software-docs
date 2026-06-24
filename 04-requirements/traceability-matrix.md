# Matriz de trazabilidad

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Requisitos

## Propósito

Mapear relaciones: Objetivos de negocio → Requisitos → Servicios → Decisiones arquitectónicas → Pruebas

---

## Objetivos de negocio → Requisitos

| Objetivo de negocio | Requisito funcional | Requisito no-funcional | HU |
|---|---|---|---|
| Reducir conflictos de asignación 100% | RF-SCHED-003 | RNF-PERF-002 | HU-003 |
| Mejorar ocupación ambientes +25% | RF-MON-001 | RNF-PERF-004 | HU-005 |
| Reducir carga administrativa -80% | RF-SCHED-001 | RNF-PERF-002 | HU-003 |
| Mejora satisfacción coordinadores +40% | RF-SCHED-001, RF-SCHED-004 | RNF-PERF-001 | HU-002, HU-003 |
| Implementar BD centralizada 100% | RF-ACAD-001, RF-ACT-001 | RNF-DATA-001 | HU-001, HU-008 |
| Implementar auditoría 100% | RF-AUD-001 | RNF-SEC-008 | HU-007 |

---

## Requisitos → Servicios

### Requisitos de IAM

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-IAM-001 | iam-service | iam-api | 🔴 |
| RF-IAM-002 | iam-service | iam-api | 🔴 |
| RF-IAM-003 | iam-service | iam-api | 🔴 |

### Requisitos de Academic Management

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-ACAD-001 | academic-management | academic-api | 🔴 |
| RF-ACAD-002 | academic-management | academic-api | 🔴 |
| RF-ACAD-003 | academic-management | academic-api | 🔴 |

### Requisitos de Environment

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-ENV-001 | training-environment | environment-api | 🔴 |
| RF-ENV-002 | training-environment | environment-api | 🔴 |
| RF-ENV-003 | training-environment | environment-api | 🔴 |

### Requisitos de Scheduling (CORE)

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-SCHED-001 | scheduling-service | scheduling-engine | 🔴 |
| RF-SCHED-002 | scheduling-service | schedules-api | 🔴 |
| RF-SCHED-003 | scheduling-service | conflict-validator | 🔴 |
| RF-SCHED-004 | scheduling-service | schedules-api | 🔴 |

### Requisitos de Actors

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-ACT-001 | actors-service | actors-api | 🔴 |
| RF-ACT-002 | actors-service | actors-api | 🔴 |
| RF-ACT-003 | actors-service | actors-api | 🔴 |

### Requisitos de Documents

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-DOC-001 | document-service | pdf-renderer-worker | 🔴 |
| RF-DOC-002 | document-service | pdf-renderer-worker | 🔴 |
| RF-DOC-003 | document-service | document-api | 🔴 |

### Requisitos de Monitoring

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-MON-001 | monitoring-service | monitoring-api | 🔴 |
| RF-MON-002 | monitoring-service | alert-worker | 🔴 |
| RF-MON-003 | monitoring-service | monitoring-api | 🔴 |

### Requisitos de Audit

| RF | Servicio | Componente | Status |
|---|---|---|---|
| RF-AUD-001 | audit-service | audit-worker | 🔴 |
| RF-AUD-002 | audit-service | audit-worker | 🔴 |

---

## Requisitos → Decisiones arquitectónicas

| RF | ADR | Decisión | Servicios afectados |
|---|---|---|---|
| RF-SCHED-001, RF-SCHED-002, RF-SCHED-003 | ADR-003 | Usar microservicios con BD independiente | scheduling, academic, actors, environment |
| RF-AUD-001 | ADR-004 | Audit append-only (nunca modificable) | audit-service |
| RF-MON-001 | ADR-005 | KPIs calculados diariamente en batch | monitoring-service |
| RF-SCHED-004, RF-ENV-002 | ADR-006 | Comunicación entre servicios vía eventos | scheduling, environment, notification |
| RF-IAM-001, RF-IAM-002, RF-IAM-003 | ADR-001 | JWT para autenticación | iam-service, todos los servicios |

---

## Requisitos no-funcionales → Pruebas

| RNF | Prueba | Métrica | Herramienta |
|---|---|---|---|
| RNF-PERF-001 | Load test REST API | p99 < 500ms | JMeter, k6 |
| RNF-PERF-002 | Throughput test | 100+ asignaciones/min | k6 |
| RNF-PERF-003 | Frontend performance | Lighthouse > 85 | Lighthouse CI |
| RNF-AVAIL-001 | Uptime monitoring | 99.9% | Application Insights |
| RNF-AVAIL-002 | Disaster recovery | RTO < 4h | Manual test |
| RNF-SEC-001 | Security test | Token válido | Postman, OWASP |
| RNF-SEC-005 | SQL injection test | No vulnerable | SQLi scanner |
| RNF-DATA-001 | Data retention | 7 años auditoria | Manual audit |

---

## Matriz de cobertura: RF → Pruebas

```
                UT  IT  API ST  E2E LoadTest
RF-SCHED-001   [X] [X] [X] [ ] [ ] [X]
RF-SCHED-002   [X] [X] [X] [X] [ ] [ ]
RF-SCHED-003   [X] [X] [X] [X] [ ] [ ]
RF-ACAD-001    [X] [X] [X] [ ] [ ] [ ]
RF-MON-001     [X] [X] [X] [ ] [X] [X]
RF-AUD-001     [X] [X] [X] [ ] [X] [ ]
RF-DOC-001     [X] [X] [X] [X] [ ] [ ]

Leyenda:
UT   = Unit Tests (tests unitarios)
IT   = Integration Tests (tests de integración)
API  = API Tests (Postman, REST)
ST   = System Tests (tests de sistema)
E2E  = End-to-End Tests (Selenium, Cypress)
LoadTest = Pruebas de carga
```

---

## Historial de cambios

| Fecha | Cambio | Motivo | Versión |
|---|---|---|---|
| 2026-06-24 | Inicial | Creación de matriz | 1.0 |

---

## Referencias cruzadas

- **Objetivos negocio:** [03-product/vision.md](../03-product/vision.md)
- **Requisitos funcionales:** [04-requirements/functional.md](./functional.md)
- **Requisitos no-funcionales:** [04-requirements/non-functional.md](./non-functional.md)
- **Historias de usuario:** [04-requirements/user-stories.md](./user-stories.md)
- **Servicios:** [09-microservices/service-catalog.md](../09-microservices/service-catalog.md)
- **ADRs:** [05-architecture/decisions/README.md](../05-architecture/decisions/README.md)
- **Testing strategy:** [11-quality/testing-strategy.md](../11-quality/testing-strategy.md)
