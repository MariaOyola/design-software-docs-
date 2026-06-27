# Vista General de Arquitectura

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Describe la arquitectura general del sistema de gestión de horarios SENA. Para decisiones técnicas específicas ver [`decisions/`](./decisions/). Para modelos de datos ver [`06-data/`](../06-data/).

## Contenido

### Estilo arquitectónico

El sistema adopta una arquitectura de **microservicios**, donde cada servicio:

```
✅ Tiene una responsabilidad única y bien definida
✅ Posee su propia base de datos (ningún servicio comparte BD)
✅ Se despliega de forma independiente en su propio contenedor
✅ Se comunica con otros servicios por API REST o eventos
✅ Puede fallar sin tumbar los demás servicios
```

### Los 9 microservicios

```
CAPA: INFRAESTRUCTURA
  01-iam-service                → autenticación, autorización, sesiones
  09-audit-service              → registro inmutable append-only

CAPA: DATOS MAESTROS
  02-reference-data-service     → macroregiones, centros, catálogos
  06-actors-service             → instructores, aprendices, empresas

CAPA: GESTIÓN ACADÉMICA
  03-academic-management-service → programas, fichas, RAPs
  04-training-environment-service → ambientes, reservas, disponibilidad

CAPA: CORE
  05-scheduling-service         → motor de horarios ⭐

CAPA: TRANSVERSALES
  07-document-service           → documentos, PDFs, plantillas
  08-monitoring-service         → KPIs, alertas, notificaciones
```

### Flujo principal del sistema

```
Cliente → API Gateway → iam-service (¿válido? ¿autorizado?)
                              ↓ sí
                      Servicio destino
                              ↓
                      audit-service (registro de toda acción)
```

### Comunicación entre servicios

| Tipo | Cuándo se usa | Ejemplo |
|---|---|---|
| **REST síncrono** | Cuando se necesita respuesta inmediata | Coordinador consulta disponibilidad de ambientes |
| **Eventos asíncronos** | Cuando no se necesita esperar la respuesta | HorarioPublicado → document-service genera PDF |

### Principios de arquitectura

```
1. Base de datos por servicio — ningún servicio accede a la BD de otro
2. API first — toda comunicación entre servicios pasa por API o eventos
3. Falla independiente — un servicio caído no tumba los demás
4. Auditoría total — toda acción relevante se registra en audit-service
5. Documentación antes del código — un servicio no llega a main sin documentación
```

## Referencias

- [deployment.md](./deployment.md) — Topología de despliegue
- [cross-cutting.md](./cross-cutting.md) — Aspectos transversales
- [decisions/](./decisions/) — ADRs con decisiones técnicas
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo de servicios
- [02-domain/domain-map.md](../02-domain/domain-map.md) — Mapa de dependencias entre servicios