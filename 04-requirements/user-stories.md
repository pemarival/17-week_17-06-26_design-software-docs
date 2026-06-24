# Historias de usuario

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Requisitos

## Template

```markdown
### HU-XXX: [Título]

**Como** [rol]
**Quiero** [acción]
**Para que** [beneficio]

#### Criterios de aceptación
- [ ] Criterio 1
- [ ] Criterio 2
- [ ] Criterio 3

#### Notas
- Nota 1
- Nota 2

#### Servicio(s) involucrado(s)
- servicio-1
- servicio-2
```

---

## HU-001: Crear ficha de formación

**Como** coordinador de centro
**Quiero** crear una nueva ficha de formación (agrupar aprendices)
**Para que** pueda asignar horarios y gestionar el grupo

#### Criterios de aceptación
- [ ] Acceso a formulario "Crear ficha"
- [ ] Seleccionar programa (ADSO, etc.)
- [ ] Seleccionar centro (mi centro)
- [ ] Seleccionar jornada (mañana/tarde/noche)
- [ ] Sistema asigna ID único
- [ ] Ficha creada en estado PLANEACION
- [ ] Puedo ver la ficha en mi listado

#### Notas
- No puedo crear fichas en otro centro
- Necesito rol COORDINADOR

#### Servicio(s) involucrado(s)
- academic-management-service
- audit-service

---

## HU-002: Ver horarios de mi ficha

**Como** coordinador
**Quiero** ver todos los horarios asignados a mi ficha
**Para que** conozca qué instructor enseña qué en dónde y cuándo

#### Criterios de aceptación
- [ ] Tabla de horarios: Instrctor | Ambiente | Franja | RAP
- [ ] Filtrar por día de la semana
- [ ] Filtrar por instructor
- [ ] Exportar como PDF
- [ ] Indicador visual de conflictos (🚨 si existe)

#### Notas
- Debe mostrar 2-4 semanas adelante

#### Servicio(s) involucrado(s)
- scheduling-service
- document-service

---

## HU-003: Autoasignar horarios

**Como** coordinador
**Quiero** que el sistema sugiera horarios automáticamente
**Para que** no tenga que asignar manualmente cada sesion

#### Criterios de aceptación
- [ ] Botón "Autoasignar"
- [ ] Sistema valida competencias necesarias
- [ ] Sistema valida disponibilidad de instructores
- [ ] Sistema valida capacidad de ambientes
- [ ] Muestra matriz de sugerencias (0 conflictos)
- [ ] Puedo aprobar/rechazar cada horario
- [ ] Si rechazo, me muestra alternativas

#### Notas
- Tiempo máximo para generar: 2 segundos

#### Servicio(s) involucrado(s)
- scheduling-service
- academic-management-service
- actors-service
- training-environment-service

---

## HU-004: Recibir notificación de cambios

**Como** instructor
**Quiero** recibir email cuando cambie mi horario
**Para que** esté siempre actualizado sin revisar el sistema

#### Criterios de aceptación
- [ ] Recibo email cuando: asignan nuevo horario, cancelan, modifican
- [ ] Email contiene: qué cambió, ficha, hora, ambiente
- [ ] Puedo desuscribirme
- [ ] Puedo elegir frecuencia (inmediata, diaria, semanal)

#### Notas
- Email desde noreply@horarios-sena.gov.co

#### Servicio(s) involucrado(s)
- monitoring-service
- notification-worker

---

## HU-005: Ver mi dashboard de KPI

**Como** director de centro
**Quiero** ver gráficos de ocupación de ambientes y carga de instructores
**Para que** optimice recursos y detecte cuellos de botella

#### Criterios de aceptación
- [ ] Dashboard con 5+ gráficos:
  - Ocupación promedio por ambiente (%)
  - Carga promedio por instructor (h/sem)
  - Tendencia ocupación (7 días)
  - Instructores sobrecargados
  - Ambientes infrautilizados
- [ ] Actualizado cada 1 hora
- [ ] Filtrar por semana

