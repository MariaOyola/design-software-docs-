# Definition of Done

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Maria | Equipo: Por definir

Este documento define el checklist que se debe completar antes de hacer merge de un PR a `develop`. Lo aplica el revisor, o el autor si trabaja solo. Para el checklist previo a abrir el PR, ver [definition-of-ready.md](./definition-of-ready.md).

## Contexto

Un documento puede haber pasado el `definition-of-ready` y aun así no estar listo para merge si el contenido es inconsistente con otros documentos, los enlaces internos están rotos o el estado no fue actualizado. Este checklist cierra ese hueco y garantiza que lo que llega a `develop` es documentación real y confiable.

## Contenido

### Checklist general

Aplica a todo documento del repositorio sin excepción:

```
[ ] Pasó todos los ítems de definition-of-ready.md sin excepciones

[ ] El estado fue actualizado a 🟢 Estable
      Un documento no puede mergearse con estado 🔴 o 🟡

[ ] El contenido es coherente con los demás documentos del repo:
      - No contradice lo definido en otros archivos
      - No duplica contenido que ya existe en otra sección
      - Si referencia otro documento, ese documento existe

[ ] Todos los enlaces internos funcionan:
      - Los [texto](./ruta.md) apuntan a archivos reales
      - No hay enlaces rotos ni rutas inventadas

[ ] El archivo está enlazado desde el README.md de su sección
      (Este ítem no aplica al README.md de gobernanza,
      que se enlaza desde el README.md raíz del repositorio)

[ ] Si el cambio afecta a múltiples secciones o equipos:
      CHANGELOG.md fue actualizado con una entrada que describe el cambio


[ ] El estado fue actualizado a 🟢 Estable

    Excepción: durante la construcción inicial de una sección,
    los documentos pueden mergearse a develop en 🟡.
    Deben estar en 🟢 antes del PR de develop → qa.
```

### Checklist adicional para microservicios

Aplica solo cuando el documento pertenece a un servicio dentro de `09-microservices/services/`:

```
[ ] El servicio está registrado en 09-microservices/service-catalog.md
      con su nombre, BD y lista de entidades correcta

[ ] Las entidades en data-model.md coinciden exactamente con
    la tabla oficial del instructor:

    iam-service          → iam_db
                           usuario, rol, permiso, sesion, token

    reference-data-service → ref_db
                           macroregion, centro_formacion, catalogo,
                           estado, parametro

    academic-management-service → academic_db
                           programa, competencia, RAP, ficha, oferta

    training-environment-service → env_db
                           ambiente, inventario, mantenimiento,
                           reserva, disponibilidad

    scheduling-service   → scheduling_db
                           horario, sesion_clase, franja,
                           asignacion, conflicto

    actors-service       → actors_db
                           instructor, aprendiz, empresa,
                           etapa_productiva, bitacora

    document-service     → document_db
                           documento, version, plantilla

    monitoring-service   → monitoring_db
                           seguimiento_kpi, alerta, notificacion,
                           sesion_seguimiento, plan_mejoramiento

    audit-service        → audit_db
                           auditoria (append-only, sin updates)

[ ] Si el servicio tiene restricciones especiales de comportamiento
    (como append-only en audit-service), están documentadas
    de forma explícita en data-model.md

[ ] El indicador de gobernabilidad en 09-microservices/README.md
    fue actualizado para reflejar el nuevo estado del servicio:
      🟢 Bueno    → documentación completa y revisada
      🟡 Regular  → existe pero incompleta
      🔴 Malo     → no existe o gravemente desactualizada
```

### ¿Qué hacer si un ítem no se cumple?

No se hace merge. Se deja el PR abierto, se corrige lo que falta con un nuevo commit en la misma rama y se vuelve a pasar el checklist completo.

Si hay un ítem que genuinamente no aplica al documento que se está cerrando, se deja una nota en el PR explicando por qué no aplica. No se omite en silencio.

### Estado del proyecto al terminar esta carpeta

Cuando los 7 archivos de `00-governance` hayan pasado este checklist y estén mergeados en `develop`, se abre el PR de `develop → qa`. Ese es el primer ciclo completo del proyecto.

```
00-governance completa en develop
        ↓
PR develop → qa
        ↓
Revisión del conjunto como sección coherente
        ↓
qa → stg → main
        ↓
Arrancar con 01-context en develop
```

## Referencias

- [definition-of-ready.md](./definition-of-ready.md)
- [documentation-rules.md](./documentation-rules.md)
- [git-conventions.md](./git-conventions.md)
- [security-rules.md](./security-rules.md)
- [microservices-documentation.md](./microservices-documentation.md)