# Reglas de límites entre servicios

> Estado: 🟡 En progreso
> Última actualización: 2026-06-22
> Autor: Por definir
> Equipo: Por definir

---

## Principios

1. **Autonomía:** Cada servicio es independiente; cambios internos no afectan otros.
2. **Aislamiento de datos:** No compartir BDs ni acceder directamente a tablas ajenas.
3. **Comunicación clara:** APIs bien definidas (REST, gRPC, eventos).
4. **Responsabilidad única:** Un servicio = un contexto de dominio.
5. **Contrato estable:** APIs son contrato; breaking changes requieren versionado.

---

## Límites permitidos

### ✅ Comunicación entre servicios

#### 1. REST (Lectura)

```text id="restok"
Scheduling
   ↓ GET /api/v1/fichas/{fichaId}
academic-management-service
```

#### 2. gRPC (Operaciones internas pesadas)

```text id="grpca"
Scheduling
   ↓ GetRaps(rapIds)
academic-management-service
```

#### 3. Eventos asíncronos

```text id="evtok"
Academic publica: FichaCreada

├─ Scheduling escucha + reacciona
└─ Audit escucha + registra
```

#### 4. Caché distribuido (Redis)

```text id="cache1"
Scheduling cachea lista de competencias
↓
Escucha CompetenciaModificada
↓
Invalida caché

TTL máximo: 4 horas
```

#### 5. Suscripción a eventos

```text id="audit1"
Audit escucha TODOS los eventos

• No modifica datos
• Solo registra
• Append-only
```

---

## Límites prohibidos

### ❌ Acceso directo a BD

```javascript id="dbforbid"
// PROHIBIDO
const fichas = db.query(`
SELECT * FROM academic_db.fichas
WHERE fichaId = $1
`);

// ← acceso directo a tabla ajena


// PERMITIDO
const ficha =
await academicService.getFicha(fichaId);
```

---

### ❌ Transacciones distribuidas

```javascript id="trxforbid"
// PROHIBIDO

const trx = db.transaction();

try {
  await scheduling.createHorario(trx);
  await academic.updateFicha(trx);

  await trx.commit();

} catch {
  await trx.rollback();
}


// PERMITIDO

const horario =
await scheduling.createHorario();

Scheduling publica HorarioAsignado

→ Academic escucha
→ Actualiza caché

Consistencia eventual (<5s)
```

---

### ❌ Compartir estructuras de datos

```typescript id="dtoforbid"
// PROHIBIDO

interface Ficha {
  id: string;

  academicData: {
    programa: string;
    competencias: Competencia[];
  };

  schedulingData: {
    horarios: Horario[];
  };
}


// PERMITIDO

interface FichaDTO {
  id: string;
  programa: string;
  coordinador: string;
}

interface HorarioDTO {
  id: string;
  fichaId: string;
  franja: string;
}
```

---

### ❌ Breaking changes sin versionado

```typescript id="versionforbid"
// PROHIBIDO

interface CompetenciaV2 {
  id: string;
  nombre: string;

  // especialidad eliminado
}


// PERMITIDO

GET /api/v1/competencias/{id}

GET /api/v2/competencias/{id}


// Alternativa:
Accept:
application/vnd.competencia+json;version=2
```

---

### ❌ Sincronización de datos en tiempo real entre BDs

```javascript id="repforbid"
// PROHIBIDO

Replication {
 source: academic_db,
 target: scheduling_db,
 mode: "real-time"
}


// PERMITIDO

Scheduling cachea datos académicos

↓

Escucha CompetenciaModificada

↓

Invalida caché
```

---

## Límites por tipo de dato

### Datos de referencia (Change rarely)

* Dueño: `reference-data-service`
* Estrategia: caché distribuido (TTL 24h)
* Acceso: REST + caché

Ejemplo: Centros, parámetros

---

### Datos transaccionales (Change often)

* Dueño: servicio específico
* Estrategia: lectura por API, cambios por eventos
* Acceso: REST + eventos

Ejemplo: Horarios, fichas, instructores

---

### Datos de auditoría (Write-only append)

* Dueño: `audit-service`
* Estrategia: append-only
* Acceso: evento → BD interna

Ejemplo: Registro de auditoría

---

### Datos calculados (Recomputable)

* Dueño: servicio que calcula
* Estrategia: caché corto (1–4h)
* Acceso: REST + recálculo

Ejemplo: KPIs, métricas

---

## Patrones de evolución

### Agregar un campo a API

1. Crear campo nuevo en v2
2. Mantener v1
3. Migración gradual
4. Deprecar v1 después de 3 meses

---

### Agregar un servicio nuevo

1. Definir bounded context
2. Planificar replicación
3. Definir eventos publicados/suscritos
4. Crear BD propia
5. Integrar por APIs/eventos
6. Documentar en `service-catalog.md`

---

### Refactorizar responsabilidad

1. Crear servicio nuevo
2. Servicio antiguo replica datos
3. Clientes migran
4. Desmantelar responsabilidad vieja
5. Deprecar servicio antiguo

---

## Anti-patrones a evitar

| Anti-patrón                    | Consecuencia           | Alternativa          |
| ------------------------------ | ---------------------- | -------------------- |
| Servicio consulta 5+ servicios | Lentitud, acoplamiento | Replicar vía eventos |
| Evento > 10KB                  | Latencia               | Enviar ID            |
| Circuito abierto > 30s         | Cascada de fallos      | Caché + degradación  |
| Transacción distribuida        | Deadlocks              | Saga                 |
| Compartir BD                   | Acoplamiento           | Una BD por servicio  |
| Cadena síncrona A→B→C→D        | Timeouts               | Eventos              |
| Ignorar versionado             | Breaking changes       | `/v1`, `/v2`         |

---

## Checklist de compliance

Antes de crear un servicio nuevo o cambiar límites:

* [ ] ¿Cada servicio tiene su propia BD?
* [ ] ¿Los cambios viajan por APIs o eventos?
* [ ] ¿Hay versionado para breaking changes?
* [ ] ¿Está documentado en `dependency-map.md`?
* [ ] ¿Está registrado en `service-catalog.md`?
* [ ] ¿Tiene eventos en `event-catalog.md`?
* [ ] ¿Usa caché distribuido cuando aplica?
* [ ] ¿Tiene circuit breaker?
* [ ] ¿Está claro el bounded context?
