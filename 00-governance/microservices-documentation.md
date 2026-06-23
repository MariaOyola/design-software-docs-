# Guía de documentación de microservicios

> Estado: 🟢 En progreso | Última actualización: 2026-06-21
> Autor: Maria | Equipo: Por definir

Este documento define cuándo y cómo registrar documentación de microservicios. Para reglas generales de documentación, ver [documentation-rules.md](./documentation-rules.md). Para convenciones de Git, ver [git-conventions.md](./git-conventions.md).

## Contexto

En una arquitectura de microservicios cada servicio es independiente y puede ser desarrollado por personas distintas. Sin un flujo claro, cada quien documenta diferente: uno usa nombres distintos para las entidades, otro se olvida de registrar los eventos, otro no sabe dónde va el runbook. Este documento establece el único flujo válido para documentar cualquier servicio del sistema, asegurando que los 9 servicios queden documentados de forma coherente y comparable.

## Contenido

### Regla crítica

```
❌ No crear carpetas en 09-microservices/services/ hasta que
   el servicio exista en el repositorio de código o su creación
   esté formalmente aprobada por arquitectura.

❌ No crear microservicios ficticios para llenar la estructura.
```

**Requisito de aprobación:** todo servicio nuevo debe tener una de estas dos condiciones cumplidas antes de crear su carpeta:

```
✅ Una ADR en 05-architecture/decisions/records/
✅ Una decisión en 15-project-control/open-questions.md
   con estado RESUELTA
```

Sin alguno de esos artefactos el PR será rechazado, sin excepción.

---

### Servicios del sistema

Estos son los 9 microservicios oficiales del proyecto. Ningún documento puede agregar, renombrar ni eliminar un servicio de esta lista sin aprobación de arquitectura:

| # | Servicio | Base de datos | Entidades |
|---|---|---|---|
| 01 | `iam-service` | `iam_db` | usuario, rol, permiso, sesion, token |
| 02 | `reference-data-service` | `ref_db` | macroregion, centro_formacion, catalogo, estado, parametro |
| 03 | `academic-management-service` | `academic_db` | programa, competencia, RAP, ficha, oferta |
| 04 | `training-environment-service` | `env_db` | ambiente, inventario, mantenimiento, reserva, disponibilidad |
| 05 | `scheduling-service` | `scheduling_db` | horario, sesion_clase, franja, asignacion, conflicto |
| 06 | `actors-service` | `actors_db` | instructor, aprendiz, empresa, etapa_productiva, bitacora |
| 07 | `document-service` | `document_db` | documento, version, plantilla |
| 08 | `monitoring-service` | `monitoring_db` | seguimiento_kpi, alerta, notificacion, sesion_seguimiento, plan_mejoramiento |
| 09 | `audit-service` | `audit_db` | auditoria (append-only, sin updates) |

> La fuente de verdad de esta tabla es `09-microservices/service-catalog.md`.
> Si hay discrepancia entre este archivo y el catálogo, el catálogo tiene prioridad.

---

### Ubicación

Cada servicio real se documenta en:

```
09-microservices/services/<nombre-del-servicio>/
```

> ⚠️ El nombre de la carpeta debe coincidir exactamente con el nombre
> del repositorio de código del servicio. Confirmar con arquitectura
> antes de crear la carpeta.

---

### Flujo completo

#### Paso 1 — Verificar el catálogo

Abrir `09-microservices/service-catalog.md` y confirmar que el servicio no exista ya registrado. Si ya existe, no se crea una carpeta nueva.

#### Paso 2 — Copiar la plantilla

```bash
cp -r 09-microservices/_template/ 09-microservices/services/<nombre-servicio>/
```

La plantilla disponible en `09-microservices/_template/` ya tiene los 5 archivos con la estructura mínima. No se crea la carpeta desde cero.

#### Paso 3 — Completar el README del servicio

Es el primer archivo que se llena. Sin él no se puede entender ninguno de los demás. Debe incluir:

```markdown
- Responsabilidad del servicio
- Bounded context al que pertenece
- Owner (equipo o persona responsable)
- Repositorio de código (enlace)
- Dependencias: qué servicios consume
- Dependientes: qué servicios lo consumen a él
- Estado de documentación: 🔴 / 🟡 / 🟢
- Enlaces a: api-contract.md, data-model.md, events.md, runbook.md
```

#### Paso 4 — Registrar en el catálogo

Agregar una fila en `09-microservices/service-catalog.md`:

```markdown
| <nombre-servicio> | <descripción> | <owner> | [repo](<url>) | 🟡 |
```

Este paso es obligatorio antes de abrir el PR. Sin el registro en el catálogo el PR será rechazado.

#### Paso 5 — Completar los 5 archivos mínimos

Los archivos se completan en este orden:

