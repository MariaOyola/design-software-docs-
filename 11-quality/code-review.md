# Revisión de Código

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los criterios y el flujo para revisar Pull Requests de código en los 9 microservicios. Para revisión de documentación, ver [`00-governance/definition-of-ready.md`](../00-governance/definition-of-ready.md) y [`definition-of-done.md`](../00-governance/definition-of-done.md).

## Contenido

### Principios de revisión

```
1. Toda PR de código requiere al menos 1 aprobación antes de merge
2. El autor de la PR nunca se auto-aprueba
3. La revisión evalúa funcionalidad, legibilidad y pruebas — no solo si "funciona"
4. El revisor da feedback constructivo, no solo señala errores
```

---

### Checklist de revisión

```
[ ] El código resuelve lo que la HU o tarea técnica pedía
[ ] Existen pruebas unitarias para la lógica nueva
[ ] La cobertura de pruebas no bajó respecto a develop
[ ] El código sigue las convenciones de estilo del lenguaje
[ ] No hay código comentado o muerto dejado por error
[ ] No hay secretos, credenciales ni datos personales hardcodeados
[ ] Los nombres de variables y funciones son claros
[ ] El PR tiene una descripción clara de qué cambia y por qué
[ ] Si el cambio afecta un contrato de API, está documentado en api-contract.md
[ ] Si el cambio afecta el modelo de datos, está documentado en data-model.md
```

---

### Tamaño de los PRs

```
✅ Preferir PRs pequeños y enfocados en un solo cambio lógico
❌ Evitar PRs que mezclan refactor + feature + fix en un mismo cambio
```

Si un PR es muy grande para revisar en una sola sesión, se debe dividir en PRs más pequeños cuando sea posible.

---

### Tiempo de respuesta esperado

| Tipo de cambio | Tiempo máximo de primera revisión |
|---|---|
| Fix urgente (afecta producción) | Inmediato |
| Feature normal | 24 horas hábiles |
| Documentación | 48 horas hábiles |

---

### Qué hacer ante desacuerdos

```
1. El revisor explica claramente la razón del comentario
2. El autor responde con su perspectiva si no está de acuerdo
3. Si no hay consenso, se escala al líder técnico para decisión final
4. La decisión final se documenta como comentario en el PR
```

---

### Después de aprobar

```
1. El autor hace el merge (squash and merge preferido)
2. Se borra la rama hija
3. Si el cambio afecta a varios servicios, se notifica al equipo
```

## Referencias

- [testing-strategy.md](./testing-strategy.md) — Qué pruebas debe tener el código antes de revisión
- [00-governance/git-conventions.md](../00-governance/git-conventions.md) — Convenciones de ramas y commits
- [00-governance/definition-of-done.md](../00-governance/definition-of-done.md) — Criterios de cierre de documentación