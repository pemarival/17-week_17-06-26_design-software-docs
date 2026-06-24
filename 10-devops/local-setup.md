# Configuración local

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de DevOps | Equipo: Desarrollo

## Requisitos previos

- Git
- Node.js / Java / Python según los servicios del repo
- Docker
- Kubernetes local (Docker Desktop, Minikube o Kind)
- Editor de código (VS Code recomendado)
- Herramientas de base de datos (pgAdmin, Azure Data Studio, DBeaver)

## Arranque del entorno local

1. Clonar el repositorio.
2. Copiar el archivo de variables de entorno de ejemplo `.env.example` a `.env`.
3. Ajustar valores de conexión a base de datos local y endpoints de servicios.
4. Levantar dependencias locales:
   - Base de datos PostgreSQL
   - Broker de mensajes (RabbitMQ / Kafka local)
   - Almacenamiento local para archivos

## Ejecutar los servicios

- En modo local, ejecutar cada servicio con su comando de desarrollo:
  - `npm run dev` o `yarn dev`
  - `gradle bootRun`
  - `python -m uvicorn app.main:app --reload`
- Asegurar que cada servicio se conecte a su base de datos local.

## Pruebas locales

- Ejecutar pruebas unitarias con `npm test`, `gradle test` o `pytest`.
- Ejecutar pruebas de contrato contra los endpoints locales.

## Notas

- Mantener las credenciales fuera del repositorio.
- Sincronizar la configuración con el `README.md` del repositorio raíz si hay detalles adicionales.

