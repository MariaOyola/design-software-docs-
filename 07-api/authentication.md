# Autenticación y Autorización

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Define la estrategia de autenticación y autorización del sistema. Todo microservicio debe implementar estos mecanismos de forma consistente. El servicio responsable de emitir y validar credenciales es `iam-service`.

## Contenido

### Estrategia general

El sistema usa **JWT (JSON Web Token)** para autenticación stateless:

```
1. El usuario envía sus credenciales a iam-service
2. iam-service valida y emite un token JWT firmado
3. El cliente incluye el token en cada solicitud
4. Cada microservicio valida el token con iam-service
5. Si el token es válido, el servicio verifica el rol y procesa la solicitud
```

---

### Flujo de autenticación

```
Cliente
  → POST /api/v1/auth/login
    { "username": "...", "password": "..." }
  ← 200 OK
    { "token": "eyJ...", "expiresIn": 3600 }

Cliente → [cualquier servicio]
  Header: Authorization: Bearer eyJ...
  ← 200 OK | 401 | 403
```

---

### Estructura del token JWT

El token contiene los siguientes claims:

```json
{
  "sub": "uuid-del-usuario",
  "username": "usuario@sena.edu.co",
  "roles": ["COORDINADOR"],
  "centroFormacion": "uuid-del-centro",
  "iat": 1718960000,
  "exp": 1718963600
}
```

---

### Validación en cada microservicio

Todo microservicio debe:

```
1. Extraer el token del header Authorization: Bearer <token>
2. Verificar la firma del token con la clave pública de iam-service
3. Verificar que el token no ha expirado
4. Verificar que el rol del usuario tiene permiso para la operación
5. Rechazar con 401 si el token es inválido o ausente
6. Rechazar con 403 si el rol no tiene el permiso requerido
```

---

### Roles y permisos por microservicio

#### `iam-service`
| Operación | Administrador | Coordinador | Instructor | Aprendiz |
|---|---|---|---|---|
| Crear usuario | ✅ | ❌ | ❌ | ❌ |
| Asignar rol | ✅ | ❌ | ❌ | ❌ |
| Ver usuarios | ✅ | ❌ | ❌ | ❌ |

#### `scheduling-service`
| Operación | Administrador | Coordinador | Instructor | Aprendiz |
|---|---|---|---|---|
| Generar horario | ✅ | ✅ | ❌ | ❌ |
| Publicar horario | ✅ | ✅ | ❌ | ❌ |
| Resolver conflicto | ✅ | ✅ | ❌ | ❌ |
| Consultar horario | ✅ | ✅ | ✅ (propio) | ✅ (su ficha) |

#### `training-environment-service`
| Operación | Administrador | Coordinador | Instructor | Aprendiz |
|---|---|---|---|---|
| Registrar ambiente | ✅ | ✅ | ❌ | ❌ |
| Ver disponibilidad | ✅ | ✅ | ✅ | ❌ |
| Registrar mantenimiento | ✅ | ✅ | ❌ | ❌ |

#### `actors-service`
| Operación | Administrador | Coordinador | Instructor | Aprendiz |
|---|---|---|---|---|
| Registrar instructor | ✅ | ✅ | ❌ | ❌ |
| Actualizar disponibilidad | ✅ | ✅ | ✅ (propia) | ❌ |
| Ver aprendices | ✅ | ✅ | ✅ (su ficha) | ❌ |

---

### Comunicación entre servicios

Cuando un microservicio llama a otro (servicio a servicio), usa un **token de servicio** diferente al token de usuario:

```
- El token de servicio se genera con credenciales del servicio, no del usuario
- Tiene un scope limitado: solo puede hacer las operaciones que necesita
- No representa a un usuario humano
- Su vigencia es más corta que la del token de usuario
```

> ⚠️ Los tokens de servicio nunca se almacenan en el repositorio.
> Se gestionan como variables de entorno según las reglas de
> `00-governance/security-rules.md`.

---

### Endpoints públicos

Los siguientes endpoints no requieren token:

```
POST /api/v1/auth/login    → obtener token
POST /api/v1/auth/register → registro de nuevo usuario (si aplica)
GET  /api/v1/health        → estado del servicio (healthcheck)
```

Todo lo demás requiere `Authorization: Bearer <token>` válido.

## Referencias

- [guidelines.md](./guidelines.md) — Convenciones generales de API
- [05-architecture/cross-cutting.md](../05-architecture/cross-cutting.md) — Aspectos transversales de seguridad
- [09-microservices/services/01-iam-service/](../09-microservices/services/01-iam-service/) — Implementación de autenticación
- [00-governance/security-rules.md](../00-governance/security-rules.md) — Reglas de seguridad del repositorio