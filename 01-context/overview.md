# Overview

> Estado: 🟡 En progreso | Última actualización: 2026-06-23
> Autor: Maria | Equipo: Por definir

## Contexto institucional

El Servicio Nacional de Aprendizaje (SENA) es una entidad pública colombiana adscrita al Ministerio del Trabajo, cuya misión es invertir en el desarrollo social y técnico de los trabajadores colombianos, ofreciendo formación profesional integral para la incorporación y el desarrollo de las personas en actividades productivas (Ley 119 de 1994, Art. 2).

La formación en el SENA se organiza alrededor de **Centros de Formación**, donde los **Aprendices** —personas matriculadas en programas de formación profesional— desarrollan su proceso formativo guiados por **Instructores** en **Ambientes de Formación** (talleres, laboratorios, aulas o espacios virtuales).

Cada grupo de aprendices que comparte un mismo programa, jornada y fecha de inicio se denomina **Ficha**. Las fichas son la unidad operativa central de la formación: todo el sistema de horarios, ambientes e instructores se organiza en torno a ellas.

El marco normativo vigente que regula la formación y los derechos de los aprendices es el **Reglamento del Aprendiz SENA — Acuerdo 009 de 2024**, que deroga los Acuerdos 07 de 2012, 02 de 2014, 06 de 2023 y 02 de 2024.

## Problema

Actualmente el SENA gestiona la asignación de horarios de forma **manual**. Esto genera tres problemas recurrentes:

**1. Conflictos de ambientes**
Dos o más fichas quedan asignadas al mismo Ambiente de Formación en el mismo bloque horario, lo que imposibilita el desarrollo normal de las clases.

**2. Conflictos de instructores**
Un instructor queda programado para atender dos fichas simultáneamente, lo que obliga a cancelaciones de último momento.

**3. Falta de visibilidad anticipada**
Los instructores y aprendices no conocen con suficiente anticipación dónde y cuándo son sus sesiones, lo que afecta la organización personal y la asistencia.

El proceso actual de construcción de un horario para una ficha puede tomar **días**, involucra múltiples hojas de cálculo y depende del conocimiento tácito de los coordinadores académicos. No existe un mecanismo automático de detección de conflictos.

## Objetivos

**Objetivo general**

Desarrollar un sistema de microservicios que automatice la generación y gestión de horarios del SENA, eliminando conflictos de ambientes e instructores y garantizando visibilidad anticipada para todos los actores del proceso formativo.

**Objetivos específicos**

1. Automatizar la asignación de sesiones de clase a fichas, instructores y ambientes de formación, respetando las reglas de negocio del dominio SENA.
2. Detectar y reportar conflictos de horario en tiempo real antes de publicar cualquier programación.
3. Gestionar la disponibilidad de ambientes de formación, incluyendo mantenimientos y reservas especiales.
4. Proveer visibilidad del horario publicado a instructores, aprendices y coordinadores desde sus respectivos roles.
5. Registrar de forma inmutable toda acción relevante del sistema para efectos de auditoría institucional.
6. Generar documentos oficiales de horario en formatos exportables (PDF).

## Arquitectura general del sistema

El sistema está compuesto por **9 microservicios independientes**, cada uno con su propia base de datos, que se comunican entre sí por API REST y eventos:

| Servicio | Responsabilidad principal |
|---|---|
| `iam-service` | Autenticación, autorización, roles y sesiones |
| `reference-data-service` | Datos maestros: macroregiones, centros de formación, catálogos |
| `academic-management-service` | Programas de formación, competencias, RAPs y fichas |
| `training-environment-service` | Ambientes de formación, inventario, reservas y disponibilidad |
| `scheduling-service` | Motor de generación de horarios y detección de conflictos |
| `actors-service` | Instructores, aprendices, empresas y etapa productiva |
| `document-service` | Generación de documentos, versiones y plantillas |
| `monitoring-service` | Seguimiento de KPIs, alertas y planes de mejoramiento |
| `audit-service` | Registro inmutable de auditoría (append-only) |

## Referencias

- Ley 119 de 1994 — Misión y funciones del SENA
- Reglamento del Aprendiz SENA — Acuerdo 009 de 2024
- [scope.md](./scope.md) — Alcance, exclusiones y restricciones del sistema
- [glossary.md](./glossary.md) — Glosario de términos del dominio SENA
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo oficial de los 9 servicios