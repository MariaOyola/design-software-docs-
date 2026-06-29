# UML

> Estado: 🟢 En progreso | Última actualización: 2026-06-28 | Equipo: Por definir

## Contexto

Repositorio de diagramas UML y arquitectura visual del sistema de gestión de horarios SENA. Todo diagrama debe tener fuente editable y exportación revisable. No se sube solo la imagen exportada sin su fuente.

## Contenido

### Archivos de esta carpeta

| Archivo | Descripción | Estado |
|---|---|---|
| [diagram-index.md](./diagram-index.md) | Índice de todas las fuentes y exportaciones registradas | 🟡 |
| [diagrams/source/](./diagrams/source/) | Fuentes editables de diagramas (`.wsd`, `.puml`) | 🔴 |
| [diagrams/exports/](./diagrams/exports/) | Exportaciones en `.svg` o `.png` | 🔴 |

### Convenciones

**Nombres de archivo:**
```
<dominio>-<tipo>.<ext>

Ejemplos:
  horario-sequence.wsd
  sistema-deployment.wsd
  iam-component.wsd
  ficha-state.wsd
  scheduling-activity.wsd
```

**Ubicación:**
```
Fuentes  → diagrams/source/   (.wsd o .puml)
Exports  → diagrams/exports/  (.svg preferido sobre .png)
```

**Tipos de diagrama soportados:**

| Tipo | Sufijo de archivo |
|---|---|
| Casos de uso | `*-use-case.wsd` |
| Clases | `*-class.wsd` |
| Secuencia | `*-sequence.wsd` |
| Actividad | `*-activity.wsd` |
| Estado | `*-state.wsd` |
| Componentes | `*-component.wsd` |
| Despliegue | `*-deployment.wsd` |

### Flujo para agregar un diagrama

```
1. Crear la fuente editable en diagrams/source/
   con el nombre correcto: <dominio>-<tipo>.wsd

2. Exportar a diagrams/exports/
   preferir .svg sobre .png

3. Registrar en diagram-index.md:
   - nombre del diagrama
   - tipo
   - ruta a la fuente
   - ruta al export
   - fecha

4. Commit en la rama correspondiente:
   feat/doc-uml-[nombre-diagrama]
```

### Relación con otras secciones

| Si necesitas saber... | Ve a... |
|---|---|
| Decisiones de arquitectura que originan un diagrama | [05-architecture/decisions/](../05-architecture/decisions/) |
| Vista general del sistema | [05-architecture/overview.md](../05-architecture/overview.md) |
| Topología de despliegue | [05-architecture/deployment.md](../05-architecture/deployment.md) |

## Referencias

- [diagram-index.md](./diagram-index.md)
- [00-governance/documentation-rules.md](../00-governance/documentation-rules.md)