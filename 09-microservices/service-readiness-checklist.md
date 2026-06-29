# Checklist de preparación de servicios

> Estado: 🟡 En progreso
> Última actualización: 2026-06-22
> Autor: Por definir
> Equipo: Por definir

---

## Propósito

Verificación sistemática de que un microservicio está listo para:

1. Merge a rama `main` (código)
2. Deploy a producción (infraestructura, seguridad, operaciones)
3. Integración en sistema (APIs, eventos, datos)

---

# Fase 1: Documentación (Pre-desarrollo)

## Definición del servicio

* [ ] Bounded context definido (`domain-map.md`)
* [ ] Responsabilidad del servicio definida en una línea
* [ ] Dependencias mapeadas (`dependency-map.md`)
* [ ] ADR creada (`05-architecture/decisions/records/ADR-XXX-service-creation.md`)
* [ ] Servicio registrado en `service-catalog.md`
* [ ] Eventos documentados en `event-catalog.md`
* [ ] Datos mapeados en `data-ownership-matrix.md`
* [ ] Límites claros (`service-boundary-rules.md`)

---

# Fase 2: Implementación

## Código y arquitectura

* [ ] Estructura de carpetas sigue convención
* [ ] Componentes independientes (`api`, `worker`, etc.)
* [ ] BD propia creada
* [ ] Conexión usa pool
* [ ] Migraciones versionadas
* [ ] Modelos de dominio ↔ schema definidos

---

## APIs

* [ ] OpenAPI 3.0 (`07-api/contracts/openapi/`)
* [ ] Endpoints documentados
* [ ] Prefijo `/api/v1/`
* [ ] HTTP codes correctos
* [ ] Paginación si aplica
* [ ] Rate limiting
* [ ] CORS configurado

---

## Seguridad

* [ ] JWT validado
* [ ] Autorización por roles
* [ ] Validación de entrada
* [ ] Sin credenciales en código
* [ ] Secrets en Key Vault
* [ ] HTTPS (TLS 1.3)
* [ ] Logs sin exponer PII

---

## Calidad

* [ ] Unit tests (>70%)
* [ ] Integration tests
* [ ] API tests
* [ ] Linting limpio
* [ ] SonarQube / code review aprobado
* [ ] Sin deuda técnica crítica

---

## Observabilidad

* [ ] Logs estructurados (JSON)
* [ ] DEBUG / INFO / WARN / ERROR configurables
* [ ] Correlation ID
* [ ] Métricas (`/metrics`)
* [ ] Health checks (`/health`, `/ready`)
* [ ] APM integrado

---

# Fase 3: Integración

## Eventos

* [ ] Publicador implementado
* [ ] Suscriptor implementado
* [ ] Idempotencia garantizada
* [ ] Dead Letter Queue
* [ ] Retry con exponential backoff
* [ ] Timeout configurado (>5 min)

---

## Comunicación síncrona

* [ ] Circuit breaker
* [ ] Fallback a caché
* [ ] Timeout < 30 s
* [ ] Retry para errores transitorios

---

## BD y datos

* [ ] BD creada (dev / qa / prod)
* [ ] Credenciales en Key Vault
* [ ] Migraciones automáticas
* [ ] Backup y restore probados
* [ ] Índices creados
* [ ] Query performance (<200ms p99)

---

## Documentación

* [ ] `README.md`
* [ ] `data-model.md`
* [ ] `api-contract.md`
* [ ] `events.md`
* [ ] `runbook.md`
* [ ] Todos los archivos en 🟡 o 🟢

---

# Fase 4: DevOps e Infraestructura

## Containerización

* [ ] Dockerfile multi-stage
* [ ] Imagen <300MB
* [ ] Health check
* [ ] Usuario non-root
* [ ] Build exitoso
* [ ] Vulnerabilidades aceptables

---

## Orquestación (Kubernetes)

* [ ] Deployment
* [ ] Service
* [ ] ConfigMap
* [ ] Secret + Key Vault
* [ ] Requests / Limits
* [ ] HPA
* [ ] Liveness / Readiness
* [ ] Resource quotas

---

## CI/CD

* [ ] Pipeline automático
* [ ] Build en push
* [ ] Tests antes de merge
* [ ] Imagen publicada
* [ ] Deploy automático dev / qa
* [ ] Deploy manual prod
* [ ] Rollback automático

---

## Monitoreo

* [ ] Application Insights / Datadog / New Relic
* [ ] Alertas >5% errores
* [ ] Alertas latencia p99
* [ ] Dashboard creado
* [ ] SLA documentado

---

## Operaciones

* [ ] Runbook disponible
* [ ] Oncall definido
* [ ] Escalation path
* [ ] Postmortem template
* [ ] Backup automático
* [ ] Disaster recovery

---

# Fase 5: Producción

## Validación previa

* [ ] Smoke tests
* [ ] Datos de prueba removidos
* [ ] Secrets reales en Key Vault
* [ ] Logs centralizados
* [ ] Alertas verificadas
* [ ] Runbook y oncall notificados

---

## Deployment

* [ ] Blue-green o Canary
* [ ] Rollback habilitado
* [ ] Release tageada
* [ ] CHANGELOG actualizado
* [ ] Release notes publicadas

---

## Post-deployment

* [ ] Monitoreo 24h
* [ ] Métricas evaluadas
* [ ] Feedback recolectado
* [ ] Observaciones documentadas
* [ ] Mejoras para v1.1

---

# Checklist rápido

## Antes de merge a main

* [ ] Documentación 🟡 o 🟢
* [ ] Tests >70%
* [ ] Linting OK
* [ ] Sin secrets
* [ ] APIs versionadas
* [ ] Eventos idempotentes
* [ ] Circuit breaker + retries

## Antes de prod

* [ ] Dockerfile multi-stage
* [ ] Kubernetes manifests
* [ ] CI/CD OK
* [ ] Monitoreo configurado
* [ ] Backup probado
* [ ] Oncall notificado
* [ ] Smoke tests

## En producción

* [ ] Monitorear 24h
* [ ] Incident response listo
* [ ] Métricas evaluadas
* [ ] Retroalimentación documentada

---

## Cambios después de producción

| Cambio              | Requiere         | Urgencia |
| ------------------- | ---------------- | -------- |
| Bug crítico (100%)  | Hotfix inmediato | CRÍTICA  |
| Bug mayor (>10%)    | Hotfix <2h       | ALTA     |
| Bug menor (<10%)    | Próximo release  | NORMAL   |
| Feature nueva       | Release planeado | NORMAL   |
| Breaking change API | Major version    | NORMAL   |
| Cambio de seguridad | Hotfix inmediato | CRÍTICA  |

---

## Estado de servicios

* 🔴 **Pendiente** → Documentación no iniciada
* 🟡 **En progreso** → Desarrollo o testing
* 🟢 **Estable** → Producción mantenida
* ⚫ **Deprecado** → Reemplazado / sunset
