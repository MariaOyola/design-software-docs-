# Backup y Recuperación

> Estado: 🟡 En progreso | Última actualización: 2026-06-30
> Autor: Maria | Equipo: Por definir

## Contexto

Define la estrategia de respaldo y recuperación para las 9 bases de datos del sistema. Garantiza que ante una falla catastrófica el sistema pueda restaurarse con pérdida mínima de datos.

## Contenido

### Objetivos de recuperación

| Métrica | Definición | Objetivo |
|---|---|---|
| **RPO** (Recovery Point Objective) | Máxima pérdida de datos aceptable | ⚠️ Por definir con el SENA |
| **RTO** (Recovery Time Objective) | Tiempo máximo para restaurar el servicio | ⚠️ Por definir con el SENA |

> Estos valores deben acordarse con el equipo institucional del SENA antes de ir a producción.

---

### Estrategia de backup por base de datos

| Base de datos | Servicio | Frecuencia | Retención | Prioridad |
|---|---|---|---|---|
| `iam_db` | iam-service | Diario | 30 días | 🔴 Alta |
| `scheduling_db` | scheduling-service | Diario | 30 días | 🔴 Alta |
| `audit_db` | audit-service | Diario | 1 año | 🔴 Alta (legal) |
| `academic_db` | academic-management-service | Diario | 30 días | 🔴 Alta |
| `env_db` | training-environment-service | Diario | 30 días | 🟠 Media |
| `actors_db` | actors-service | Diario | 30 días | 🟠 Media |
| `ref_db` | reference-data-service | Semanal | 30 días | 🟡 Baja |
| `document_db` | document-service | Diario | 30 días | 🟠 Media |
| `monitoring_db` | monitoring-service | Diario | 30 días | 🟡 Baja |

---

### Consideración especial: `audit_db`

```
audit_db tiene retención de 1 año (no 30 días) porque:
  - Los registros de auditoría pueden tener implicaciones legales e institucionales
  - Son requeridos para trazabilidad de acciones del sistema
  - Son append-only: no se pueden regenerar si se pierden
```

---

### Procedimiento de restauración

```
1. Identificar el backup más reciente antes del incidente
   (según RPO acordado)

2. Detener el servicio afectado
   docker stop [nombre-servicio]

3. Restaurar la BD desde el backup
   pg_restore -d [nombre_db] [archivo_backup]

4. Verificar integridad de los datos restaurados

5. Reiniciar el servicio
   docker start [nombre-servicio]

6. Ejecutar smoke tests del servicio
   curl http://localhost:[puerto]/api/v1/health

7. Registrar el incidente y la restauración en
   15-project-control/technical-backlog.md
```

---

### Pruebas de recuperación

```
[ ] Realizar una prueba de restauración completa cada 3 meses en el ambiente stg
[ ] Verificar que el tiempo de restauración cumple el RTO acordado
[ ] Documentar los resultados en 15-project-control/technical-backlog.md
```

## Referencias

- [observability.md](./observability.md) — Monitoreo que puede detectar pérdida de datos
- [incident-management.md](./incident-management.md) — Proceso de respuesta a incidentes
- [06-data/models.md](../06-data/models.md) — Estructura de las BDs respaldadas