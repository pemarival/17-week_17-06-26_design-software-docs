# Requisitos no-funcionales

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Requisitos

## Rendimiento

### RNF-PERF-001: Latencia de respuesta API
- **Estándar:** p50 < 100ms, p99 < 500ms
- **Medida:** Por endpoint HTTP
- **Excepciones:** Motor de asignación p99 < 2s
- **Herramienta:** Application Insights

### RNF-PERF-002: Throughput de asignaciones
- **Estándar:** Mínimo 100 asignaciones/minuto sin degradación
- **Medida:** Requests/s en peak
- **Centro:** 1 ficha = 30-50 horarios en < 2s

### RNF-PERF-003: Tiempo de carga del dashboard
- **Estándar:** < 1 segundo (First Contentful Paint)
- **Medida:** Lighthouse, WebPageTest
- **Target:** Score > 85

### RNF-PERF-004: Cálculo de KPIs
- **Estándar:** Diarios a las 23:59, completan en < 5 minutos
- **Medida:** Tiempo de job
- **Escala:** 1000+ fichas/día

---

## Disponibilidad y confiabilidad

### RNF-AVAIL-001: Uptime objetivo
- **Estándar:** 99.9% (SLA)
- **Equivalente:** < 43 minutos downtime/mes
- **Medida:** Heartbeat de servicios
- **Exclusiones:** Downtime planeado (comunicado 7 días antes)

### RNF-AVAIL-002: Recovery Time Objective (RTO)
- **Estándar:** < 4 horas
- **Procedimiento:** Restauración desde backup
- **Responsable:** DevOps

### RNF-AVAIL-003: Recovery Point Objective (RPO)
- **Estándar:** < 1 hora
- **Significado:** Máximo 1 hora de datos perdidos
- **Frecuencia:** Backups cada 4 horas

### RNF-AVAIL-004: Resiliencia de motor de asignación
- **Comportamiento:** Si falla validación de instructor, sugerir otro
- **No bloquear:** Sistema no genera horarios sin validación
- **Fallback:** Mantener última asignación válida en cache

---

## Escalabilidad

### RNF-ESCAL-001: Capacidad de fichas
- **Target:** 10,000 fichas simultáneas
- **Crecimiento:** Autoscaling horizontal
- **Estrategia:** Sharding por centro

### RNF-ESCAL-002: Usuarios concurrentes
- **Target:** 5,000 usuarios concurrentes
- **Peak:** 8:00 AM - 5:00 PM (horario laboral)
- **Carga:** Repartir en instancias via load balancer

### RNF-ESCAL-003: Almacenamiento
- **Crecimiento:** 50GB/año (documentos, logs, auditoría)
- **Estrategia:** Tiered storage (hot 30d, cold 1año)
- **Base datos:** Particionada por fecha

### RNF-ESCAL-004: Tasa de eventos
- **Peak:** 10,000 eventos/minuto
- **Broker:** Azure Service Bus con particiones
- **DLQ:** Monitorear y alertar

---

## Seguridad

### RNF-SEC-001: Autenticación
- **Estándar:** JWT con firma RS256
- **Expiración:** 1 hora de inactividad
- **Refresh token:** Sí, expira en 7 días
- **MFA:** No requerido en fase 1, planeado v2

### RNF-SEC-002: Autorización
- **Modelo:** RBAC (Role-Based Access Control)
- **Validación:** En cada endpoint
- **Ejemplo:** Coordinador NO puede ver auditoría global, solo de su centro

