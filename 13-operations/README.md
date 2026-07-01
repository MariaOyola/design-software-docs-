# Operaciones

> Estado: 🟡 En progreso | Última actualización: 2026-06-30
> Autor: Maria | Equipo: Por definir

## Contexto

Describe cómo operar, monitorear, responder incidentes y recuperar el sistema de gestión de horarios SENA en producción.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [observability.md](./observability.md) | Métricas, logs, trazas, alertas y tableros | 🟡 |
| [incident-management.md](./incident-management.md) | Clasificación, respuesta y comunicación de incidentes | 🟡 |
| [backup-and-recovery.md](./backup-and-recovery.md) | Backups, restauración, RPO/RTO y pruebas de recuperación | 🟡 |

### Flujo de lectura sugerido

```
¿Cómo sé si el sistema está funcionando bien?
  → observability.md

¿Algo salió mal — qué hago?
  → incident-management.md

¿Se perdieron datos — cómo los recupero?
  → backup-and-recovery.md
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Runbook específico de un servicio | [09-microservices/services/](../09-microservices/services/) |
| Ambientes donde ocurren los incidentes | [10-devops/environments.md](../10-devops/environments.md) |
| Deuda técnica o pendientes post-incidente | [15-project-control/technical-backlog.md](../15-project-control/technical-backlog.md) |

## Referencias

- [observability.md](./observability.md)
- [incident-management.md](./incident-management.md)
- [backup-and-recovery.md](./backup-and-recovery.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)