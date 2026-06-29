# Datos

> Estado: 🟢 En progreso | Última actualización: 2026-06-2
> Autor: Por definir | Equipo: Por definir

## Contexto

Documenta los modelos de datos, diccionario y estrategia de migración del sistema de gestión de horarios SENA.

> **Diferencia con `02-domain`:** allá se describen las entidades de negocio y sus reglas. Aquí se describe cómo esas entidades se implementan en bases de datos: tablas, columnas, tipos y relaciones.

> **Diferencia con `09-microservices`:** aquí vive el modelo de datos global del sistema — diccionario conceptual compartido y estrategia de migración. El modelo transaccional propio de cada servicio se documenta en `09-microservices/services/<servicio>/data-model.md`. No duplicar: si un concepto es solo del servicio, va allá; si es compartido entre varios servicios, va aquí.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [models.md](./models.md) | Panorama general de las 9 BDs y sus entidades | 🟢 |
| [data-dictionary.md](./data-dictionary.md) | Convenciones globales de nomenclatura y campos compartidos | 🟢 |
| [migration-strategy.md](./migration-strategy.md) | Estrategia para cambios y migraciones de datos | 🟢 |

### Flujo de lectura sugerido

```
¿Qué BD tiene cada servicio y qué entidades contiene?
  → models.md

¿Cómo se nombran los campos y qué convenciones aplican a todos?
  → data-dictionary.md

¿Cómo se gestiona un cambio en el esquema de una BD?
  → migration-strategy.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Definición de negocio de cada entidad | [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) |
| Esquema específico de tablas de un servicio | [09-microservices/services/](../09-microservices/services/) |
| Decisiones técnicas sobre persistencia | [05-architecture/decisions/](../05-architecture/decisions/) |

## Referencias

- [models.md](./models.md)
- [data-dictionary.md](./data-dictionary.md)
- [migration-strategy.md](./migration-strategy.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)