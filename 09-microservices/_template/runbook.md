# Runbook — [Nombre del Servicio]

> Este archivo es una PLANTILLA. Copiar a `09-microservices/services/[NN-nombre-service]/runbook.md`
> y eliminar esta línea antes de hacer commit.

> Estado: 🔴 Pendiente | Última actualización: YYYY-MM-DD
> Autor: Por definir | Equipo: Por definir

## Contexto

Procedimientos operativos para cuando este servicio falla en producción. Escrito para que cualquier persona del equipo pueda seguirlo a cualquier hora sin conocimiento previo del servicio.

## Contenido

### Variables de entorno requeridas

<!--
Listar las variables sin valores reales. Ver security-rules.md.
-->

| Variable | Descripción | Requerida |
|---|---|---|
| `DB_HOST` | Host de la base de datos | Sí |
| `DB_PORT` | Puerto de la base de datos | Sí |
| `DB_NAME` | Nombre de la base de datos | Sí |
| `DB_USER` | Usuario de la base de datos | Sí |
| `DB_PASSWORD` | Contraseña de la base de datos | Sí |
| `JWT_PUBLIC_KEY` | Clave pública para validar tokens JWT | Sí |
| `[VARIABLE_ESPECIFICA]` | Descripción | Sí/No |

---

### Verificar que el servicio está sano

```bash
# Verificar que el contenedor está corriendo
docker ps | grep [nombre-servicio]

# Verificar el healthcheck
curl http://localhost:[puerto]/api/v1/health

# Respuesta esperada
{ "status": "UP", "service": "[nombre-servicio]" }
```

---

### Revisar logs

```bash
# Ver logs de los últimos 15 minutos
docker logs [nombre-servicio] --since=15m

# Buscar errores
docker logs [nombre-servicio] 2>&1 | grep -E "ERROR|FATAL"
```

---

### Procedimiento de reinicio

```bash
# 1. Verificar estado actual
docker ps -a | grep [nombre-servicio]

# 2. Detener el servicio
docker stop [nombre-servicio]

# 3. Reiniciar el servicio
docker start [nombre-servicio]

# 4. Verificar que levantó correctamente
docker logs [nombre-servicio] --tail=50
```

---

### Síntomas comunes y soluciones

| Síntoma | Causa probable | Pasos |
|---|---|---|
| El servicio no responde | Contenedor caído | Ejecutar procedimiento de reinicio |
| Error 500 en todos los endpoints | Problema de conexión a BD | Verificar variables de entorno y conectividad a `[nombre_db]` |
| Error de token inválido | `iam-service` no disponible | Verificar estado de `iam-service` |
| [Síntoma específico del servicio] | [Causa] | [Pasos] |

---

### Rollback

```bash
# 1. Identificar la versión anterior estable
docker images [nombre-servicio] --format "table {{.Tag}}\t{{.CreatedAt}}"

# 2. Detener la versión actual
docker stop [nombre-servicio]

# 3. Levantar la versión anterior
docker run -d --name [nombre-servicio] [nombre-servicio]:[version-anterior]

# 4. Verificar funcionamiento
curl http://localhost:[puerto]/api/v1/health
```

---

### Cuándo escalar

```
Escalar a líder técnico si:
  - El servicio no levanta después de 3 intentos de reinicio
  - Hay pérdida de datos en la base de datos
  - El problema afecta a más de un servicio simultáneamente
  - No se identifica la causa en 30 minutos
```

## Referencias

- [README.md](./README.md) — Contexto del servicio
- [13-operations/incident-management.md](../../13-operations/incident-management.md) — Gestión de incidentes
- [13-operations/observability.md](../../13-operations/observability.md) — Monitoreo y alertas