# Glosario

> Estado: 🟢 En progreso | Última actualización: 2026-06-24
> Autor: Maria | Equipo: Por definir

## Contexto

Este glosario define los términos oficiales del dominio SENA y del sistema de gestión de horarios. Es la fuente de verdad para nombrar entidades en el código, la base de datos y la documentación. Cuando exista duda sobre cómo llamar algo, este archivo tiene la última palabra.

Todo término nuevo debe agregarse aquí antes de usarse en cualquier otro documento o en código.

## Contenido

### Términos del dominio SENA

Definiciones basadas en el Reglamento del Aprendiz SENA — Acuerdo 009 de 2024 y la Ley 119 de 1994.

| Término | Definición | Servicio relacionado |
|---|---|---|
| **Aprendiz** | Persona matriculada en los programas de formación profesional del SENA en sus diferentes modalidades | `actors-service` |
| **Instructor** | Persona encargada de guiar el proceso formativo de una o más fichas. Puede tener vínculo de planta, contrato o por hora cátedra | `actors-service` |
| **Ficha** | Grupo de aprendices matriculados en un mismo programa de formación, jornada y fecha de inicio, identificado con un número único en el sistema académico del SENA | `academic-management-service` |
| **Programa de Formación** | Estructura curricular que define los conocimientos, habilidades y competencias que debe desarrollar un aprendiz. Puede ser técnico, tecnólogo u otro nivel | `academic-management-service` |
| **Competencia** | Unidad de aprendizaje dentro de un programa de formación que agrupa un conjunto de Resultados de Aprendizaje relacionados | `academic-management-service` |
| **RAP** | Resultado de Aprendizaje del Proyecto. Unidad mínima de evaluación dentro de una competencia. Define qué debe saber hacer el aprendiz al finalizar una etapa | `academic-management-service` |
| **Oferta** | Apertura de un programa de formación en un centro específico, con fechas y cupos definidos | `academic-management-service` |
| **Ambiente de Formación** | Espacio físico o virtual donde se desarrollan las sesiones de clase. Puede ser laboratorio, taller, aula, campo deportivo o aula virtual | `training-environment-service` |
| **Centro de Formación** | Sede física del SENA donde operan los ambientes de formación y se ejecutan los programas | `reference-data-service` |
| **Macroregión** | Agrupación geográfica de centros de formación del SENA a nivel nacional | `reference-data-service` |
| **Etapa Productiva** | Fase del programa de formación donde el aprendiz aplica sus conocimientos en una empresa real. Durante esta etapa no tiene sesiones presenciales programadas | `actors-service` |
| **Comunidad Educativa SENA** | Conjunto de actores del proceso formativo: aprendices, instructores, personal administrativo, directivos, familias, empresarios e instituciones aliadas (Acuerdo 009 de 2024) | Transversal |

---

### Términos del sistema de horarios

Términos específicos del sistema construido, que pueden no existir en el vocabulario institucional del SENA pero son necesarios para el diseño técnico.

| Término | Definición | Servicio relacionado |
|---|---|---|
| **Horario** | Programación completa de sesiones de clase para una ficha en un período determinado. Un horario tiene un estado: borrador, en revisión o publicado | `scheduling-service` |
| **Sesión de Clase** | Encuentro programado entre un instructor y una ficha en un ambiente de formación específico, en una franja horaria definida | `scheduling-service` |
| **Franja Horaria** | Bloque de tiempo disponible para asignación de sesiones. Tiene hora de inicio, hora de fin y día de la semana | `scheduling-service` |
| **Asignación** | Acto de vincular una sesión de clase con un instructor, un ambiente y una franja horaria específicos | `scheduling-service` |
| **Conflicto** | Situación en la que dos sesiones de clase compiten por el mismo recurso (ambiente o instructor) en la misma franja horaria. Debe resolverse antes de publicar el horario | `scheduling-service` |
| **Reserva** | Bloqueo temporal de un ambiente de formación para un uso específico, que lo hace no disponible para otras asignaciones | `training-environment-service` |
| **Disponibilidad** | Estado de un ambiente de formación o instructor que indica si puede ser asignado en una franja horaria determinada | `training-environment-service` |
| **Inventario** | Registro de los recursos físicos (equipos, herramientas, mobiliario) disponibles en un ambiente de formación | `training-environment-service` |
| **Mantenimiento** | Período durante el cual un ambiente de formación no está disponible por razones de reparación o adecuación | `training-environment-service` |
| **Bitácora** | Registro cronológico de eventos o acciones relevantes asociados a un actor (instructor o aprendiz) dentro del sistema | `actors-service` |
| **Plan de Mejoramiento** | Documento que registra las acciones acordadas para corregir desviaciones detectadas en el seguimiento de KPIs | `monitoring-service` |
| **Auditoría** | Registro inmutable de toda acción relevante ejecutada en el sistema. No permite actualizaciones ni eliminaciones (append-only) | `audit-service` |

---

### Términos de roles y acceso

| Término | Definición | Servicio relacionado |
|---|---|---|
| **Usuario** | Persona registrada en el sistema con credenciales de acceso. Puede tener uno o más roles | `iam-service` |
| **Rol** | Conjunto de permisos que determina qué puede hacer un usuario en el sistema. Roles definidos: Administrador, Coordinador, Instructor, Aprendiz | `iam-service` |
| **Permiso** | Acción específica que un rol puede ejecutar sobre un recurso del sistema | `iam-service` |
| **Sesión** | Período activo de uso del sistema por parte de un usuario autenticado | `iam-service` |
| **Token** | Credencial digital generada al autenticarse, usada para validar la identidad del usuario en cada petición al sistema (JWT) | `iam-service` |

---

### Acrónimos

| Acrónimo | Significado |
|---|---|
| SENA | Servicio Nacional de Aprendizaje |
| RAP | Resultado de Aprendizaje del Proyecto |
| JWT | JSON Web Token |
| KPI | Key Performance Indicator (Indicador Clave de Desempeño) |
| ADR | Architecture Decision Record |
| BD | Base de Datos |
| API | Application Programming Interface |
| PDF | Portable Document Format |

## Referencias

- Reglamento del Aprendiz SENA — Acuerdo 009 de 2024
- Ley 119 de 1994 — Misión y funciones del SENA
- [overview.md](./overview.md) — Contexto institucional del sistema
- [02-domain/entities-and-rules.md](../02-domain/entities-and-rules.md) — Reglas de negocio asociadas a estas entidades
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo oficial de servicios y entidades