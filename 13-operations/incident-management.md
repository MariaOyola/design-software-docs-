# Gestión de Incidentes

> Estado: 🟡 En progreso | Última actualización: 2026-06-30
> Autor: Maria| Equipo: Por definir

## Contexto

Define cómo clasificar, responder y comunicar incidentes en producción. En una arquitectura de microservicios un incidente puede involucrar varios servicios simultáneamente, por lo que el proceso debe ser claro y rápido.

## Contenido

### Clasificación de severidad

| Severidad | Descripción | Tiempo de respuesta |
|---|---|---|
| 🔴 P1 — Crítico | Sistema completamente caído o pérdida de datos | Inmediato (< 15 min) |
| 🟠 P2 — Alto | Funcionalidad principal no disponible (no se pueden generar horarios) | < 1 hora |
| 🟡 P3 — Medio | Funcionalidad secundaria degradada (PDFs no se generan) | < 4 horas |
| 🟢 P4 — Bajo | Problema menor sin impacto en operación | Próximo día hábil |

---

### Proceso de respuesta

```
1. DETECTAR
   Alerta de observability.md o reporte de usuario
        ↓
2. CLASIFICAR
   Determinar severidad P1-P4
        ↓
3. COMUNICAR
   Notificar al equipo según severidad
   P1/P2: notificación inmediata al equipo técnico y al instructor
   P3/P4: registrar en 15-project-control/open-questions.md
        ↓
4. DIAGNOSTICAR
   Revisar logs, métricas y trazas del servicio afectado
   Consultar runbook del servicio en 09-microservices/services/<svc>/runbook.md
        ↓
5. MITIGAR
   Aplicar solución temporal para restaurar el servicio
   (reiniciar, rollback, redirigir tráfico)
        ↓
6. RESOLVER
   Aplicar solución definitiva en una rama fix/
        ↓
7. POSTMORTEM
   Documentar qué pasó, por qué y cómo evitarlo
   Registrar en 15-project-control/technical-backlog.md si queda deuda técnica
```

---

### Escenarios más probables en microservicios

| Síntoma | Servicio probable | Primer paso |
|---|---|---|
| No se pueden generar horarios | `scheduling-service` | Ver runbook del servicio |
| No llegan notificaciones | `monitoring-service` → `notification-worker` | Revisar cola de eventos |
| No se generan PDFs | `document-service` → `pdf-renderer-worker` | Revisar cola de eventos |
| Login falla para todos | `iam-service` | Ver healthcheck y logs |
| Datos maestros no cargan | `reference-data-service` | Ver healthcheck y BD |
| Auditoría sin registros nuevos | `audit-service` → `audit-worker` | Revisar cola de eventos |

---

### Comunicación durante un incidente P1/P2

```
Cada 30 minutos mientras dure el incidente:
  "Incidente activo: [descripción breve]
   Severidad: P[N]
   Estado: [en diagnóstico / mitigado / resuelto]
   Próxima actualización: [hora]"
```

---

### Postmortem

Todo incidente P1 y P2 requiere un postmortem escrito con:

```
[ ] ¿Qué pasó? (línea de tiempo)
[ ] ¿Cuál fue el impacto?
[ ] ¿Por qué pasó? (causa raíz)
[ ] ¿Cómo se detectó?
[ ] ¿Cómo se resolvió?
[ ] ¿Qué se hace para que no vuelva a pasar?
```

El postmortem se guarda en `15-project-control/technical-backlog.md` o como ADR si implica un cambio de arquitectura.

## Referencias

- [observability.md](./observability.md) — Métricas y alertas
- [backup-and-recovery.md](./backup-and-recovery.md) — Recuperación de datos
- [09-microservices/services/](../09-microservices/services/) — Runbooks por servicio
- [15-project-control/technical-backlog.md](../15-project-control/technical-backlog.md) — Deuda técnica post-incidente