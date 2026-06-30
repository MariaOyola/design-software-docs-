# Requisitos Funcionales

> Estado:  🟢 En progreso | Última actualización: Última actualización: 2026-06-27 | Equipo: Por definir

## Contexto

Define qué debe hacer el sistema. Cada requisito funcional describe una capacidad concreta que el sistema debe proveer. Se derivan de las historias de usuario de [`03-product/product-backlog.md`](../03-product/product-backlog.md) y las reglas de negocio de [`02-domain/entities-and-rules.md`](../02-domain/entities-and-rules.md).

## Contenido

### RF-01 · Identidad y Acceso

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-01-01 | El sistema debe permitir autenticar usuarios mediante usuario y contraseña, generando un token JWT válido | HU-001 |
| RF-01-02 | El sistema debe controlar el acceso a funcionalidades según el rol del usuario autenticado | HU-001, HU-002 |
| RF-01-03 | El sistema debe permitir asignar y revocar roles a usuarios | HU-002 |
| RF-01-04 | El sistema debe invalidar tokens revocados inmediatamente | HU-001 |
| RF-01-05 | El sistema debe registrar el inicio y cierre de cada sesión | HU-001 |

---

### RF-02 · Datos Maestros

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-02-01 | El sistema debe permitir registrar y administrar centros de formación asociados a macroregiones | HU-003 |
| RF-02-02 | El sistema debe gestionar catálogos de valores válidos usados por otros módulos | HU-003 |
| RF-02-03 | El sistema debe permitir configurar parámetros globales con efecto inmediato | HU-004 |

---

### RF-03 · Gestión Académica

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-03-01 | El sistema debe permitir crear y administrar programas de formación con competencias y RAPs | HU-005 |
| RF-03-02 | El sistema debe permitir crear fichas asociadas a un programa y centro de formación | HU-005 |
| RF-03-03 | El sistema debe permitir consultar fichas activas filtrando por estado, programa y jornada | HU-006 |
| RF-03-04 | El sistema debe gestionar ofertas de formación con cupos definidos | HU-005 |

---

### RF-04 · Ambientes de Formación

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-04-01 | El sistema debe permitir registrar ambientes con tipo, capacidad y centro de formación | HU-007 |
| RF-04-02 | El sistema debe consultar disponibilidad de ambientes por franja horaria en tiempo real | HU-007 |
| RF-04-03 | El sistema debe bloquear ambientes durante mantenimientos registrados | HU-008 |
| RF-04-04 | El sistema debe gestionar reservas de ambientes evitando doble ocupación | HU-007 |

---

### RF-05 · Actores

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-05-01 | El sistema debe permitir registrar instructores y su disponibilidad horaria | HU-009 |
| RF-05-02 | El sistema debe permitir vincular aprendices a fichas activas | HU-005 |
| RF-05-03 | El sistema debe registrar el inicio y fin de la etapa productiva de un aprendiz | HU-010 |
| RF-05-04 | El sistema debe excluir aprendices en etapa productiva de la programación presencial | HU-010 |

---

### RF-06 · Programación de Horarios

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-06-01 | El sistema debe generar automáticamente un horario para una ficha respetando disponibilidad de ambientes e instructores | HU-011 |
| RF-06-02 | El sistema debe detectar automáticamente conflictos de ambiente e instructor | HU-012 |
| RF-06-03 | El sistema debe permitir al coordinador resolver conflictos manualmente | HU-012 |
| RF-06-04 | El sistema debe impedir publicar un horario con conflictos pendientes | HU-013 |
| RF-06-05 | El sistema debe permitir consultar el horario publicado por ficha, instructor y aprendiz | HU-014 |
| RF-06-06 | El sistema debe notificar a instructores y aprendices al publicar o modificar un horario | HU-013 |

---

### RF-07 · Documentos

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-07-01 | El sistema debe generar el horario publicado en formato PDF | HU-015 |
| RF-07-02 | El sistema debe registrar una versión por cada documento generado | HU-015 |

---

### RF-08 · Monitoreo y Auditoría

| ID | Requisito | HU relacionada |
|---|---|---|
| RF-08-01 | El sistema debe registrar de forma inmutable toda acción relevante en el log de auditoría | HU-018 |
| RF-08-02 | El sistema debe generar alertas automáticas cuando un KPI supere su umbral | HU-017 |
| RF-08-03 | El sistema debe permitir consultar el log de auditoría filtrado por usuario, fecha y acción | HU-018 |

## Referencias

- [03-product/product-backlog.md](../03-product/product-backlog.md) — HU de origen
- [non-functional.md](./non-functional.md) — Requisitos de calidad
- [user-stories.md](./user-stories.md) — Detalle de cada HU
- [traceability-matrix.md](./traceability-matrix.md) — Trazabilidad completa
- [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) — Reglas de negocio base