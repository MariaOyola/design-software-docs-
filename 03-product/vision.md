# Visión del Producto

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Este documento define la visión, los objetivos de producto y la propuesta de valor del sistema de gestión de horarios del SENA. Es la estrella norte del proyecto: toda decisión de producto debe evaluarse contra lo que aquí se define.

## Contenido

### Declaración de visión

> Permitir que los coordinadores académicos del SENA generen horarios sin conflictos en minutos, garantizando visibilidad anticipada para instructores y aprendices, y optimizando el uso de los ambientes de formación disponibles.

---

### Problema que resuelve

| Problema actual | Impacto |
|---|---|
| Los horarios se construyen manualmente en hojas de cálculo | El proceso toma días y depende del conocimiento de una sola persona |
| No existe detección automática de conflictos | Ambientes e instructores quedan doble asignados sin saberlo |
| Instructores y aprendices no conocen su horario con anticipación | Afecta asistencia, organización personal y calidad de la formación |
| No hay trazabilidad de cambios en los horarios | Cuando algo falla no se sabe qué cambió ni quién lo cambió |

---

### Propuesta de valor

**Para el Coordinador Académico:**
Generar y publicar horarios sin conflictos en minutos, con detección automática de inconsistencias y resolución asistida.

**Para el Instructor:**
Conocer con anticipación dónde y cuándo son sus sesiones, y recibir notificación inmediata cuando algo cambie.

**Para el Aprendiz:**
Acceder al horario de su ficha en cualquier momento, con información actualizada y confiable.

**Para la Institución:**
Optimizar el uso de ambientes de formación, reducir cancelaciones de último momento y tener trazabilidad completa de la operación académica.

---

### Usuarios del sistema

| Usuario | Rol en el sistema | Necesidad principal |
|---|---|---|
| Coordinador Académico | Coordinador | Generar y publicar horarios sin conflictos |
| Instructor | Instructor | Consultar su horario y recibir notificaciones de cambios |
| Aprendiz | Aprendiz | Ver el horario de su ficha actualizado |
| Administrador SENA | Administrador | Configurar parámetros, roles y datos maestros |

---

### Criterios de éxito del producto

```
✅ Un coordinador puede generar el horario completo de una ficha
   en menos de 5 minutos sin conflictos pendientes

✅ El sistema detecta automáticamente el 100% de los conflictos
   de ambiente e instructor antes de publicar

✅ Instructores y aprendices ven su horario actualizado
   en menos de 1 minuto después de una publicación

✅ Toda acción relevante queda registrada en auditoría
   de forma inmutable

✅ El sistema está disponible durante el horario académico
   del SENA sin interrupciones no planificadas
```

## Referencias

- [roadmap.md](./roadmap.md) — Fases y evolución del producto
- [product-backlog.md](./product-backlog.md) — Funcionalidades priorizadas
- [01-context/overview.md](../01-context/overview.md) — Contexto institucional
- [01-context/scope.md](../01-context/scope.md) — Alcance y restricciones
- [04-requirements/functional.md](../04-requirements/functional.md) — Requisitos derivados de esta visión