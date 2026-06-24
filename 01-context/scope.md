# Alcance

> Estado: 🟡 En progreso | Última actualización: 2026-06-21
> Autor: Por definir | Equipo: Por definir

## Contexto

Este documento define los límites exactos del sistema de gestión de horarios del SENA. Establece qué funcionalidades están dentro del alcance, qué está explícitamente excluido, qué supuestos se asumen como válidos y bajo qué restricciones opera el sistema. Cualquier solicitud que no esté contemplada en la sección "En alcance" requiere aprobación formal de arquitectura antes de ser desarrollada.

## Contenido

### En alcance

Las siguientes funcionalidades forman parte del sistema y deben ser implementadas:

**Gestión de identidad y acceso**
- Autenticación de usuarios con JWT
- Autorización basada en roles: Coordinador, Instructor, Aprendiz, Administrador
- Gestión de sesiones y tokens
- Administración de permisos por rol

**Gestión de datos maestros**
- Registro y consulta de macroregiones y centros de formación
- Administración de catálogos institucionales (estados, parámetros, tipos)
- Parametrización general del sistema

**Gestión académica**
- Registro de programas de formación y sus competencias
- Gestión de Resultados de Aprendizaje del Proyecto (RAPs)
- Creación y administración de fichas activas
- Gestión de ofertas de formación

**Gestión de ambientes de formación**
- Registro de ambientes con su tipo, capacidad y ubicación
- Control de inventario por ambiente
- Registro y gestión de mantenimientos
- Gestión de reservas y disponibilidad de ambientes

**Generación y gestión de horarios**
- Generación automática de horarios para fichas
- Asignación de sesiones de clase a ambientes e instructores
- Detección automática de conflictos de ambiente e instructor
- Resolución manual de conflictos por parte del coordinador
- Publicación de horarios validados

**Gestión de actores**
- Registro y administración de instructores y su disponibilidad
- Registro de aprendices y su vinculación a fichas
- Gestión de empresas vinculadas a etapa productiva
- Registro de bitácoras de seguimiento

**Generación de documentos**
- Generación de horarios exportados en PDF
- Administración de plantillas de documentos
- Control de versiones de documentos generados

**Monitoreo y seguimiento**
- Seguimiento de KPIs del proceso de formación
- Generación de alertas por incumplimiento o anomalía
- Notificaciones a instructores y aprendices
- Registro de sesiones de seguimiento y planes de mejoramiento

**Auditoría**
- Registro inmutable (append-only) de toda acción relevante del sistema
- Trazabilidad completa de cambios en horarios, ambientes e instructores

---

### Fuera de alcance

Las siguientes funcionalidades están explícitamente excluidas del sistema. Su inclusión requiere una nueva decisión formal de arquitectura:

```
❌ Nómina o pagos a instructores
❌ Calificación de aprendices y registro de notas
❌ Control de asistencia en tiempo real
❌ Gestión financiera o presupuestal del SENA
❌ Integración directa con Sofia Plus (sistema legado del SENA)
❌ Procesos disciplinarios de aprendices
```

---

### Supuestos

El sistema se diseña asumiendo que las siguientes condiciones son verdaderas. Si alguna cambia, debe abrirse una pregunta en `15-project-control/open-questions.md`:

1. Cada ficha tiene al menos un instructor asignado antes de generar su horario.
2. Los ambientes de formación ya están registrados en el sistema con su tipo y capacidad antes de iniciar la generación de horarios.
3. Los usuarios del sistema (coordinadores, instructores, aprendices) tienen acceso a internet y a un navegador web moderno.
4. El SENA provee los datos maestros iniciales (centros de formación, programas, fichas activas) para la carga inicial del sistema.
5. Un aprendiz en etapa productiva no requiere sesiones presenciales programadas en el sistema.
6. Los horarios se generan por ficha, no por aprendiz individual.
7. Cada microservicio es desplegado y mantenido de forma independiente.

---

### Restricciones

Limitaciones técnicas, institucionales o de negocio que el sistema debe respetar obligatoriamente:

**Rendimiento**
- El registro o autenticación de un usuario no debe tardar más de 3 segundos.
- La generación de un horario para una ficha no debe tardar más de 30 segundos.
- La detección de conflictos debe completarse antes de permitir la publicación del horario.

**Seguridad**
- Ningún endpoint puede ser accedido sin autenticación válida, excepto los de registro y login.
- Los datos personales de aprendices e instructores deben tratarse conforme a la Ley 1581 de 2012 (habeas data).
- Los registros de auditoría no pueden ser modificados ni eliminados bajo ninguna circunstancia.

**Arquitectura**
- Cada microservicio debe tener su propia base de datos. Ningún servicio puede acceder directamente a la BD de otro.
- Toda comunicación entre servicios debe hacerse por API REST o eventos, nunca por acceso directo a BD.
- La documentación de un microservicio debe existir antes de su primer merge a main.

**Institucionales**
- El sistema debe respetar las reglas del Reglamento del Aprendiz SENA — Acuerdo 009 de 2024.
- Los roles y permisos deben reflejar la estructura jerárquica real del SENA.

## Referencias

- [overview.md](./overview.md) — Contexto institucional y objetivos del sistema
- [glossary.md](./glossary.md) — Definición de términos usados en este documento
- [04-requirements/non-functional.md](../04-requirements/non-functional.md) — Requisitos no funcionales derivados de las restricciones
- [15-project-control/open-questions.md](../15-project-control/open-questions.md) — Preguntas abiertas sobre supuestos no confirmados
- Reglamento del Aprendiz SENA — Acuerdo 009 de 2024
- Ley 1581 de 2012 — Protección de datos personales