# Criterios de aceptación

**Tarea 2 · Propuesta y planificación** · Autor: Oleksandr Rudynskyy · Rama `tarea-02-planificacion`

Cada requisito obligatorio tiene al menos un criterio comprobable con el formato
**«Dado [estado inicial], cuando [usuario y acción], entonces [resultado observable]»**.
Se incluyen casos correctos (✅), datos inválidos (⚠️) y acciones sin permiso (⛔).

Los requisitos se describen en [`01-propuesta-y-alcance.pdf`](01-propuesta-y-alcance.pdf) y las tareas que los implementan en [`07-planificacion.md`](07-planificacion.md).

## Datos de prueba comunes

| Dato | Valor |
|---|---|
| Organizadora A | `ana@techfest.example` / contraseña `Prueba1234!` |
| Organizador B | `beto@techfest.example` / contraseña `Prueba1234!` |
| Evento E1 (de A) | «Taller de Docker», aforo 40, publicado, tipo «General» con 40 plazas |
| Evento E2 (de A) | «Charla: IA en el aula», borrador, sin tipos de entrada |
| Evento E3 (de B) | «Hackathon TechFest», publicado |

---

## RF-01 · Acceso del organizador

| ID | Tipo | Criterio |
|---|---|---|
| CA-01.1 | ✅ | **Dado** que existe la organizadora A, **cuando** A introduce su email y contraseña correctos y pulsa «Entrar», **entonces** accede a «Mis eventos» y su nombre aparece en la barra superior. |
| CA-01.2 | ⚠️ | **Dado** que existe la organizadora A, **cuando** introduce una contraseña incorrecta, **entonces** permanece en «Iniciar sesión», ve el mensaje «Email o contraseña incorrectos» y el campo email conserva su valor. |
| CA-01.3 | ⚠️ | **Dado** el formulario de inicio de sesión vacío, **cuando** se pulsa «Entrar», **entonces** se muestran «Introduce tu email» e «Introduce tu contraseña» junto a cada campo y no se envía nada al servidor. |
| CA-01.4 | ⛔ | **Dado** un visitante sin sesión, **cuando** abre directamente la dirección de «Mis eventos», **entonces** se le redirige a «Iniciar sesión». |
| CA-01.5 | ✅ | **Dado** que A tiene la sesión iniciada, **cuando** pulsa «Cerrar sesión» y después usa el botón «Atrás» del navegador, **entonces** vuelve a «Iniciar sesión» y no ve datos de eventos. |

## RF-02 · Panel «Mis eventos»

| ID | Tipo | Criterio |
|---|---|---|
| CA-02.1 | ✅ | **Dado** que A tiene E1 (con 38 inscritos) y E2, **cuando** abre «Mis eventos», **entonces** ve dos filas ordenadas por fecha de inicio, con E1 «Publicado · 38/40» y E2 «Borrador · 0/120». |
| CA-02.2 | ✅ | **Dado** un organizador sin eventos, **cuando** abre «Mis eventos», **entonces** ve el texto «Todavía no has creado ningún evento» y el botón «Crear el primer evento». |
| CA-02.3 | ⛔ | **Dado** que B tiene sesión iniciada, **cuando** abre «Mis eventos», **entonces** solo aparece E3 y no aparecen E1 ni E2. |

## RF-03 · Crear evento

| ID | Tipo | Criterio |
|---|---|---|
| CA-03.1 | ✅ | **Dado** que A está en «Crear evento», **cuando** completa título «Taller de Git», lugar «Sala B», inicio 20/11/2026 10:00, fin 20/11/2026 12:00, aforo 30 y pulsa «Guardar borrador», **entonces** vuelve a «Mis eventos» con el aviso «Evento guardado como borrador» y el evento aparece con estado «Borrador». |
| CA-03.2 | ⚠️ | **Dado** el formulario «Crear evento», **cuando** A escribe el título «AI» (2 caracteres) y guarda, **entonces** ve «El título debe tener entre 3 y 120 caracteres» junto al campo y el evento no se guarda. |
| CA-03.3 | ⚠️ | **Dado** el formulario «Crear evento», **cuando** la fecha de fin es anterior o igual a la de inicio, **entonces** ve «La fecha de fin debe ser posterior al inicio» y el resto de valores introducidos se conservan. |
| CA-03.4 | ⚠️ | **Dado** el formulario «Crear evento», **cuando** el aforo es 0, negativo, decimal o mayor de 5.000, **entonces** ve «El aforo debe ser un número entero entre 1 y 5.000». |
| CA-03.5 | ⚠️ | **Dado** que la validación del navegador se ha desactivado, **cuando** se envía un evento sin título directamente al servidor, **entonces** Laravel devuelve el mismo error y no se crea ningún registro en `events`. |

