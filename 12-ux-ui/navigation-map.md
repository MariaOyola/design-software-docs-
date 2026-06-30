# Mapa de Navegación

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Por definir | Equipo: Por definir

## Contexto

Define la jerarquía de pantallas del sistema y cómo se navega entre ellas según el rol del usuario autenticado.

## Contenido

### Navegación por rol

```
Login
  ↓
Dashboard (según rol)

COORDINADOR
  └── Dashboard
        ├── Fichas
        │     ├── Lista de fichas activas
        │     └── Detalle de ficha
        │           └── Generar / editar horario
        │                 ├── Vista de conflictos
        │                 └── Publicar horario
        ├── Ambientes
        │     ├── Lista de ambientes
        │     ├── Disponibilidad
        │     └── Registrar mantenimiento
        ├── Instructores
        │     └── Disponibilidad por instructor
        └── Reportes
              └── Exportar horario en PDF

INSTRUCTOR
  └── Dashboard
        ├── Mi horario
        ├── Mi disponibilidad
        └── Notificaciones

APRENDIZ
  └── Dashboard
        ├── Horario de mi ficha
        └── Notificaciones

ADMINISTRADOR
  └── Dashboard
        ├── Usuarios y roles
        ├── Centros de formación
        ├── Catálogos y parámetros
        └── Auditoría
```

---

### Pantallas compartidas entre roles

| Pantalla | Roles que acceden |
|---|---|
| Login | Todos |
| Notificaciones | Coordinador, Instructor, Aprendiz |
| Perfil propio | Todos |

---

### Reglas de navegación

```
1. El menú lateral muestra solo las opciones permitidas para el rol activo
2. Un usuario sin sesión válida es redirigido al Login automáticamente
3. Las acciones restringidas por rol no se muestran en la UI
   (no solo se bloquean en backend)
```

## Referencias

- [design-system.md](./design-system.md) — Componentes y patrones visuales
- [wireframes.md](./wireframes.md) — Wireframes de cada pantalla
- [07-api/authentication.md](../07-api/authentication.md) — Roles y permisos del sistema