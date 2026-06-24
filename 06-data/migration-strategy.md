# Estrategia de migración de datos

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Datos | Equipo: DevOps

## Objetivo

Definir un proceso seguro y reversible para evolucionar esquemas de datos, migraciones y cambios de modelo sin interrumpir la operación del sistema.

## Principios

- Migraciones versionadas y revisadas como código.
- Cambios incrementales y no destructivos siempre que sea posible.
- Pruebas de migración en `qa` y `preprod` antes de desplegar en `prod`.
- Rollback documentado y fácil de ejecutar.
- Monitoreo de tiempo de ejecución y validación de consistencia.

## Flujo de migración

1. Crear script de migración con herramienta de base de datos (`Flyway`, `Liquibase` o equivalente).
2. Ejecutar en ambiente de desarrollo y validar datos.
3. Aplicar en `qa` y verificar que la aplicación funciona con el nuevo esquema.
4. Revisar impacto de índices y tiempo de migración.
5. Desplegar en `preprod` y ejecutar pruebas de integración.
6. Desplegar en `prod` fuera de ventanas de mantenimiento cuando sea necesario.

## Tipos de migración

- Cambios de esquema: agregar/eliminar columnas, modificar tipos, crear índices.
- Transformaciones de datos: backfills, normalizaciones, consolidaciones.
- Migraciones de referencia: actualización de catálogos y parámetros.

## Reglas operativas

- No eliminar columnas en `prod` hasta que no haya dependencias activas.
- Para cambios complejos, usar `feature toggles` o tablas temporales.
- Respaldar la base de datos antes de cualquier migración destructiva.
- Documentar cada migración con propósito, alcance y reversión.

## Monitoreo y validación

- Verificar conteos de registros antes y después.
- Revisar errores de migración y tiempos de ejecución.
- Validar consistencia de datos claves en `preprod` y `prod`.
- Mitigar caídas de rendimiento creando índices y ejecutando en horarios de baja carga.

