# Análisis de riesgos

**Tarea 2 · Propuesta y planificación** · Autor: Oleksandr Rudynskyy · Responsable de todos los riesgos: **Oleksandr Rudynskyy** (trabajo individual)

**Escala:** probabilidad e impacto **Baja / Media / Alta**. La prioridad combina ambos: se vigilan primero los riesgos con nivel **Alto**.

## Registro de riesgos

| ID | Categoría | Riesgo | Probabilidad | Impacto | Nivel | Prevención | Respuesta si ocurre | Responsable |
|---|---|---|---|---|---|---|---|---|
| R1 | Tecnología antigua | La aplicación actual (PHP 7.4, Laravel 6, Debian 10) no es compatible con las versiones nuevas de PHP y Laravel, y una actualización «en el sitio» rompe Attendize sin llegar a funcionar la nueva. | Alta | Alto | **Alto** | No actualizar Attendize: la nueva aplicación se crea en un proyecto y contenedores separados. Attendize se mantiene solo como referencia y fuente de datos. | Volver a la etiqueta `tarea-01-entrega`, que funciona. Documentar la incompatibilidad en el README. | O. Rudynskyy |
| R2 | Pérdida de datos | Al migrar desde la base de datos de Attendize se pierden o se duplican inscripciones. | Media | Alto | **Alto** | Copia con `mysqldump` antes de cada prueba; migrar primero a una base de datos de prueba; comparar recuentos antes/después; índice único `(event_id, email)`; informe de filas rechazadas. | Restaurar la copia, corregir el script con el informe de rechazados y repetir. | O. Rudynskyy |
| R3 | Seguridad | Exposición de datos personales de asistentes (nombre, email) a otro organizador o a terceros; inyección SQL o envíos falsificados. | Media | Alto | **Alto** | Autenticación de Laravel, políticas de acceso por organizador (CA-02.3, CA-05.4, CA-08.4), validación siempre en servidor, consultas mediante Eloquent, protección CSRF, `.env` fuera de Git, minimización de datos (solo nombre, apellidos y email). | Revocar sesiones, regenerar `APP_KEY` y contraseñas, revisar registros y corregir la política afectada. | O. Rudynskyy |
| R4 | Dependencias | Paquetes de Composer o npm con vulnerabilidades, abandonados o con cambios incompatibles (problema ya visto en la Tarea 1). | Media | Medio | Medio | Versiones fijadas con `composer.lock` y `package-lock.json`; ejecutar `composer audit` y `npm audit` al cerrar cada hito; usar solo paquetes oficiales o muy usados. | Actualizar el paquete a una versión corregida o sustituirlo; anotar el cambio en el README. | O. Rudynskyy |
| R5 | Tiempo | Subestimar el aprendizaje de React, TypeScript e Inertia.js y no terminar el núcleo obligatorio. | Alta | Alto | **Alto** | Alcance mínimo de 9 requisitos; 20 % de margen; empezar por el recorrido completo más simple (H1–H3) antes de pulir; tareas deseables solo tras H3. | Pasar requisitos deseables a «fuera de alcance» y comunicarlo en `08-validacion.md`. | O. Rudynskyy |
| R6 | Organización personal | Coincidencia con exámenes y entregas de otros módulos que retrasa el proyecto. | Media | Medio | Medio | Planificación semanal; revisión del estado cada viernes en `07-planificacion.md`; trabajar en bloques cortos y con commits pequeños. | Replanificar las tareas pendientes y avisar al profesorado antes de la fecha de entrega. | O. Rudynskyy |
| R7 | Despliegue | El entorno Docker en Windows vuelve a fallar (finales de línea, `env_file`, puertos ocupados, volumen montado que oculta dependencias). | Media | Medio | Medio | Reutilizar las soluciones de la Tarea 1 (`.gitattributes`, recrear contenedores tras cambiar `.env`, instalar dependencias en el contenedor); README con los pasos exactos; comprobar con un clon limpio. | Revisar `docker compose logs`, aplicar la solución documentada o registrar el nuevo problema con causa y solución. | O. Rudynskyy |

## Matriz probabilidad × impacto

| Probabilidad \ Impacto | Bajo | Medio | Alto |
|---|---|---|---|
| **Alta** | — | — | R1, R5 |
| **Media** | — | R4, R6, R7 | R2, R3 |
| **Baja** | — | — | — |

## Seguimiento

Los riesgos se revisan al cerrar cada hito (H1–H4) junto con la planificación.

| Fecha | Riesgo | Cambio | Observaciones |
|---|---|---|---|
| 28/10/2026 | Todos | Registro inicial | — |
