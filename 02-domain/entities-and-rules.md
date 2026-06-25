# Entidades y Reglas de Negocio

> Estado: 🟢 En progreso | Última actualización: 2026-06-24
> Autor: Maria  | Equipo: Por definir

## Contexto

Define las entidades del dominio y las reglas de negocio que las gobiernan. Representa conceptos del mundo real institucional, no tablas de base de datos. Los detalles de implementación van en [`06-data/models.md`](../06-data/models.md).

## Contenido

### Identidad y Acceso → `iam-service`

| Entidad | Qué representa |
|---|---|
| **Usuario** | Persona que interactúa con el sistema mediante credenciales |
| **Rol** | Conjunto de permisos: Administrador, Coordinador, Instructor, Aprendiz |
| **Permiso** | Autorización específica sobre una funcionalidad |
| **Sesión** | Conexión activa de un usuario autenticado |
| **Token** | Credencial digital que identifica al usuario en cada solicitud (JWT) |

Reglas clave:
```
RN-001: Un usuario debe tener al menos un rol para acceder al sistema
RN-002: Los permisos se asignan a roles, nunca directamente a usuarios
RN-003: Un token revocado no puede reutilizarse bajo ninguna circunstancia
RN-004: Todo microservicio valida el token en iam-service antes de procesar solicitudes
```

---

### Datos Maestros → `reference-data-service`

| Entidad | Qué representa |
|---|---|
| **Macroregión** | Agrupación geográfica de centros de formación |
| **Centro de Formación** | Sede institucional donde se ejecutan los programas |
| **Catálogo** | Lista controlada de valores válidos (modalidades, jornadas, tipos) |
| **Estado** | Condición válida dentro del sistema (activo, inactivo, cancelado) |
| **Parámetro** | Configuración global que ajusta el comportamiento del sistema |

Reglas clave:
```
RN-005: Todo centro de formación debe pertenecer a una macroregión
RN-006: Solo valores del catálogo pueden usarse en otros procesos
RN-007: Solo el Administrador puede modificar parámetros del sistema
```

---

### Gestión Académica → `academic-management-service`

| Entidad | Qué representa |
|---|---|
| **Programa** | Estructura curricular oficial ofrecida por el SENA |
| **Competencia** | Capacidad que el aprendiz debe desarrollar |
| **RAP** | Resultado de Aprendizaje del Proyecto — unidad mínima de evaluación |
| **Ficha** | Grupo de aprendices en un mismo programa, jornada y fecha de inicio |
| **Oferta** | Disponibilidad de un programa para un período con cupos definidos |

Reglas clave:
```
RN-008: Una ficha debe tener al menos un aprendiz para generar su horario
RN-009: Una ficha no puede tener dos sesiones en la misma franja horaria
RN-010: El horario de una ficha solo puede publicarse sin conflictos pendientes
RN-011: Una ficha TERMINADA o CANCELADA no recibe nuevas sesiones
```

---

### Ambientes de Formación → `training-environment-service`

| Entidad | Qué representa |
|---|---|
| **Ambiente** | Espacio físico o virtual donde se desarrollan las sesiones |
| **Inventario** | Recursos físicos y tecnológicos disponibles en el ambiente |
| **Mantenimiento** | Intervención que deja el ambiente fuera de operación temporalmente |
| **Reserva** | Asignación temporal de un ambiente para una actividad |
| **Disponibilidad** | Estado del ambiente en una franja horaria específica |

Reglas clave:
```
RN-012: Un ambiente en mantenimiento no puede reservarse ni asignarse
RN-013: No pueden existir dos reservas activas para el mismo ambiente en la misma franja
RN-014: La disponibilidad se consulta siempre antes de generar una asignación
```

---

### Programación Académica → `scheduling-service`

| Entidad | Qué representa |
|---|---|
| **Horario** | Planificación completa de sesiones para una ficha (Borrador / En revisión / Publicado) |
| **Sesión de Clase** | Encuentro programado entre instructor, ficha y ambiente en una franja |
| **Franja Horaria** | Bloque de tiempo con día, hora inicio y hora fin |
| **Asignación** | Vínculo entre sesión, instructor, ambiente y franja |
| **Conflicto** | Incompatibilidad que impide publicar el horario |

Reglas clave:
```
RN-015: Un horario solo puede publicarse si no tiene conflictos pendientes
RN-016: Un horario publicado debe pasarse a Borrador para poder editarse
RN-017: Solo el Coordinador puede publicar un horario
RN-018: Un conflicto se genera automáticamente al detectar doble asignación
         de ambiente o instructor en la misma franja
```

---

### Actores → `actors-service`

| Entidad | Qué representa |
|---|---|
| **Instructor** | Responsable de orientar y evaluar el proceso formativo |
| **Aprendiz** | Persona matriculada en un programa de formación |
| **Empresa** | Organización que facilita escenarios de práctica |
| **Etapa Productiva** | Fase de aplicación práctica en empresa real |
| **Bitácora** | Registro cronológico de actividades en etapa productiva |

Reglas clave:
```
RN-019: Un instructor no puede tener dos sesiones en la misma franja horaria
RN-020: Un aprendiz en etapa productiva no tiene sesiones presenciales programadas
RN-021: La etapa productiva inicia solo después de completar la etapa lectiva
RN-022: Los registros de bitácora no pueden eliminarse, solo marcarse inactivos
```

---

### Documentos → `document-service`

| Entidad | Qué representa |
|---|---|
| **Documento** | Archivo oficial generado por el sistema (PDF, actas, reportes) |
| **Versión** | Registro histórico de cada generación de un documento |
| **Plantilla** | Modelo base para la generación de documentos oficiales |

Reglas clave:
```
RN-023: Un documento publicado no puede modificarse, debe generarse una nueva versión
RN-024: Toda versión de un documento queda registrada para trazabilidad
```

---

### Monitoreo → `monitoring-service`

| Entidad | Qué representa |
|---|---|
| **Seguimiento KPI** | Registro del cumplimiento de indicadores del proceso formativo |
| **Alerta** | Notificación generada cuando un KPI supera su umbral |
| **Notificación** | Mensaje enviado a instructores o aprendices por cambios relevantes |
| **Sesión de Seguimiento** | Reunión o actividad de acompañamiento registrada en el sistema |
| **Plan de Mejoramiento** | Acciones acordadas para corregir desviaciones detectadas en KPIs |

Reglas clave:
```
RN-025: Un KPI fuera de umbral genera automáticamente una alerta
RN-026: Todo plan de mejoramiento debe estar asociado a una alerta generada
```

---

### Auditoría → `audit-service`

| Entidad | Qué representa |
|---|---|
| **Auditoría** | Registro inmutable de toda acción relevante ejecutada en el sistema |

Reglas clave:
```
RN-027: Todo evento relevante del sistema debe registrarse en auditoría
RN-028: Los registros de auditoría no pueden modificarse ni eliminarse
RN-029: Auditoría es append-only: solo se agregan registros, nunca se actualizan
```

## Referencias

- [domain-map.md](./domain-map.md) — Mapa de relaciones entre entidades
- [domain-events.md](./domain-events.md) — Eventos generados por estas entidades
- [01-context/glossary.md](../01-context/glossary.md) — Definiciones oficiales
- [06-data/models.md](../06-data/models.md) — Implementación técnica en BD
- Reglamento del Aprendiz SENA — Acuerdo 009 de 2024