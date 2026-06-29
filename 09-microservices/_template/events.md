# Eventos — [Nombre del Servicio]

> Este archivo es una PLANTILLA. Copiar a `09-microservices/services/[NN-nombre-service]/events.md`
> y eliminar esta línea antes de hacer commit.

> Estado: 🔴 Pendiente | Última actualización: YYYY-MM-DD
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los eventos que este servicio emite y los que consume de otros servicios. Para el catálogo completo de eventos del sistema ver [`02-domain/domain-events.md`](../../02-domain/domain-events.md).

## Contenido

### Eventos que emite

| Evento | Cuándo ocurre | Datos que lleva | Quién lo consume |
|---|---|---|---|
| `[NombreEvento]` | Descripción del momento | `{ campo: tipo }` | `[servicio-consumidor]` |

---

### Eventos que consume

| Evento | Viene de | Qué hace con él |
|---|---|---|
| `[NombreEvento]` | `[servicio-emisor]` | Descripción de la reacción |

---

### Notas

<!--
Si este servicio no emite eventos, indicarlo explícitamente.
Ejemplo: audit-service no emite eventos — solo los recibe y registra.

Si este servicio no consume eventos, indicarlo también.
-->

## Referencias

- [README.md](./README.md) — Contexto del servicio
- [02-domain/domain-events.md](../../02-domain/domain-events.md) — Catálogo de eventos de dominio
- [09-microservices/communication-patterns.md](../communication-patterns.md) — Patrones de comunicación