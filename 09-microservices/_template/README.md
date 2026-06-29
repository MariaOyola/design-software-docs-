# [Nombre del Servicio]

> Este archivo es una PLANTILLA. Copiar la carpeta `_template/` completa a
> `09-microservices/services/[NN-nombre-service]/` y eliminar esta línea antes de hacer commit.

> Estado: 🔴 Pendiente | Última actualización: YYYY-MM-DD
> Autor: Por definir | Equipo: Por definir

## Contexto

<!--
Describe en 2-3 párrafos:
- Qué problema resuelve este servicio dentro del sistema
- Por qué existe como servicio independiente y no como módulo de otro
- Qué bounded context representa
-->

## Contenido

### Responsabilidad principal

<!--
Una sola frase que describe qué hace este servicio.
Ejemplo: "Gestionar la identidad digital y el control de acceso de todos los usuarios del sistema."
-->

### Bounded context

<!--
Nombre del contexto de dominio al que pertenece este servicio.
Ejemplo: "Identidad y Acceso"
-->

### Base de datos

| Base de datos | Motor | Tipo |
|---|---|---|
| `[nombre_db]` | PostgreSQL | Transaccional |

### Entidades que posee

<!--
Lista las entidades de las que este servicio es dueño.
Solo este servicio puede escribir sobre ellas.
-->

```
[entidad_1]  → descripción breve
[entidad_2]  → descripción breve
```

### Owner

| Campo | Valor |
|---|---|
| Equipo responsable | Por definir |
| Repositorio de código | Por definir |

### Dependencias

**Consume de:**
```
[servicio-origen] → qué datos o eventos consume
```

**Es consumido por:**
```
[servicio-destino] → qué datos o eventos provee
```

### Estado de documentación

| Archivo | Estado |
|---|---|
| README.md | 🔴 |
| data-model.md | 🔴 |
| events.md | 🔴 |
| api-contract.md | 🔴 |
| runbook.md | 🔴 |

## Referencias

- [data-model.md](./data-model.md)
- [events.md](./events.md)
- [api-contract.md](./api-contract.md)
- [runbook.md](./runbook.md)
- [09-microservices/service-catalog.md](../../service-catalog.md)