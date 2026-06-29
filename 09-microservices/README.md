# Microservicios

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria | Equipo: Por definir

## Contexto

Centraliza el catálogo de microservicios, los patrones de comunicación y la documentación específica de cada servicio del sistema de gestión de horarios SENA.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [service-catalog.md](./service-catalog.md) | Inventario de servicios, owners, repos y estado documental | 🟡 |
| [communication-patterns.md](./communication-patterns.md) | Patrones síncronos, asíncronos y resiliencia | 🟡 |
| [_template/](./_template/) | Plantilla para documentar un servicio nuevo — no es un microservicio real | 🟡 |
| [services/](./services/) | Documentación específica por microservicio | 🔴 |

### Estado de documentación por servicio

| # | Servicio | README | data-model | events | api-contract | runbook | Estado |
|---|---|---|---|---|---|---|---|
| 01 | `iam-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 02 | `reference-data-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 03 | `academic-management-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 04 | `training-environment-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 05 | `scheduling-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 06 | `actors-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 07 | `document-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 08 | `monitoring-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |
| 09 | `audit-service` | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 | 🔴 |

> Esta tabla se actualiza con cada PR que completa o modifica la documentación de un servicio.

### Cómo documentar un servicio nuevo

```bash
# 1. Verificar que el servicio no existe ya en service-catalog.md

# 2. Copiar la plantilla
cp -r 09-microservices/_template/ \
      09-microservices/services/[NN-nombre-service]/

# 3. Completar los 5 archivos en orden:
#    README.md → data-model.md → events.md → api-contract.md → runbook.md

# 4. Registrar en service-catalog.md

# 5. Actualizar esta tabla de estado

# 6. Commit y PR
git checkout -b feat/doc-service-[nombre-servicio]
git add 09-microservices/services/[NN-nombre-service]/
git add 09-microservices/service-catalog.md
git commit -m "docs(09-microservices): register [nombre-servicio] service"
```

Ver flujo completo en [00-governance/microservices-documentation.md](../00-governance/microservices-documentation.md).

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Modelo de datos global del sistema | [06-data/models.md](../06-data/models.md) |
| Lineamientos de API | [07-api/guidelines.md](../07-api/guidelines.md) |
| Eventos de dominio | [02-domain/domain-events.md](../02-domain/domain-events.md) |
| Operación en producción | [13-operations/](../13-operations/) |

## Referencias

- [service-catalog.md](./service-catalog.md)
- [communication-patterns.md](./communication-patterns.md)
- [_template/README.md](./_template/README.md)
- [00-governance/microservices-documentation.md](../00-governance/microservices-documentation.md)