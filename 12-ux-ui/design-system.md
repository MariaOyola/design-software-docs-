# Sistema de Diseño

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los tokens, componentes, patrones visuales y reglas de UX/UI del sistema de gestión de horarios SENA. Garantiza consistencia visual entre las pantallas usadas por coordinadores, instructores y aprendices.

## Contenido

### Principios de diseño

```
1. Claridad sobre estética — los coordinadores trabajan bajo presión de tiempo
2. Prevención de errores — el sistema avisa antes de que un conflicto se publique
3. Accesibilidad — debe ser usable por personas con discapacidad visual o motriz
4. Consistencia — los mismos componentes se ven y comportan igual en todo el sistema
```

---

### Tokens de diseño

> ⚠️ Pendiente definir con el equipo de diseño: paleta de colores oficial,
> tipografía y espaciados. Esta sección se completa cuando el equipo de
> diseño defina los valores concretos.

| Token | Valor | Uso |
|---|---|---|
| `color-primary` | Por definir | Acciones principales (publicar, generar) |
| `color-danger` | Por definir | Conflictos y alertas |
| `color-success` | Por definir | Confirmaciones (horario publicado sin conflictos) |
| `font-family` | Por definir | Tipografía base del sistema |
| `spacing-unit` | Por definir | Unidad base de espaciado |

---

### Componentes principales

| Componente | Dónde se usa |
|---|---|
| Tabla de fichas | Consulta de fichas activas |
| Calendario semanal | Vista de horario por ficha, instructor o aprendiz |
| Indicador de conflicto | Resaltar sesiones con conflicto pendiente |
| Selector de disponibilidad | Instructor registra sus franjas disponibles |
| Tarjeta de ambiente | Mostrar disponibilidad de un ambiente |
| Badge de estado | Mostrar estado de ficha, horario o ambiente |

---

### Patrones visuales por estado

| Estado | Color sugerido | Dónde aplica |
|---|---|---|
| `EJECUCION` / `DISPONIBLE` / `ACTIVO` | Verde | Fichas, ambientes, instructores activos |
| `EN_MANTENIMIENTO` / `EN_REVISION` | Amarillo | Ambientes en mantenimiento, horarios en revisión |
| `CANCELADA` / `INACTIVO` | Rojo | Fichas canceladas, instructores inactivos |
| `PUBLICADO` | Azul | Horarios ya publicados |

---

### Accesibilidad

```
[ ] Contraste mínimo AA según WCAG 2.1
[ ] Navegación completa por teclado
[ ] Textos alternativos en iconos informativos
[ ] Tamaño de fuente mínimo legible (16px en cuerpo de texto)
```

## Referencias

- [navigation-map.md](./navigation-map.md) — Mapa de navegación del sistema
- [wireframes.md](./wireframes.md) — Wireframes de referencia
- [04-requirements/non-functional.md](../04-requirements/non-functional.md) — Requisitos de usabilidad