# Manual de Administración

> Estado: 🟡  En progreso | Última actualización: 2026-06-30
> Autor: Maria| Equipo: Por definir

## Contexto

Guía para el administrador del sistema. Cubre la gestión de usuarios, roles, datos maestros y configuración del sistema. Para procedimientos operativos ante fallos técnicos, ver [`13-operations/`](../13-operations/).

## Contenido

### Gestión de usuarios

**Cómo crear un nuevo usuario**
```
1. Ve a "Usuarios y roles" en el panel de administración
2. Click en "Nuevo usuario"
3. Ingresa nombre, correo institucional y rol inicial
4. El usuario recibirá instrucciones para crear su contraseña
```

**Cómo asignar o revocar un rol**
```
1. Busca el usuario en la lista
2. Click en "Editar roles"
3. Activa o desactiva los roles según corresponda
4. Los cambios aplican de forma inmediata
```

**Roles disponibles:**
| Rol | Puede hacer |
|---|---|
| Administrador | Todo — gestión de usuarios, datos maestros, auditoría |
| Coordinador | Fichas, horarios, ambientes, instructores |
| Instructor | Consultar su horario, registrar disponibilidad |
| Aprendiz | Consultar el horario de su ficha |

---

### Gestión de datos maestros

**Cómo agregar un centro de formación**
```
1. Ve a "Centros de formación"
2. Click en "Nuevo centro"
3. Ingresa nombre, macroregión y ubicación
4. Guarda — el centro queda disponible para asociar ambientes y fichas
```

**Cómo agregar un valor a un catálogo**
```
1. Ve a "Catálogos"
2. Selecciona el catálogo a modificar (modalidades, jornadas, tipos de ambiente, etc.)
3. Click en "Agregar valor"
4. El valor queda disponible inmediatamente en el sistema
```

**Cómo modificar un parámetro del sistema**
```
1. Ve a "Parámetros"
2. Busca el parámetro a modificar
3. Edita el valor y guarda
4. El cambio aplica de forma inmediata a todos los procesos que lo usan
```

---

### Auditoría

**Cómo consultar el log de auditoría**
```
1. Ve a "Auditoría" en el panel de administración
2. Filtra por usuario, fecha o tipo de acción
3. Los registros muestran qué se hizo, cuándo y quién lo hizo
4. Los registros no pueden modificarse ni eliminarse
```

---

### Escalamiento de soporte

| Nivel | Situación | Quién atiende |
|---|---|---|
| Nivel 1 | Dudas de uso, preguntas frecuentes | Administrador del sistema |
| Nivel 2 | Error técnico o comportamiento inesperado | Equipo de desarrollo |
| Nivel 3 | Incidente crítico (sistema caído, pérdida de datos) | Líder técnico — seguir 13-operations/incident-management.md |

## Referencias

- [user-manual.md](./user-manual.md) — Manual para usuarios finales
- [technical-onboarding.md](./technical-onboarding.md) — Onboarding técnico
- [13-operations/](../13-operations/) — Operación y respuesta a incidentes