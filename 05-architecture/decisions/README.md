# Architecture Decision Records (ADR)

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Registro de todas las decisiones de arquitectura del sistema de gestión de horarios SENA. Los ADRs documentan qué se decidió, por qué y qué alternativas se descartaron. Son la memoria técnica del proyecto.

## Contenido

### Convenciones

- Formato: `ADR-NNN-titulo-corto.md`
- Los ADRs **nunca se eliminan ni se mueven** — permanecen en `records/` con `status: DEPRECATED`
- Cuando una ADR queda obsoleta: cambiar su estado a `DEPRECATED` y agregar al inicio del archivo:
  ```
  > Reemplazada por: ADR-NNN-nueva.md
  ```
- `99-archive/old-decisions/` se usa solo para documentos de decisión que existían antes de adoptar el formato ADR
- Numeración secuencial desde `ADR-001`


### Estados válidos de un ADR

| Estado | Significado |
|---|---|
| `PROPOSED` | En discusión, aún no aprobada |
| `ACCEPTED` | Aprobada y vigente |
| `DEPRECATED` | Reemplazada por otra ADR — nunca se elimina |
| `REJECTED` | Evaluada y descartada — se conserva para trazabilidad |

### Registro de ADRs

| ADR | Título | Estado |
|---|---|---|
| — | Sin ADRs registradas aún | — |

> Cada ADR nueva debe agregarse a esta tabla antes de cerrar su PR.

## Referencias

- [_template-adr.md](./_template-adr.md) — Plantilla para nuevas ADRs
- [../overview.md](../overview.md) — Vista general de arquitectura
- [../cross-cutting.md](../cross-cutting.md) — Aspectos transversales
- [../../04-requirements/non-functional.md](../../04-requirements/non-functional.md) — Requisitos que originan estas decisiones