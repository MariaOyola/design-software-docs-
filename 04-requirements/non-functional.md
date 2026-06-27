# Requisitos No Funcionales

> Estado:  🟢 En progreso | Última actualización: Última actualización: 2026-06-27 | Equipo: Por definir | Equipo: Por definir

## Contexto

Define los atributos de calidad, seguridad, rendimiento y operación que el sistema debe cumplir. Se derivan de las restricciones definidas en [`01-context/scope.md`](../01-context/scope.md). Las decisiones técnicas para cumplirlos se documentan como ADRs en [`05-architecture/decisions/`](../05-architecture/decisions/).

## Contenido

### RNF-01 · Rendimiento

| ID | Requisito | Métrica |
|---|---|---|
| RNF-01-01 | La autenticación de un usuario debe completarse en tiempo aceptable | ≤ 3 segundos |
| RNF-01-02 | La generación automática de un horario para una ficha debe completarse en tiempo aceptable | ≤ 30 segundos |
| RNF-01-03 | La consulta de disponibilidad de ambientes debe responder en tiempo aceptable | ≤ 3 segundos |
| RNF-01-04 | La consulta del horario por instructor o aprendiz debe responder en tiempo aceptable | ≤ 3 segundos |
| RNF-01-05 | Las notificaciones de cambio de horario deben enviarse en tiempo aceptable | ≤ 1 minuto tras el evento |

---

### RNF-02 · Seguridad

| ID | Requisito |
|---|---|
| RNF-02-01 | Todo endpoint del sistema requiere token JWT válido, excepto login y registro |
| RNF-02-02 | Los datos personales de aprendices e instructores deben tratarse conforme a la Ley 1581 de 2012 |
| RNF-02-03 | Los registros de auditoría no pueden modificarse ni eliminarse bajo ninguna circunstancia |
| RNF-02-04 | Las contraseñas deben almacenarse con hash seguro, nunca en texto plano |
| RNF-02-05 | Ningún servicio puede acceder directamente a la base de datos de otro servicio |

---

### RNF-03 · Disponibilidad y operación

| ID | Requisito |
|---|---|
| RNF-03-01 | El sistema debe estar disponible durante el horario académico del SENA sin interrupciones no planificadas |
| RNF-03-02 | Cada microservicio debe poder desplegarse y reiniciarse de forma independiente sin afectar los demás |
| RNF-03-03 | El sistema debe tener mecanismo de backup para las 9 bases de datos |

---

### RNF-04 · Arquitectura

| ID | Requisito |
|---|---|
| RNF-04-01 | Cada microservicio debe tener su propia base de datos — ningún servicio comparte BD con otro |
| RNF-04-02 | La comunicación entre servicios debe hacerse por API REST o eventos, nunca por acceso directo a BD |
| RNF-04-03 | La documentación de un microservicio debe existir antes de su primer merge a main |

---

### RNF-05 · Usabilidad

| ID | Requisito |
|---|---|
| RNF-05-01 | El sistema debe funcionar en navegadores web modernos (Chrome, Firefox, Edge) sin instalación adicional |
| RNF-05-02 | Los mensajes de error deben ser claros e indicar al usuario qué acción tomar |

## Referencias

- [01-context/scope.md](../01-context/scope.md) — Restricciones de origen
- [functional.md](./functional.md) — Requisitos funcionales relacionados
- [05-architecture/decisions/](../05-architecture/decisions/) — Decisiones técnicas para cumplir estos requisitos
- [traceability-matrix.md](./traceability-matrix.md) — Trazabilidad completa