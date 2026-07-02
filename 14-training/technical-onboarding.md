# Onboarding Técnico

> Estado: 🟡  En progreso | Última actualización: 2026-06-30
> Autor: Maria | Equipo: Por definir

## Contexto

Guía de entrada para nuevos integrantes técnicos del proyecto. El objetivo es que en el primer día tengas el sistema corriendo localmente y entiendas cómo está organizado el proyecto.

## Contenido

### Día 1 — Configurar el entorno

```
[ ] Leer 00-governance/ completo (empieza por el README)
    → Entiende las reglas antes de tocar cualquier archivo

[ ] Seguir 10-devops/local-setup.md
    → Levanta el sistema completo en tu máquina

[ ] Verificar que los 9 servicios responden correctamente
    → Ejecuta los healthchecks de local-setup.md

[ ] Solicitar acceso a:
    → Repositorios de código de los 9 servicios
    → Repositorio de documentación (design-software-docs)
    → Herramienta de gestión de proyectos del equipo
```

---

### Día 2 — Entender el sistema

```
[ ] Leer en este orden:
    1. 01-context/overview.md         → qué problema resuelve el sistema
    2. 01-context/scope.md            → qué está dentro y qué no
    3. 02-domain/entities-and-rules.md → entidades y reglas de negocio
    4. 02-domain/domain-map.md        → cómo se relacionan los servicios
    5. 05-architecture/overview.md    → arquitectura técnica

[ ] Revisar el catálogo de servicios
    → 09-microservices/service-catalog.md

[ ] Revisar el servicio al que estás asignado
    → 09-microservices/services/[tu-servicio]/README.md
```

---

### Día 3 — Primer contribución

```
[ ] Leer 00-governance/git-conventions.md
    → Cómo crear ramas y hacer commits

[ ] Hacer tu primer commit pequeño (documentación o fix menor)
    → Sigue el flujo: feat/... → PR → develop

[ ] Leer 11-quality/testing-strategy.md
    → Qué pruebas debes escribir antes de abrir un PR

[ ] Leer 11-quality/code-review.md
    → Cómo revisar el código de otros y cómo recibir feedback
```

---

### Recursos de referencia rápida

| Pregunta | Dónde buscar |
|---|---|
| ¿Cómo se llama esta entidad del negocio? | `01-context/glossary.md` |
| ¿Qué regla aplica a esta entidad? | `02-domain/entities-and-rules.md` |
| ¿Qué endpoints tiene este servicio? | `09-microservices/services/<svc>/api-contract.md` |
| ¿Qué eventos emite este servicio? | `09-microservices/services/<svc>/events.md` |
| ¿Qué hacer si el servicio falla? | `09-microservices/services/<svc>/runbook.md` |
| ¿Cómo hago un commit? | `00-governance/git-conventions.md` |
| ¿Qué necesita un PR para aprobarse? | `00-governance/definition-of-ready.md` |
s
---

### A quién preguntarle qué

> ⚠️ Pendiente completar con los contactos reales del equipo.

| Tema | Contacto |
|---|---|
| Dudas de negocio / dominio SENA | Por definir |
| Dudas de arquitectura técnica | Por definir |
| Accesos y permisos | Por definir |
| Dudas de un microservicio específico | Owner del servicio (ver service-catalog.md) |

## Referencias

- [00-governance/](../00-governance/) — Reglas del repositorio
- [10-devops/local-setup.md](../10-devops/local-setup.md) — Configuración del entorno local
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo de servicios