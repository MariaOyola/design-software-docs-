# Definition of Ready

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Maria  | Equipo: Por definir

Este documento define el checklist que el **autor** debe completar antes de abrir un Pull Request. Si algún ítem no se cumple, el documento no está listo para revisión. Para el checklist de cierre, ver [definition-of-done.md](./definition-of-done.md).

## Contexto

Un documento puede estar bien escrito pero no estar listo para revisión si le falta el encabezado, no está enlazado desde su sección o el commit tiene el formato incorrecto. Este checklist evita que el revisor pierda tiempo señalando problemas de forma en lugar de revisar el contenido real.

## Contenido

### Checklist general

Aplica a todo documento del repositorio sin excepción:

```
[ ] El archivo tiene encabezado completo:
      # Título descriptivo
      > Estado: 🔴 o 🟡 | Última actualización: YYYY-MM-DD
      > Autor: nombre | Equipo: nombre

[ ] El estado es 🔴 Pendiente o 🟡 En progreso (nunca vacío)

[ ] El nombre del archivo está en kebab-case.md
      Correcto:   data-model.md, api-contract.md
      Incorrecto: Data Model.md, dataModel.md

[ ] El archivo está enlazado desde el README.md de su sección

[ ] Las secciones mínimas están presentes:
      ## Contexto
      ## Contenido
      ## Referencias

[ ] El commit que agrega este archivo sigue el formato:
      docs(NN-seccion): mensaje en inglés en presente

[ ] La rama sigue el patrón:
      feat/doc-[sección]-[tema]
      fix/doc-[sección]-[tema]

[ ] No contiene secretos, contraseñas, tokens ni datos personales
      Ver criterio completo en security-rules.md

[ ] Si el documento tiene diagramas:
      - Existe la fuente editable (.puml, .wsd, .drawio)
      - La fuente está en 08-uml/diagrams/source/
      - El exportado está en 08-uml/diagrams/exports/
```

### Checklist adicional para microservicios

Aplica solo cuando el documento pertenece a un servicio dentro de `09-microservices/services/`:

```
[ ] El servicio está registrado en 09-microservices/service-catalog.md

[ ] Las entidades documentadas en data-model.md coinciden exactamente
    con la tabla oficial de service-catalog.md
    (no se inventan entidades sin aprobación de arquitectura)

[ ] La estructura de carpetas del servicio sigue la plantilla:
      09-microservices/services/[NN-nombre-service]/
        ├── README.md
        ├── data-model.md
        ├── events.md
        ├── api-contract.md
        └── runbook.md

[ ] El servicio está referenciado en 09-microservices/README.md
```

### ¿Qué hacer si un ítem no se cumple?

No se abre el PR. Se corrige primero y luego se vuelve a pasar el checklist completo. No hay ítems opcionales.

Si hay duda sobre si un ítem aplica o no al documento que se está revisando, la respuesta por defecto es que sí aplica. Para casos excepcionales, consultar con el líder técnico antes de abrir el PR.

## Referencias

- [documentation-rules.md](./documentation-rules.md)
- [git-conventions.md](./git-conventions.md)
- [definition-of-done.md](./definition-of-done.md)
- [security-rules.md](./security-rules.md)
- [microservices-documentation.md](./microservices-documentation.md)