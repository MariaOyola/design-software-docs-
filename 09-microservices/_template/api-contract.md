# Contrato de API — [Nombre del Servicio]

> Este archivo es una PLANTILLA. Copiar a `09-microservices/services/[NN-nombre-service]/api-contract.md`
> y eliminar esta línea antes de hacer commit.

> Estado: 🔴 Pendiente | Última actualización: YYYY-MM-DD
> Autor: Por definir | Equipo: Por definir

## Contexto

Contrato operativo de la API de este servicio durante el desarrollo. Cuando el contrato sea estable y aprobado por arquitectura, se publica la versión OpenAPI en `07-api/contracts/openapi/[nombre-servicio].yaml`.

> Si hay diferencia entre este archivo y el de `07-api/contracts/openapi/`, el de `07-api/` tiene precedencia para consumidores externos.

## Contenido

### Base URL

```
/api/v1/[recurso-principal]
```

### Autenticación

Todos los endpoints requieren `Authorization: Bearer <token>` excepto los indicados como públicos. Ver [`07-api/authentication.md`](../../07-api/authentication.md).

---

### Endpoints

#### `GET /api/v1/[recurso]`

**Descripción:** Lista los recursos disponibles con paginación.

**Roles permitidos:** `ADMINISTRADOR`, `COORDINADOR`

**Query params:**
| Parámetro | Tipo | Requerido | Descripción |
|---|---|---|---|
| `page` | `integer` | No | Número de página (defecto: 1) |
| `size` | `integer` | No | Registros por página (defecto: 20, máx: 100) |

**Respuesta exitosa `200 OK`:**
```json
{
  "data": [ ],
  "meta": {
    "timestamp": "2026-06-21T10:00:00Z",
    "service": "[nombre-servicio]",
    "pagination": {
      "page": 1,
      "size": 20,
      "total": 0,
      "totalPages": 0
    }
  }
}
```

---

#### `GET /api/v1/[recurso]/{id}`

**Descripción:** Obtiene un recurso por su ID.

**Roles permitidos:** `ADMINISTRADOR`, `COORDINADOR`

**Path params:**
| Parámetro | Tipo | Descripción |
|---|---|---|
| `id` | `UUID` | Identificador del recurso |

**Respuesta exitosa `200 OK`:**
```json
{
  "data": { },
  "meta": {
    "timestamp": "2026-06-21T10:00:00Z",
    "service": "[nombre-servicio]"
  }
}
```

**Errores posibles:**
| Código | Cuándo |
|---|---|
| `401` | Token ausente o inválido |
| `403` | Sin permiso para esta operación |
| `404` | Recurso no encontrado |

---

#### `POST /api/v1/[recurso]`

**Descripción:** Crea un nuevo recurso.

**Roles permitidos:** `ADMINISTRADOR`, `COORDINADOR`

**Body:**
```json
{
  "[campo_1]": "valor",
  "[campo_2]": "valor"
}
```

**Respuesta exitosa `201 Created`:**
```json
{
  "data": { },
  "meta": {
    "timestamp": "2026-06-21T10:00:00Z",
    "service": "[nombre-servicio]"
  }
}
```

**Errores posibles:**
| Código | Cuándo |
|---|---|
| `400` | Datos de entrada inválidos |
| `401` | Token ausente o inválido |
| `403` | Sin permiso para esta operación |
| `409` | Conflicto con registro existente |
| `422` | Datos válidos pero violan regla de negocio |

---

<!-- Repetir el bloque anterior por cada endpoint del servicio -->

## Referencias

- [README.md](./README.md) — Contexto del servicio
- [07-api/guidelines.md](../../07-api/guidelines.md) — Lineamientos de API
- [07-api/authentication.md](../../07-api/authentication.md) — Autenticación