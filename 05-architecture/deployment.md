# Despliegue

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Equipo de Infraestructura | Equipo: Operaciones / Arquitectura

## Topología de despliegue

El sistema se despliega como un conjunto de microservicios en contenedores. Cada servicio es independiente y se ejecuta en su propio espacio de nombres / cluster lógico.

### Ambientes principales

- `dev`: desarrollo local y de feature branches.
- `qa`: pruebas de integración y validación funcional.
- `preprod`: ensayo de despliegue con datos sintéticos o copia parcial de producción.
- `prod`: ambiente en vivo para usuarios finales.

## Infraestructura recomendada

- Plataforma de contenedores: Kubernetes / AKS / OpenShift.
- Registro de contenedores: Azure Container Registry (ACR) o equivalente.
- Bases de datos: PostgreSQL gestionado para cada servicio.
- Mensajería de eventos: Kafka, RabbitMQ o Azure Service Bus según el entorno.
- Almacenamiento de archivos: Blob Storage para documentos y servicios de generación de PDF.
- Observabilidad: Prometheus + Grafana / Azure Monitor.

## Componentes de despliegue

- Gateway/API: proxy que enruta llamadas hacia servicios backend.
- Servicios API: cada microservicio ofrece su propia API REST.
- Workers asíncronos: motores y validadores que procesan colas de eventos.
- Base de datos por servicio: esquemas independientes para evitar acoplamiento.
- Almacenamiento de archivos: buckets/containers separados por tipo de contenido.

## Recomendaciones de despliegue

- Desplegar cada servicio como unidad independiente.
- Usar rollouts canary o blue/green en `preprod` y `prod`.
- Mantener transformaciones de datos reversibles.
- Versionar imágenes y definir etiquetas semánticas (`service:1.0.0`, `service:main` sólo en `dev`).

## Seguridad de despliegue

- Las conexiones a base de datos deben ser privadas y cifradas.
- Variables sensibles gestionadas con Azure Key Vault o equivalente.
- El acceso al cluster debe gestionarse con RBAC y acceso mínimo.