### RNF-SEC-003: Encriptación en tránsito
- **Estándar:** TLS 1.3 obligatorio
- **Certificados:** Renovación automática (Let's Encrypt)
- **Hosts:** HTTPS solo, redirigir HTTP → HTTPS

### RNF-SEC-004: Encriptación en reposo
- **BD:** AES-256 para datos sensibles (documentos, audit)
- **Llaves:** Gestión en Azure Key Vault
- **Rotación:** Trimestral

### RNF-SEC-005: Inyección SQL
- **Prevención:** Prepared statements, no concatenación
- **Validación:** Input validation + output encoding
- **Testing:** OWASP Top 10 scans

### RNF-SEC-006: XSS (Cross-Site Scripting)
- **Prevención:** Content Security Policy (CSP)
- **Framework:** React con escaping automático
- **Headers:** X-Content-Type-Options, X-Frame-Options

### RNF-SEC-007: CSRF (Cross-Site Request Forgery)
- **Prevención:** SameSite cookies + CSRF tokens
- **Aplicación:** En formularios POST, PUT, DELETE

### RNF-SEC-008: Auditoría append-only
- **Inmutabilidad:** Nunca modificable, no DELETE
- **Redundancia:** Replicada en BD de audit
- **Cumplimiento:** SGPL, normativa SENA

---

## Datos y privacidad

### RNF-DATA-001: Retención de datos
- **Transacciones:** 7 años (legal)
- **Audit:** 7 años (legal)
- **Documentos:** 3 años (historial)
- **Sesiones:** 90 días (compliance)
- **Logs:** 30 días (troubleshooting)

### RNF-DATA-002: Privacidad de aprendices
- **Restricción:** Aprendiz solo ve su ficha
- **Instructor:** Ve sus horarios + aprendices asignados
- **Director:** Ve todo de su centro
- **Admin:** Ve todo

### RNF-DATA-003: Anonimización
- **Para reportes:** Remover nombres de aprendices en reportes públicos
- **Solo IDs:** Usar fichaID, no nombreAprendiz
- **Analytics:** Datos pseudoanonimizados

### RNF-DATA-004: Cumplimiento normativo
- **SGPL:** Implementar accesos privilegiados monitoreados
- **SENA:** Normativa sobre datos de menores de edad
- **Auditoría:** Disponible para compliance team

---

## Mantenibilidad y calidad

### RNF-MAINT-001: Cobertura de tests
- **Estándar:** > 70% de líneas de código
- **Unit tests:** > 80%
- **Integration tests:** > 60%
- **Herramienta:** SonarQube

### RNF-MAINT-002: Deuda técnica
- **Objetivo:** SonarQube grade A
- **Code smells:** < 5% del código
- **Security hotspots:** 0 críticos
- **Revisión:** Mensual

### RNF-MAINT-003: Documentación
- **APIs:** OpenAPI 3.0, actualizado
- **Runbooks:** Deployment, troubleshooting
- **Architecture:** Diagramas C4, ADRs
- **Wiki:** Actualización per-sprint

### RNF-MAINT-004: Logging
- **Nivel:** INFO por defecto, DEBUG en dev
- **Formato:** JSON estructurado
- **Retención:** 30 días en hot storage
- **Searchable:** Azure Log Analytics

### RNF-MAINT-005: Monitoreo y alertas
- **Dashboards:** Por servicio + global
- **Alertas:** Error rate > 1%, latency p99 > 500ms
- **Oncall:** Rotación 24/7
- **Escalación:** Tech lead → Arquitecto

---

## Compatibilidad

### RNF-COMPAT-001: Navegadores
- **Soportados:** Chrome 120+, Firefox 120+, Safari 17+, Edge 120+
- **No soportado:** IE 11
- **Testing:** BrowserStack (automatizado)

### RNF-COMPAT-002: Dispositivos
- **Desktop:** 1920x1080 mínimo
- **Tablet:** iPad 768x1024
- **Mobile:** iPhone 375x812 (planeado v2)
- **Responsive:** Mobile-first (planeado v2)

### RNF-COMPAT-003: Accesibilidad (WCAG 2.1)
- **Nivel:** AA (Objetivo)
- **Requerimientos:**
  - Contraste 4.5:1 (texto)
  - Navegación por teclado
  - Screen reader compatible
  - Semántica HTML5

---

## Operaciones

### RNF-OPS-001: Deployment
- **Frecuencia:** Diaria (blue-green deployment)
- **Tiempo:** < 15 minutos
- **Rollback:** Automático si health checks fallan

### RNF-OPS-002: Migración de BD
- **Estrategia:** Migration files, versionadas
- **Reversibilidad:** Todos migrations tienen rollback
- **Testing:** Probadas en staging antes de prod

### RNF-OPS-003: Capacitación
- **Usuarios:** Video tutoriales + manual
- **Desarrolladores:** Onboarding en 1 día
- **Wiki:** Documentación siempre accesible

---

## Referencias

- [04-requirements/functional.md](./functional.md) — 26 requisitos funcionales
- [09-microservices/communication-patterns.md](../09-microservices/communication-patterns.md) — Patrones de comunicación
- [09-microservices/service-readiness-checklist.md](../09-microservices/service-readiness-checklist.md) — Checklist de producción
