# Observabilidad

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Operaciones | Equipo: DevOps

## Objetivo

Monitorear la salud, desempeño y comportamiento del sistema de forma centralizada.

## Métricas clave

- Disponibilidad de APIs.
- Latencia de respuesta.
- Tasa de errores.
- Uso de CPU y memoria.
- Tasa de eventos procesados.
- Disponibilidad de cola y mensajes pendientes.

## Logging

- Logs estructurados con `traceId` y `spanId`.
- Registro de errores críticos y operaciones importantes.
- Normalizar niveles: `DEBUG`, `INFO`, `WARN`, `ERROR`.

## Trazas

- Instrumentar transacciones distribuidas.
- Capturar secuencias de llamada en el motor de asignación.
- Usar OpenTelemetry o equivalente.

## Alertas

- Alertar en `5xx` frecuentes.
- Alertar en retrasos del motor de asignación.
- Alertar en desbordes de cola o fallos de base de datos.

## Dashboards

- Dashboard de salud del sistema.
- Dashboard de uso de ambientes y horarios.
- Dashboard de rendimiento de APIs.

