# Ambientes

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria
> Autor: Por definir | Equipo: Por definir

## Contexto

Define los ambientes donde se ejecuta el sistema, su propósito y las reglas de uso de cada uno.

## Contenido

### Ambientes del sistema

| Ambiente | Propósito | Rama | Quién accede |
|---|---|---|---|
| `develop` | Integración continua de desarrollo activo | `develop` | Equipo de desarrollo |
| `qa` | Validación de calidad antes de staging | `qa` | Equipo de desarrollo y QA |
| `stg` | Staging — pre-producción, pruebas finales | `stg` | Equipo de desarrollo, QA e instructor |
| `main` | Producción | `main` | Usuarios finales del SENA |

---

### Reglas de uso por ambiente

**`develop`**
```
- Puede tener errores o funcionalidades incompletas
- Se actualiza con cada PR aprobado de una rama hija
- No requiere datos reales — usar datos ficticios de prueba
```

**`qa`**
```
- Debe estar libre de errores conocidos antes de promoverse
- Se usa para validar que una sección o funcionalidad está completa
- Datos de prueba, nunca datos reales de aprendices o instructores
```

**`stg`**
```
- Debe ser una réplica fiel de producción en configuración
- Última validación antes de pasar a main
- Se ejecutan las pruebas E2E completas aquí
```

**`main`**
```
- Solo código y documentación aprobados llegan aquí
- Cualquier cambio requiere PR desde stg
- Cualquier incidente aquí sigue el proceso de 13-operations/incident-management.md
```

---

### Diferencias de configuración entre ambientes

| Aspecto | develop | qa | stg | main |
|---|---|---|---|---|
| Datos | Ficticios | Ficticios | Réplica anonimizada | Reales |
| Logging | Verbose (debug) | Verbose | Info | Info / Warning |
| Recursos de infraestructura | Mínimos | Mínimos | Similares a producción | Producción |
| Acceso | Equipo dev | Equipo dev + QA | Equipo dev + QA + instructor | Usuarios SENA |

> ⚠️ Ningún ambiente que no sea `main` debe usar datos personales reales
> de aprendices o instructores. Ver `00-governance/security-rules.md`.

## Referencias

- [local-setup.md](./local-setup.md) — Configuración del ambiente local
- [ci-cd.md](./ci-cd.md) — Pipeline de promoción entre ambientes
- [00-governance/git-conventions.md](../00-governance/git-conventions.md) — Flujo de ramas asociado
- [13-operations/incident-management.md](../13-operations/incident-management.md) — Manejo de incidentes en producción