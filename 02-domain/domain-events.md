# Eventos de Dominio

> Estado: 🟢 En progreso | Última actualización: Última actualización: 2026-06-24
> Autor: Maria  | Equipo: Por definir

## Contexto

Este documento define los eventos relevantes del dominio del sistema. Un evento de dominio representa algo que ocurrió en el negocio y que otros servicios necesitan conocer para reaccionar. No son eventos técnicos internos sino hechos significativos del proceso formativo del SENA.

Para el catálogo técnico completo de eventos con sus esquemas y tópicos, ver [`09-microservices/event-catalog.md`](../09-microservices/event-catalog.md).

## Contenido

### Qué es un evento de dominio

```
Un evento de dominio es algo que YA OCURRIÓ en el sistema.
Se nombra siempre en pasado: HorarioPublicado, ConflictoDetectado.

No es una solicitud ("publicar horario") sino un hecho ("el horario fue publicado").
Cuando ocurre, otros servicios reaccionan de forma independiente.
```

---

### Eventos por servicio emisor

#### `iam-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `UsuarioCreado` | Se registra un nuevo usuario en el sistema | `audit-service` |
| `SesionIniciada` | Un usuario se autentica exitosamente | `audit-service` |
| `SesionCerrada` | Un usuario cierra sesión o el token expira | `audit-service` |
| `RolAsignado` | Se asigna un rol a un usuario | `audit-service` |
| `TokenRevocado` | Un token es invalidado antes de su vencimiento | `audit-service` |

---

#### `reference-data-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `CatalogoActualizado` | Se modifica un valor de catálogo | `audit-service` |
| `ParametroModificado` | Se cambia un parámetro del sistema | `audit-service` |
| `CentroFormacionCreado` | Se registra un nuevo centro de formación | `audit-service` |

---

#### `academic-management-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `FichaCreada` | Se crea una nueva ficha | `scheduling-service`, `audit-service` |
| `FichaCambioEstado` | Una ficha cambia a TERMINADA o CANCELADA | `scheduling-service`, `audit-service` |
| `ProgramaActualizado` | Se modifica un programa de formación activo | `audit-service` |
| `AprendizVinculado` | Un aprendiz se matricula en una ficha | `actors-service`, `audit-service` |

---

#### `training-environment-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `AmbienteDisponible` | Un ambiente queda libre para programación | `scheduling-service` |
| `AmbienteReservado` | Se reserva un ambiente para una actividad | `scheduling-service`, `audit-service` |
| `AmbienteEnMantenimiento` | Un ambiente entra en mantenimiento | `scheduling-service`, `audit-service` |
| `MantenimientoFinalizado` | Un mantenimiento termina y el ambiente queda disponible | `scheduling-service` |
| `ReservaCancelada` | Se cancela una reserva activa | `scheduling-service`, `audit-service` |

---

#### `scheduling-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `HorarioGenerado` | El motor crea un borrador de horario para una ficha | `audit-service` |
| `HorarioPublicado` | Un coordinador publica el horario de una ficha | `document-service`, `monitoring-service`, `audit-service` |
| `ConflictoDetectado` | El validador encuentra un conflicto de ambiente o instructor | `monitoring-service`, `audit-service` |
| `ConflictoResuelto` | Un conflicto pendiente es resuelto por el coordinador | `audit-service` |
| `SesionAsignada` | Se asigna una sesión de clase a instructor y ambiente | `audit-service` |
| `InstructorReasignado` | Se cambia el instructor de una sesión ya asignada | `actors-service`, `audit-service` |

---

#### `actors-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `InstructorRegistrado` | Se crea un nuevo instructor en el sistema | `audit-service` |
| `DisponibilidadActualizada` | Un instructor actualiza su disponibilidad horaria | `scheduling-service`, `audit-service` |
| `EtapaProductivaIniciada` | Un aprendiz inicia su etapa productiva | `scheduling-service`, `audit-service` |
| `EtapaProductivaFinalizada` | Un aprendiz termina su etapa productiva | `audit-service` |

---

#### `document-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `DocumentoGenerado` | Se genera exitosamente un documento (PDF u otro) | `audit-service` |
| `NuevaVersionDocumento` | Se crea una nueva versión de un documento existente | `audit-service` |

---

#### `monitoring-service`

| Evento | Cuándo ocurre | Quién reacciona |
|---|---|---|
| `AlertaGenerada` | Un KPI supera su umbral definido | `audit-service` |
| `NotificacionEnviada` | Se envía una notificación a instructor o aprendiz | `audit-service` |
| `PlanMejoramientoCreado` | Se crea un plan de mejoramiento por desviación detectada | `audit-service` |

---

#### `audit-service`

El `audit-service` no emite eventos — solo los recibe y registra.
Es el destino final de todos los eventos relevantes del sistema.

```
audit-service consume eventos de:
  iam-service, reference-data-service, academic-management-service,
  training-environment-service, scheduling-service, actors-service,
  document-service, monitoring-service

audit-service no emite eventos hacia ningún servicio.
audit-service no recibe llamadas directas de usuarios.
```

---

### Flujo de eventos del proceso principal

El flujo más importante del sistema — desde la creación de una ficha hasta la publicación de su horario:

```
1. FichaCreada (academic-management-service)
        ↓
2. scheduling-service recibe el evento y prepara el contexto
        ↓
3. AmbienteDisponible (training-environment-service)
   DisponibilidadActualizada (actors-service)
        ↓
4. HorarioGenerado (scheduling-service)
        ↓
5. ConflictoDetectado (scheduling-service) → si hay conflictos
   ConflictoResuelto (scheduling-service) → el coordinador los resuelve
        ↓
6. HorarioPublicado (scheduling-service)
        ↓
7. document-service genera el PDF del horario
   monitoring-service inicia seguimiento de KPIs
   audit-service registra la publicación
```

## Referencias

- [entities-and-rules.md](./entities-and-rules.md) — Entidades que generan estos eventos
- [domain-map.md](./domain-map.md) — Relaciones entre servicios
- [09-microservices/event-catalog.md](../09-microservices/event-catalog.md) — Catálogo técnico de eventos