# Backlog Técnico

> Estado: 🟡  En progreso | Última actualización: 2026-06-1
> Autor: Maria | Equipo: Por definir

## Contexto

Registro de pendientes técnicos, deuda técnica y mejoras identificadas durante el desarrollo. No es el backlog de producto (eso vive en `03-product/product-backlog.md`), sino el backlog de decisiones técnicas y mejoras internas del sistema.

## Contenido

### Deuda técnica activa

| ID | Descripción | Servicio afectado | Impacto | Prioridad |
|---|---|---|---|---|
| TK-001 | Definir RPO y RTO concretos con el SENA para backup-and-recovery.md | Todos | Riesgo operacional | 🔴 Alta |
| TK-002 | Definir tokens de diseño reales (colores, tipografía) en design-system.md | Frontend | UX inconsistente | 🟠 Media |
| TK-003 | Completar contactos del equipo en technical-onboarding.md | Todos | Onboarding lento | 🟠 Media |
| TK-004 | Registrar ADRs pendientes en 05-architecture/decisions/ | Todos | Falta trazabilidad de decisiones | 🟠 Media |
| TK-005 | Completar owners y repos en service-catalog.md | Todos | Catálogo incompleto | 🟠 Media |

---

### Pendientes post-incidente

> Esta sección se llena después de cada incidente según el proceso de
> `13-operations/incident-management.md`.

| Fecha | Incidente | Acción pendiente | Responsable | Estado |
|---|---|---|---|---|
| — | Sin incidentes registrados | — | — | — |

---

### Mejoras identificadas

| ID | Descripción | Origen | Prioridad |
|---|---|---|---|
| MJ-001 | Agregar prueba de restauración de BD cada 3 meses | backup-and-recovery.md | 🟠 Media |

---

### Cómo agregar un ítem

```
1. Asignar un ID correlativo (TK-NNN para deuda técnica, MJ-NNN para mejoras)
2. Describir el problema o mejora de forma concreta
3. Indicar servicio afectado, impacto y prioridad
4. Abrir PR en la rama feat/doc-project-control-technical-backlog
```

## Referencias

- [risks.md](./risks.md) — Riesgos del proyecto
- [open-questions.md](./open-questions.md) — Preguntas abiertas que pueden generar deuda
- [13-operations/incident-management.md](../13-operations/incident-management.md) — Origen de pendientes post-incidente