# Wireframes

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Por definir | Equipo: Por definir

## Contexto

Referencia de wireframes e interacciones de las pantallas principales del sistema. Los wireframes visuales (imágenes) se almacenan en `assets/images/`, este documento describe su contenido y flujo de interacción.

## Contenido

### Wireframes pendientes por pantalla

| Pantalla | Rol principal | Prioridad | Estado |
|---|---|---|---|
| Login | Todos | 🔴 Alta | 🔴 Pendiente |
| Dashboard Coordinador | Coordinador | 🔴 Alta | 🔴 Pendiente |
| Lista de fichas activas | Coordinador | 🔴 Alta | 🔴 Pendiente |
| Generación de horario | Coordinador | 🔴 Alta | 🔴 Pendiente |
| Vista de conflictos | Coordinador | 🔴 Alta | 🔴 Pendiente |
| Calendario semanal (consulta) | Instructor, Aprendiz | 🔴 Alta | 🔴 Pendiente |
| Disponibilidad de ambientes | Coordinador | 🟠 Media | 🔴 Pendiente |
| Disponibilidad de instructor | Instructor | 🟠 Media | 🔴 Pendiente |
| Notificaciones | Instructor, Aprendiz | 🟡 Baja | 🔴 Pendiente |
| Panel de auditoría | Administrador | 🟡 Baja | 🔴 Pendiente |

---

### Interacciones clave a documentar

**Generación de horario (la más crítica)**
```
1. Coordinador selecciona ficha desde la lista
2. Click en "Generar horario"
3. Sistema muestra estado de carga (puede tardar hasta 30s)
4. Sistema muestra horario en Borrador con conflictos resaltados en rojo
5. Coordinador hace click en un conflicto para ver opciones de resolución
6. Al resolver todos los conflictos, el botón "Publicar" se habilita
7. Click en "Publicar" muestra confirmación antes de ejecutar
8. Tras publicar, se muestra mensaje de éxito y notificación enviada
```

**Consulta de horario (instructor/aprendiz)**
```
1. Usuario entra a "Mi horario"
2. Sistema muestra vista de calendario semanal
3. Cada sesión muestra: ambiente, hora, ficha (si es instructor)
4. Click en una sesión muestra detalle expandido
```

---

### Formato de entrega de wireframes

```
Cada wireframe debe incluir:
[ ] Nombre de la pantalla
[ ] Rol(es) que la usan
[ ] Imagen del wireframe en assets/images/
[ ] Descripción de los elementos interactivos principales
[ ] Estados de la pantalla (vacío, cargando, con datos, con error)
```

## Referencias

- [design-system.md](./design-system.md) — Componentes y patrones visuales
- [navigation-map.md](./navigation-map.md) — Cómo se conectan estas pantallas
- [assets/images/](../assets/images/) — Ubicación de las imágenes de wireframes