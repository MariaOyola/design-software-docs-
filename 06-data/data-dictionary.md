# Diccionario de Datos

> Estado: 🟢 En progreso | Última actualización: 2026-06-2
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los campos compartidos y convenciones de nomenclatura que aplican a todas las bases de datos del sistema. Los campos específicos de cada servicio se documentan en `09-microservices/services/<servicio>/data-model.md`.

> No duplicar: si un campo es solo del servicio, va en su `data-model.md`. Si es una convención que aplica a todos, va aquí.

## Contenido

### Convenciones globales de nomenclatura

| Convención | Regla | Ejemplo |
|---|---|---|
| Nombres de tablas | `snake_case`, singular | `sesion_clase`, `centro_formacion` |
| Nombres de columnas | `snake_case` | `fecha_inicio`, `id_instructor` |
| Llaves primarias | `id_[nombre_tabla]` con tipo UUID | `id_ficha UUID` |
| Llaves foráneas | `id_[tabla_referenciada]` | `id_ambiente UUID` |
| Fechas | `TIMESTAMP WITH TIME ZONE` para momentos, `DATE` para fechas sin hora | `fecha_inicio DATE` |
| Estados | `VARCHAR` con valores controlados en catálogo | `estado VARCHAR(20)` |
| Booleanos | `BOOLEAN` con valor por defecto explícito | `activo BOOLEAN DEFAULT true` |

---

### Campos de auditoría base

Toda tabla del sistema debe incluir estos campos de trazabilidad:

| Campo | Tipo | Descripción |
|---|---|---|
| `created_at` | `TIMESTAMP WITH TIME ZONE` | Fecha y hora de creación del registro |
| `updated_at` | `TIMESTAMP WITH TIME ZONE` | Fecha y hora de última modificación |
| `created_by` | `UUID` | ID del usuario que creó el registro |
| `updated_by` | `UUID` | ID del usuario que modificó por última vez |

> **Excepción:** `audit_db.auditoria` no tiene `updated_at` ni `updated_by`
> porque es append-only — sus registros nunca se modifican.

---

### Campos de estado comunes

Los estados de las entidades principales usan valores controlados por `ref_db.catalogo`:

| Entidad | Estados válidos |
|---|---|
| `ficha` | `EJECUCION`, `TERMINADA`, `CANCELADA` |
| `horario` | `BORRADOR`, `EN_REVISION`, `PUBLICADO` |
| `ambiente` | `DISPONIBLE`, `EN_MANTENIMIENTO`, `INACTIVO` |
| `instructor` | `ACTIVO`, `INACTIVO` |
| `aprendiz` | `ACTIVO`, `ETAPA_PRODUCTIVA`, `CERTIFICADO`, `RETIRADO` |
| `conflicto` | `PENDIENTE`, `RESUELTO` |
| `mantenimiento` | `PROGRAMADO`, `EN_CURSO`, `FINALIZADO` |

---

### Tipos de ambiente

El campo `tipo` de la entidad `ambiente` acepta los siguientes valores:

| Valor | Descripción |
|---|---|
| `LABORATORIO` | Espacio con equipos especializados |
| `TALLER` | Espacio para trabajo práctico manual |
| `AULA` | Salón de clases convencional |
| `CAMPO` | Espacio al aire libre (deportivo, agropecuario) |
| `VIRTUAL` | Ambiente de formación en línea |

---

### Tipos de vínculo de instructor

| Valor | Descripción |
|---|---|
| `PLANTA` | Empleado directo del SENA |
| `CONTRATO` | Vinculado por contrato de prestación de servicios |
| `HORA_CATEDRA` | Vinculado por horas específicas de cátedra |

---

### Identificadores externos

Algunos servicios referencian IDs de otros servicios. Convención:

```
El campo que referencia un ID externo usa el mismo nombre
que la llave primaria del servicio dueño.

Ejemplo:
  scheduling_db.asignacion.id_instructor
  → referencia actors_db.instructor.id_instructor

  scheduling_db.asignacion.id_ambiente
  → referencia env_db.ambiente.id_ambiente
```

Estas referencias son lógicas — no existen foreign keys entre BDs distintas.

## Referencias

- [models.md](./models.md) — Modelos de datos por servicio
- [migration-strategy.md](./migration-strategy.md) — Estrategia de migraciones
- [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) — Definición de negocio de cada entidad
- [09-microservices/services/](../09-microservices/services/) — Data models específicos por servicio