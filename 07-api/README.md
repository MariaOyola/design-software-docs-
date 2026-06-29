# API

> Estado: 🟢 En progreso | Última actualización: 2026-06-28
> Autor: Maria 
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los lineamientos de diseño de APIs, la estrategia de autenticación y la ubicación de los contratos OpenAPI del sistema de gestión de horarios SENA.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [guidelines.md](./guidelines.md) | Convenciones de diseño de APIs: rutas, métodos, respuestas y paginación | 🟢 |
| [authentication.md](./authentication.md) | Estrategia de autenticación JWT y autorización por roles | 🟢 |
| [contracts/openapi/](./contracts/openapi/) | Contratos OpenAPI validados y publicables por servicio | 🔴 |

### Dónde va cada contrato

| Tipo de contrato | Dónde vive | Cuándo se usa |
|---|---|---|
| Contrato de implementación (borrador, en evolución) | `09-microservices/services/<svc>/api-contract.md` | Durante el desarrollo del servicio |
| Contrato OpenAPI publicable (estable, revisado) | `07-api/contracts/openapi/<svc>.yaml` | Cuando el contrato es estable y puede compartirse con consumidores externos |

> **Regla:** el contrato en `07-api/contracts/openapi/` es la versión aprobada por arquitectura. Si hay diferencia entre ambos, el de `07-api/` tiene precedencia para consumidores externos.

### Flujo de lectura sugerido

```
¿Cómo se diseñan las rutas y respuestas de un endpoint?
  → guidelines.md

¿Cómo se autentica un usuario o un servicio?
  → authentication.md

¿Cuál es el contrato oficial de un servicio específico?
  → contracts/openapi/<nombre-servicio>.yaml
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Aspectos transversales de seguridad y errores | [05-architecture/cross-cutting.md](../05-architecture/cross-cutting.md) |
| Contrato de implementación de un servicio específico | [09-microservices/services/](../09-microservices/services/) |
| Implementación de autenticación | [09-microservices/services/01-iam-service/](../09-microservices/services/01-iam-service/) |

## Referencias

- [guidelines.md](./guidelines.md)
- [authentication.md](./authentication.md)
- [contracts/openapi/](./contracts/openapi/)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)