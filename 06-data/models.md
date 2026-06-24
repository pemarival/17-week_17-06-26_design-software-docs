# Modelos de datos

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Datos | Equipo: Arquitectura / Desarrollo

## Propósito

Documentar los modelos de datos conceptuales que sostienen el dominio Horarios SENA y orientar la implementación de los esquemas físicos de cada servicio.

## Modelos conceptuales principales

### Ficha de formación

- `Ficha` incluye `programa`, `centro`, `jornada`, `periodo`, `competencias`, `instructor` y `aprendices`.
- Cada `Ficha` representa un conjunto de aprendices asociados a un plan formativo.

### Ambiente

- `Ambiente` describe un espacio físico o virtual con `capacidad`, `tipo`, `centro`, `recursos` y `estado`.
- Los `Ambientes` pueden tener periodos de no disponibilidad por mantenimiento.

### Instructor y Aprendiz

- `Instructor` es el actor responsable de impartir sesiones.
- `Aprendiz` es el beneficiario que participa en una ficha.
- El servicio de `actors` gestiona las identidades y roles.

### Horario y Sesión

- `Horario` es la asignación de una `Sesión` a un `Ambiente`, una `Ficha`, un `Instructor` y un intervalo temporal.
- `Sesión` puede estar relacionada con un `Resultado de aprendizaje` o una `Competencia`.

### Evento de dominio

- `FichaCreada`, `AmbienteNoDisponible`, `HorarioAsignado`, `ConflictoDetectado`, `DocumentoGenerado`.

## Niveles de modelado

1. Modelo conceptual: entidades y relaciones principales del negocio.
2. Modelo lógico: atributos, cardinalidades y reglas de validación.
3. Modelo físico: tablas, columnas, índices y tipos específicos de base de datos.

## Principios de diseño

- Usar nombres semánticos y consistentes con el dominio.
- Modelar relaciones con claridad: 1:N, N:M y agregados.
- Mantener los datos del servicio localmente y evitar referencias directas a tablas de otros servicios.
- Favorecer la normalización cuando el dominio lo requiera y la desnormalización controlada para rendimiento en consultas frecuentes.

