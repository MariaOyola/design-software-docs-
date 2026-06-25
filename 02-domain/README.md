# Dominio

> Estado: 🟢 En progreso |  Última actualización: 2026-06-24
> Autor: Maria  | Equipo: Por definir

## Contexto

Esta carpeta define el modelo de dominio del sistema de gestión de horarios del SENA: las entidades del negocio, sus reglas y los eventos que las conectan. Debe leerse antes de diseñar cualquier microservicio o modelo de datos.

> **Diferencia con `06-data`:** esta sección describe el dominio en términos de negocio (entidades, reglas, lenguaje ubicuo). No describe tablas, columnas ni esquemas de base de datos. Esos detalles van en [`06-data/`](../06-data/).

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [entities-and-rules.md](./entities-and-rules.md) | Entidades del dominio y reglas de negocio organizadas por microservicio | 🟢 |
| [domain-map.md](./domain-map.md) | Jerarquía y relaciones entre entidades y entre microservicios | 🟢 |
| [domain-events.md](./domain-events.md) | Eventos de dominio, quién los emite y quién reacciona | 🟢 |

### Flujo de lectura sugerido

```
¿Qué entidades existen y qué reglas las gobiernan?
  → entities-and-rules.md

¿Cómo se relacionan las entidades entre sí?
  → domain-map.md

¿Qué ocurre cuando algo cambia en el sistema?
  → domain-events.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Definición oficial de cada término | [01-context/glossary.md](../01-context/glossary.md) |
| Implementación técnica en BD | [06-data/models.md](../06-data/models.md) |
| Catálogo técnico de eventos | [09-microservices/event-catalog.md](../09-microservices/event-catalog.md) |
| Documentación de cada microservicio | [09-microservices/services/](../09-microservices/services/) |
| Requisitos funcionales derivados | [04-requirements/functional.md](../04-requirements/functional.md) |

## Referencias

- [entities-and-rules.md](./entities-and-rules.md)
- [domain-map.md](./domain-map.md)
- [domain-events.md](./domain-events.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)