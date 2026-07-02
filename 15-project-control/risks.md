# Riesgos

> Estado: 🟡  En progreso | Última actualización: 2026-06-1
> Autor: Maria|  | Equipo: Por definir

## Contexto

Registro de riesgos identificados para el proyecto, su impacto, probabilidad y estrategia de mitigación. Se actualiza en cada revisión de proyecto o cuando se identifica un riesgo nuevo.

## Contenido

### Escala de evaluación

| Nivel | Probabilidad | Impacto |
|---|---|---|
| 🔴 Alto | > 70% de ocurrencia | Detiene el proyecto o afecta producción |
| 🟠 Medio | 30-70% de ocurrencia | Retrasa entregas o degrada el servicio |
| 🟡 Bajo | < 30% de ocurrencia | Impacto menor o recuperable fácilmente |

---

### Registro de riesgos

| ID | Riesgo | Probabilidad | Impacto | Mitigación | Estado |
|---|---|---|---|---|---|
| R-001 | RPO y RTO no definidos con el SENA — si hay pérdida de datos no se sabe cuánto es aceptable | 🟠 Medio | 🔴 Alto | Acordar y documentar en backup-and-recovery.md antes de ir a producción | 🔴 Abierto |
| R-002 | El scheduling-service es el core del sistema — si falla, bloquea toda la generación de horarios | 🟠 Medio | 🔴 Alto | Runbook detallado, pruebas de carga, circuit breaker configurado | 🟠 Mitigado parcialmente |
| R-003 | audit-service pierde eventos si la cola está caída — pérdida de trazabilidad | 🟡 Bajo | 🟠 Medio | Alerta si audit-service no recibe eventos por > 2 min, reintentos automáticos | 🟠 Mitigado parcialmente |
| R-004 | Datos maestros desactualizados en ref_db — fichas o centros con info incorrecta | 🟠 Medio | 🟠 Medio | Proceso de actualización periódica con el SENA, validaciones en el sistema | 🔴 Abierto |
| R-005 | Rotación de personal técnico — pérdida de conocimiento si alguien sale sin documentar | 🟠 Medio | 🟠 Medio | Documentación obligatoria por servicio antes de merge a main | 🟠 Mitigado parcialmente |

---

### Cómo agregar un riesgo

```
1. Asignar ID correlativo R-NNN
2. Describir el riesgo de forma concreta y específica
3. Evaluar probabilidad e impacto con la escala
4. Definir una estrategia de mitigación concreta
5. Indicar estado: Abierto / Mitigado parcialmente / Cerrado
```

## Referencias

- [technical-backlog.md](./technical-backlog.md) — Acciones pendientes derivadas de riesgos
- [open-questions.md](./open-questions.md) — Preguntas que pueden materializarse como riesgos
- [dependencies.md](./dependencies.md) — Dependencias que pueden generar riesgos