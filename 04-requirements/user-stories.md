# Historias de Usuario

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Detalle de las historias de usuario del sistema de gestión de horarios SENA. Las HU de alto nivel viven en [`03-product/product-backlog.md`](../03-product/product-backlog.md). Este archivo agrega el detalle técnico: tareas de implementación y microservicio responsable.

## Contenido

---

### HU-001 · Autenticación de usuario

**Como** usuario del sistema
**Quiero** iniciar sesión con mis credenciales
**Para** acceder a las funcionalidades de mi rol

**Microservicio:** `iam-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] El sistema valida usuario y contraseña correctamente
[ ] Se genera token JWT al autenticarse
[ ] Credenciales incorrectas retornan error claro
[ ] La autenticación responde en ≤ 3 segundos
[ ] Token expirado obliga a iniciar sesión nuevamente
```

**Tareas técnicas:**
```
[ ] Implementar endpoint POST /auth/login en iam-service
[ ] Configurar generación y firma de JWT
[ ] Implementar middleware de validación de token para todos los servicios
[ ] Documentar contrato en 09-microservices/services/01-iam-service/api-contract.md
```

---

### HU-002 · Gestión de roles

**Como** administrador
**Quiero** asignar y revocar roles a usuarios
**Para** controlar qué puede hacer cada persona en el sistema

**Microservicio:** `iam-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Puedo asignar uno o más roles a un usuario
[ ] Puedo revocar un rol sin eliminar el usuario
[ ] Los permisos aplican inmediatamente tras asignar el rol
[ ] Solo el Administrador puede gestionar roles
```

**Tareas técnicas:**
```
[ ] Implementar endpoints de gestión de roles en iam-service
[ ] Implementar control de acceso basado en roles (RBAC)
[ ] Registrar cambios de rol en audit-service
[ ] Documentar contrato en 09-microservices/services/01-iam-service/api-contract.md
```

---

### HU-003 · Creación de fichas

**Como** coordinador académico
**Quiero** crear una ficha asociada a un programa de formación
**Para** programar sus actividades y generar su horario

**Microservicio:** `academic-management-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Puedo crear ficha con programa, jornada y fecha de inicio
[ ] No puedo crear ficha con programa inactivo
[ ] La ficha inicia en estado EJECUCION
[ ] Se emite evento FichaCreada al crear exitosamente
```

**Tareas técnicas:**
```
[ ] Implementar endpoint POST /fichas en academic-management-service
[ ] Publicar evento FichaCreada hacia scheduling-service
[ ] Registrar acción en audit-service
[ ] Documentar contrato en 09-microservices/services/03-academic-management-service/api-contract.md
```

---

### HU-004 · Consulta de disponibilidad de ambientes

**Como** coordinador académico
**Quiero** consultar ambientes disponibles en una franja horaria
**Para** asignarlos correctamente al generar el horario

**Microservicio:** `training-environment-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Puedo filtrar por tipo, capacidad y franja horaria
[ ] El sistema excluye ambientes en mantenimiento o con reserva activa
[ ] La consulta responde en ≤ 3 segundos
[ ] La disponibilidad se actualiza en tiempo real
```

**Tareas técnicas:**
```
[ ] Implementar endpoint GET /ambientes/disponibilidad en training-environment-service
[ ] Integrar con scheduling-service para consultas durante generación de horario
[ ] Documentar contrato en 09-microservices/services/04-training-environment-service/api-contract.md
```

---

### HU-005 · Generación automática de horario

**Como** coordinador académico
**Quiero** generar automáticamente el horario de una ficha
**Para** obtener una propuesta sin conflictos en minutos

**Microservicio:** `scheduling-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Selecciono la ficha y el sistema genera el horario
[ ] Se respeta disponibilidad de ambientes e instructores
[ ] El horario se genera en ≤ 30 segundos
[ ] El horario generado queda en estado Borrador
[ ] Si no es posible sin conflictos, el sistema indica qué falta
```

**Tareas técnicas:**
```
[ ] Implementar scheduling-engine-workflow en scheduling-service
[ ] Consumir disponibilidad de training-environment-service y actors-service
[ ] Implementar conflict-validator-worker asíncrono
[ ] Publicar evento HorarioGenerado hacia audit-service
[ ] Documentar contrato en 09-microservices/services/05-scheduling-service/api-contract.md
```

---

### HU-006 · Publicación de horario

**Como** coordinador académico
**Quiero** publicar el horario cuando esté sin conflictos
**Para** que instructores y aprendices puedan consultarlo

**Microservicio:** `scheduling-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Solo puedo publicar si no hay conflictos pendientes
[ ] Al publicar se notifica a instructores y aprendices
[ ] El horario publicado no puede editarse directamente
[ ] La publicación queda registrada en auditoría
```

**Tareas técnicas:**
```
[ ] Implementar endpoint PUT /horarios/{id}/publicar en scheduling-service
[ ] Publicar evento HorarioPublicado hacia document-service, monitoring-service y audit-service
[ ] Implementar notificación en monitoring-service al recibir HorarioPublicado
[ ] Documentar contrato en 09-microservices/services/05-scheduling-service/api-contract.md
```

---

### HU-007 · Exportar horario en PDF

**Como** coordinador o instructor
**Quiero** descargar el horario publicado en PDF
**Para** compartirlo como documento oficial

**Microservicio:** `document-service`
**Prioridad:** 🟠 Should

**Criterios de aceptación:**
```
[ ] Puedo descargar el PDF desde la vista de consulta
[ ] El PDF incluye ficha, programa, sesiones, ambientes e instructores
[ ] El PDF generado queda registrado con versión
[ ] Solo se genera PDF de horarios en estado Publicado
```

**Tareas técnicas:**
```
[ ] Implementar pdf-renderer-worker en document-service
[ ] Consumir evento HorarioPublicado para generar PDF automáticamente
[ ] Implementar endpoint GET /documentos/{id}/pdf
[ ] Documentar contrato en 09-microservices/services/07-document-service/api-contract.md
```

---

### HU-008 · Trazabilidad de auditoría

**Como** administrador
**Quiero** consultar el historial de acciones del sistema
**Para** verificar qué ocurrió y quién lo hizo en caso de incidente

**Microservicio:** `audit-service`
**Prioridad:** 🔴 Must

**Criterios de aceptación:**
```
[ ] Puedo filtrar por usuario, fecha y tipo de acción
[ ] Los registros no pueden modificarse ni eliminarse
[ ] Toda acción relevante queda registrada automáticamente
[ ] Solo el Administrador consulta el log completo
```

**Tareas técnicas:**
```
[ ] Implementar audit-worker como consumidor de eventos de todos los servicios
[ ] Implementar endpoint GET /auditoria con filtros en audit-service
[ ] Garantizar que la BD audit_db sea append-only a nivel de configuración
[ ] Documentar contrato en 09-microservices/services/09-audit-service/api-contract.md
```

## Referencias

- [03-product/product-backlog.md](../03-product/product-backlog.md) — HU de alto nivel
- [functional.md](./functional.md) — Requisitos funcionales relacionados
- [traceability-matrix.md](./traceability-matrix.md) — Trazabilidad completa
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Servicios responsables