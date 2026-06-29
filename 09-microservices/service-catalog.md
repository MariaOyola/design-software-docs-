# Catálogo de Microservicios

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Inventario oficial de los microservicios del sistema de gestión de horarios SENA. Todo servicio nuevo debe registrarse aquí antes de que su PR pueda aprobarse. Es la fuente de verdad sobre qué servicios existen, qué datos poseen y cuál es su estado documental.

## Contenido

### Inventario de servicios

| # | Servicio | Base de datos | Entidades | Owner | Repo | Estado doc |
|---|---|---|---|---|---|---|
| 01 | `iam-service` | `iam_db` | usuario, rol, permiso, sesion, token | Por definir | Por definir | 🔴 |
| 02 | `reference-data-service` | `ref_db` | macroregion, centro_formacion, catalogo, estado, parametro | Por definir | Por definir | 🔴 |
| 03 | `academic-management-service` | `academic_db` | programa, competencia, RAP, ficha, oferta | Por definir | Por definir | 🔴 |
| 04 | `training-environment-service` | `env_db` | ambiente, inventario, mantenimiento, reserva, disponibilidad | Por definir | Por definir | 🔴 |
| 05 | `scheduling-service` | `scheduling_db` | horario, sesion_clase, franja, asignacion, conflicto | Por definir | Por definir | 🔴 |
| 06 | `actors-service` | `actors_db` | instructor, aprendiz, empresa, etapa_productiva, bitacora | Por definir | Por definir | 🔴 |
| 07 | `document-service` | `document_db` | documento, version, plantilla | Por definir | Por definir | 🔴 |
| 08 | `monitoring-service` | `monitoring_db` | seguimiento_kpi, alerta, notificacion, sesion_seguimiento, plan_mejoramiento | Por definir | Por definir | 🔴 |
| 09 | `audit-service` | `audit_db` | auditoria (append-only, sin updates) | Por definir | Por definir | 🔴 |

**Total: 9 servicios · 9 bases de datos independientes**

---

### Componentes desplegables por servicio

| Servicio | Componentes |
|---|---|
| `iam-service` | `iam-api` |
| `reference-data-service` | `reference-data-api` |
| `academic-management-service` | `academic-management-api` |
| `training-environment-service` | `training-environment-api` |
| `scheduling-service` | `schedules-api`, `scheduling-engine-workflow`, `conflict-validator-worker` |
| `actors-service` | `actors-api` |
| `document-service` | `document-api`, `template-api`, `pdf-renderer-worker`, `document-lifecycle-worker` |
| `monitoring-service` | `monitoring-api`, `alert-worker`, `notification-worker` |
| `audit-service` | `audit-worker` |

**Total: 17 componentes desplegables**

---

### Reglas del catálogo

```
✅ Todo servicio nuevo se registra aquí antes de crear su carpeta en services/
✅ El nombre del servicio debe coincidir con el nombre del repositorio de código
✅ El estado documental se actualiza con cada PR que modifica la documentación del servicio
❌ No se registra un servicio sin ADR o decisión RESUELTA en 15-project-control/open-questions.md
```

## Referencias

- [communication-patterns.md](./communication-patterns.md) — Cómo se comunican los servicios
- [09-microservices/services/](./services/) — Documentación de cada servicio
- [06-data/models.md](../06-data/models.md) — Modelos de datos globales
- [00-governance/microservices-documentation.md](../00-governance/microservices-documentation.md) — Flujo para documentar un servicio