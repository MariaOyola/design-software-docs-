# Índice de Diagramas

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Registro de todos los diagramas del sistema. Todo diagrama nuevo debe agregarse aquí antes de cerrar su PR. Si un diagrama tiene fuente editable y exportación, ambas rutas deben registrarse.

## Contenido

### Convención de registro

| Campo | Descripción |
|---|---|
| Nombre | Nombre descriptivo del diagrama |
| Tipo | Tipo UML: secuencia, componentes, estado, etc. |
| Dominio | Área del sistema que representa |
| Fuente | Ruta al archivo `.wsd` o `.puml` en `diagrams/source/` |
| Export | Ruta al archivo `.svg` o `.png` en `diagrams/exports/` |
| Estado | 🔴 Pendiente / 🟡 En progreso / 🟢 Estable |

---

### Registro de diagramas

| Nombre | Tipo | Dominio | Fuente | Export | Estado |
|---|---|---|---|---|---|
| — | — | — | — | — | Sin diagramas registrados aún |

> Todo diagrama nuevo debe agregarse a esta tabla antes de cerrar su PR.

---

### Diagramas pendientes por crear

Los siguientes diagramas son prioritarios para documentar el sistema:

| Nombre sugerido | Tipo | Dominio | Prioridad |
|---|---|---|---|
| `sistema-deployment` | Despliegue | Sistema completo | 🔴 Alta |
| `sistema-component` | Componentes | Los 9 microservicios | 🔴 Alta |
| `scheduling-sequence` | Secuencia | Flujo de generación de horario | 🔴 Alta |
| `horario-state` | Estado | Estados del horario | 🟠 Media |
| `iam-sequence` | Secuencia | Flujo de autenticación | 🟠 Media |
| `ficha-state` | Estado | Estados de la ficha | 🟠 Media |
| `conflicto-activity` | Actividad | Resolución de conflictos | 🟡 Baja |

## Referencias

- [README.md](./README.md) — Convenciones de la carpeta UML
- [05-architecture/overview.md](../05-architecture/overview.md) — Arquitectura que estos diagramas representan
- [05-architecture/deployment.md](../05-architecture/deployment.md) — Topología de despliegue