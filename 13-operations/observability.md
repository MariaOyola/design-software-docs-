# Observabilidad

> Estado: 🟡 En progreso | Última actualización: 2026-06-30
> Autor: Maria| Equipo: Por definir

## Contexto

Define qué se monitorea, cómo se registran los logs, cómo se trazan las solicitudes entre servicios y qué alertas existen. Es la base para detectar problemas antes de que afecten a los usuarios.

## Contenido

### Los tres pilares

```
Métricas  → números que miden el estado del sistema (tiempos, errores, uso de recursos)
Logs      → registro cronológico de eventos del sistema
Trazas    → seguimiento de una solicitud a través de múltiples microservicios
```

---

### Métricas por servicio

Todo microservicio debe exponer al menos estas métricas:

| Métrica | Descripción | Umbral de alerta |
|---|---|---|
| `response_time_ms` | Tiempo de respuesta de endpoints | > 3000ms |
| `error_rate` | Porcentaje de respuestas 5xx | > 1% |
| `request_count` | Volumen de solicitudes por minuto | Por definir |
| `db_connection_pool` | Conexiones activas a la BD | > 80% del pool |

**Métricas específicas de `scheduling-service`:**
| Métrica | Umbral |
|---|---|
| Tiempo de generación de horario | > 30 segundos |
| Conflictos sin resolver por más de 24h | > 0 |

**Métricas específicas de `audit-service`:**
| Métrica | Umbral |
|---|---|
| Eventos sin procesar en cola | > 100 |
| Tiempo sin recibir eventos | > 2 minutos |

---

### Logs

**Qué registrar:**
```
✅ Solicitudes recibidas: método, ruta, usuario (ID), tiempo de respuesta
✅ Errores con stack trace completo
✅ Eventos emitidos y consumidos con timestamp
✅ Cambios de estado de entidades críticas (horario, ficha, ambiente)
```

**Qué nunca registrar:**
```
❌ Contraseñas o tokens completos
❌ Datos personales de aprendices o instructores
❌ Credenciales de bases de datos
```

**Niveles de log por ambiente:**
| Ambiente | Nivel |
|---|---|
| `develop` | DEBUG |
| `qa` | DEBUG |
| `stg` | INFO |
| `main` | INFO / WARNING |

---

### Trazas distribuidas

Cuando una solicitud pasa por varios microservicios, se usa un `trace-id` para seguirla de punta a punta:

```
Cliente → API Gateway → scheduling-service → training-environment-service
                              ↓
                        audit-service

Todos comparten el mismo trace-id para que los logs se puedan correlacionar.
```

---

### Alertas configuradas

| Alerta | Condición | Severidad | Quién recibe |
|---|---|---|---|
| Servicio caído | Healthcheck falla 3 veces seguidas | 🔴 Crítica | Equipo técnico |
| Tiempo de respuesta alto | `response_time_ms` > 3000ms por 5 min | 🟠 Alta | Equipo técnico |
| Tasa de error alta | `error_rate` > 1% por 5 min | 🟠 Alta | Equipo técnico |
| audit-service sin eventos | Sin eventos por > 2 min | 🟠 Alta | Equipo técnico |
| BD cerca del límite | Conexiones > 80% del pool | 🟡 Media | Equipo técnico |
| Conflictos sin resolver | Más de 24h sin resolver | 🟡 Media | Coordinador + equipo |

## Referencias

- [incident-management.md](./incident-management.md) — Qué hacer cuando salta una alerta
- [backup-and-recovery.md](./backup-and-recovery.md) — Recuperación ante pérdida de datos
- [09-microservices/services/](../09-microservices/services/) — Runbook de cada servicio