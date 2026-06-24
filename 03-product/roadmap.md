# Roadmap de producto

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Por definir | Equipo: Producto

## Timeline de alto nivel

```
Q3 2026         Q4 2026         Q1 2027         Q2-Q3 2027
├─ MVP          ├─ V1.0         ├─ V1.5         ├─ V2.0
│  (M1-5)       │  (M6-9)       │  (M10-15)      │  (M16-18)
│               │               │                │
│  ✅ Fichas    │  ✅ Actores   │  ✅ KPIs       │  ✅ Mobile
│  ✅ Motor     │  ✅ Docs      │  ✅ Alertas    │  ✅ Integraciones
│  ✅ Conflicto │  ✅ Reports   │  ✅ Etapa Prod │  ✅ Analytics
└────────────────┴────────────────┴────────────────┴────────────────
```

## Fases detalladas

### **Fase 1: MVP (Julio - Agosto 2026)**

**Hito:** Sistema básico de asignación sin conflictos

#### Sprint 1 (Semana 1-2)
- [ ] Infraestructura base (BD, APIs, eventos)
- [ ] Servicio de referencia (centros, parámetros)
- [ ] Servicio de ambientes
- [ ] Servicio de gestión académica (programas, competencias, fichas)

#### Sprint 2 (Semana 3-4)
- [ ] Servicio de actores (instructores, aprendices básico)
- [ ] Motor de asignación (motor de scheduling)
- [ ] Validación de conflictos
- [ ] API REST de horarios

#### Sprint 3 (Semana 5-6)
- [ ] Servicio de auditoría
- [ ] UI web básica (coordinador)
- [ ] Tests, documentación API
- [ ] Deploy a staging

#### Sprint 4 (Semana 7-8)
- [ ] Pruebas de carga
- [ ] Hardening de seguridad
- [ ] Entrenamiento de usuarios piloto
- [ ] Pilot con 1-2 centros

**Entregables:** 
- Código en GitHub
- APIs documentadas (OpenAPI)
- UI funcional (coordinadores asignan horarios)
- Auditoría registra operaciones

**KPI de éxito:**
- 100% asignaciones sin conflictos
- Performance: < 2s para asignar ficha típica
- Uptime: 99.5% en staging

---

### **Fase 2: V1.0 (Septiembre - Octubre 2026)**

**Hito:** Sistema completo con documentos, reportes y notificaciones

#### Sprint 5-6 (Semana 9-12)
- [ ] Servicio de actores (instructor + aprendiz completo)
- [ ] Servicio de documentos (plantillas, generación PDF)
- [ ] Servicio de notificaciones (email, SMS)
- [ ] UI para instructores (consultar horarios)

#### Sprint 7-8 (Semana 13-16)
- [ ] Reportes de horarios (PDF)
- [ ] Reportes de ocupación por ambiente
- [ ] Reportes de carga de instructor
- [ ] Dashboard básico para director

**Entregables:**
- Documentos generados automáticamente
- Notificaciones a usuarios
- Reportes operacionales
- UI para 3 roles (coordinador, instructor, director)

**KPI de éxito:**
- 95% de fichas con horarios completos en < 24h
- Satisfacción coordinadores: NPS > 30
- Disponibilidad: 99.9%

---

### **Fase 3: V1.5 (Noviembre 2026 - Marzo 2027)**

**Hito:** Inteligencia de datos y monitoreo

#### Sprint 9-12 (Semana 17-28)
- [ ] Servicio de monitoreo (KPIs)
- [ ] Cálculo automático de métricas (ocupación, carga)
- [ ] Alertas inteligentes (umbral sobrecarga)
- [ ] Dashboard avanzado (gráficos, tendencias)
- [ ] Etapa productiva (empresas, bitácora)
- [ ] API para consultas analíticas

**Entregables:**
- KPIs calculados diariamente
- Dashboard con 5+ gráficos
- Alertas automáticas por email
- Gestión de etapa productiva

**KPI de éxito:**
- Ocupación promedio ambientes: 75%+
- Carga promedio instructor: < 25 h/semana
- Reducción tiempo asignación: -70%

---

### **Fase 4: V2.0 (Abril - Junio 2027)**

**Hito:** Expansión a mobile, integraciones externas, analytics predictivo

#### Sprint 13-18 (Semana 29-40)
- [ ] App mobile (iOS, Android)
- [ ] Integración con calendario (Google, Outlook)
- [ ] Analytics predictivo (ML: predicción demanda)
- [ ] API de terceros (webhook, webhooks)
- [ ] Soporte multi-idioma (ES, EN)
- [ ] Optimizaciones de performance

**Entregables:**
- Aplicación móvil nativa
- Integraciones de calendario
- Recomendaciones predictivas
- Public APIs para partners

**KPI de éxito:**
- Adopción mobile: > 40% de usuarios
- Precisión predictiva: > 85%
- NPS coordinadores: > 45

---

## Hitos críticos por trimestre

| Trimestre | Hito | Dependencia |
|-----------|------|-------------|
| Q3 2026 | MVP con motor de asignación | Infraestructura ✅ |
| Q4 2026 | V1.0 con documentos | MVP ✅ |
| Q1 2027 | V1.5 con KPIs | V1.0 ✅ |
| Q2 2027 | V2.0 con mobile | V1.5 ✅ |

## Riesgos y mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|--------|------------|
| Retraso en desarrollo del motor | MEDIA | ALTO | Sprint adicional en Q3 |
| Baja adopción en pilotos | BAJA | MEDIO | Entrenamiento previo, soporte |
| Performance bajo en prod | BAJA | ALTO | Load testing mensual |
| Cambio en requisitos SENA | MEDIA | ALTO | Reviews quincenales con sponsor |
| Falta de datos históricos | MEDIA | MEDIO | ETL preparado para migración |

## Referencias

- [03-product/vision.md](./vision.md) — Visión de negocio
- [04-requirements/functional.md](../04-requirements/functional.md) — Requisitos funcionales
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Servicios por fase
