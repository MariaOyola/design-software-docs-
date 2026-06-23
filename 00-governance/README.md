# 00 · Gobernanza de la documentación

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

Esta carpeta define cómo se trabaja en este repositorio de documentación. Debe leerse antes de crear, editar o revisar cualquier documento del proyecto.

## Contexto

Sin reglas claras, equipos de varias personas generan inconsistencias inevitables: archivos con nombres distintos para lo mismo, commits sin formato, documentos a medias sin estado, secretos subidos por accidente. Esta carpeta establece el lenguaje común que todo el equipo debe seguir para que la documentación sea confiable y mantenible.

## Contenido

### Archivos de esta carpeta

| Archivo | Qué define | Cuándo consultarlo | Estado |
|---|---|---|---|
| `documentation-rules.md` | Estructura mínima de todo documento, naming, estados, índices y diagramas | Antes de crear cualquier documento | 🟡 |
| `git-conventions.md` | Nomenclatura de ramas, formato de commits y flujo `develop → qa → stg → main` | Antes de crear una rama o hacer un commit | 🟡 |
| `definition-of-ready.md` | Checklist que el autor pasa antes de abrir un PR | Antes de abrir un Pull Request | 🟡 |
| `definition-of-done.md` | Checklist que el revisor pasa antes de aprobar un merge | Antes de aprobar y mergear un PR | 🟡 |
| `security-rules.md` | Qué nunca puede aparecer en la documentación y cómo actuar si ya se subió | Antes de hacer push de cualquier archivo | 🟡 |
| `microservices-documentation.md` | Flujo completo para documentar cada uno de los 9 microservicios | Cuando se va a documentar un servicio nuevo | 🟡 |

### Flujo rápido de referencia

```
¿Vas a crear un documento nuevo?
  → Leer documentation-rules.md primero

¿Vas a crear una rama o hacer un commit?
  → Leer git-conventions.md

¿Vas a abrir un PR?
  → Pasar el checklist de definition-of-ready.md

¿Vas a aprobar y mergear un PR?
  → Pasar el checklist de definition-of-done.md

¿Vas a subir algo al repo?
  → Verificar security-rules.md antes del push

¿Vas a documentar un microservicio?
  → Seguir el flujo de microservices-documentation.md
```

### Estado de la documentación del proyecto

| Sección | Descripción | Estado |
|---|---|---|
| `00-governance` | Reglas del repositorio | 🟡 |
| `01-context` | Contexto y alcance del proyecto | 🔴 |
| `02-domain` | Dominio SENA: entidades, reglas y eventos | 🔴 |
| `03-product` | Visión, roadmap y backlog de producto | 🔴 |
| `04-requirements` | Requisitos funcionales y no funcionales | 🔴 |
| `05-architecture` | Arquitectura del sistema y decisiones (ADRs) | 🔴 |
| `06-data` | Modelos de datos y diccionario | 🔴 |
| `07-api` | Estándares y contratos de API | 🔴 |
| `08-uml` | Diagramas UML del sistema | 🔴 |
| `09-microservices` | Catálogo y documentación de los 9 servicios | 🔴 |
| `10-devops` | CI/CD, ambientes y configuración local | 🔴 |
| `11-quality` | Estrategia de pruebas y revisión de código | 🔴 |
| `12-ux-ui` | Diseño, navegación y wireframes | 🔴 |
| `13-operations` | Operación, incidentes y observabilidad | 🔴 |
| `14-training` | Manuales de usuario y onboarding técnico | 🔴 |
| `15-project-control` | Riesgos, dependencias y preguntas abiertas | 🔴 |

> Esta tabla se actualiza cada vez que una sección cambia de estado.
> Cuando `00-governance` pase a 🟢, se abre el primer PR de `develop → qa`.

## Referencias

- [documentation-rules.md](./documentation-rules.md)
- [git-conventions.md](./git-conventions.md)
- [definition-of-ready.md](./definition-of-ready.md)
- [definition-of-done.md](./definition-of-done.md)
- [security-rules.md](./security-rules.md)
- [microservices-documentation.md](./microservices-documentation.md)