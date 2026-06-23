# Reglas de seguridad

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Maria | Equipo: Por definir

Este documento define qué información nunca puede aparecer en ningún archivo de este repositorio, sin excepción. Para convenciones de Git, ver [git-conventions.md](./git-conventions.md). Para reglas generales de documentación, ver [documentation-rules.md](./documentation-rules.md).

## Contexto

Un repositorio de documentación puede parecer inofensivo comparado con el código fuente, pero contiene información que puede comprometer todo el sistema si se maneja mal: credenciales de bases de datos, tokens de acceso, datos personales de aprendices e instructores. Estas reglas aplican a todos los archivos del repo, incluyendo ejemplos, plantillas y borradores en ramas hijas.

## Contenido

### Qué nunca puede aparecer

**Credenciales e infraestructura**

```
❌ Contraseñas de bases de datos (iam_db, scheduling_db, audit_db, etc.)
❌ Connection strings con credenciales reales
❌ API keys o tokens de acceso reales
❌ Credenciales de servicios cloud (AWS, GCP, Azure)
❌ IPs reales de servidores de producción, staging o qa
❌ URLs internas reales de servicios en producción
❌ Nombres de usuario reales de bases de datos
❌ Certificados o claves privadas (.pem, .key, .p12)
❌ Variables de entorno con valores reales (.env con datos reales)
```

**Datos personales**

Los servicios `iam-service` y `actors-service` manejan datos de personas reales. Ninguno de esos datos puede aparecer en la documentación, ni siquiera como ejemplo:

```
❌ Nombres reales de aprendices o instructores
❌ Números de documento de identidad
❌ Correos electrónicos reales
❌ Números de teléfono reales
❌ Fotografías o datos biométricos
❌ Información de empresas de etapa productiva con datos reales
```

**Información sensible del sistema**

```
❌ Estructura interna de redes o VPCs
❌ Nombres reales de contenedores o pods en producción
❌ Tokens JWT reales (ni siquiera expirados)
❌ Hashes de contraseñas reales
❌ Logs reales con datos de usuarios
```

---

### Cómo reemplazarlo en ejemplos

Cuando un documento necesite mostrar un ejemplo con datos, usar siempre datos ficticios o marcadores de posición:

| Dato prohibido | Reemplazar con |
|---|---|
| Contraseña real | `[REDACTED]` o `${DB_PASSWORD}` |
| Token JWT real | `eyJhbGciOiJIUzI1NiJ9.[REDACTED]` |
| IP de producción | `192.168.x.x` o `servidor.ejemplo.internal` |
| URL de producción | `https://api.ejemplo.sena.gov.co` |
| Nombre de aprendiz real | `Juan Pérez (ficticio)` |
| Correo real | `usuario.ejemplo@sena.edu.co` |
| Documento de identidad | `1234567890 (ficticio)` |
| Credencial de BD | `jdbc:postgresql://localhost:5432/iam_db` (sin usuario ni contraseña) |

**Ejemplo correcto de documentación de conexión:**

```
# Correcto
Base de datos: iam_db
Host: ${DB_HOST}
Puerto: ${DB_PORT}
Usuario: ${DB_USER}
Contraseña: ${DB_PASSWORD}

# Incorrecto — nunca hacer esto
Base de datos: iam_db
Host: 10.0.1.45
Puerto: 5432
Usuario: admin_iam
Contraseña: M1C0ntr4s3ña!
```

---

### Qué hacer si ya se subió información prohibida

Borrar el archivo o el contenido en un nuevo commit **no es suficiente**. El commit anterior sigue existiendo en el historial de Git y cualquiera puede verlo.

El proceso correcto es:

```
1. Notificar inmediatamente al líder técnico o al instructor
2. Revocar la credencial o token expuesto (cambiar contraseña,
   invalidar token) — esto es lo primero y más urgente
3. Limpiar el historial de Git:
   git filter-branch o git filter-repo para eliminar el commit
4. Hacer force push de la rama limpia
5. Si ya llegó a main, notificar a todo el equipo para
   que actualicen su copia local
6. Registrar el incidente en 15-project-control/open-questions.md
   con fecha, qué se expuso y cómo se resolvió
```

> ⚠️ Si la credencial expuesta da acceso a cualquiera de las 9 bases de datos del sistema (`iam_db`, `ref_db`, `academic_db`, `env_db`, `scheduling_db`, `actors_db`, `document_db`, `monitoring_db`, `audit_db`), el paso 2 es inmediato sin importar la hora.

---

### Revisión en PR

Todo PR debe verificar que no se incluye información prohibida antes de aprobarse. Esta verificación forma parte del checklist de [definition-of-done.md](./definition-of-done.md).

Si hay duda sobre si un dato es sensible o no, la respuesta por defecto es que sí lo es. Consultar con el líder técnico antes de incluirlo.

## Referencias

- [documentation-rules.md](./documentation-rules.md)
- [git-conventions.md](./git-conventions.md)
- [definition-of-ready.md](./definition-of-ready.md)
- [definition-of-done.md](./definition-of-done.md)
- [microservices-documentation.md](./microservices-documentation.md)