# Aspectos transversales

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Arquitectura | Equipo: Arquitectura / Seguridad / Calidad

## Seguridad

- Todos los endpoints deben exigir autenticación con JWT.
- Uso de roles y scopes para autorización por recurso.
- Cifrado en tránsito TLS 1.2+ y cifrado en reposo en bases de datos.
- Protecciones contra ataques de fuerza bruta y enumeración de usuarios.
- Control de acceso basado en rol (RBAC) para APIs administrativas.

## Logging

- Todas las aplicaciones deben enviar logs estructurados en JSON.
- Incluir trazas de correlación (`traceId`, `spanId`) para cada petición.
- Loggear eventos de error, warnings y operaciones críticas.
- No registrar datos sensibles como contraseñas, tokens o identificadores personales completos.

## Auditoría

- Todas las operaciones CRUD relevantes deben publicar un evento de auditoría.
- El `audit-service` debe almacenar registros append-only con metadatos de quién, cuándo y qué cambió.
- Las auditorías se usan para trazabilidad, cumplimiento y forense.

## Manejo de errores

- Usar códigos HTTP apropiados: 400, 401, 403, 404, 409, 500.
- Devolver mensajes de error amigables para cliente y detalles técnicos mínimos.
- Implementar retry con backoff exponencial para errores transitorios.
- Definir límites de tiempo de espera (`timeouts`) y circuit breakers para dependencias externas.

## Versionado y compatibilidad

- Versionar APIs mediante prefijo de ruta `/v1/`, `/v2/`.
- Mantener compatibilidad hacia atrás para consumidores externos durante al menos un ciclo de lanzamiento.
- Documentar cambios de contrato en `07-api/contracts/openapi/`.

## Observabilidad

- Exponer métricas Prometheus en cada servicio.
- Medir latencia, tasa de error, tráfico y saturación de recursos.
- Instrumentar transacciones clave del motor de asignación y del acceso a datos.

## Gobernanza de datos

- Cada servicio define y mantiene su propio modelo de datos.
- No compartir bases de datos entre servicios.
- Las integraciones deben usar eventos o APIs explícitos.
- Definir campos obligatorios, formatos y reglas de validación centralizadas.

