# Visión de producto

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Producto y Arquitectura

## Visión

**"Sistema inteligente de asignación de horarios que automatiza y centraliza la gestión de fichas de formación en el SENA, eliminando conflictos, mejorando ocupación de recursos y permitiendo decisiones basadas en datos."**

## Propuesta de valor

### Para Coordinadores de fichas
- ✅ Automatización de asignaciones complejas (ahorro 20+ horas/mes)
- ✅ Visibilidad inmediata de conflictos antes de guardar
- ✅ Notificaciones automáticas de cambios
- ✅ Reportes de ocupación por instructor y ambiente

### Para Directores de centro
- ✅ Dashboard con KPIs de eficiencia de ambientes
- ✅ Datos consolidados para toma de decisiones
- ✅ Alertas de sobrecarga de instructores
- ✅ Auditoría completa de operaciones

### Para Instructores
- ✅ Visibilidad de horarios en tiempo real
- ✅ Notificaciones de cambios en sus asignaciones
- ✅ Consulta de disponibilidad de ambientes
- ✅ Histórico de sesiones impartidas

### Para Aprendices
- ✅ Acceso a horarios de su ficha
- ✅ Alertas de cambios en jornada
- ✅ Consulta de documentos (certificados, diplomas)

## Objetivos de negocio

| Objetivo | Meta | Indicador |
|----------|------|----------|
| Reducir conflictos de asignación | 100% | Cero conflictos post-asignación |
| Mejorar ocupación de ambientes | +25% | Ambiente-hora utilizado / disponible |
| Reducir carga administrativa | -80% | Horas/mes asignación manual |
| Mejorar satisfacción de coordinadores | +40% | NPS > 40 |
| Implementar base datos centralizada | 100% | Todas fichas en sistema |
| Implementar auditoría | 100% | 100% de operaciones registradas |

## Promesa del producto

> **"Horarios SENA asigna automáticamente, valida en tiempo real y notifica cambios."**

En una sola plataforma:
1. Ingresa ficha con aprendices e instructor requerido
2. Sistema sugiere horarios sin conflictos
3. Coordinador revisa y aprueba en 2 clics
4. Todos notificados automáticamente
5. Disponible en cualquier navegador, en cualquier momento

## Diferenciadores clave

1. **Motor de asignación inteligente**
   - Respeta 8 reglas de negocio automáticamente
   - Optimiza uso de ambientes (occupancy)
   - Balancea carga de instructores

2. **Integración con ecosistema SENA**
   - Datos de referencia centralizados
   - Auditoría inmutable (normativa)
   - Multi-centro y multi-región

3. **Datos en tiempo real**
   - Dashboard de KPIs actualizado cada hora
   - Alertas inteligentes ante anomalías
   - Notificaciones a stakeholders

## Evolución esperada (18 meses)

### MVP (M1-M5, Q3 2026)
Gestión básica de fichas, competencias, ambientes, motor de asignación

### V1.0 (M6-M9, Q4 2026)
+ Instructores y aprendices, documentos, reportes básicos

### V1.5 (M10-M15, Q1-Q2 2027)
+ KPIs avanzados, alertas inteligentes, etapa productiva

### V2.0 (M16-M18, Q2-Q3 2027)
+ Integraciones externas, mobile app, analytics predictivo

## Referencias

- [01-context/overview.md](../01-context/overview.md) — Contexto institucional
- [02-domain/domain-map.md](../02-domain/domain-map.md) — Modelo de dominio
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Servicios del sistema