## RF-04 · Tipos de entrada gratuitos

| ID | Tipo | Criterio |
|---|---|---|
| CA-04.1 | ✅ | **Dado** un evento con aforo 120, **cuando** A añade «General» (90 plazas) y «Estudiantes» (30 plazas) y guarda, **entonces** ambos tipos aparecen en el evento con un total de 120 plazas. |
| CA-04.2 | ⚠️ | **Dado** un evento con aforo 120, **cuando** A intenta guardar tipos cuya suma es 130, **entonces** ve «La suma de plazas (130) supera el aforo (120)» y no se guarda ningún cambio. |
| CA-04.3 | ⚠️ | **Dado** un tipo de entrada nuevo, **cuando** el nombre está vacío o las plazas son 0, **entonces** se muestra el error correspondiente junto a ese campo. |

## RF-05 · Publicar y página pública

| ID | Tipo | Criterio |
|---|---|---|
| CA-05.1 | ✅ | **Dado** un evento en borrador con al menos un tipo de entrada, **cuando** A pulsa «Publicar», **entonces** el estado cambia a «Publicado» y la página pública muestra título, fechas, lugar, descripción y plazas libres por tipo. |
| CA-05.2 | ⚠️ | **Dado** E2 (sin tipos de entrada), **cuando** A pulsa «Publicar», **entonces** ve «Añade al menos un tipo de entrada antes de publicar» y E2 sigue en borrador. |
| CA-05.3 | ⛔ | **Dado** E2 en borrador, **cuando** un visitante abre su dirección pública, **entonces** ve «Evento no disponible» y ningún dato del evento. |
| CA-05.4 | ⛔ | **Dado** que B tiene sesión iniciada, **cuando** intenta publicar E1 de A (por ejemplo, reenviando la petición), **entonces** recibe «No tienes permiso» (403) y E1 no cambia. |

## RF-06 · Inscripción

| ID | Tipo | Criterio |
|---|---|---|
| CA-06.1 | ✅ | **Dado** E1 publicado con plazas libres, **cuando** un asistente elige «General», escribe nombre «Lucía», apellidos «Pérez», email `lucia@example.com`, acepta el tratamiento de datos y pulsa «Confirmar inscripción», **entonces** ve «Inscripción confirmada» con una referencia con formato `TF-XXXX-NNNN` y existe una fila en `registrations`. |
| CA-06.2 | ⚠️ | **Dado** el formulario de inscripción, **cuando** el email es `lucia@example` o está vacío, **entonces** ve «Introduce un email válido (ej.: nombre@dominio.com)» y no se crea la inscripción. |
| CA-06.3 | ⚠️ | **Dado** el formulario de inscripción, **cuando** no se marca la aceptación del tratamiento de datos, **entonces** ve «Debes aceptar el tratamiento de datos para inscribirte». |
| CA-06.4 | ⚠️ | **Dado** el formulario de inscripción, **cuando** el nombre o los apellidos superan 80 caracteres o están vacíos, **entonces** ve el error junto al campo y se conservan los demás datos escritos. |

## RF-07 · Control de aforo y duplicados

| ID | Tipo | Criterio |
|---|---|---|
| CA-07.1 | ⚠️ | **Dado** que `lucia@example.com` ya está inscrita en E1, **cuando** se intenta inscribir `Lucia@Example.com ` (mayúsculas y espacio final) en E1, **entonces** ve «Este email ya está inscrito en este evento» y el número de inscritos no cambia. |
| CA-07.2 | ✅ | **Dado** que `lucia@example.com` está inscrita en E1, **cuando** se inscribe con el mismo email en E3, **entonces** la inscripción se acepta (el control es por evento). |
| CA-07.3 | ⚠️ | **Dado** que «General» de E1 tiene 0 plazas libres, **cuando** un asistente abre la página pública, **entonces** el tipo aparece como «Agotado», no se puede seleccionar, y si se envía igualmente la petición el servidor responde «No quedan plazas para este tipo de entrada». |
| CA-07.4 | ⚠️ | **Dado** que queda 1 plaza, **cuando** dos asistentes confirman a la vez, **entonces** solo una inscripción se guarda y la otra persona ve «No quedan plazas para este tipo de entrada». |

