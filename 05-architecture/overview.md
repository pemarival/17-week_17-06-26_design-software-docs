# Arquitectura del sistema

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Arquitectura | Equipo: Arquitectura

## Visión general

La arquitectura de Horarios SENA se basa en un conjunto de microservicios orientados a dominio, diseñados para soportar la gestión de fichas, ambientes, instructores, horarios y auditoría en un entorno distribuido.

El sistema adopta un patrón de **Database per Service** y una mezcla de comunicación **sincrónica REST** para APIs frontales y **asincrónica de eventos** para integración entre servicios.

## Componentes principales

- `iam-service`: autenticación, autorización y sesiones.
- `reference-data-service`: catálogos de centros, programas, jornadas y parámetros institucionales.
- `academic-management-service`: gestión de programas, competencias, fichas y resultados de aprendizaje.
- `training-environment-service`: inventario de ambientes, mantenimientos y disponibilidad.
- `scheduling-service`: motor de asignación, validación de conflictos y generación de horarios.
- `actors-service`: registro de instructores, aprendices y empresas.
- `document-service`: gestión de documentos, plantillas y generación de PDF.
- `monitoring-service`: métricas, alertas y notificaciones.
- `audit-service`: registro inmutable de eventos de auditoría.

## Principios arquitectónicos

- Separación clara de responsabilidades y límites de contexto.
- Independencia de despliegue por servicio.
- Persistencia local para cada servicio con event sourcing parcial cuando sea necesario.
- Resiliencia mediante circuit breakers, retries y fallbacks en comunicaciones externas.
- Diseño basado en APIs contractuales y versionado explícito.

## Cómo usar esta sección

- `overview.md`: descripción general de arquitectura, raíces de diseño y decisiones de alto nivel.
- `deployment.md`: topología de despliegue, infraestructura y ambientes.
- `cross-cutting.md`: reglas generales de seguridad, logging, errores y gobernanza.
- `decisions/`: historial de decisiones arquitectónicas documentadas.

