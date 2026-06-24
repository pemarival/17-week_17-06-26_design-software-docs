# Autenticación y autorización

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Seguridad | Equipo: Arquitectura / Desarrollo

## Modelo de autenticación

- Autenticación basada en JWT.
- El `iam-service` emite tokens que contienen `sub`, `roles`, `exp`, `iat` y `aud`.
- Los tokens deben tener un tiempo de expiración corto (ej: 15 min).
- Se puede implementar refresh token con un tiempo de expiración mayor y control de revocación.

## Flujos de acceso

### Inicio de sesión

- `POST /api/v1/auth/login`
- Entrada: `email`, `password`.
- Salida: `accessToken`, `refreshToken`, `expiresIn`.

### Renovación de token

- `POST /api/v1/auth/refresh`
- Entrada: `refreshToken`.
- Salida: nuevo `accessToken`.

### Cierre de sesión

- `POST /api/v1/auth/logout`
- Invalidar refresh token cuando corresponda.

## Autorización por rol

- Roles principales:
  - `DIRECTOR`
  - `COORDINADOR`
  - `INSTRUCTOR`
  - `APRENDIZ`
- Cada endpoint debe validar que el rol del usuario tenga permiso para la operación.
- Las acciones con alto impacto (gestión de fichas, asignación de horarios, eliminación de ambientes) deben estar restringidas a roles administrativos.

## Servicio a servicio

- Las comunicaciones internas entre microservicios deben usar tokens de servicio o certificados mTLS.
- Se recomienda que cada servicio valide la identidad de la llamada y los permisos a nivel de recurso.

## Protección de datos

- No exponer datos sensibles en tokens.
- No almacenar contraseñas en texto claro; usar bcrypt o equivalente.
- Implementar control de fugas de información en mensajes de error.