## RF-08 · Lista de asistentes

| ID | Tipo | Criterio |
|---|---|---|
| CA-08.1 | ✅ | **Dado** E1 con 38 inscritos, **cuando** A abre «Asistentes» de E1, **entonces** ve 25 filas con nombre, email, tipo, referencia y fecha, el total «38 / 40 inscritos» y la página 2 con las 13 restantes. |
| CA-08.2 | ✅ | **Dado** la lista de E1, **cuando** A busca «pérez» o la referencia completa de Lucía, **entonces** solo aparecen las inscripciones que coinciden. |
| CA-08.3 | ✅ | **Dado** la lista de E1, **cuando** la búsqueda no tiene resultados, **entonces** ve «Ningún asistente coincide con «zz»» y el botón «Limpiar búsqueda». |
| CA-08.4 | ⛔ | **Dado** que B tiene sesión iniciada, **cuando** abre la dirección de «Asistentes» de E1 de A, **entonces** recibe «No tienes permiso para ver este evento» (403) y no ve ningún dato personal. |

## RNF-01 · Interfaz adaptable y usable con teclado

| ID | Tipo | Criterio |
|---|---|---|
| CA-R1.1 | ✅ | **Dado** un navegador con 360 px de ancho, **cuando** se recorren las pantallas P1–P5, **entonces** no aparece desplazamiento horizontal y las tablas se muestran como tarjetas. |
| CA-R1.2 | ✅ | **Dado** cualquier pantalla del recorrido, **cuando** se navega solo con Tab, Mayús+Tab, Enter y Espacio, **entonces** se alcanzan todos los controles en orden lógico y el foco siempre es visible. |
| CA-R1.3 | ⚠️ | **Dado** un formulario con errores, **cuando** se envía, **entonces** el foco pasa al resumen de errores, cada error enlaza con su campo y el lector de pantalla lo anuncia (`aria-describedby`, `role="alert"`). |

---

## Requisitos deseables y opcionales

| ID | Req. | Criterio |
|---|---|---|
| CA-09.1 | RF-09 | **Dado** E1 con 38 inscritos, **cuando** A cambia el aforo a 30, **entonces** ve «El aforo no puede ser menor que los inscritos (38)» y no se guarda. |
| CA-10.1 | RF-10 | **Dado** que el worker está en marcha, **cuando** Lucía confirma su inscripción, **entonces** en menos de 1 minuto aparece en MailDev (`http://localhost:1080`) un correo a `lucia@example.com` con su referencia. |
| CA-11.1 | RF-11 | **Dado** que Lucía no ha llegado, **cuando** el personal de acceso busca su referencia y pulsa «Registrar llegada», **entonces** se guarda la hora y un segundo intento muestra «Llegada ya registrada a las HH:MM». |

## Matriz de trazabilidad

| Requisito | Prioridad | Criterios | Pantalla del prototipo | Tarea |
|---|---|---|---|---|
| RF-01 | Obligatoria | CA-01.1–01.5 | P1 | T-03 |
| RF-02 | Obligatoria | CA-02.1–02.3 | P2 | T-04 |
| RF-03 | Obligatoria | CA-03.1–03.5 | P3 | T-05 |
| RF-04 | Obligatoria | CA-04.1–04.3 | P3 | T-06 |
| RF-05 | Obligatoria | CA-05.1–05.4 | P2, P4 | T-07 |
| RF-06 | Obligatoria | CA-06.1–06.4 | P4 | T-08 |
| RF-07 | Obligatoria | CA-07.1–07.4 | P4 | T-09 |
| RF-08 | Obligatoria | CA-08.1–08.4 | P5 | T-10 |
| RNF-01 | Obligatoria | CA-R1.1–R1.3 | P1–P5 | T-11 |
| RF-09 | Deseable | CA-09.1 | (P3 en modo edición) | T-14 |
| RF-10 | Deseable | CA-10.1 | P4 (confirmación) | T-15 |
| RF-11 | Opcional | CA-11.1 | — | T-17 |
