# Roadmap

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Define las fases de construcción del sistema y qué microservicios o funcionalidades se entregan en cada una. El orden respeta las dependencias técnicas entre servicios: no se puede construir el motor de horarios sin tener primero los datos de fichas, ambientes e instructores.

## Contenido

### Fase 1 — Base del sistema

Objetivo: tener la infraestructura de identidad y datos maestros lista para que los demás servicios puedan operar.

| Servicio | Funcionalidades |
|---|---|
| `iam-service` | Registro de usuarios, autenticación JWT, gestión de roles y permisos |
| `reference-data-service` | Macroregiones, centros de formación, catálogos y parámetros |

Criterio de salida: un usuario puede autenticarse y el sistema tiene datos maestros cargados.

---

### Fase 2 — Gestión académica y ambientes

Objetivo: tener la información académica e institucional necesaria para generar horarios.

| Servicio | Funcionalidades |
|---|---|
| `academic-management-service` | Programas, competencias, RAPs, fichas y ofertas |
| `training-environment-service` | Ambientes, inventario, mantenimientos, reservas y disponibilidad |
| `actors-service` | Instructores, aprendices, empresas y etapa productiva |

Criterio de salida: existen fichas activas con aprendices, ambientes disponibles e instructores registrados.

---

### Fase 3 — Core del sistema

Objetivo: implementar el motor de generación de horarios, la detección de conflictos y la publicación.

| Servicio | Funcionalidades |
|---|---|
| `scheduling-service` | Generación de horarios, asignación de sesiones, detección y resolución de conflictos, publicación |

Criterio de salida: un coordinador puede generar y publicar un horario sin conflictos para una ficha.

---

### Fase 4 — Servicios transversales

Objetivo: agregar generación de documentos, monitoreo y auditoría completa.

| Servicio | Funcionalidades |
|---|---|
| `document-service` | Generación de PDFs de horarios, plantillas y versiones |
| `monitoring-service` | KPIs, alertas, notificaciones y planes de mejoramiento |
| `audit-service` | Registro inmutable de toda acción relevante del sistema |

Criterio de salida: el sistema genera documentos oficiales, monitorea la operación y tiene trazabilidad completa.

---

### Resumen de dependencias entre fases

```
Fase 1 (iam + reference-data)
        ↓
Fase 2 (academic + training-environment + actors)
        ↓
Fase 3 (scheduling) ← core del proyecto
        ↓
Fase 4 (document + monitoring + audit)
```

Ninguna fase puede iniciarse sin que la anterior esté completa y estable.

## Referencias

- [vision.md](./vision.md) — Visión y criterios de éxito del producto
- [product-backlog.md](./product-backlog.md) — Funcionalidades detalladas por fase
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo oficial de servicios
- [15-project-control/dependencies.md](../15-project-control/dependencies.md) — Dependencias técnicas entre servicios