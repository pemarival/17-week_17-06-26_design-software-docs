# CI/CD

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de DevOps | Equipo: Desarrollo

## Objetivo

Garantizar la entrega continua de código con calidad, seguridad y despliegue estable en los diferentes ambientes.

## Etapas del pipeline

1. `checkout` del código.
2. Instalación de dependencias.
3. `lint` y validación de estilo.
4. `build` de los servicios.
5. Ejecución de pruebas unitarias.
6. Ejecución de pruebas de integración y contratos.
7. Escaneo de seguridad de dependencias.
8. Construcción y publicación de imágenes de contenedor.
9. Despliegue automatizado en `dev` / `qa`.

## Reglas de calidad

- Todo PR debe pasar lint y pruebas unitarias.
- No se debe fusionar código que no tenga revisión aprobada.
- Las pruebas de integración deben ejecutarse en `qa` antes de promover a `preprod`.

## Mecanismo de despliegue

- `dev`: despliegue automático desde la rama `develop`.
- `qa`: despliegue tras merge a `release` o `main` con validación.
- `preprod`: despliegue manual con aprobación antes de producción.
- `prod`: despliegue manual con revisión de checklist y ventanas de mantenimiento.

## Artefactos

- Imágenes de contenedor versionadas por `service:semver`.
- Documentos de contrato generados.
- Reportes de pruebas y análisis de cobertura.

## Monitoreo del pipeline

- Registrar estado de ejecución en la herramienta CI/CD.
- Enviar alertas de fallos críticos por canal de comunicaciones del equipo.

