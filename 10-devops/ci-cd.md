# CI/CD

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Maria | Equipo: Por definir

## Contexto

Define los pipelines de integración y despliegue continuo, y los controles de calidad automatizados que se ejecutan antes de promover código entre ambientes.

## Contenido

### Pipeline por microservicio

Cada uno de los 9 microservicios tiene su propio pipeline independiente:

```
push a rama feat/fix
        ↓
[1] Build           → compilar el servicio
[2] Lint             → validar estilo de código
[3] Unit tests       → pruebas unitarias
        ↓
PR hacia develop
        ↓
[4] Integration tests → pruebas de integración con servicios dependientes
[5] Code review       → aprobación de al menos 1 revisor
        ↓
merge a develop
        ↓
PR develop → qa
        ↓
[6] Deploy a qa      → despliegue automático
[7] Smoke tests      → pruebas básicas post-despliegue
        ↓
PR qa → stg
        ↓
[8] Deploy a stg     → despliegue automático
[9] E2E tests        → pruebas end-to-end completas
        ↓
PR stg → main
        ↓
[10] Deploy a main   → despliegue a producción
[11] Healthcheck     → verificación post-despliegue
```

---

### Controles de calidad automatizados

| Control | Cuándo se ejecuta | Bloquea el merge si falla |
|---|---|---|
| Lint | En cada push | ✅ Sí |
| Unit tests | En cada push | ✅ Sí |
| Cobertura mínima de pruebas | En cada PR | ✅ Sí (mínimo 70%) |
| Integration tests | Antes de merge a develop | ✅ Sí |
| Escaneo de secretos | En cada push | ✅ Sí |
| E2E tests | Antes de merge a main | ✅ Sí |

---

### Despliegue de documentación

El repositorio de documentación (`design-software-docs`) tiene su propio flujo, sin build ni tests automatizados de código:

```
feat/doc-* → develop → qa → stg → main
```

Controles que sí aplican a documentación:
```
[ ] Lint de Markdown (formato, enlaces rotos)
[ ] Verificación de que todo archivo tiene encabezado válido
[ ] Verificación de que no hay secretos en el contenido
```

---

### Rollback automático

Si el healthcheck post-despliegue falla en `main`, el pipeline revierte automáticamente a la versión anterior estable y notifica al equipo.

## Referencias

- [local-setup.md](./local-setup.md) — Configuración local
- [environments.md](./environments.md) — Ambientes del sistema
- [00-governance/git-conventions.md](../00-governance/git-conventions.md) — Flujo de ramas
- [11-quality/testing-strategy.md](../11-quality/testing-strategy.md) — Detalle de cada tipo de prueba