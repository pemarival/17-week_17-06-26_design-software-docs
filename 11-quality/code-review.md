# Revisión de código

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Calidad | Equipo: Desarrollo

## Objetivo

Garantizar calidad, coherencia y seguridad del código antes de fusionarlo a ramas compartidas.

## Proceso de revisión

1. Crear PR con descripción clara y objetivos.
2. Incluir referencias a tickets, requisitos o historias de usuario.
3. Ejecutar pipelines de CI antes de solicitar revisión.
4. Asignar al menos un revisor técnico y un revisor de QA cuando aplique.
5. Revisar:
   - Legibilidad y estilo.
   - Cumplimiento de patrones de arquitectura.
   - Cobertura de pruebas.
   - Manejo de errores y validaciones.
   - Seguridad y unión de datos.

## Criterios mínimos

- El código debe tener tests asociados.
- No deben existir comentarios de código obsoletos.
- Los cambios deben ser pequeños y atómicos.
- Los nombres deben ser descriptivos.
- Las dependencias nuevas deben estar justificadas.

## Aprobación

- Un PR puede fusionarse solo cuando todas las revisiones requeridas están aprobadas.
- Si hay comentarios abiertos, deben resolverse antes de merge.
- Documentar decisiones relevantes en el cuerpo del PR.

