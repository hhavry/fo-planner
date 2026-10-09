# FO Planner Hotel Monserrat — contexto del proyecto

Archivo de contexto para quien retome esta app (una persona o un asistente de IA). Leelo antes de tocar `index.html`.

## Qué es

App web de estudio de Front Office para alumnos de primer año de la materia **Departamento de Front Office y Housekeeping (2.6.106)**, 2026. La docente es Helena Havrylets.

En la app se llama **«Front Office»** (título y pestaña del navegador): pedido de la docente. «FO Planner» queda solo como nombre del repositorio y del proyecto.

Es la app **hermana de HK Planner** (Housekeeping): misma estructura, mismo hotel ficticio, mismas reglas de trabajo, con la paleta en verdes.

- Repositorio: https://github.com/hhavry/fo-planner (rama `main`)
- Público: https://fo-planner-three.vercel.app (Vercel publica solo cada push a `main`; la dirección `fo-planner.vercel.app` pertenece a otro proyecto)
- App hermana: https://hk-planner.vercel.app · https://github.com/hhavry/hk-planner

El «Hotel Monserrat» es **ficticio**: 24 habitaciones en 3 pisos (101–108, 201–208, 301–308).

## Cómo está hecha

- Un único archivo `index.html` con HTML, CSS y JavaScript adentro. Sin build, sin dependencias, sin backend.
- Única carga externa: Google Fonts (Bricolage Grotesque para títulos, Figtree para texto), con fuentes de respaldo.
- El avance de cada alumno se guarda en `localStorage`, clave `foplanner.v1`, solo en su dispositivo. No hay nombres, cuentas ni seguimiento: es una decisión de la docente.
- Todo el DOM se arma con la función `h(tag, attrs, ...hijos)`. El texto ingresado por el usuario se inserta siempre con `textContent`.
- Navegación por hash: `#reservas` (pantalla inicial), `#checkin`, `#checkout`, `#conserjeria`, `#telefonia`.
- Debe verse bien en celular (probada a 360 y 400 px) y no tener scroll horizontal de página. Solo las tablas anchas se deslizan dentro de su propio contenedor (`.tbl`).

### Publicar un cambio

1. Editar `index.html`.
2. Probarlo abriéndolo en el navegador (y a 400 px de ancho).
3. Commit y push a `main`. Vercel publica solo en el mismo link en un minuto.

## Estructura de la app

Cinco pestañas, una por tema. Todas tienen modo **Estudiar** y modo **Practicar**, y un botón **Glosario** propio de la pestaña, con buscador. El selector de modo va en un recuadro destacado con borde verde, «¿Qué querés hacer?», y el botón del glosario va debajo, fuera del recuadro, a ancho completo (`modeBar`): pedido de la docente para que se vean bien.

| Pestaña | Estudiar | Practicar | Funciones en el código |
| --- | --- | --- | --- |
| Reservas | Objetivos; tomar una reserva (10 pasos en 4 fases); tipos de reserva; canales, conductos, voucher; tipos de habitación; tarifas y planes; cómo se enuncia la tarifa; planillas; grupos; modificaciones, cancelaciones y no show; overbooking; comunicación | Formulario de reserva que no se guarda si falta un dato; planning de ocupación de 24 habitaciones × 7 noches (se asigna tocando el número o cualquier casillero de la fila; los días quedan fijos arriba al desplazarse y la reserva elegida y el veredicto, en una barra fija abajo; con las cinco resueltas aparece «Empezar de nuevo» arriba); caso de overbooking | `vReservas`, `reservaForm`, `planning`, datos en `R_STEPS`, `OCC`, `PEND`, `ESCENAS`, `CASO_OVB` |
| Check in | Funciones y perfil; turnos y pase de turno; tipos de check in; antes de la llegada; 10 pasos (R·A·D, 4 minutos); después, no show, grupos; ficha de registro; control de documentos; garantía y preautorización; PP/EP/FC | Ordenar los 10 pasos; calcular la garantía; caso en el mostrador | `vCheckin`, `garantiaGame`, `CI_STEPS`, `CI_ANTES`, `CI_CUPON`, `CASO_CI` |
| Check out | Tipos; antes; 12 pasos; después; late check out; cuenta, folio y factura; auditoría nocturna; quejas en 6 pasos; encuestas y fidelización; tecnología | «¿Quién paga esto?» (repartir cargos en folios); caso de queja; ordenar los 12 pasos | `vCheckout`, `pagaGame`, `CO_STEPS`, `CO_ANTES`, `QUEJA`, `PAGA`, `CASO_QJ` |
| Conserjería | Tareas del conserje; depósito de equipaje; correspondencia y paquetes; normas de seguridad; bellboy, doorman y valet; Les Clefs d'Or | Registrar un equipaje en tránsito (no se guarda sin troquel, datos y lugar seguro; retiro con o sin comprobante); «¿De quién es la tarea?»; caso del paquete | `vConserjeria`, `equipajeForm`, `EQ_STEPS`, `CORR_STEPS`, `TAREAS`, `CASO_PQ` |
| Telefonía | Pautas; speech externo e interno (español e inglés); atender y transferir; toma de mensajes; despiertes; otras pautas | Armar el speech; tomar un mensaje (no se guarda incompleto); caso «un turno en la central» | `vTelefonia`, `mensajeForm`, `TEL_STEPS`, `MSG_STEPS`, `DESP_STEPS`, `FRASES`, `CASO_TEL` |

Componentes compartidos: `steps` (procedimiento con casillas y «Por qué»), `modelo` y `sheet` (planillas que se abren con un clic), `glosario`, `quiz`, `orderGame`, `caseGame` (caso con decisiones), `classGame` (clasificar), `losNo`.

