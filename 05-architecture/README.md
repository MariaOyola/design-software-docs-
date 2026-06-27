# Arquitectura

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Describe la arquitectura del sistema de gestión de horarios SENA, su topología de despliegue, decisiones técnicas y aspectos transversales. Debe leerse antes de implementar cualquier microservicio o tomar decisiones de infraestructura.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [overview.md](./overview.md) | Vista general de arquitectura y componentes | 🟡 |
| [deployment.md](./deployment.md) | Topología de despliegue y ambientes | 🟡 |
| [cross-cutting.md](./cross-cutting.md) | Seguridad, logging, auditoría y manejo de errores | 🟡 |
| [decisions/](./decisions/) | Registro de decisiones de arquitectura (ADR) | 🔴 |

### Architecture Decision Records (ADR)

#### Convenciones

- Formato: `ADR-NNN-titulo-corto.md`
- Los ADRs **nunca se eliminan ni se mueven** — permanecen en `records/` con `status: DEPRECATED`
- Cuando una ADR queda obsoleta: cambiar su estado a `DEPRECATED` y agregar al inicio del archivo `> Reemplazada por: ADR-NNN-nueva.md`
- `99-archive/old-decisions/` se usa solo para documentos de decisión anteriores al formato ADR
- Numeración secuencial desde `ADR-001`

#### Cómo crear una ADR

```bash
cp 05-architecture/decisions/_template-adr.md \
   05-architecture/decisions/records/ADR-NNN-titulo-corto.md
```

#### Registro de ADRs

| ADR | Título | Estado |
|---|---|---|
| — | Sin ADRs registradas aún | — |

### Flujo de lectura sugerido

```
¿Cómo está organizado el sistema?
  → overview.md

¿Cómo se despliega?
  → deployment.md

¿Qué aplica a todos los servicios por igual?
  → cross-cutting.md

¿Por qué se tomó una decisión técnica específica?
  → decisions/records/ADR-NNN-titulo.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Requisitos no funcionales que originan estas decisiones | [04-requirements/non-functional.md](../04-requirements/non-functional.md) |
| Modelos de datos de cada servicio | [06-data/models.md](../06-data/models.md) |
| Estándares de API | [07-api/guidelines.md](../07-api/guidelines.md) |
| Diagramas del sistema | [08-uml/](../08-uml/) |
| Documentación de cada microservicio | [09-microservices/services/](../09-microservices/services/) |

## Referencias

- [overview.md](./overview.md)
- [deployment.md](./deployment.md)
- [cross-cutting.md](./cross-cutting.md)
- [decisions/README.md](./decisions/README.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)