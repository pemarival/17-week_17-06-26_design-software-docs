# Estrategia de pruebas

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Calidad | Equipo: QA / Desarrollo

## Objetivo

Asegurar que el sistema Horarios SENA cumple los requisitos funcionales y no funcionales mediante pruebas estructuradas en todos los niveles.

## Niveles de prueba

- **Unitarias:** validar lógica de negocio en módulos y servicios.
- **Integración:** verificar integración entre servicios y bases de datos.
- **Contrato:** asegurar que los APIs cumplen los contratos especificados.
- **E2E:** validar flujos críticos del usuario desde la UI hasta los servicios.
- **Performance:** medir tiempos de respuesta del motor de asignación y APIs clave.
- **Seguridad:** pruebas de autenticación, autorización y protección de datos.

## Criterios

- Cada PR debe tener pruebas unitarias asociadas.
- El código no debe reducir la cobertura de pruebas crítica del proyecto.
- Las pruebas de integración y E2E se ejecutan en `qa` y `preprod`.
- Los fallos de seguridad bloquean el despliegue.

## Herramientas sugeridas

- Frameworks de prueba: Jest, JUnit, Pytest.
- Pruebas de contratos: Pact o Postman/Newman.
- Pruebas de carga: k6, JMeter.
- Escaneo de calidad: SonarQube o herramienta equivalente.

## Flujo de pruebas

1. Desarrollo de la funcionalidad.
2. Pruebas unitarias locales.
3. Merge a rama de integración.
4. Ejecución de pipeline CI con pruebas unitarias y lint.
5. Ejecución de pruebas de integración y contratos.
6. Validación en `qa` y `preprod`.
7. Monitoreo en producción con alertas de regresión.

