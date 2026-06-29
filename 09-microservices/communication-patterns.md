# Patrones de Comunicación

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria | Equipo: Por definir

## Contexto

Define cómo se comunican los microservicios entre sí. Establece cuándo usar comunicación síncrona (REST) y cuándo usar comunicación asíncrona (eventos), y las reglas de resiliencia que aplican en cada caso.

## Contenido

### Tipos de comunicación

#### REST síncrono

Se usa cuando el servicio necesita una respuesta inmediata para continuar su operación.

```
Cuándo usarlo:
  ✅ El resultado es necesario para continuar el procesamiento
  ✅ La operación es una consulta de datos en tiempo real
  ✅ Se necesita confirmación inmediata

Ejemplos en el sistema:
  scheduling-service → training-environment-service
    GET /api/v1/ambientes/disponibilidad?franja={id}
    (necesita saber si el ambiente está libre antes de asignar)

  scheduling-service → actors-service
    GET /api/v1/instructores/{id}/disponibilidad
    (necesita confirmar disponibilidad antes de asignar sesión)

  cualquier servicio → iam-service
    GET /api/v1/auth/validate
    (necesita validar el token antes de procesar la solicitud)
```

#### Eventos asíncronos

Se usa cuando el servicio no necesita esperar la respuesta para continuar.

```
Cuándo usarlo:
  ✅ La operación puede procesarse en segundo plano
  ✅ Múltiples servicios deben reaccionar al mismo hecho
  ✅ No se necesita respuesta inmediata

Ejemplos en el sistema:
  scheduling-service emite HorarioPublicado
    → document-service genera el PDF (no bloquea al coordinador)
    → monitoring-service inicia seguimiento de KPIs
    → audit-service registra la publicación

  academic-management-service emite FichaCreada
    → scheduling-service prepara el contexto para generar horario
    → audit-service registra la creación
```

---

### Mapa de comunicación entre servicios

```
iam-service
  ← todos los servicios lo consultan para validar tokens

reference-data-service
  ← academic-management-service (centros, catálogos)
  ← training-environment-service (centros, catálogos)
  ← actors-service (catálogos, estados)

academic-management-service
  → emite: FichaCreada, FichaCambioEstado
  ← scheduling-service lo consulta para obtener datos de fichas

training-environment-service
  → emite: AmbienteDisponible, AmbienteReservado, AmbienteEnMantenimiento
  ← scheduling-service lo consulta para disponibilidad

actors-service
  → emite: DisponibilidadActualizada, EtapaProductivaIniciada
  ← scheduling-service lo consulta para disponibilidad de instructores

scheduling-service  ← CORE
  → emite: HorarioGenerado, HorarioPublicado, ConflictoDetectado, ConflictoResuelto
  ← consume eventos de: academic, training-environment, actors

document-service
  → consume: HorarioPublicado
  → emite: DocumentoGenerado

monitoring-service
  → consume: HorarioPublicado, ConflictoDetectado
  → emite: AlertaGenerada, NotificacionEnviada

audit-service
  → consume eventos de TODOS los servicios
  → no emite eventos
  → no recibe llamadas directas de usuarios
```

---

### Reglas de resiliencia

```
1. Timeout: toda llamada REST entre servicios debe tener timeout definido
   Recomendado: 5 segundos para consultas, 30 segundos para operaciones pesadas

2. Retry: las llamadas fallidas pueden reintentarse máximo 3 veces
   con backoff exponencial (1s, 2s, 4s)

3. Circuit breaker: si un servicio falla repetidamente,
   el circuit breaker lo aísla para evitar cascada de fallos

4. Fallback: si un servicio no responde, el servicio llamante
   debe tener un comportamiento degradado definido
   (no simplemente fallar sin mensaje)

5. Idempotencia: las operaciones que pueden reintentarse
   deben ser idempotentes (mismo resultado si se ejecutan múltiples veces)
```

---

### Regla absoluta

```
❌ Ningún servicio accede directamente a la base de datos de otro servicio
✅ Toda interacción entre servicios pasa por API REST o eventos
```

## Referencias

- [service-catalog.md](./service-catalog.md) — Catálogo de servicios
- [02-domain/domain-events.md](../02-domain/domain-events.md) — Eventos de dominio
- [05-architecture/cross-cutting.md](../05-architecture/cross-cutting.md) — Aspectos transversales
- [07-api/guidelines.md](../07-api/guidelines.md) — Lineamientos de API