| Archivo | Qué documentar |
|---|---|
| `README.md` | Responsabilidad, bounded context, owner, dependencias y enlaces |
| `api-contract.md` | Endpoints, request, response y errores |
| `data-model.md` | Modelo transaccional propio del servicio |
| `events.md` | Eventos publicados y consumidos |
| `runbook.md` | Deploy, rollback, variables de entorno y troubleshooting |

**Regla de prioridad para el primer merge a main del código:**

```
README.md y api-contract.md deben estar en 🟡 como mínimo
antes del primer merge a main del código del servicio.
```

---

### Detalle de cada archivo

**`data-model.md`**

Documenta las entidades de la BD del servicio. Debe coincidir exactamente con la tabla oficial. Si una entidad tiene restricciones especiales, deben quedar explícitas.

```markdown
Contenido mínimo por entidad:
- Nombre de la entidad y tabla en BD
- Campos con tipo, nulo/no nulo y significado de negocio
- Restricciones especiales de comportamiento
- Relaciones con otras entidades del mismo servicio
```

> ⚠️ `audit-service` es el único servicio con restricción append-only.
> La entidad `auditoria` no permite UPDATE ni DELETE bajo ninguna
> circunstancia. Esto debe quedar explícito en su `data-model.md`.

**`events.md`**

Define los eventos que el servicio emite y los que consume de otros servicios.

```markdown
Contenido mínimo:
- Eventos que emite: nombre, cuándo se emite, qué datos lleva
- Eventos que consume: nombre, de qué servicio viene, qué hace con él
```

Ejemplo para `scheduling-service`:

```
Emite:
  HorarioPublicado    → cuando un horario pasa a estado publicado
  ConflictoDetectado  → cuando el validador encuentra un conflicto

Consume:
  AmbienteReservado   → viene de training-environment-service
  FichaCambioEstado   → viene de academic-management-service
  InstructorAsignado  → viene de actors-service
```

**`api-contract.md`**

Documenta los endpoints que expone el servicio siguiendo el formato de `07-api/guidelines.md`.

```markdown
Contenido mínimo por endpoint:
- Método HTTP y ruta
- Descripción de qué hace
- Parámetros de entrada
- Respuesta exitosa
- Respuestas de error posibles
- Roles que pueden acceder
```

> Si existe un archivo OpenAPI formal, se almacena en
> `07-api/contracts/openapi/` y se mantiene un enlace cruzado
> desde `api-contract.md` hacia ese archivo.

**`runbook.md`**

Procedimientos operativos para cuando el servicio falla en producción.

```markdown
Contenido mínimo:
- Cómo verificar que el servicio está sano
- Procedimiento de deploy y rollback
- Variables de entorno requeridas (sin valores reales, ver security-rules.md)
- Síntomas comunes y pasos de troubleshooting
- Cuándo escalar y a quién
```

---

### Ramas y commits para microservicios

A diferencia de otros documentos del repo, la documentación de un microservicio se agrupa en **una sola rama por servicio**, no una rama por archivo:

```bash
git checkout -b feat/doc-service-<nombre-servicio>
```

Ejemplos:

```
feat/doc-service-iam-service
feat/doc-service-scheduling-service
feat/doc-service-audit-service
feat/doc-service-actors-service
```

El commit agrupa el servicio completo:

```bash
git add 09-microservices/services/<nombre-servicio>/
git add 09-microservices/service-catalog.md
git commit -m "docs(09-microservices): register <service-name> service"
git push origin feat/doc-service-<nombre-servicio>
```

Si se documentan varios servicios, usar un commit por microservicio cuando sea posible.

---

### Indicador de gobernabilidad por servicio

El `README.md` de cada servicio y el `09-microservices/README.md` deben mostrar el indicador actualizado:

| Indicador | Significa |
|---|---|
| 🟢 Bueno | Los 5 archivos completos, revisados y en estado 🟢 |
| 🟡 Regular | Algunos archivos existen pero están incompletos o en 🟡 |
| 🔴 Malo | No existe la carpeta o la mayoría de archivos faltan |

---

### Checklist antes de cerrar la documentación de un servicio

Un servicio se considera completamente documentado cuando:

```
[ ] Existe ADR o decisión RESUELTA en 15-project-control/open-questions.md
    que aprueba la creación del servicio

[ ] La carpeta usa el mismo nombre que el repositorio de código

[ ] Los 5 archivos existen y están en estado 🟢

[ ] Las entidades de data-model.md coinciden con la tabla oficial

[ ] Los eventos de events.md están cruzados con los demás servicios
    que los emiten o consumen

[ ] Está registrado en service-catalog.md con estado 🟢

[ ] El indicador en 09-microservices/README.md está en 🟢

[ ] Pasó definition-of-ready.md y definition-of-done.md
```

## Referencias

- [documentation-rules.md](./documentation-rules.md)
- [git-conventions.md](./git-conventions.md)
- [definition-of-ready.md](./definition-of-ready.md)
- [definition-of-done.md](./definition-of-done.md)
- [security-rules.md](./security-rules.md)