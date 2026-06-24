# Contexto

> Estado: 🟡 En progreso | Última actualización: 2026-06-24
> Autor: Maria | Equipo: Por definir

## Contexto

Esta carpeta describe el problema que el sistema resuelve, los límites de lo que construye y el vocabulario oficial del dominio SENA. Debe leerse antes de diseñar cualquier microservicio, escribir código o tomar decisiones de arquitectura.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [overview.md](./overview.md) | Contexto institucional del SENA, problema que resuelve el sistema y objetivos generales | 🟡 |
| [scope.md](./scope.md) | Qué hace el sistema, qué no hace, supuestos y restricciones | 🟡 |
| [glossary.md](./glossary.md) | Glosario oficial de términos del dominio SENA y del sistema | 🟡 |

### Flujo de lectura sugerido

```
¿Qué es el sistema y por qué existe?
  → overview.md

¿Qué hace y qué NO hace el sistema?
  → scope.md

¿Cómo se llama cada cosa oficialmente?
  → glossary.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Las reglas de negocio del dominio SENA | [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) |
| Los requisitos funcionales y no funcionales | [04-requirements/](../04-requirements/) |
| La arquitectura técnica del sistema | [05-architecture/overview.md](../05-architecture/overview.md) |
| Los 9 microservicios y sus responsabilidades | [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) |
| Preguntas abiertas sobre supuestos no confirmados | [15-project-control/open-questions.md](../15-project-control/open-questions.md) |

## Referencias

- [overview.md](./overview.md)
- [scope.md](./scope.md)
- [glossary.md](./glossary.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)