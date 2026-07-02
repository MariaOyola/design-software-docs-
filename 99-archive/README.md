# Archivo

> Estado: 🟡  En progreso | Última actualización: 2026-06-1
> Autor: Maria | Equipo: Por definir

## Contexto

Contiene documentos deprecados o decisiones antiguas que ya no aplican al proyecto. **No se elimina nada de esta carpeta** — se conserva todo para trazabilidad histórica.

## Contenido

### Carpetas

| Carpeta | Descripción | Cuándo se usa |
|---|---|---|
| [deprecated/](./deprecated/) | Documentos que ya no aplican pero se conservan por historial | Cuando un documento es reemplazado por otro en su sección original |
| [old-decisions/](./old-decisions/) | Decisiones antiguas previas al formato ADR | Solo para documentos anteriores a la adopción del formato ADR |

---

### Reglas de uso

**Para documentos deprecados:**
```
1. Cambiar el estado del documento original a ⚫ Deprecado
2. Agregar al inicio del documento original:
   > Reemplazado por: [enlace al nuevo documento]
3. Dejar el documento en su ubicación original (NO moverlo aquí)
   → La excepción es cuando la sección completa fue eliminada o reestructurada

Si la sección fue eliminada:
1. Mover el documento a 99-archive/deprecated/
2. Registrar el movimiento en CHANGELOG.md
```

**Para decisiones antiguas (`old-decisions/`):**
```
Solo se mueven aquí documentos de decisión que existían
ANTES de adoptar el formato ADR.

Las ADRs en 05-architecture/decisions/records/
NUNCA se mueven aquí — se deprecan en su lugar con status: DEPRECATED.
```

---

### Qué NO va aquí

```
❌ ADRs obsoletas → se deprecan en 05-architecture/decisions/records/
❌ Documentos activos que "ya no necesito" → no se archivan, se deprecan
❌ Archivos temporales o borradores → nunca debieron existir en el repo
```

---

### Contenido actual

| Carpeta | Archivos | Estado |
|---|---|---|
| `deprecated/` | Vacío | — |
| `old-decisions/` | Vacío | — |

## Referencias

- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md) — Criterios para deprecar documentos
- [CHANGELOG.md](../CHANGELOG.md) — Registro de movimientos a este archivo
- [05-architecture/decisions/](../05-architecture/decisions/) — ADRs obsoletas van ahí, no aquí