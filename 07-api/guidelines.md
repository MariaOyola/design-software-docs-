# Lineamientos de API

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Define las convenciones de diseño que todos los microservicios deben seguir al exponer sus APIs. El objetivo es que cualquier consumidor pueda interactuar con cualquier servicio del sistema de forma predecible y consistente.

## Contenido

### Estilo general

El sistema usa **REST sobre HTTP**. Todos los endpoints siguen estas reglas:

```
- Rutas en kebab-case y en plural: /sesiones-clase, /centros-formacion
- Sustantivos en rutas, nunca verbos: /horarios (no /generarHorario)
- Versión en la ruta: /api/v1/horarios
- Respuestas siempre en JSON
- Charset UTF-8 en todos los responses
```

---

### Estructura de rutas

```
/api/v1/{recurso}              → colección
/api/v1/{recurso}/{id}         → recurso individual
/api/v1/{recurso}/{id}/{sub}   → subrecurso

Ejemplos reales:
GET  /api/v1/horarios
GET  /api/v1/horarios/{id}
POST /api/v1/horarios/{id}/publicar
GET  /api/v1/fichas/{id}/sesiones-clase
```

---

### Métodos HTTP

| Método | Uso | Idempotente |
|---|---|---|
| `GET` | Consultar un recurso o colección | ✅ |
| `POST` | Crear un nuevo recurso | ❌ |
| `PUT` | Reemplazar un recurso completo | ✅ |
| `PATCH` | Modificar campos específicos de un recurso | ❌ |
| `DELETE` | Eliminar un recurso | ✅ |

---

### Códigos de respuesta

| Código | Cuándo usarlo |
|---|---|
| `200 OK` | Consulta o actualización exitosa |
| `201 Created` | Recurso creado exitosamente |
| `204 No Content` | Operación exitosa sin cuerpo de respuesta |
| `400 Bad Request` | Datos de entrada inválidos |
| `401 Unauthorized` | Token ausente o inválido |
| `403 Forbidden` | Sin permiso para la operación |
| `404 Not Found` | Recurso no encontrado |
| `409 Conflict` | Conflicto con el estado actual (ej: doble reserva) |
| `422 Unprocessable Entity` | Datos válidos pero que violan reglas de negocio |
| `500 Internal Server Error` | Error interno del servicio |

---

### Formato de respuesta exitosa

```json
{
  "data": { },
  "meta": {
    "timestamp": "2026-06-21T10:30:00Z",
    "service": "scheduling-service"
  }
}
```

Para colecciones con paginación:

```json
{
  "data": [ ],
  "meta": {
    "timestamp": "2026-06-21T10:30:00Z",
    "service": "scheduling-service",
    "pagination": {
      "page": 1,
      "size": 20,
      "total": 150,
      "totalPages": 8
    }
  }
}
```

---

### Formato de respuesta de error

```json
{
  "error": {
    "code": "CONFLICT_DETECTED",
    "message": "El ambiente ya tiene una reserva activa en esa franja horaria",
    "timestamp": "2026-06-21T10:30:00Z",
    "service": "scheduling-service"
  }
}
```

---

### Paginación

Toda consulta de colecciones debe soportar paginación por parámetros de query:

```
GET /api/v1/fichas?page=1&size=20&sort=fecha_inicio&order=desc

Parámetros:
  page   → número de página (desde 1)
  size   → registros por página (máximo 100, defecto 20)
  sort   → campo por el que ordenar
  order  → asc | desc
```

---

### Filtros

Los filtros se pasan como query parameters:

```
GET /api/v1/fichas?estado=EJECUCION&programa=123&jornada=DIURNA
```

---

### Versionado

La versión va en la ruta, no en el header:

```
✅ /api/v1/horarios
❌ Header: API-Version: 1
```

Cuando se introduce una versión nueva (`v2`), la versión anterior se mantiene activa durante un período de deprecación acordado con los consumidores.

## Referencias

- [authentication.md](./authentication.md) — Autenticación y autorización
- [contracts/openapi/](./contracts/openapi/) — Contratos OpenAPI publicables
- [05-architecture/cross-cutting.md](../05-architecture/cross-cutting.md) — Aspectos transversales de seguridad y errores
- [09-microservices/services/](../09-microservices/services/) — Contratos de implementación por servicio