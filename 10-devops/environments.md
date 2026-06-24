# Ambientes

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de DevOps | Equipo: Arquitectura / QA

## Ambientes definidos

### `dev`
- Uso: desarrollo diario y testing local.
- Acceso: equipo de desarrollo.
- Datos: datos sintéticos o subset de datos de prueba.
- Regla: puede reiniciarse frecuentemente.

### `qa`
- Uso: pruebas de integración, regresión y validación funcional.
- Acceso: QA, desarrollo, arquitectura.
- Datos: copia parcial y anonimizada de producción si es posible.
- Regla: se deben ejecutar suites completas de pruebas.

### `preprod`
- Uso: ensayo de despliegue antes de producción.
- Acceso: operación, QA y soporte.
- Datos: copia representativa de producción o datos sintéticos avanzados.
- Regla: validación de rollout y performance.

### `prod`
- Uso: ambiente de usuario final.
- Acceso: solo personal autorizado.
- Datos: datos reales de operación.
- Regla: alta disponibilidad y monitoreo permanente.

## Reglas de acceso y uso

- Separar credenciales por ambiente.
- No compartir datos reales fuera de producción.
- Cualquier cambio en `prod` debe pasar por control de cambios.
- Implementar políticas de backup para `prod` y `preprod`.

## Consideraciones de datos

- `prod` y `preprod` deben usar cifrado en reposo.
- `qa` puede usar datos anonimizados para pruebas.
- `dev` usa datos no sensibles o datos generados.

