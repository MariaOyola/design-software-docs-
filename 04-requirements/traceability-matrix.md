# Matriz de Trazabilidad

> Estado:  🟢 En progreso | Última actualización: Última actualización: 2026-06-27 | Equipo: Por definir | Equipo: Por definir

## Contexto

Relaciona las historias de usuario con los requisitos funcionales, microservicios responsables y criterios de prueba. Permite responder: ¿qué servicio implementa esta HU? y ¿qué HU se ve afectada si cambio este servicio?

## Contenido

### Trazabilidad HU → Requisito → Microservicio

| HU | Descripción | Requisitos funcionales | Microservicio | Pruebas |
|---|---|---|---|---|
| HU-001 | Autenticación de usuario | RF-01-01, RF-01-04, RF-01-05 | `iam-service` | Unitaria, integración |
| HU-002 | Gestión de roles | RF-01-02, RF-01-03 | `iam-service` | Unitaria, integración |
| HU-003 | Gestión de centros de formación | RF-02-01, RF-02-02 | `reference-data-service` | Unitaria |
| HU-004 | Configuración de parámetros | RF-02-03 | `reference-data-service` | Unitaria |
| HU-005 | Creación de fichas | RF-03-01, RF-03-02 | `academic-management-service` | Unitaria, integración |
| HU-006 | Consulta de fichas activas | RF-03-03 | `academic-management-service` | Integración |
| HU-007 | Disponibilidad de ambientes | RF-04-01, RF-04-02, RF-04-04 | `training-environment-service` | Unitaria, integración |
| HU-008 | Mantenimiento de ambiente | RF-04-03 | `training-environment-service` | Unitaria |
| HU-009 | Disponibilidad del instructor | RF-05-01 | `actors-service` | Unitaria |
| HU-010 | Etapa productiva | RF-05-03, RF-05-04 | `actors-service` | Unitaria, integración |
| HU-011 | Generación automática de horario | RF-06-01, RF-06-02 | `scheduling-service` | Integración, e2e |
| HU-012 | Detección y resolución de conflictos | RF-06-02, RF-06-03, RF-06-04 | `scheduling-service` | Unitaria, integración |
| HU-013 | Publicación de horario | RF-06-04, RF-06-06 | `scheduling-service` | Integración, e2e |
| HU-014 | Consulta de horario | RF-06-05 | `scheduling-service` | Integración |
| HU-015 | Exportar horario en PDF | RF-07-01, RF-07-02 | `document-service` | Integración |
| HU-016 | Notificación de cambios | RF-06-06 | `monitoring-service` | Integración |
| HU-017 | Seguimiento de KPIs | RF-08-02 | `monitoring-service` | Unitaria |
| HU-018 | Trazabilidad de auditoría | RF-08-01, RF-08-03 | `audit-service` | Integración |

---

### Trazabilidad Requisito No Funcional → Decisión técnica

| RNF | Descripción | Decisión técnica (ADR) |
|---|---|---|
| RNF-01-01 | Autenticación ≤ 3 segundos | ⚠️ Pendiente ADR |
| RNF-01-02 | Generación horario ≤ 30 segundos | ⚠️ Pendiente ADR — procesamiento asíncrono con worker |
| RNF-02-01 | Todo endpoint requiere JWT | ⚠️ Pendiente ADR |
| RNF-02-03 | Auditoría inmutable | ⚠️ Pendiente ADR — audit_db append-only |
| RNF-04-01 | BD por servicio | ⚠️ Pendiente ADR |
| RNF-04-02 | Comunicación por API o eventos | ⚠️ Pendiente ADR |

> Las ADRs se registran en `05-architecture/decisions/records/` a medida que se toman las decisiones técnicas.

## Referencias

- [functional.md](./functional.md) — Requisitos funcionales
- [non-functional.md](./non-functional.md) — Requisitos no funcionales
- [user-stories.md](./user-stories.md) — Historias de usuario detalladas
- [05-architecture/decisions/](../05-architecture/decisions/) — ADRs relacionadas
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Servicios responsables