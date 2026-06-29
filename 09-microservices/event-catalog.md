# Catálogo de eventos

> Estado: 🟡 En progreso
> Última actualización: 2026-06-22
> Autor: Por definir
> Equipo: Por definir

---

## Estructura de evento

Todo evento sigue este *envelope*:

```json
{
  "id": "evt-uuid",
  "type": "dominio.entidad.verbo",
  "version": "1.0",
  "timestamp": "2026-06-22T14:30:00Z",
  "userId": "usr-001",
  "source": "iam-service",
  "payload": {},
  "metadata": {
    "correlationId": "corr-uuid",
    "causationId": "evt-uuid-anterior",
    "environment": "production"
  }
}
```

---

# Catálogo por servicio

## IAM Service

| Evento                    | Disparador              | Consumidores                     | Payload                             |
| ------------------------- | ----------------------- | -------------------------------- | ----------------------------------- |
| `iam.usuario.creado`      | Usuario registrado      | Audit, Notifications             | usuarioId, email, rol, timestamp    |
| `iam.usuario.desactivado` | Admin desactiva usuario | Scheduling, Audit, Notifications | usuarioId, razon                    |
| `iam.sesion.iniciada`     | Login exitoso           | Audit, Monitoring                | usuarioId, ip, userAgent            |
| `iam.rol.modificado`      | Cambio en permisos      | Audit, todos (revalidar)         | rolId, permisosAntes, permisosAhora |

---

## Reference Data Service

| Evento                          | Disparador                | Consumidores                       | Payload                              |
| ------------------------------- | ------------------------- | ---------------------------------- | ------------------------------------ |
| `refdata.parametro.actualizado` | Admin actualiza parámetro | Audit, Scheduling (invalida caché) | parametroKey, valorAntes, valorAhora |
| `refdata.centro.registrado`     | Nuevo centro agregado     | Audit, Notifications               | centroId, nombre                     |
| `refdata.centro.modificado`     | Centro editado            | Audit, todos (caché)               | centroId, cambios                    |

---

## Academic Management Service

| Evento                            | Disparador             | Consumidores                                 | Payload                                         |
| --------------------------------- | ---------------------- | -------------------------------------------- | ----------------------------------------------- |
| `academic.ficha.creada`           | Nueva ficha registrada | Scheduling, Audit, Notifications             | fichaId, programa, centro, jornada, coordinador |
| `academic.ficha.modificada`       | Cambio en ficha        | Scheduling, Audit, Notifications, Monitoring | fichaId, cambios                                |
| `academic.ficha.finalizada`       | Cierre de ficha        | Documents, Audit, Monitoring, Notifications  | fichaId, fecha                                  |
| `academic.competencia.modificada` | Cambio en competencia  | Scheduling (invalida caché), Audit           | competenciaId, cambios                          |
| `academic.rap.modificado`         | RAP editado            | Scheduling, Document, Audit                  | rapId, cambios                                  |
| `academic.aprendiz.asignado`      | Aprendiz inscrito      | Audit, Notifications, Monitoring             | aprendizId, fichaId                             |

---

## Training Environment Service

| Evento                       | Disparador                | Consumidores                     | Payload                                           |
| ---------------------------- | ------------------------- | -------------------------------- | ------------------------------------------------- |
| `env.ambiente.creado`        | Nuevo ambiente            | Scheduling, Audit                | ambienteId, nombre, capacidad, centro             |
| `env.ambiente.nodisponible`  | Ambiente en mantenimiento | Scheduling, Audit, Notifications | ambienteId, fechaInicio, fechaFin, razon          |
| `env.ambiente.disponible`    | Mantenimiento finalizado  | Scheduling (revalidar), Audit    | ambienteId                                        |
| `env.inventario.actualizado` | Cambio en recursos        | Audit                            | ambienteId, recurso, cantidadAntes, cantidadAhora |

---

## Actors Service

