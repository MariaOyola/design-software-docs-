# Estrategia de Migración

> Estado: 🟢 En progreso | Última actualización: 2026-06-2
> Autor: Por definir | Equipo: Por definir

## Contexto

Define cómo se gestionan los cambios en los esquemas de base de datos de los 9 microservicios. Cada servicio maneja sus propias migraciones de forma independiente.

## Contenido

### Principios

```
1. Cada microservicio gestiona sus propias migraciones — no existe migración global
2. Las migraciones son versionadas y se ejecutan en orden secuencial
3. Toda migración debe poder revertirse (rollback) sin pérdida de datos
4. Nunca se modifican migraciones ya ejecutadas en producción
5. Los cambios en audit_db son irreversibles por diseño (append-only)
```

---

### Tipos de cambio y su impacto

| Tipo de cambio | Impacto | Precaución |
|---|---|---|
| Agregar columna nullable | Bajo — no rompe nada | Ninguna |
| Agregar columna NOT NULL | Alto — requiere valor por defecto | Definir DEFAULT antes del NOT NULL |
| Renombrar columna | Alto — rompe consultas existentes | Usar alias temporal, migrar en fases |
| Eliminar columna | Alto — pérdida de datos | Deprecar primero, eliminar después |
| Agregar tabla nueva | Bajo — no afecta lo existente | Ninguna |
| Eliminar tabla | Muy alto — pérdida de datos | Solo si ningún servicio la referencia |
| Cambiar tipo de columna | Alto — puede perder datos | Crear columna nueva, migrar datos, eliminar vieja |

---

### Proceso para cambios en producción

```
1. Crear migración en la rama del servicio afectado
2. Probar la migración en ambiente develop
3. Validar rollback: la migración debe poder revertirse
4. PR hacia develop → qa → stg
5. Ejecutar migración en stg y validar
6. PR hacia main
7. Ejecutar migración en producción durante ventana de mantenimiento
8. Registrar el cambio en CHANGELOG.md
```

---

### Reglas especiales por servicio

**`audit_db` — audit-service**
```
❌ No se permiten migraciones que eliminen o modifiquen registros existentes
✅ Solo se permiten migraciones que agregan columnas o tablas nuevas
La restricción append-only es a nivel de aplicación y de BD
```

**`scheduling_db` — scheduling-service**
```
⚠️ Los cambios en tablas de horario o sesion_clase requieren
   revisión de arquitectura antes de ejecutarse en producción
   porque afectan directamente el core del sistema
```

---

### Carga inicial de datos maestros

Antes de la primera ejecución del sistema, `ref_db` debe tener cargados:

```
[ ] Macroregiones del SENA
[ ] Centros de formación activos
[ ] Catálogos: modalidades, jornadas, tipos de ambiente, estados
[ ] Parámetros iniciales del sistema
```

Esta carga se realiza con scripts de seed versionados, no con migraciones.

## Referencias

- [models.md](./models.md) — Modelos de datos por servicio
- [data-dictionary.md](./data-dictionary.md) — Convenciones de campos
- [09-microservices/services/](../09-microservices/services/) — Data models específicos por servicio
- [10-devops/environments.md](../10-devops/environments.md) — Ambientes donde se ejecutan migraciones