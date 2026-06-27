# Aspectos Transversales

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los aspectos que aplican a todos los microservicios por igual: seguridad, logging, manejo de errores y auditoría. Cada servicio debe implementarlos de forma consistente.

## Contenido

### Autenticación y autorización

Todo microservicio debe:

```
1. Recibir el token JWT en el header: Authorization: Bearer <token>
2. Validar el token con iam-service antes de procesar la solicitud
3. Verificar que el rol del usuario tiene permiso para la operación
4. Rechazar solicitudes sin token válido con HTTP 401
5. Rechazar solicitudes sin permiso suficiente con HTTP 403
```

Roles del sistema y sus capacidades generales:

| Rol | Capacidades principales |
|---|---|
| Administrador | Acceso total — gestión de usuarios, roles y parámetros |
| Coordinador | Gestión de fichas, horarios, ambientes e instructores |
| Instructor | Consulta de horario propio y registro de disponibilidad |
| Aprendiz | Consulta de horario de su ficha |

---

### Manejo de errores

Todos los servicios deben retornar errores en el mismo formato:

```json
{
  "error": "CODIGO_ERROR",
  "message": "Descripción clara del error para el usuario",
  "timestamp": "2026-06-21T10:30:00Z",
  "service": "nombre-del-servicio"
}
```

Códigos HTTP estándar:

| Código | Cuándo usarlo |
|---|---|
| 400 | Datos de entrada inválidos |
| 401 | Token ausente o inválido |
| 403 | Sin permiso para la operación |
| 404 | Recurso no encontrado |
| 409 | Conflicto (ej: doble reserva de ambiente) |
| 500 | Error interno del servicio |

---

### Logging

Cada servicio debe registrar:

```
- Solicitudes recibidas: método, ruta, usuario y timestamp
- Errores con stack trace completo
- Eventos emitidos y consumidos
- Tiempo de respuesta de operaciones críticas
```

Los logs nunca deben contener:
```
❌ Contraseñas o tokens completos
❌ Datos personales de aprendices o instructores
❌ Credenciales de bases de datos
```

---

### Auditoría

Toda acción relevante debe publicar un evento hacia `audit-service`:

```
Acciones que siempre se auditan:
  - Creación, modificación o eliminación de cualquier entidad
  - Cambios de estado (ficha, horario, ambiente)
  - Publicación de horarios
  - Asignación y revocación de roles
  - Intentos de acceso fallidos
```

El `audit-service` consume estos eventos de forma asíncrona. Los servicios no esperan confirmación de auditoría para responder al cliente.

---

### Comunicación entre servicios

```
REST síncrono  → cuando se necesita respuesta inmediata
                 ejemplo: scheduling consulta disponibilidad de ambiente

Eventos        → cuando no se necesita esperar
                 ejemplo: HorarioPublicado → document-service genera PDF

Regla absoluta → ningún servicio accede directamente a la BD de otro
```

## Referencias

- [overview.md](./overview.md) — Principios de arquitectura
- [decisions/](./decisions/) — ADRs que justifican estas decisiones
- [07-api/authentication.md](../07-api/authentication.md) — Detalle de autenticación en API
- [00-governance/security-rules.md](../00-governance/security-rules.md) — Reglas de seguridad del repositorio