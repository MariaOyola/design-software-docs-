# Requisitos

> Estado:  🟢 En progreso | Última actualización: Última actualización: 2026-06-27 | Equipo: Por definir | Equipo: Por definir

## Contexto

Centraliza los requisitos funcionales, no funcionales, historias de usuario y trazabilidad del sistema de gestión de horarios SENA. Debe leerse antes de diseñar o implementar cualquier microservicio.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [functional.md](./functional.md) | Requisitos funcionales organizados por microservicio | 🟢 |
| [non-functional.md](./non-functional.md) | Requisitos de calidad, seguridad, rendimiento y operación | 🟢 |
| [user-stories.md](./user-stories.md) | Historias de usuario con tareas técnicas por microservicio | 🟢 |
| [traceability-matrix.md](./traceability-matrix.md) | Relación entre HU, requisitos, microservicios y pruebas | 🟢 |

### Flujo de lectura sugerido

```
¿Qué debe hacer el sistema?
  → functional.md

¿Bajo qué condiciones de calidad y seguridad?
  → non-functional.md

¿Qué necesita cada actor y qué tareas técnicas implica?
  → user-stories.md

¿Qué HU implementa cada microservicio?
  → traceability-matrix.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| El contexto y alcance del sistema | [01-context/scope.md](../01-context/scope.md) |
| Las reglas de negocio que originan estos requisitos | [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) |
| Las HU de alto nivel priorizadas | [03-product/product-backlog.md](../03-product/product-backlog.md) |
| Las decisiones técnicas para cumplir los RNF | [05-architecture/decisions/](../05-architecture/decisions/) |

## Referencias

- [functional.md](./functional.md)
- [non-functional.md](./non-functional.md)
- [user-stories.md](./user-stories.md)
- [traceability-matrix.md](./traceability-matrix.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)