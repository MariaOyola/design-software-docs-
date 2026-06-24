# Convenciones de Git

> Estado: 🟢 En progreso | Última actualización: 2026-06-21
> Autor: Maria | Equipo: Por definir

Este documento define cómo se trabaja con Git en este repositorio: nomenclatura de ramas, formato de commits y el flujo de trabajo entre ramas. Para reglas de documentos, ver [documentation-rules.md](./documentation-rules.md).

## Contexto

Con múltiples personas documentando al mismo tiempo es fácil generar conflictos, pisarse el trabajo o perder trazabilidad de qué cambió y por qué. Estas convenciones aseguran que el historial de Git sea legible, que los PRs sean revisables y que cualquier persona pueda entender el estado del proyecto con solo mirar las ramas activas.

## Contenido

### Ramas principales

Estas ramas existen siempre y nunca se trabaja directamente sobre ellas. Solo reciben cambios por Pull Request.

| Rama | Propósito |
|---|---|
| `main` | Producción. Solo contiene documentación aprobada y estable |
| `stg` | Staging. Pre-producción, validación final antes de main |
| `qa` | Control de calidad. Validación antes de pasar a stg |
| `develop` | Integración. Donde se juntan todas las ramas hijas |

**Flujo entre ramas principales:**

```
develop → qa → stg → main
```

Cada avance requiere que la rama destino acepte un PR desde la rama origen. Nunca se hace push directo.

> ⚠️ Pendiente definir con el equipo:
>
> ¿Quién decide cuándo `develop` pasa a `qa`?
>
> ¿Es manual por el líder técnico o existe un criterio automático?

---

## Opción - Por hito completo

`develop` pasa a `qa` cuando una sección completa está terminada; no se valida archivo por archivo.

### Ejemplo

```text
Toda la carpeta 00-governance
mergeada a develop
        ↓
Se abre Pull Request
develop → qa
        ↓
      Maria revisa
        ↓
Aprobado
        ↓
qa → stg → main
```

Por esta razón, es más conveniente revisar y aprobar toda la sección completa antes de promoverla a `qa`.

---

### Ramas hijas (donde se trabaja)

Toda la documentación nueva o corregida se trabaja en ramas hijas que nacen de `develop` y regresan a `develop` por PR.

**Patrón de nomenclatura:**

```
feat/doc-[sección]-[tema]   → contenido nuevo
fix/doc-[sección]-[tema]    → corrección de contenido existente
```

- `[sección]` es el nombre de la carpeta sin el número (ej: `governance`, `context`, `microservices`).
- `[tema]` describe el archivo o tópico concreto que se trabaja.
- Todo en `kebab-case`, sin espacios ni mayúsculas.

**Ejemplos con la estructura real del proyecto:**

```
feat/doc-governance-git-conventions
feat/doc-governance-security-rules
feat/doc-context-glossary
feat/doc-context-overview
feat/doc-domain-entities-and-rules
feat/doc-domain-events
feat/doc-requirements-non-functional
feat/doc-requirements-user-stories
feat/doc-architecture-overview
feat/doc-data-models
feat/doc-api-authentication
feat/doc-uml-diagram-index
feat/doc-microservices-iam-service-data-model
feat/doc-microservices-scheduling-service-events
feat/doc-microservices-audit-service-runbook
feat/doc-microservices-actors-service-data-model
fix/doc-governance-documentation-rules
fix/doc-microservices-audit-service-data-model
```

---

### Formato de commits

Se usa **Conventional Commits** en inglés. La estructura es:

```
docs(NN-seccion): mensaje corto en presente
```

- `docs` es el tipo. Toda documentación usa `docs`.
- `(NN-seccion)` es el número y nombre de la carpeta afectada.
- El mensaje describe qué se hizo, en presente, en inglés, sin mayúscula inicial ni punto final.

**Ejemplos reales del proyecto:**

```bash
docs(00-governance): add git conventions
docs(00-governance): add security rules
docs(01-context): add SENA domain glossary
docs(01-context): add project scope
docs(02-domain): add entities and business rules
docs(02-domain): add domain events catalog
docs(04-requirements): add non-functional requirements
docs(05-architecture): add architecture overview
docs(09-microservices): add iam-service data model
docs(09-microservices): add scheduling-service events
docs(09-microservices): add audit-service runbook
docs(09-microservices): fix audit-service append-only note
docs(15-project-control): add open questions
```

**Regla clave:** un commit, un cambio lógico. No mezclar cambios de distintos archivos o secciones en un mismo commit.

---

### Flujo completo de trabajo

Este es el proceso que se sigue cada vez que se va a crear o modificar un documento:

```
1. Pararse sobre develop actualizado
   git checkout develop
   git pull origin develop

2. Crear la rama hija
   git checkout -b feat/doc-[sección]-[tema]

3. Crear o editar el documento

4. Hacer commit
   git add [archivo]
   git commit -m "docs(NN-seccion): mensaje"

5. Hacer push
   git push origin feat/doc-[sección]-[tema]

6. Abrir Pull Request en GitHub
   base:    develop
   compare: feat/doc-[sección]-[tema]

7. Pasar el checklist de definition-of-ready.md antes de pedir revisión

8. Esperar aprobación de otra persona (no auto-aprobarse)

9. Merge a develop

10. Borrar la rama hija (botón "Delete branch" en GitHub)
```

---

### Reglas generales

- Nunca hacer push directo a `develop`, `qa`, `stg` ni `main`.
- Nunca trabajar en una rama hija de otra rama hija. Siempre desde `develop`.
- Una rama hija resuelve un tema específico. No acumular cambios de múltiples archivos no relacionados en una misma rama.
- Si una rama lleva más de una semana sin PR, debe actualizarse con `develop` para evitar conflictos:
  ```bash
  git checkout develop
  git pull origin develop
  git checkout feat/doc-[sección]-[tema]
  git merge develop
  ```
- Una vez mergeada, la rama hija se elimina. No se reutilizan ramas cerradas.

---

### Checklist antes de abrir un PR

Antes de abrir cualquier PR, verificar:

```
[ ] La rama nació desde develop (no desde otra rama hija)
[ ] El nombre de la rama sigue el patrón feat/doc o fix/doc
[ ] Los commits siguen el formato docs(NN-seccion): mensaje
[ ] El documento cumple la estructura mínima de documentation-rules.md
[ ] El archivo está enlazado desde el README.md de su sección
[ ] No se subieron secretos, contraseñas ni datos personales
```

Para el checklist completo de cierre, ver [definition-of-done.md](./definition-of-done.md).

## Referencias

- [documentation-rules.md](./documentation-rules.md)
- [definition-of-ready.md](./definition-of-ready.md)
- [definition-of-done.md](./definition-of-done.md)
- [microservices-documentation.md](./microservices-documentation.md)
