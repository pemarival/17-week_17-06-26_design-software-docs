# UML y diagramación

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Arquitectura | Equipo: Diseño / Desarrollo

Esta sección centraliza los diagramas UML y los artefactos visuales que describen la estructura y comportamiento del sistema.

## Objetivo

- Documentar la arquitectura y el diseño mediante diagramas editables.
- Garantizar que exista una versión fuente y una exportación revisable.
- Facilitar la comunicación entre arquitectura, desarrollo y producto.

## Convenciones

- Fuentes en `diagrams/source/` con extensión `.wsd`, `.puml` o `.drawio`.
- Exportaciones en `diagrams/exports/` con formato `.svg` o `.png`.
- Nombre de archivo: `<dominio>-<tipo>.<ext>` (ej: `horario-sequence.wsd`).
- Registrar cada diagrama en `diagram-index.md`.

## Tipos de diagrama

| Tipo | Uso |
|------|-----|
| Casos de uso | Describir interacciones usuario-sistema |
| Clases | Modelo de datos y objetos del sistema |
| Secuencia | Flujo de eventos entre componentes |
| Actividad | Procesos y decisiones operativas |
| Estado | Ciclo de vida de entidades clave |
| Componentes | Relación entre servicios y módulos |
| Despliegue | Infraestructura y topología de despliegue |

## Cómo trabajar con los diagramas

1. Crear la fuente en `diagrams/source/`.
2. Generar exportaciones en `diagrams/exports/`.
3. Actualizar `diagram-index.md` con el nombre, descripción y último estado.
4. Confirmar que la exportación coincide con la fuente.