#### Notas
- Basado en horarios COMPLETADOS

#### Servicio(s) involucrado(s)
- monitoring-service

---

## HU-006: Descargar mi certificado

**Como** aprendiz
**Quiero** descargar PDF de mi certificado
**Para que** lo use para mis antecedentes laborales

#### Criterios de aceptación
- [ ] Sólo aparece mi certificado (no de otros)
- [ ] PDF con logo SENA, mi nombre, competencias, firma
- [ ] Descargable sin expiración
- [ ] Puedo descargar múltiples veces
- [ ] Versión y fecha en PDF

#### Notas
- Sólo disponible si ficha está FINALIZADA

#### Servicio(s) involucrado(s)
- document-service

---

## HU-007: Consultar auditoría

**Como** director de centro
**Quiero** ver el log de qué coordinador cambio qué horario y cuándo
**Para que** tenga trazabilidad y detecte cambios sospechosos

#### Criterios de aceptación
- [ ] Tabla: Usuario | Acción | Entidad | Antes | Después | Timestamp
- [ ] Filtrar por usuario, rango fechas, tipo acción
- [ ] Exportar como CSV
- [ ] No puedo modificar registros

#### Notas
- Inmutable, append-only

#### Servicio(s) involucrado(s)
- audit-service

---

## HU-008: Registrar instructor con especialidades

**Como** administrador
**Quiero** crear cuenta para nuevo instructor indicando qué competencias enseña
**Para que** el motor de asignación lo considere en horarios compatibles

#### Criterios de aceptación
- [ ] Formulario: Nombre, Documento, Centro, Especialidades (múltiple)
- [ ] Crear usuario en sistema (rol INSTRUCTOR)
- [ ] Enviar email con credenciales temporales
- [ ] Especialidades vinculadas a competencias de programas

#### Notas
- Puedo modificar especialidades después

#### Servicio(s) involucrado(s)
- iam-service
- actors-service

---

## HU-009: Marcar ambiente en mantenimiento

**Como** administrador
**Quiero** bloquear un ambiente (aula, lab) por un período
**Para que** no se asignen horarios durante mantenimiento

#### Criterios de aceptación
- [ ] Indicar ambiente, fecha inicio, fecha fin, razón
- [ ] Sistema invalida horarios solapados
- [ ] Notifica a coordinador si hay conflictos
- [ ] Puedo cancelar el bloqueo

#### Notas
- Cancela horarios existentes o sugiere alternativas

#### Servicio(s) involucrado(s)
- training-environment-service
- scheduling-service
- notification-worker

---

## HU-010: Ver mi ocupación como instructor

**Como** instructor
**Quiero** ver cuántas horas tengo asignadas y disponibilidad
**Para que** planifique mi semana

#### Criterios de aceptación
- [ ] Calendario semanal con mis horarios
- [ ] Horas totales/semana
- [ ] Disponibilidad (% de tiempo libre)
- [ ] Alerta si > 30 h/semana (sobrecarga)

#### Notas
- Solo veo mis propios horarios

#### Servicio(s) involucrado(s)
- scheduling-service
- actors-service

---

## Resumen de RFs cubiertos por HUs

| HU | RF cubierto | Servicio(s) |
|----|---------|-------------|
| HU-001 | RF-ACAD-001 | academic-management |
| HU-002 | RF-SCHED-004 (lectura) | scheduling |
| HU-003 | RF-SCHED-001 | scheduling |
| HU-004 | RF-MON-002 | monitoring |
| HU-005 | RF-MON-003 | monitoring |
| HU-006 | RF-DOC-001 | document |
| HU-007 | RF-AUD-002 | audit |
| HU-008 | RF-ACT-001 | actors |
| HU-009 | RF-ENV-002 | environment |
| HU-010 | RF-ACT-003 | actors |

---

## Referencias

- [04-requirements/functional.md](./functional.md) — 26 requisitos funcionales
- [03-product/product-backlog.md](../03-product/product-backlog.md) — 10 epics, 50 RFs
