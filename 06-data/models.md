# Modelos de Datos

> Estado: 🟢 En progreso | Última actualización: 2026-06-2
> Autor: Por definir | Equipo: Por definir

## Contexto

Documenta los modelos de datos del sistema a nivel global. El modelo transaccional específico de cada servicio (tablas internas, esquemas locales) se documenta en `09-microservices/services/<servicio>/data-model.md`. Aquí vive el panorama general: qué BD tiene cada servicio y cómo se relacionan conceptualmente los datos entre ellos.

> **Diferencia con `02-domain`:** allá se describen las entidades de negocio y sus reglas. Aquí se describe cómo esas entidades se implementan en bases de datos: tablas, columnas, tipos y relaciones.

## Contenido

### Base de datos por servicio

Cada microservicio tiene su propia base de datos. Ningún servicio accede a la BD de otro directamente.

| Servicio | Base de datos | Motor | Tipo |
|---|---|---|---|
| `iam-service` | `iam_db` | PostgreSQL | Transaccional |
| `reference-data-service` | `ref_db` | PostgreSQL | Transaccional |
| `academic-management-service` | `academic_db` | PostgreSQL | Transaccional |
| `training-environment-service` | `env_db` | PostgreSQL | Transaccional |
| `scheduling-service` | `scheduling_db` | PostgreSQL | Transaccional |
| `actors-service` | `actors_db` | PostgreSQL | Transaccional |
| `document-service` | `document_db` | PostgreSQL | Transaccional |
| `monitoring-service` | `monitoring_db` | PostgreSQL | Transaccional |
| `audit-service` | `audit_db` | PostgreSQL | Append-only |

> `audit_db` es la única BD con restricción de solo escritura — no permite UPDATE ni DELETE bajo ninguna circunstancia.

---

### Entidades por base de datos

#### `iam_db`
```
usuario         → persona registrada con credenciales de acceso
rol             → conjunto de permisos asignable a un usuario
permiso         → autorización específica sobre una funcionalidad
sesion          → conexión activa de un usuario autenticado
token           → credencial JWT de autenticación
```

#### `ref_db`
```
macroregion     → agrupación geográfica de centros de formación
centro_formacion → sede institucional del SENA
catalogo        → lista controlada de valores válidos
estado          → condición válida dentro del sistema
parametro       → configuración global del sistema
```

#### `academic_db`
```
programa        → estructura curricular oficial
competencia     → capacidad que el aprendiz debe desarrollar
RAP             → resultado de aprendizaje del proyecto (unidad mínima)
ficha           → grupo de aprendices en un mismo programa y jornada
oferta          → disponibilidad de un programa con cupos definidos
```

#### `env_db`
```
ambiente        → espacio físico o virtual de formación
inventario      → recursos físicos disponibles en el ambiente
mantenimiento   → intervención que bloquea el ambiente temporalmente
reserva         → asignación temporal de un ambiente
disponibilidad  → estado operativo del ambiente en una franja horaria
```

#### `scheduling_db`
```
horario         → planificación completa de sesiones para una ficha
sesion_clase    → encuentro programado instructor-ficha-ambiente
franja          → bloque de tiempo disponible para programación
asignacion      → vínculo sesión-instructor-ambiente-franja
conflicto       → incompatibilidad detectada durante la programación
```

#### `actors_db`
```
instructor      → responsable de orientar el proceso formativo
aprendiz        → persona matriculada en un programa de formación
empresa         → organización vinculada a etapa productiva
etapa_productiva → fase de aplicación práctica en empresa real
bitacora        → registro cronológico de actividades en etapa productiva
```

#### `document_db`
```
documento       → archivo oficial generado por el sistema
version         → registro histórico de cada generación de un documento
plantilla       → modelo base para generación de documentos
```

#### `monitoring_db`
```
seguimiento_kpi      → registro de indicadores del proceso formativo
alerta               → notificación por KPI fuera de umbral
notificacion         → mensaje enviado a instructores o aprendices
sesion_seguimiento   → reunión de acompañamiento registrada
plan_mejoramiento    → acciones para corregir desviaciones detectadas
```

#### `audit_db`
```
auditoria       → registro inmutable de toda acción relevante (append-only)
```

---

### Relaciones conceptuales entre bases de datos

Los servicios no comparten BD, pero sí comparten datos por referencia (ID). Las relaciones más importantes son:

```
iam_db.usuario.id
  → referenciado por todos los servicios para identificar al actor de cada acción

ref_db.centro_formacion.id
  → referenciado por env_db.ambiente y academic_db.ficha

academic_db.ficha.id
  → referenciado por scheduling_db.horario y actors_db.aprendiz

actors_db.instructor.id
  → referenciado por scheduling_db.asignacion

env_db.ambiente.id
  → referenciado por scheduling_db.asignacion y scheduling_db.reserva

scheduling_db.horario.id
  → referenciado por document_db.documento y monitoring_db.seguimiento_kpi
```

> Estas referencias son lógicas, no físicas. No existen foreign keys entre BDs.
> Cada servicio es responsable de validar la existencia del ID que referencia
> consultando el servicio dueño por API.

## Referencias

- [data-dictionary.md](./data-dictionary.md) — Detalle de campos por entidad
- [migration-strategy.md](./migration-strategy.md) — Estrategia de migraciones
- [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) — Entidades de negocio
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Servicios y sus BDs