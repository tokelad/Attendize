# Tarea 2 · Propuesta y planificación

**Modernización de Attendize v2.8.0 para la gestión de eventos de TechFest**

| Dato | Valor |
|---|---|
| Autor | Oleksandr Rudynskyy |
| Repositorio | https://github.com/tokelad/Attendize |
| Rama | `tarea-02-planificacion` |
| Versión de partida | `tarea-01-entrega` (= `tarea-02-inicio`) |
| Versión final | `tarea-02-entrega` |
| Tecnologías objetivo | Laravel · React · TypeScript · Inertia.js · MySQL |

> En esta tarea no se modifica el código de Attendize: solo se define qué se construirá.

## Resumen de la propuesta

- **Recorrido principal:** «De la publicación a la lista de inscritos». El organizador crea y publica un evento con tipos de entrada gratuitos, un asistente se inscribe desde la página pública y el organizador consulta la lista de inscritos.
- **Usuarios:** organizador/a de TechFest, asistente y personal de acceso.
- **Núcleo obligatorio:** 9 requisitos (RF-01 a RF-08 y RNF-01), unas 58 h + 20 % de margen.
- **Fuera de alcance:** pagos, reembolsos, impuestos, entradas en PDF, afiliados, multidioma, API pública.

## Documentos

| # | Documento | Contenido |
|---|---|---|
| 1 | [01-propuesta-y-alcance.pdf](01-propuesta-y-alcance.pdf) | Problema (hechos y supuestos), usuarios, alcance y 12 requisitos |
| 2 | [02-criterios-aceptacion.md](02-criterios-aceptacion.md) | Criterios «Dado / cuando / entonces» y matriz de trazabilidad |
| 3 | [03-prototipo.pdf](03-prototipo.pdf) | Mapa de navegación y 5 pantallas en escritorio y móvil, con estados y teclado |
| 4 | [04-arquitectura-y-datos.pdf](04-arquitectura-y-datos.pdf) | Arquitectura, recorrido de una petición, entidades, validaciones y correspondencia de datos |
| 5 | [05-riesgos.md](05-riesgos.md) | 7 riesgos con probabilidad, impacto, prevención y respuesta |
| 6 | [06-digitalizacion-sostenibilidad.pdf](06-digitalizacion-sostenibilidad.pdf) | Mejora del proceso, 2 indicadores y 2 medidas de sostenibilidad |
| 7 | [07-planificacion.md](07-planificacion.md) | Hitos, tareas, dependencias, estimaciones y estados |
| 8 | [08-validacion.md](08-validacion.md) | Revisión con el profesorado (**pendiente**) |

## Trazabilidad

| Requisito | Prioridad | Criterios | Pantalla | Tarea |
|---|---|---|---|---|
| RF-01 Acceso del organizador | Obligatoria | CA-01.1–01.5 | P1 | T-03 |
| RF-02 Panel «Mis eventos» | Obligatoria | CA-02.1–02.3 | P2 | T-04 |
| RF-03 Crear evento | Obligatoria | CA-03.1–03.5 | P3 | T-05 |
| RF-04 Tipos de entrada | Obligatoria | CA-04.1–04.3 | P3 | T-06 |
| RF-05 Publicar y página pública | Obligatoria | CA-05.1–05.4 | P2, P4 | T-07 |
| RF-06 Inscripción | Obligatoria | CA-06.1–06.4 | P4 | T-08 |
| RF-07 Aforo y duplicados | Obligatoria | CA-07.1–07.4 | P4 | T-09 |
| RF-08 Lista de asistentes | Obligatoria | CA-08.1–08.4 | P5 | T-10 |
| RNF-01 Adaptable y teclado | Obligatoria | CA-R1.1–R1.3 | P1–P5 | T-11 |
| RF-09 Editar evento | Deseable | CA-09.1 | P3 | T-14 |
| RF-10 Correo de confirmación | Deseable | CA-10.1 | P4 | T-15 |
| RF-11 Check-in | Opcional | CA-11.1 | — | T-17 |
