# Configuración del Entorno Local

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria
> Autor: Por definir | Equipo: Por definir

## Contexto

Guía para que un desarrollador nuevo pueda levantar el sistema completo en su máquina local. Seguir los pasos en el orden indicado.

## Contenido

### Requisitos previos

| Herramienta | Versión mínima | Para qué se usa |
|---|---|---|
| Docker | 24.x | Contenedores de servicios y BDs |
| Docker Compose | 2.x | Orquestación local de los 9 servicios |
| Git | 2.x | Control de versiones |
| Java JDK | 17+ | Backend de microservicios |
| Node.js | 18+ | Frontend (si aplica) |
| psql | 14+ | Acceso directo a BDs para debugging |

---

### Clonar los repositorios

```bash
# Repositorio de documentación
git clone https://github.com/[org]/design-software-docs
cd design-software-docs
git checkout develop

# Repositorios de servicios (uno por microservicio)
git clone https://github.com/[org]/iam-service
git clone https://github.com/[org]/reference-data-service
git clone https://github.com/[org]/academic-management-service
git clone https://github.com/[org]/training-environment-service
git clone https://github.com/[org]/scheduling-service
git clone https://github.com/[org]/actors-service
git clone https://github.com/[org]/document-service
git clone https://github.com/[org]/monitoring-service
git clone https://github.com/[org]/audit-service
```

---

### Variables de entorno

Cada servicio tiene un archivo `.env.example` en su raíz. Copiar y completar:

```bash
cp .env.example .env
# Editar .env con los valores del ambiente local
```

> ⚠️ Nunca subir el archivo `.env` al repositorio.
> Ver `00-governance/security-rules.md`.

---

### Levantar el sistema con Docker Compose

```bash
# Levantar todos los servicios y sus BDs
docker compose up -d

# Verificar que todos los contenedores están corriendo
docker compose ps

# Ver logs de un servicio específico
docker compose logs -f iam-service
```

---

### Verificar que el sistema está sano

```bash
# Verificar cada servicio por su healthcheck
curl http://localhost:8081/api/v1/health  # iam-service
curl http://localhost:8082/api/v1/health  # reference-data-service
curl http://localhost:8083/api/v1/health  # academic-management-service
curl http://localhost:8084/api/v1/health  # training-environment-service
curl http://localhost:8085/api/v1/health  # scheduling-service
curl http://localhost:8086/api/v1/health  # actors-service
curl http://localhost:8087/api/v1/health  # document-service
curl http://localhost:8088/api/v1/health  # monitoring-service
curl http://localhost:8089/api/v1/health  # audit-service
```

---

### Carga inicial de datos maestros

```bash
# Ejecutar scripts de seed en ref_db
docker compose exec reference-data-service ./scripts/seed.sh
```

Esto carga: macroregiones, centros de formación, catálogos y parámetros iniciales.

---

### Problemas frecuentes

| Problema | Causa probable | Solución |
|---|---|---|
| Puerto ya en uso | Otro proceso ocupa el puerto | `lsof -i :[puerto]` y matar el proceso |
| BD no conecta | Variables de entorno incorrectas | Revisar `.env` del servicio |
| Contenedor en CrashLoopBackOff | Error en el código o config | `docker compose logs [servicio]` |
| Seed falla | BD no inicializada | `docker compose down -v` y volver a levantar |

## Referencias

- [environments.md](./environments.md) — Ambientes y sus diferencias
- [ci-cd.md](./ci-cd.md) — Pipeline de integración continua
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Puertos y repos de cada servicio