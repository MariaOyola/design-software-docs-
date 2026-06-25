# Mapa de Dominio

> Estado: 🟢 En progreso |  Última actualización: 2026-06-24
> Autor: Maria  | Equipo: Por definir

## Contexto

Este documento muestra cómo se relacionan las entidades del dominio entre sí. No describe implementación técnica ni tablas de BD. Para reglas de cada entidad ver [`entities-and-rules.md`](./entities-and-rules.md). Para modelos de datos ver [`06-data/models.md`](../06-data/models.md).

## Contenido

### Jerarquía institucional

```
Macroregión
  └── Centro de Formación
        ├── Ambiente de Formación
        │     ├── Inventario
        │     ├── Mantenimiento
        │     └── Reserva / Disponibilidad
        └── Oferta
              └── Programa de Formación
                    └── Competencia
                          └── RAP
```

---

### Jerarquía académica

```
Programa de Formación
  └── Competencia
        └── RAP
              └── Ficha (grupo de aprendices)
                    ├── Aprendiz
                    │     └── Etapa Productiva
                    │           ├── Empresa
                    │           └── Bitácora
                    └── Horario
                          └── Sesión de Clase
                                ├── Franja Horaria
                                ├── Instructor
                                ├── Ambiente
                                └── Asignación / Conflicto
```

---

### Relaciones entre microservicios

Muestra qué servicio consulta o depende de qué otro para operar:

```
iam-service
  └── valida identidad para todos los demás servicios

reference-data-service
  └── provee datos maestros a:
        ├── academic-management-service (centros, catálogos)
        ├── training-environment-service (centros, catálogos)
        └── actors-service (catálogos, estados)

academic-management-service
  └── provee fichas y programas a:
        ├── scheduling-service (para generar horarios)
        └── actors-service (para vincular aprendices)

training-environment-service
  └── provee disponibilidad de ambientes a:
        └── scheduling-service (para asignar sesiones)

actors-service
  └── provee instructores y aprendices a:
        └── scheduling-service (para asignar sesiones)

scheduling-service
  └── consume de: academic, training-environment, actors
  └── publica horarios que consume:
        ├── document-service (para generar PDFs)
        └── monitoring-service (para seguimiento de KPIs)

document-service
  └── genera documentos a partir de datos de scheduling

monitoring-service
  └── genera alertas y notificaciones a instructores y aprendices

audit-service
  └── recibe eventos de todos los servicios (append-only)
      nunca recibe llamadas directas de usuarios
```

---

### Entidades compartidas por contexto

Algunas entidades son propiedad de un servicio pero son consultadas por otros:

| Entidad | Dueño | Consultada por |
|---|---|---|
| `usuario` | iam-service | todos los servicios (validación de token) |
| `ficha` | academic-management-service | scheduling-service, actors-service |
| `ambiente` | training-environment-service | scheduling-service |
| `instructor` | actors-service | scheduling-service |
| `aprendiz` | actors-service | academic-management-service |
| `horario` | scheduling-service | document-service, monitoring-service |
| `catalogo` | reference-data-service | academic, training-environment, actors |

> Regla de oro: un servicio puede **consultar** datos de otro por API,
> pero nunca puede **escribir** directamente en la BD de otro servicio.

## Referencias

- [entities-and-rules.md](./entities-and-rules.md) — Reglas de negocio de cada entidad
- [domain-events.md](./domain-events.md) — Eventos que conectan estos dominios
- [09-microservices/service-catalog.md](../09-microservices/service-catalog.md) — Catálogo oficial de servicios
- [05-architecture/overview.md](../05-architecture/overview.md) — Arquitectura técnica del sistema