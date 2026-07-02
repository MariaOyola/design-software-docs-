# Dependencias

> Estado: 🟡  En progreso | Última actualización: 2026-06-1
> Autor: Maria| Equipo: Por definir

## Contexto

Registro de dependencias internas entre microservicios y dependencias externas del proyecto. Permite identificar qué debe estar listo antes de construir cada parte del sistema.

## Contenido

### Dependencias entre microservicios

| Servicio | Depende de | Tipo | Descripción |
|---|---|---|---|
| `todos los servicios` | `iam-service` | REST síncrono | Validación de token en cada solicitud |
| `academic-management-service` | `reference-data-service` | REST síncrono | Centros de formación y catálogos |
| `training-environment-service` | `reference-data-service` | REST síncrono | Centros de formación y catálogos |
| `actors-service` | `reference-data-service` | REST síncrono | Catálogos y estados |
| `scheduling-service` | `academic-management-service` | REST síncrono + eventos | Datos de fichas y programas |
| `scheduling-service` | `training-environment-service` | REST síncrono + eventos | Disponibilidad de ambientes |
| `scheduling-service` | `actors-service` | REST síncrono + eventos | Disponibilidad de instructores |
| `document-service` | `scheduling-service` | Eventos | Consume HorarioPublicado para generar PDF |
| `monitoring-service` | `scheduling-service` | Eventos | Consume HorarioPublicado y ConflictoDetectado |
| `audit-service` | `todos los servicios` | Eventos | Consume eventos de todos para registro inmutable |

---

### Orden de construcción requerido

Por las dependencias anteriores, los servicios deben construirse en este orden:

```
Fase 1 (base):
  iam-service
  reference-data-service

Fase 2 (datos):
  academic-management-service
  training-environment-service
  actors-service

Fase 3 (core):
  scheduling-service

Fase 4 (transversales):
  document-service
  monitoring-service
  audit-service
```

---

### Dependencias externas

| Dependencia | Tipo | Para qué | Estado |
|---|---|---|---|
| PostgreSQL | Base de datos | Motor de BD para los 9 servicios | ⚠️ Por definir versión |
| Sistema de mensajería (cola de eventos) | Infraestructura | Comunicación asíncrona entre servicios | ⚠️ Por definir — ADR pendiente |
| Servicio de email / push notifications | Externo | Notificaciones a instructores y aprendices | ⚠️ Por definir |
| Sofia Plus (sistema legado SENA) | Externo | Fuera de alcance en esta versión | ❌ No aplica v1 |

---

### Dependencias de documentación

Algunas secciones del repo dependen de que otras estén completas:

| Sección | Depende de |
|---|---|
| `04-requirements/traceability-matrix.md` | `03-product/product-backlog.md` |
| `09-microservices/services/` | `05-architecture/decisions/` (ADR aprobada) |
| `06-data/models.md` | `02-domain/entities-and-rules.md` |
| `07-api/contracts/openapi/` | `09-microservices/services/<svc>/api-contract.md` |

## Referencias

- [risks.md](./risks.md) — Riesgos derivados de dependencias
- [technical-backlog.md](./technical-backlog.md) — Pendientes para resolver dependencias
- [03-product/roadmap.md](../03-product/roadmap.md) — Orden de entrega que respeta dependencias