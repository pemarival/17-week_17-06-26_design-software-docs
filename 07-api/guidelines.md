# Directrices de diseño de APIs

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Arquitectura | Equipo: Arquitectura / Desarrollo

## Principios de diseño

- Diseñar APIs centradas en recursos y siguiendo convenciones REST.
- Uso de verbos HTTP correctos: `GET` para lectura, `POST` para creación, `PUT/PATCH` para actualización y `DELETE` para eliminación.
- Rutas claras y consistentes: `/v1/fichas`, `/v1/ambientes`, `/v1/horarios`.
- Versionado explícito en la ruta: `/api/v1/`.
- Documentar todos los contratos en `07-api/contracts/openapi/`.

## Contratos y estabilidad

- Cada microservicio debe publicar un contrato OpenAPI aprobado.
- El contrato en `07-api/contracts/openapi/` representa la versión pública estable aprobada por arquitectura.
- Los cambios en el contrato deben revisarse y compararse con versiones previas.

## Formato de respuesta

- Respuestas exitosas deben devolver el cuerpo en JSON.
- En caso de error, usar un formato uniforme:

```json
{
  "code": "USER_NOT_FOUND",
  "message": "El usuario no existe.",
  "details": []
}
```

## Paginación y filtros

- Usar paginación basada en `limit` y `offset` o `cursor` para listas grandes.
- Permitir filtrado y ordenamiento en endpoints de colección.
- Incluir metadatos de paginación: `total`, `limit`, `offset`, `next`.

## Seguridad y autenticación

- Todas las APIs deben exigir autenticación por JWT.
- Los endpoints públicos deben ser mínimos y sólo para recursos no sensibles.

## Errores y códigos HTTP

- `200 OK` para respuestas correctas.
- `201 Created` para recursos creados.
- `204 No Content` para eliminaciones exitosas sin contenido.
- `400 Bad Request` para solicitudes inválidas.
- `401 Unauthorized` para autenticación fallida.
- `403 Forbidden` para autorización insuficiente.
- `404 Not Found` para recursos no existentes.
- `409 Conflict` para violaciones de reglas de negocio.
- `500 Internal Server Error` sólo para fallos inesperados.

## Buenas prácticas

- Evitar respuestas excesivamente grandes en consultas.
- Exponer sólo los campos necesarios.
- Mantener la coherencia de nombres entre APIs y modelo de dominio.
- Documentar cada endpoint con ejemplos de petición y respuesta.