Las preguntas de repaso están en `QUIZ` (58 en total: opción múltiple y verdadero/falso; una pregunta sin `o` es verdadero/falso, con `a:0` verdadero y `a:1` falso). El glosario está en `GLOS` (definiciones) y `GTAB` (qué términos muestra cada pestaña).

Los datos del hotel están en `TIPOS`, `tipoDe` y `OCC`.

## De dónde sale el contenido

Fuente única: las **presentaciones de clase** de la cátedra (PDF), que siguen a Simón, M. Á., *Recepción: Front Office*, y los apuntes de Di Muro:

- Clase 3 · Unidad 2.1 Reservas (parte 1) y Clase 4 · Unidad 2.2 Reservas (parte 2) → pestaña Reservas.
- Clase 6-7 · Unidad 3 Recepción, Check in → pestaña Check in.
- Clase 8 · Check out y otros → pestaña Check out.
- Clase 8 · Conserjería y Telefonía → pestañas Conserjería y Telefonía.

La **Unidad 1** (Clases 1 y 2: hospitalidad, estructura del hotel, ciclo del huésped) quedó afuera por decisión de la docente; solo se usa su glosario.

Regla de trabajo: **no inventar contenido hotelero**. Si algo no está en las presentaciones, se consulta a la docente. Los datos que hubo que inventar para poder practicar llevan en la app la etiqueta **«Modelo de ejemplo»**.

### Decisiones de la docente sobre el contenido

- **PP, EP y FC** se usan como en la Clase 8: PP = Paga Pax, EP = Extras Pax (el cliente paga el alojamiento; el pasajero, los extras), FC = Full Credit. La Clase 3 (2.9) los define distinto; no se usa esa versión.
- **Espera telefónica:** «no más de 30 segundos» (una diapositiva decía 20-30).
- **Preguntas de repaso:** opción múltiple o verdadero/falso.

### Lo que no sale de las presentaciones (pendiente de revisión de la docente)

- **Datos del Hotel Monserrat:** distribución de tipos por piso (x01-x02 sencilla, x03-x04 doble twin, x05-x06 doble matrimonial, x07 triple, x08 superior), tarifas, la 101 como accesible y la 205-206 como comunicadas.
- **Planning:** la ocupación de la semana modelo y las cinco reservas a asignar.
- **Datos de los modelos:** voucher, rooming list, ficha de registro, planillas de equipaje, de correspondencia y de despiertes. Los campos son los de las clases; los datos y el formato, no. La ficha de reserva, el cálculo de garantía, los cuatro casos de folios, las tres facturas y el mensaje telefónico sí están tomados de las clases.
- **Escenas de práctica:** los tres pedidos de reserva y las tres situaciones de equipaje.
- **Algunos «Por qué»**, redactados cuando la diapositiva no daba la razón: Reservas pasos 1 y 5 y los cuatro del protocolo de overbooking; «antes de la llegada» paso 3; check in pasos 2, 3, 7, 9 y 10; «antes del check out» paso 3; check out pasos 1 y 2; correspondencia pasos 1, 3 y 4; atender y transferir pasos 2, 4 y 5; mensajes paso 1; despiertes pasos 2 y 3.
- **Los No:** el contenido sale de las diapositivas, pero la redacción con «Nunca…» y «Jamás…» es propia.
- **Las 58 preguntas de repaso** y **los cinco casos con decisiones** (las opciones incorrectas son inventadas).
- **Garantía en una reserva EP:** el ejercicio le pide al huésped el 50 % del alojamiento como previsión de extras. La clase dice «solo por los extras» y da el 50 % para el caso PP; aplicarlo a EP es una extrapolación.
- **Dos respuestas de los casos** combinan diapositivas: tarjeta a nombre de otro → pedir otro medio; habitación no lista → ofrecer el depósito de Conserjería.
- **Speech:** el ejemplo de la clase dice «Hotel Escuela»; en la app dice «Hotel Monserrat».
- **Definiciones del glosario** armadas a partir del texto de las clases y no de su glosario: troquel, walking, speech, preautorización, POS, room status, libro de novedades, luggage room, despierte, release, bedbank, city ledger, incidentals, split folio, express check out, room & tax.
- **Motivos de algunos campos obligatorios** en los formularios (apellido y nombre, canal de entrada, destinatario y acción requerida del mensaje).

No se incluyeron: los ejemplos de hoteles y cadenas reales, las estadísticas marcadas «Informativo» (D-EDGE, American Express), el marco legal, y el «muestreo de habitaciones» (lo menciona una pregunta del cuadernillo pero no está desarrollado en ninguna presentación).

## Preferencias de la docente (respetarlas)

- Idioma: español rioplatense, con voseo («tocá», «elegí»).
- El recuadro de prohibiciones se titula **«Los No»** y cada ítem empieza con «Nunca…» o «Jamás…».
- La práctica se llama **«Preguntas de repaso»**, no «tipo parcial».
- Las pestañas llevan **iconos de línea de un solo tono** (calendario, llave, cuenta, campana, teléfono).
- Paleta en **verdes**, tomada de las diapositivas de Front Office: fondo crema `#f5f3ee`, verde muy oscuro `#12241c` para texto, `#143a2b` para las bandas de sección, `#1c6a4c` como acento. En modo oscuro, fondo verde casi negro y acento menta `#7fd3aa`.
- Alto contraste y secciones bien separadas: cada título de sección (`h3`) es una banda oscura de ancho completo.
- Los colores con significado no se tocan: verde/rojo de respuesta, rojo de «Los No», ámbar de «Modelo de ejemplo».
- Quiere visibilidad: tareas a la vista, modelos que se abren con un clic.
- El glosario se abre dentro de cada pestaña, con los términos propios de ese tema.
