# Backlog de producto

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Producto

## Epics priorizadas

### Epic 1: Gestión de fichas (M1-2)
**Descripción:** Coordinador puede crear, editar y visualizar fichas de formación
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 8 | **Estimado:** 4 sprints

- [ ] RF-01: Crear ficha con programa, centro, jornada, coordinador
- [ ] RF-02: Editar ficha (cambio de jornada, coordinador, aprendices)
- [ ] RF-03: Listar fichas del centro (filtros, búsqueda)
- [ ] RF-04: Consultar detalle de ficha (RAPs, competencias, horarios)
- [ ] RF-05: Finalizar ficha (marcar como completada)

### Epic 2: Gestión de ambientes (M1)
**Descripción:** Administrador puede registrar ambientes, capacidad, disponibilidad
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 5 | **Estimado:** 2 sprints

- [ ] RF-06: Registrar ambiente (nombre, capacidad, centro, tipo)
- [ ] RF-07: Marcar ambiente como no disponible (mantenimiento)
- [ ] RF-08: Editar disponibilidad de ambiente
- [ ] RF-09: Consultar calendario de ocupación de ambiente

### Epic 3: Motor de asignación (M2)
**Descripción:** Sistema sugiere horarios automáticamente sin conflictos
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 13 | **Estimado:** 6 sprints

- [ ] RF-10: Ejecutar motor de asignación para ficha
- [ ] RF-11: Validar asignación contra 8 reglas de negocio
- [ ] RF-12: Detectar conflictos (instructor/ambiente duplicado)
- [ ] RF-13: Sugerir horarios alternativos si hay conflicto
- [ ] RF-14: Guardar horarios aceptados
- [ ] RF-15: Cancelar/modificar horario existente

### Epic 4: Gestión de actores (M3-5)
**Descripción:** Registrar y mantener instructores, aprendices, empresas
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 8 | **Estimado:** 4 sprints

- [ ] RF-16: Registrar instructor (nombre, especialidades, disponibilidad)
- [ ] RF-17: Modificar especialidades de instructor
- [ ] RF-18: Registrar aprendiz (nombre, documento, ficha)
- [ ] RF-19: Registrar empresa (razón social, NIT, sector)
- [ ] RF-20: Consultar disponibilidad de instructor

### Epic 5: Documentos y certificados (M6)
**Descripción:** Generar certificados, diplomas y reportes automáticamente
**Prioridad:** 🟡 ALTA | **Complejidad:** 8 | **Estimado:** 4 sprints

- [ ] RF-21: Crear plantillas de documentos (certificado, diploma)
- [ ] RF-22: Generar certificado para aprendiz
- [ ] RF-23: Generar diploma al egresar
- [ ] RF-24: Descargar documento generado (PDF)
- [ ] RF-25: Generar reporte de horarios por ficha

### Epic 6: Notificaciones y alertas (M7-9)
**Descripción:** Notificar cambios de horarios, alertas de sobrecarga
**Prioridad:** 🟡 ALTA | **Complejidad:** 6 | **Estimado:** 3 sprints

- [ ] RF-26: Enviar notificación al crear horario (coordinador, instructor)
- [ ] RF-27: Enviar notificación al cancelar horario
- [ ] RF-28: Enviar alerta si instructor sobrecargado (> 30 h/sem)
- [ ] RF-29: Enviar alerta si ambiente infrautilizado (< 50%)
- [ ] RF-30: Suscribirse/desuscribirse de notificaciones

### Epic 7: KPIs y Dashboard (M8)
**Descripción:** Calcular métricas de eficiencia y mostrar en dashboard
**Prioridad:** 🟡 ALTA | **Complejidad:** 8 | **Estimado:** 4 sprints

- [ ] RF-31: Calcular ocupación de ambiente (%)
- [ ] RF-32: Calcular carga de instructor (h/semana)
- [ ] RF-33: Calcular eficiencia de centro
- [ ] RF-34: Mostrar dashboard con 5+ gráficos de KPI
- [ ] RF-35: Exportar reportes de KPI (XLSX)

### Epic 8: Auditoría (M4)
**Descripción:** Registrar todas las operaciones para compliance
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 5 | **Estimado:** 2 sprints

- [ ] RF-36: Registrar creación de ficha (usuario, timestamp, datos)
- [ ] RF-37: Registrar modificación de horario
- [ ] RF-38: Registrar cancelación de horario (motivo)
- [ ] RF-39: Generar reporte de auditoría (descargable)
- [ ] RF-40: Garantizar audit log append-only (no modificable)

### Epic 9: Autenticación (M1)
**Descripción:** Control de acceso y sesiones de usuario
**Prioridad:** 🔴 CRÍTICA | **Complejidad:** 6 | **Estimado:** 3 sprints

- [ ] RF-41: Login con correo y contraseña
- [ ] RF-42: Control de roles (director, coordinador, instructor, aprendiz)
- [ ] RF-43: Logout y cierre de sesión
- [ ] RF-44: Recuperación de contraseña
- [ ] RF-45: Cambio de contraseña

### Epic 10: Etapa productiva (M10-15)
**Descripción:** Gestión de empresas y bitácora de etapa productiva
**Prioridad:** 🟢 BAJA | **Complejidad:** 6 | **Estimado:** 3 sprints

- [ ] RF-46: Registrar empresa para etapa productiva
- [ ] RF-47: Asignar aprendiz a empresa
- [ ] RF-48: Crear bitácora de actividades (etapa productiva)
- [ ] RF-49: Consultar bitácora como aprendiz/empresa
- [ ] RF-50: Generar reporte de etapa productiva

---

## Priorización de la cartera

```
Q3 2026 (MVP)
├─ Epic 1: Fichas              [████████] 100%
├─ Epic 2: Ambientes          [████████] 100%
├─ Epic 3: Motor asignación    [████████] 100%
├─ Epic 8: Auditoría           [████████] 100%
└─ Epic 9: Autenticación       [████████] 100%

Q4 2026 (V1.0)
├─ Epic 4: Actores            [████████] 100%
├─ Epic 5: Documentos          [████████] 100%
└─ Epic 6: Notificaciones      [████████] 100%

Q1 2027 (V1.5)
├─ Epic 7: KPIs               [████████] 100%
└─ Epic 10: Etapa productiva   [████░░░░] 50%

Q2-Q3 2027 (V2.0 & Beyond)
├─ Mobile app                  [ future ]
├─ Integraciones               [ future ]
└─ Analytics predictivo        [ future ]
```

## Criterios de aceptación generales

**Para cada requisito funcional:**
- [ ] Código escrito con tests (TDD)
- [ ] Integrado con BD
- [ ] API documentada (OpenAPI)
- [ ] Eventos publicados (si aplica)
- [ ] Auditoría registra operación
- [ ] UI accesible (WCAG 2.1 AA)
- [ ] Performance > 95%ile < 200ms
- [ ] Code review aprobado
- [ ] Tests pasan 100%
- [ ] Documentado en wiki

## Definición de hecho (DoD)

```
✅ SPRINT DONE cuando:
  • Todos los criterios de aceptación cumplidos
  • Code review aprobado (2 reviewers)
  • Tests pasan 100% (coverage > 70%)
  • Merge a rama main
  • Deploy a staging
  • Documentación actualizada
  • Demo al PO
  • Sin deuda técnica crítica
```

## Referencias

- [03-product/vision.md](./vision.md) — Visión del producto
- [03-product/roadmap.md](./roadmap.md) — Timeline y fases
- [04-requirements/functional.md](../04-requirements/functional.md) — Requisitos funcionales detallados
