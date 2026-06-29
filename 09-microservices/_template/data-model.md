# Modelo de Datos — [Nombre del Servicio]

> Este archivo es una PLANTILLA. Copiar a `09-microservices/services/[NN-nombre-service]/data-model.md`
> y eliminar esta línea antes de hacer commit.

> Estado: 🔴 Pendiente | Última actualización: YYYY-MM-DD
> Autor: Por definir | Equipo: Por definir

## Contexto

Documenta el modelo de datos transaccional de este servicio. Solo este servicio puede escribir sobre estas entidades. Para las convenciones globales de nomenclatura ver [`06-data/data-dictionary.md`](../../06-data/data-dictionary.md).

## Contenido

### Base de datos: `[nombre_db]`

---

#### `[nombre_entidad]`

> Descripción breve de qué representa esta entidad en el negocio.

| Campo | Tipo | Nulo | Descripción |
|---|---|---|---|
| `id_[entidad]` | `UUID` | No | Llave primaria |
| `[campo_1]` | `VARCHAR(N)` | No | Descripción del campo |
| `[campo_2]` | `TIMESTAMP WITH TIME ZONE` | Sí | Descripción del campo |
| `created_at` | `TIMESTAMP WITH TIME ZONE` | No | Fecha de creación |
| `updated_at` | `TIMESTAMP WITH TIME ZONE` | No | Fecha de última modificación |
| `created_by` | `UUID` | No | Usuario que creó el registro |
| `updated_by` | `UUID` | No | Usuario que modificó por última vez |

**Restricciones especiales:**
```
<!-- Si aplica, documentar restricciones como:
  - append-only (audit-service)
  - valores válidos de un campo
  - unicidad de combinación de campos
-->
```

**Relaciones:**
```
[campo_fk] → referencia lógica a [otro-servicio].[entidad].[campo]
             (no existe FK física entre BDs distintas)
```

---

<!-- Repetir el bloque anterior por cada entidad del servicio -->

## Referencias

- [README.md](./README.md) — Contexto del servicio
- [06-data/data-dictionary.md](../../06-data/data-dictionary.md) — Convenciones globales
- [02-domain/entities-and-rules.md](../../02-domain/entities-and-rules.md) — Reglas de negocio