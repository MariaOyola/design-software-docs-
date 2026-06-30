# DevOps

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria
> Autor: Por definir | Equipo: Por definir

## Contexto

Documenta la instalación local, el pipeline de CI/CD y los ambientes del proyecto.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [local-setup.md](./local-setup.md) | Preparación del entorno local de desarrollo | 🟡 |
| [ci-cd.md](./ci-cd.md) | Pipelines, despliegues y controles de calidad automatizados | 🟡 |
| [environments.md](./environments.md) | Ambientes, propósito y reglas de uso | 🟡 |

### Flujo de lectura sugerido

```
¿Cómo levanto el sistema en mi máquina?
  → local-setup.md

¿Cómo se despliega el código entre ambientes?
  → ci-cd.md

¿Qué diferencia hay entre develop, qa, stg y main?
  → environments.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Convenciones de ramas y commits | [00-governance/git-conventions.md](../00-governance/git-conventions.md) |
| Topología de despliegue técnica | [05-architecture/deployment.md](../05-architecture/deployment.md) |
| Estrategia de pruebas | [11-quality/testing-strategy.md](../11-quality/testing-strategy.md) |
| Qué hacer si algo falla en producción | [13-operations/](../13-operations/) |

## Referencias

- [local-setup.md](./local-setup.md)
- [ci-cd.md](./ci-cd.md)
- [environments.md](./environments.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)