| Evento                         | Disparador           | Consumidores                     | Payload                               |
| ------------------------------ | -------------------- | -------------------------------- | ------------------------------------- |
| `actors.instructor.registrado` | Nuevo instructor     | Scheduling, Audit                | instructorId, especialidades, centro  |
| `actors.instructor.modificado` | Cambio en instructor | Scheduling, Audit, Notifications | instructorId, cambios                 |
| `actors.aprendiz.registrado`   | Nuevo aprendiz       | Academic, Audit, Monitoring      | aprendizId, documento, nombre, centro |
| `actors.empresa.registrada`    | Empresa registrada   | Audit                            | empresaId, razonSocial, nit           |

---

## Scheduling Service (CORE)

| Evento                           | Disparador        | Consumidores                                | Payload                                              |
| -------------------------------- | ----------------- | ------------------------------------------- | ---------------------------------------------------- |
| `scheduling.horario.asignado`    | Horario creado    | Audit, Notifications, Documents, Monitoring | horarioId, fichaId, instructorId, ambienteId, franja |
| `scheduling.horario.cancelado`   | Cancelación       | Audit, Notifications, Monitoring            | horarioId, razon                                     |
| `scheduling.conflicto.detectado` | Solapamiento      | Audit, Notifications                        | conflictoId, tipo, horariosInvolucrados              |
| `scheduling.sesion.completada`   | Clase finalizada  | Audit, Monitoring, Documents                | sesionId, aprendicesPresentes                        |
| `scheduling.motor.ejecutado`     | Algoritmo termina | Audit, Notifications                        | fichaId, horariosAsignados, conflictosEncontrados    |

---

## Document Service

| Evento                          | Disparador         | Consumidores         | Payload                                        |
| ------------------------------- | ------------------ | -------------------- | ---------------------------------------------- |
| `document.documento.generado`   | PDF creado         | Audit, Notifications | documentoId, tipo, destinatarioId, urlDescarga |
| `document.documento.descargado` | Descarga realizada | Audit, Monitoring    | documentoId, usuarioId                         |
| `document.documento.archivado`  | Documento obsoleto | Audit                | documentoId, razon                             |

---

## Monitoring Service

| Evento                            | Disparador        | Consumidores                    | Payload                                             |
| --------------------------------- | ----------------- | ------------------------------- | --------------------------------------------------- |
| `monitoring.kpi.calculado`        | Cálculo diario    | Audit, Notifications            | fecha, kpis                                         |
| `monitoring.alerta.generada`      | KPI supera umbral | Audit, Notifications, Dashboard | alertaId, tipo, kpi, valor, umbral, entidadAfectada |
| `monitoring.notificacion.enviada` | Mensaje enviado   | Audit                           | notificacionId, usuarioId, tipo, canal              |

---

## Audit Service

| Evento                       | Disparador               | Consumidores   | Payload                                        |
| ---------------------------- | ------------------------ | -------------- | ---------------------------------------------- |
| `audit.operacion.registrada` | Recibe todos los eventos | BD append-only | timestamp, usuarioId, accion, entidad, cambios |

---

# Ejemplo: Flujo completo de creación de ficha

```text
1. Usuario crea ficha vía academic-api
   ↓

2. Academic-service publica:
   "academic.ficha.creada"

   {
     "fichaId": "F123",
     "programa": "ADSO",
     "centro": "C001",
     "jornada": "MANANA",
     "coordinador": "U456"
   }

   ↓

3. Consumidores reaccionan en paralelo

├─ Scheduling-service
│   ├─ Escucha evento
│   ├─ Prepara matriz de horarios
│   └─ Publica "scheduling.motor.ejecutado"

├─ Audit-service
│   ├─ Escucha evento
│   └─ Guarda registro append-only

└─ Notifications-service
    ├─ Escucha evento
    ├─ Envía email
    └─ Publica "monitoring.notificacion.enviada"
```

---

# Garantías de entrega

* **At-least-once:** cada evento se entrega mínimo una vez
* **Idempotencia:** consumidores preparados para duplicados
* **Ordenamiento:** FIFO por `fichaId` (partición)
* **Timeout:** si un evento no se procesa en 5 minutos → Dead Letter Queue (DLQ)

---

# Versionado de eventos

Si cambia el schema:

1. Crear nueva versión → `academic.ficha.creada@2.0`
2. Consumidores antiguos siguen escuchando `@1.0`
3. Consumidores nuevos migran a `@2.0`
4. Un bridge puede traducir versiones
5. Deprecar `@1.0` después de 6 meses
