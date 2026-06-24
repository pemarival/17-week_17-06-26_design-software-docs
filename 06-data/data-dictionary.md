# Diccionario de datos

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Datos | Equipo: Arquitectura / Desarrollo

## Entidades principales

### Ficha
- `id`: Identificador único de la ficha.
- `programaId`: Referencia al programa formativo.
- `centroId`: Centro educativo asociado.
- `jornada`: Mañana / Tarde / Noche.
- `periodo`: Periodo académico vigente.
- `estado`: Planeacion / Activa / Cerrada.
- `fechaCreacion`: Fecha de creación.

### Ambiente
- `id`: Identificador único del ambiente.
- `centroId`: Centro donde se ubica.
- `nombre`: Nombre del aula, laboratorio o taller.
- `tipo`: Aula / Laboratorio / Taller.
- `capacidad`: Número máximo de personas.
- `estado`: Disponible / Mantenimiento / Inhabilitado.
- `recursos`: Lista de recursos asociados.

### Instructor
- `id`: Identificador único.
- `nombre`: Nombre completo.
- `documento`: Número de identificación.
- `competencias`: Lista de competencias certificadas.
- `estado`: Activo / Inactivo.

### Aprendiz
- `id`: Identificador único.
- `nombre`: Nombre completo.
- `fichaId`: Ficha registrada.
- `programaId`: Programa asociado.
- `estado`: Activo / Egresado.

### Horario
- `id`: Identificador único.
- `fichaId`: Ficha asignada.
- `ambienteId`: Ambiente asignado.
- `instructorId`: Instructor asignado.
- `fechaInicio`: Fecha y hora de inicio.
- `fechaFin`: Fecha y hora de fin.
- `estado`: Pendiente / Confirmado / Cancelado.

### Documento
- `id`: Identificador único.
- `tipo`: Acta / Certificado / Notificación.
- `propietarioId`: Referencia a perfil, ficha o usuario.
- `estado`: Generado / Enviado / Archivado.
- `url`: Ruta de almacenamiento.

## Reglas de campos

- `id`: UUID en todos los servicios.
- `fechaCreacion` y `fechaActualizacion`: timestamps con zona UTC.
- `codigo` o `referencia`: valores únicos cuando aplican.
- `estado`: usar vocabulario controlado y documentado.

## Notas

- El diccionario debe mantenerse sincronizado con los esquemas físicos y las APIs.
- Si un campo es interno a un servicio, documentarlo en el modelo local del servicio en `09-microservices/services/<svc>/data-model.md`.

