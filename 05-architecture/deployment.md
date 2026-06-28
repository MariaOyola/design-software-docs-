# Topología de Despliegue

> Estado: 🟢 En progreso | Última actualización: 2026-06-28
> Autor: Por definir | Equipo: Por definir

## Contexto

Define cómo se despliega el sistema, qué ambientes existen y cómo se estructura la infraestructura. Para la estrategia de CI/CD ver [`10-devops/ci-cd.md`](../10-devops/ci-cd.md).

## Contenido

### Ambientes

| Ambiente | Propósito | Rama asociada |
|---|---|---|
| `develop` | Integración continua — desarrollo activo | `develop` |
| `qa` | Validación de calidad antes de staging | `qa` |
| `stg` | Staging — pre-producción, pruebas finales | `stg` |
| `main` | Producción — versión estable y operativa | `main` |

### Modelo de contenedores

Cada microservicio se despliega en su propio contenedor Docker:

```
[API Gateway]
      │
      ├── [01-iam-service]          → iam_db
      ├── [02-reference-data]       → ref_db
      ├── [03-academic-management]  → academic_db
      ├── [04-training-environment] → env_db
      ├── [05-scheduling-service]   → scheduling_db
      │     ├── schedules-api
      │     ├── scheduling-engine-workflow
      │     └── conflict-validator-worker
      ├── [06-actors-service]       → actors_db
      ├── [07-document-service]     → document_db
      │     ├── document-api
      │     ├── template-api
      │     ├── pdf-renderer-worker
      │     └── document-lifecycle-worker
      ├── [08-monitoring-service]   → monitoring_db
      │     ├── monitoring-api
      │     ├── alert-worker
      │     └── notification-worker
      └── [09-audit-service]        → audit_db
            └── audit-worker
```

### Principios de despliegue

```
- Cada servicio tiene su propio Dockerfile
- Los servicios se despliegan y reinician de forma independiente
- Las variables de entorno (credenciales, URLs) se gestionan fuera del código
- Nunca se incluyen secretos en el repositorio (ver 00-governance/security-rules.md)
```

> ⚠️ Los detalles específicos de infraestructura (IPs, URLs, credenciales)
> no se documentan aquí. Ver 00-governance/security-rules.md.

## Referencias

- [overview.md](./overview.md) — Vista general de arquitectura
- [10-devops/ci-cd.md](../10-devops/ci-cd.md) — Pipeline de CI/CD
- [10-devops/environments.md](../10-devops/environments.md) — Configuración de ambientes
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Componentes desplegables