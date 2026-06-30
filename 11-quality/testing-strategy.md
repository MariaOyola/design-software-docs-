# Estrategia de Pruebas

> Estado: 🟡 En progreso | Última actualización: 2026-06-29
> Autor: Por definir | Equipo: Por definir

## Contexto

Define la estrategia de pruebas por nivel y tipo para los 9 microservicios del sistema. El objetivo es garantizar que cada servicio funcione correctamente de forma aislada y en conjunto con los demás.

## Contenido

### Niveles de prueba

```
Unitarias        → valida una función o clase de forma aislada
Integración      → valida la comunicación entre un servicio y su BD,
                    o entre dos servicios por API
End-to-end (e2e)  → valida un flujo completo de negocio de principio a fin
```

---

### Pirámide de pruebas

```
        /\
       /e2e\          ← pocas, lentas, validan flujos críticos
      /------\
     /  integ. \      ← moderadas, validan contratos entre servicios
    /------------\
   /   unitarias   \  ← muchas, rápidas, validan lógica interna
  /------------------\
```

---

### Pruebas unitarias

| Aspecto | Definición |
|---|---|
| Qué se prueba | Lógica de negocio interna de cada servicio (reglas, validaciones, cálculos) |
| Cobertura mínima | 70% del código |
| Cuándo se ejecutan | En cada push, antes de cualquier PR |
| Responsable | El desarrollador que escribe el código |

**Ejemplo en `scheduling-service`:**
```
- Validar que una sesión no puede asignarse fuera de la disponibilidad del instructor
- Validar que el conflict-validator detecta correctamente doble asignación de ambiente
```

---

### Pruebas de integración

| Aspecto | Definición |
|---|---|
| Qué se prueba | Comunicación real entre un servicio y su BD, o entre dos servicios por API |
| Cuándo se ejecutan | Antes de merge a `develop` |
| Responsable | El equipo del servicio afectado |

**Ejemplo en `scheduling-service`:**
```
- Verificar que scheduling-service consulta correctamente la disponibilidad
  de ambientes en training-environment-service
- Verificar que el horario generado se persiste correctamente en scheduling_db
```

**Consumer-driven contract testing** entre servicios:
```
El servicio consumidor define el contrato esperado del servicio proveedor.
Si el proveedor cambia su API rompiendo el contrato, la prueba falla
antes de llegar a producción.
```

---

### Pruebas end-to-end (e2e)

| Aspecto | Definición |
|---|---|
| Qué se prueba | Flujo completo de negocio cruzando varios microservicios |
| Cuándo se ejecutan | Antes de merge a `main` |
| Responsable | Equipo de QA |

**Flujos críticos a probar:**
```
1. Crear ficha → generar horario → resolver conflictos → publicar horario
2. Autenticarse → consultar horario propio (instructor/aprendiz)
3. Registrar mantenimiento de ambiente → verificar que queda excluido de programación
4. Publicar horario → verificar generación de PDF → verificar notificación enviada
```

---

### Pruebas específicas por tipo de servicio

**Servicios con worker asíncrono** (`scheduling-service`, `document-service`, `monitoring-service`, `audit-service`)
```
- Probar que el worker procesa correctamente los eventos recibidos
- Probar el comportamiento ante eventos duplicados (idempotencia)
- Probar el comportamiento si el worker falla a mitad de proceso
```

**`audit-service`**
```
- Probar que ningún endpoint permite UPDATE o DELETE sobre auditoria
- Probar que todos los eventos del sistema llegan correctamente
```

---

### Quality gates

Un servicio no puede mergearse a `develop` si:
```
❌ La cobertura de pruebas unitarias es menor al 70%
❌ Hay pruebas de integración fallando
❌ El lint reporta errores
```

Un servicio no puede mergearse a `main` si:
```
❌ Las pruebas e2e del flujo que afecta están fallando
❌ No tiene documentación completa según definition-of-done.md
```

## Referencias

- [code-review.md](./code-review.md) — Criterios de revisión de código
- [10-devops/ci-cd.md](../10-devops/ci-cd.md) — Dónde se ejecutan estas pruebas
- [00-governance/definition-of-done.md](../00-governance/definition-of-done.md) — Criterios de cierre