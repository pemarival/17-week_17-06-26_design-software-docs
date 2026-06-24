# Backup y recuperación

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Operaciones | Equipo: DevOps

## Objetivo

Establecer políticas y procedimientos de respaldo y restauración para minimizar pérdida de datos.

## Política de backup

- Backups diarios para bases de datos `prod`.
- Backups de archivos de documento con frecuencia acorde a la criticidad.
- Retención mínima de 30 días.
- Respaldos cifrados en reposo.

## Recuperación

- Documentar procedimientos de restauración paso a paso.
- Probar restauraciones periódicamente en `preprod`.
- Validar tiempos de recuperación y datos restaurados.

## RPO / RTO

- RPO objetivo: 1 hora para datos críticos.
- RTO objetivo: 4 horas para restauración completa en `prod`.

## Notas

- Asegurar que los backups no impacten el rendimiento de producción.
- Verificar integridad después de cada backup.

