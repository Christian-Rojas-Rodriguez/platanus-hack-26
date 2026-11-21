# Feedback del mentor (reunión de producto)

- **Fecha:** 21 de noviembre de 2026, ~12:36–12:55 (hora de Chile)
- **Evento:** Platanus Hack 26, track AI Safety
- **Fuente:** nota de voz de la reunión de producto con el mentor (~18 min 50 s). Transcripción ASR (faster-whisper `medium`, CPU int8, por tramos). Los hablantes se separaron de forma heurística (Mentor / Equipo); no se asignaron nombres propios porque no se oyen con claridad. Puede tener errores, sobre todo en nombres propios y en tramos con crosstalk.

## Quiénes hablan

- **Mentor:** da el feedback de producto y de demo. No se pudo confirmar un nombre a partir del audio.
- **Equipo:** al menos dos personas del equipo. Responden sobre papers, usuario, estado de la demo y proponen casos reales / una vulnerabilidad histórica. No se etiquetan con nombres (Jaime, Mauricio, Smoke u otros) porque el ASR no los deja oír con seguridad.

## Decisiones y feedback

El mentor les dice que van **muy bien encaminados** frente a otros grupos que todavía están definiendo el problema o evaluando cambiarse de track o de solución. Tienen espacio para ser **súper ambiciosos**. Ya tienen un *statement* de demo: hoy podrían armar una demo básica y, en su opinión, estarían en condiciones de presentar en aproximadamente una hora. Aun así, quiere ver hasta dónde pueden llevarlo con seguridad.

Preguntó tres cosas y el equipo respondió así:

1. **¿Hay investigación (labs, organizaciones, papers)?** Hay papers (no una organización detrás): el equipo menciona unos cuatro a favor y uno en contra. Todavía no los tenían todos leídos. Compararon con lo que se está haciendo en los Platanus de este año y vieron ese espacio **muy saturado**; de *esta* idea, en cambio, sienten que **nadie la está haciendo**.
2. **¿Hay alguien en el mercado con una solución parecida?** No tan de cerca en lo técnico. Hay productos más terminados, pero el equipo cree que puede aportar un approach más científico. Lo ven poco explorado.
3. **¿Quién es el usuario final?** Developers e engineers que mantienen **codebases grandes**, no proyectos de un fin de semana. La empresa compraría la solución y se la pediría a su equipo. Quieren que sirva con **Claude Code, Codex o herramientas equivalentes**. El mentor aclara que no le importa tanto la parte comercial, pero sí la propuesta de valor: el cliente es **la empresa o la persona que usa el modelo del AI lab, no el lab directamente**.

Sobre la demo en vivo: si les dieran ~5 minutos, ¿pueden correr un test entero, no una grabación ni una simulación? El equipo **no confiaría del todo**. En las pruebas actuales, un ejemplo tarda ~2 minutos, y **todavía no lo probaron en un repo real**. Proponen tomar repos, tener un **dashboard de resultados** y disparar una corrida mientras lo muestran; si no termina, usan lo corrido hoy para mañana. También pensaron que, si encuentran algo, podrían **reportar** un recorte / hallazgo en código open source y mencionarlo mañana.

### Qué les pide el mentor (esto es lo central)

- El problema y una solución (al menos un esbozo) ya están definidos. El siguiente paso, de acá a la **sesión de la noche**, es pensar cómo hacer la demo **más impresionante / más wow** en el tiempo acotado, y cómo comunicar el valor. A la noche hablan el *storyline*.
- **No arriesgar** una evaluación larga en vivo sobre un repo grande: es muy probable que no termine y queden en blanco. Puede servir una simulación con datos ya corridos y reales, o un **repo chico con PRs chicos** que sí corra en ~1 minuto en vivo, más una demo ambiciosa prearmada en la que confíen. No bombardear con muchas demostraciones: casarse con un par.
- Tres palancas de valor, en este orden:
  1. **Investigación** (hay camino empírico; no alargarla demasiado).
  2. **Cadena especulativa:** si no se implementa la solución, en un futuro con más PRs lanzadas y aprobadas 100% por IA pueden aparecer incidentes de ciberseguridad (y otros escenarios). El wow está en **visualizar esa cadena** —una PR mala o nociva se aprueba → incidente → efecto real y preocupante— y mostrar dónde entra Contraprueba a cortarla.
  3. **Demo práctica**, que es donde más trabajo hay que meter. Si el MVP ya corre, ir a una demo ambiciosa.
- **Enmarcar en ciberseguridad, no en calidad de producto.** El mentor no se enfocaría en “esto hace mejor el producto” o “evita que un feature se rompa en producción”: eso no se lee como *safety*. El nicho wow son los **incidentes de ciberseguridad, que están *on the rise***. Comunicar esos incidentes de forma preocupante, mostrar cómo interviene la solución y **probar con métricas** que es efectiva. Un ejemplo de métrica que sugiere: pedir PRs malas o nocivas al jurado o a gente de la hackatón y poder decir “nos tiraron 100 y agarramos el 80%”.
- La solución es **más compleja de comunicar** que la de otro grupo con el que acababa de hablar (esa otra corre de punta a punta de un saque, pero es más chica y simple). El equipo coincide: les está costando articular la propuesta de valor, aunque sienten que lo técnico está sólido.

### Features adicionales, branding y casos reales

El equipo preguntó si conviene agregar algo más *flashy*: un lado más técnico, más fácil de usar para un agente tipo Claude, o **SLMs corriendo en local**. El mentor pregunta si eso **cambia la demo**. El equipo dice que no tanto. Entonces: **no aporta demasiado**. Priorizar una muy buena demo.

Sí aporta un **branding mínimo**: no decir “creamos un repo o un mecanismo”, sino “creamos un **producto**, se llama X y funciona así”. Empezar por una **metáfora**, ponerle un nombre, contar la historia no solo con código. (El ASR registró “se llama Tanto”; parece un ejemplo genérico del mentor, no un bautismo confirmado.)

**No enfocarse en features adicionales:** el producto ya es complejo; más features lo complican. Invertir el tiempo en que el MVP corra bien (lo ve bastante sólido) y en comunicar el problema y las palancas de valor.

Si hay que agregar algo, **calidad sobre cantidad**, features fáciles de comunicar, y que se entiendan como capas sobre el core (un producto 360), no como un “flop” de features sueltas. Distingue dos tipos:

- **Más líneas de core** (otras formas de detectar/evaluar PRs, “otras líneas de negocio”): **no iría por ahí**, porque cada una pide su propia demo.
- **Features higiénicas / estéticas / *nice to have*** (dashboard con checks, poder correrlo en cualquier momento y no solo como PR): no crean una forma nueva de mostrar valor, pero hacen que se vea un producto más consolidado. Como están en un buen lugar y tienen capacidad, **vale la pena explorarlas**.

El equipo pregunta si causaría más impacto mostrar que **encontraron una vulnerabilidad** (el nombre del blanco no quedó claro: el ASR oscila entre “grupo de Barcelona / Varsel”) y si conviene hacer **ataques reales**. El mentor lo ve bien. También proponen reproducir un caso de **hace unos meses**: un agente presentó una vulnerabilidad en un PR; simular el estado anterior del repo público, correr la herramienta sobre esa PR y decir “esto se podría haber detectado”. **Todavía no lo hicieron.** El mentor pregunta si tienen una buena hipótesis de que lo detectarían; el equipo dice que sí, hay que ir al blog, al momento justo y agarrar el commit. Al mentor **le gusta mucho** para la demo.

Cierre: le tiene **harta fe**, la ve bien *frameada* y prometedora. Prioridades claras. Quedan en hablar **esta noche, tipo 19:00–20:00 (hora de Chile)**, de la demo y la presentación; el mentor dice que tiene opiniones sobre cómo armar una presentación clara. Se ofrecen a mandar ideas por WhatsApp. Al final, ya en un tramo más informal (incluye charla sobre un objeto impreso en 3D, de edición limitada), el equipo repasó el esquema “número, caso real, demo” y comentó que **5 minutos les pareció demasiado**: creen tener **3 minutos**, como la última vez.

## Cómo impacta en Contraprueba y en las opciones A y B

- El mentor **avala Contraprueba como el camino**. No pide cambiar de idea; pide demo, encuadre y comunicación.
- **Opción A (villano real medido)** queda **fuertemente respaldada**: casos reales, una vulnerabilidad histórica reproducida, pedir PRs nocivas al jurado o a la hackatón, métricas del tipo “100 malas, agarramos el 80%”, y no vender solo un ejemplo sintético. Encaja con el “demo maxing” de acá a la noche.
- **Opción B (atribución causal / más core técnico, SLM local, más features de detección)** queda **desaconsejada para esta hackatón**. El mentor fue explícito: si no cambia la demo, no aporta; no sumar líneas de core que exijan más demos; el producto ya es difícil de explicar. Se puede retomar después. Lo *nice to have* (dashboard, correr fuera de un PR) sí puede explorarse si no come tiempo de la demo.
- **Cerrojo** y **Brecha ES-CL** no se discuten con claridad en esta grabación. Hay un tramo muy ruidoso (~1:15–1:20) en el que el ASR dice algo como “cancelamos el [sórro?]” después de hablar de saturación en los Platanus de este año; la palabra no es confiable (probabilidad baja) y no se toma como decisión confirmada.

## Próximos pasos (los que quedaron acordados)

- De acá a la tarde-noche, dividir el trabajo en: **1) demo maxing** (MVP sólido, casos reales, posiblemente un form o PRs pedidas al jurado / a gente de la hackatón, más un repo chico que corra en vivo) y **2) ser muy críticos** con cualquier feature extra o capa de producto 360.
- Intentar el caso histórico (blog + commit + estado anterior del repo) si hay hipótesis de detección.
- Branding mínimo: nombre de producto + metáfora.
- Encuadre: cadena de incidente de ciberseguridad + métricas, no “mejor calidad de software”.
- **Reunión con el mentor esta noche, ~19:00–20:00 (hora de Chile),** sobre demo y presentación.
- Confirmar con la organización la duración del pitch (el equipo maneja 3 minutos; en la charla se habló también de 5).

## Notas sobre la transcripción

Calidad **aceptable, no literal**. Idioma detectado: español (p=1.0). Primera pasada continua se rompió ~12:50 con alucinaciones (puntos repetidos); se rehizo por tramos de 90 s y se rellenaron huecos. El final es más ruidoso (despidos, conversación informal). Se aplicaron correcciones probables:

| ASR | Corrección (probable) |
|---|---|
| jacatón | hackatón |
| codex / Covex / cobwebs grandes o pequeñas | codebases grandes o pequeñas |
| Cloud / CloudCloud / cloud codex | Claude Code o Codex |
| revisión de perros | revisión de PRs |
| sears / Ciud seguridad | ciberseguridad |
| hacking phase | Hugging Face (incierto) |
| presentaion / unachotada / cotado | presentación / de una sentada / acotado |
| plátanos de este año | (proyectos de) Platanus de este año |
| envidia de la solución | esbozo / embrión de la solución (incierto) |
| el producto se llama Tanto | ejemplo de branding del mentor, no un nombre confirmado |
| grupo de Barcelona / Varsel / barcel | nombre del blanco no confirmado |
| sórro / cancelamos el sórro | no confiable; no se interpreta como decisión |

Pueden quedar otros errores. No se versionó el audio (el `.m4a` pesa ~18 MB y el repo no guarda audios). No aparecieron tokens, API keys ni contraseñas.

## Transcripción completa (ASR, hablantes heurísticos)

Los tiempos son minutos:segundos desde el inicio de la grabación. Los corchetes marcan tramos inciertos o inaudibles.

**[00:00–00:36] Mentor.** Y que ya eso da algo de confianza, porque significa que están muy bien encaminados. Yo como que he escuchado un par de grupos por encima, y hay algunos que recién ahora están definiendo el problema y están evaluando si cambiarse de track ahora o cambiar la solución completa. Así que están bien encaminados, y creo que tienen espacio para ser súper ambiciosos, que es algo muy bueno. Eso, por un lado. Y, dos: creo que tienen bien definido como su *statement* de demo. Creo que pueden armar hoy una demo muy básica y como sacar la lista; yo creo que podrían presentar en una hora más, más o menos. Y dado que tienen eso, quiero hacer un par de preguntas para ver qué tan lejos lo pueden llevar de una forma como segura.

**[00:36–01:03] Mentor.** Uno es: ¿hay investigación de esto? Se me dieron a ver, como investigación de organizaciones, labs, lo que sea.

**Equipo.** Hay cuatro que están a favor de esto, que se los [dieron / midieron]. Hay uno que está en contra.

**Mentor.** ¿Quiénes son?

**Equipo.** Acá no terminé… no me puse a leer bien los papers, pero son *researchers* independientes, no es como una organización. Parece que son *researchers* independientes. Son como papers, más bien. [¿Monja de la Universidad? — inaudible].

**[01:03–01:26] Equipo.** Creo que nos pasó que habíamos [usado / encontrado] otra versión, que había salido, y lo habíamos [colgado / colado] a la noche. Pero en realidad después le empezamos a comparar con los Platanus de este año. Estaban muy saturadas las opciones. [Tramo ruidoso, ~01:15–01:20: el ASR oye algo como “cancelamos el sórro”, no confiable.] Y esta sí está: no hay nadie haciendo esto.

**Mentor.** Eso les iba a preguntar: ¿no hay nadie en el mercado que tenga alguna solución parecida?

**[01:26–01:41] Equipo.** No tan técnico. Sí hay cosas como mucho mejores o mejor terminadas desde el lado [producto], pero siento que nosotros le podemos dar un lado técnico, más como desde un *approach* científico. Está muy poco explorado. Más [completo / competido — incierto].

**[01:41–02:24] Mentor.** ¿Quién es su usuario final?

**Equipo.** Nuestro usuario final serían developers, engineers que mantengan codebases grandes, pero no codebases pequeñas o que sean proyectos de un fin de semana. La empresa lo compra y se lo pide a todos [sus devs]. [Tramo breve poco claro.] Quisiera que usen Claude Code o Codex o cualquiera de estas [herramientas].

**Mentor.** O sea, al final su cliente es… no me importa demasiado la parte comercial, pero [quiero] entender para quién es la propuesta de valor. Su cliente es la empresa o la persona que ocupa el modelo del AI lab. No es el AI lab directamente. ¿No van a salir a decirle a…?

**Equipo.** No, no.

**Mentor.** Ya. Ok, clarísimo.

**[02:24–03:40] Mentor.** Y si fueran a correr una demo ahora en vivo, un MVP: ¿logran mostrarlo en tiempo real en una presentación? Si les dieran cinco minutos para presentar, ¿logran correr un test entero que corra en vivo y que no sea una grabación o una simulación?

**Equipo.** Creo que sí, pero no confiaríamos tanto. En las pruebas que estábamos haciendo ahorita, dependiendo, en cinco minutos tardaba unos dos minutos. Pero bueno, hicimos como un ejemplo; hasta el momento no lo hemos probado en un repo real, con algún [laboratorio / repo de verdad]. Sí, [la] propuesta era agarrar algunos repos y tener un dashboard de resultados, y poder mostrar eso, ponerlo a correr mientras lo mostramos. Si da el tiempo de que termine, oye, y si no, bueno, vamos a tener por lo menos lo que corrimos hoy para mañana. Habíamos pensado que si encontramos algo, [hacer] algún recorte a alguno de los códigos open source que [ayudemos / auditamos], y poder mencionar mañana que reportamos.

**[03:40–05:10] Mentor.** Ok. De lo que veo, para mí su siguiente paso ideal es: ya tienen definido el problema, tienen definida una solución, al menos un [esbozo] de la solución. Creo que el siguiente paso, para poder llegar a la sesión de la noche —en la noche hablar de la demo en particular y el *storyline* de la demo, cómo presentarlo, cómo comunicar su valor— es pensar y dedicarle tiempo ahora a cómo podemos hacer el demo más impresionante y más wow, en el tiempo acotado que vamos a tener. Porque yo creo que, si fueran a correr un repo más grande, con más [PRs / licencias], es muy probable que si lo parten durante la presentación no termine, y queden un poquito en blanco, como “esperen, tenemos que esperar a que termine la evaluación”. Entonces tienen que buscar la forma de… no sé si se puede hacer más rápido, y si eso sacrificaría algo. No sé si de repente es bueno una simulación con datos de cosas que ya corrimos, que sean reales. No sé si de repente pueden contactar al jurado o a gente en la hackatón y pedirles que les tiren PRs malas o PRs como nocivas, y que eso lo incluyan en el demo, para que puedan decir: “nos tiraron 100 malas y agarramos el 80% de ellas”, no sé. Si el [jurado] no está [viendo] directamente, por más que no lo vea funcionando en vivo, ve que hubo una demo [de verdad].

**[05:10–06:10] Mentor.** Lo pienso porque estaba hablando recién con una solución que sí logra correr de principio a fin, 100%, de una sentada, pero es como una solución más chica y más simple. Creo que su solución es más compleja y, por tanto, no correría el riesgo, sinceramente, de correrlo [todo] en vivo. Así que cranearía ahora esa demo más ambiciosa, una que puedan hacer que funcione y de la que confíen que va a ser buena. Pueden tener ya una demo ambiciosa, pero para en vivo tener algo, no sé, un repo pequeño con unos PRs pequeños que sí sean capaces de correr rápidamente, no sé, a un minuto más. Puede ser. Tampoco trataría de bombardear con demostraciones; me casaría con un par.

**[06:10–07:18] Mentor.** Creo que hay tres [formas] por las que pueden demostrar el valor de lo suyo. La primera es con investigación. La investigación yo creo que es el primer paso, porque sugiere que ya hay algo de camino hecho, recorrido, empírico. El segundo es una cadena más especulativa: decir, si es que no se implementa nuestra solución, entonces en un futuro en el cual más PRs son lanzadas y aprobadas por inteligencia artificial al 100%, puede llegar a incidentes de ciberseguridad, puede llegar a más [incidentes tipo Hugging Face?], puede llegar a ABCD escenarios, de una forma más especulativa, para que entiendan la importancia de tener un sistema como [este]. Y el tercero es ya mostrarlo en vivo, que es la demo. Creo que eso es, secuencialmente, como lo haría yo: primero investigación —no andaría mucho en investigación—; segundo, los incidentes de una forma más especulativa; y después llevarlo a lo práctico y algo que puedan ver. Y creo que esa demo es donde más trabajo tenemos que meter ahora. Pueden tratar de afinar un poco mejor el MVP, pero si es que funciona, trataría de buscar una demo ambiciosa.

**[07:18–08:16] Mentor.** Yo creo que el efecto wow es cuando logran visualizar, con la especulación, qué es lo malo que puede pasar o qué es lo malo que ya ha estado pasando en ciberseguridad, y dónde su solución entra a cortar esta cadena. Si ustedes logran, como visualmente, mostrar la cadena que lleva a que una PR mal hecha o nociva se apruebe, y eso lleva a un incidente, lleva a un [changelog / chat log?] público que puede hacer que la gente se [coordine / exponga] en [ese] separado, y que esto tiene un efecto real y preocupante, entonces creo que así logran conectar el valor.

**[08:16–09:42] Equipo.** Hay una duda que me [queda], y es que si lo direccionamos hacia test de vulnerabilidades de ciberseguridad… porque esto también se puede llevar como para revisión de PRs que no te [las] tire en producción, por ejemplo. O sea, no te está atacando a tus datos o a tus datos accesibles, pero sí te está dañando [la calidad / con bugs — tramo poco claro].

**Mentor.** Desde un punto de vista de producto, creo que no me enfocaría en la parte de producto, porque no tiene que ver con *safety* o seguridad. Yo creo que para mí el factor wow acá no es “esto va a hacer que el producto sea mejor” o “va a evitar que un *feature* se me rompa en producción”, sino que… yo creo que el [nicho] ciberseguridad tiene un buen nicho. Para mí, los incidentes de ciberseguridad están *on the rise* y están haciendo temas, y creo que su solución justamente abarca esto. Creo que [el wow] es que logren comunicar de forma preocupante los incidentes de ciberseguridad que hay y cómo su solución interviene en esto, y después logran demostrar que su solución es efectiva, con métricas. Eso es como el factor [wow]. Creo que su solución está en el lado más complejo de [comunicar]. Creo que el grupo con el que estaba hablando recientemente tiene una solución más simple de comunicar. Creo que los suyos van a tener que hacer un esfuerzo.

**Equipo.** Sí, eso es muy difícil, nos estaba costando ahorita, cuando llegaste, y te lo dijimos ahorita: te hablamos porque sí está difícil de articular y volverlo fácil. De explicar la propuesta de valor. O sea, sentimos que técnicamente es sólido.

**[09:42–11:16] Equipo.** Podríamos agregar alguna cosita más como para hacerlo más *flashy* o algo diferente. Tenemos varias opciones de cómo llevarlo para cierto lado: si queremos ser más técnico o más fácil de usar para un agente tipo Claude, o si queremos usar estos SLMs y poder correrlo en el local, por ejemplo. ¿Para vos eso aporta, o tenemos que hacerlo un poco más producto y olvidarnos un poco de esa parte?

**Mentor.** Buena pregunta. ¿Les cambiaría la demo?

**Equipo.** No tanto. [Tramo breve poco claro.]

**Mentor.** Ok, entonces creo que no. Creo que no aporta demasiado. Creo que aporta más tener una muy buena demo. Aporta igual tener un branding mínimo. Creo que es bueno, en vez de decir “nosotros creamos un repo o un mecanismo o no sé qué”, [decir] “nosotros creamos un producto, el producto se llama [Tanto / X] y funciona de esta forma”. Y también creo que sirven mucho las metáforas. Creo que si cuentan la historia no con solamente código, sino que primero parten con la metáfora, casi como ni siquiera pensando en [código]: “vamos a ponerle un nombre”, ¿cachai? [Intercambios cortos: “¿Cuánto?”, “cachai”, “funciona, funciona”.] Yo creo que es una [sátira?] bonita, una buena [sátira / metáfora]. Entonces creo que no me enfocaría mucho en *features* adicionales, porque ya tienen un producto complejo, y comunicar más *features* aparte de eso ya lo complica mucho. Creo que invertiría tiempo en la demo, en asegurar que su MVP corre bien, que creo que está bastante sólido, y después en la noche podemos conversar sobre cómo armar la demo, cómo comunicar el problema, cuáles son las palancas de valor que tienen.

**[11:16–12:54] Equipo.** Siento que esto quedó como muy sólido en el core, pero es el core, sí. Oye, ¿a vos te causaría impacto ver, por ejemplo, que encontramos una vulnerabilidad en el grupo de [Barcelona / Varsel — incierta], o sea, que suma más a la demo, o eso?

**Mentor / Equipo.** Sí. Claro, yo lo que pensaba era hacer como ataques reales, aprovechar el tiempo en eso, y encontramos [eso].

**Mentor.** Claro, capaz dividiría como el trabajo de aquí a la noche, o la tarde-noche, en dos. Uno es como *demo maxing*, por decirlo así: lograr una demo muy buena, quizás con casos reales, quizás mandar de nuevo como un form al jurado o pedirle PRs a gente de acá para que tengan data súper concreta que muestren después en la demo. Y después el segundo *track* —y creo que es un buen *pushback*— es como: ¿qué otros *features* le podemos meter? Creo que en los *features* es importante que prioricen calidad sobre cantidad, para que no tengan como puros flop de *features*, y creo que tienen que enfocarse en *features* que sean fáciles de comunicar, porque su solución, una vez que logran explicar el core, perfecto. Después de eso, si es que logran tener [la atención de] al jurado, necesitan asegurarse de que sobre eso puedan agregar más capas y volver después a explicar cada capa al core, y que esto se entienda como un producto 360. Entonces, sería súper crítico en ver cuáles son los *features* adicionales que quieren. Estoy de acuerdo con que existe la posibilidad.

**[12:54–14:48]** [Tramo más enmarañado, ~14:18–14:32, sobre una interacción o visualización en tiempo real y el evaluador; el ASR no se deja leer con seguridad.]

**Equipo.** Vamos con lo que tenemos, podemos [conformarnos / informarlo], de maravilla, hasta ahí. Yo he pensado [en detectarla] como hace unos meses: [un agente] presentó una vulnerabilidad en un PR, y simulamos el estado anterior del repo [público], la PR, corremos [la herramienta] sobre [esa] PR y decimos: bueno, esto se podría detectar.

**Mentor.** ¿Eso ya lo hicieron?

**Equipo.** No, no, no.

**Mentor.** ¿Y tienen una buena hipótesis de que lo podrían detectar?

**Equipo.** [Sí], la hipótesis es leer el blog, ir al momento justo, agarrar el commit, y bueno.

**Mentor.** Eso me parece una buena idea. Creo que cae bien en una demo, me gusta harto.

**[14:48–16:48] Mentor.** Ahora, creo que, pensando en *features*, hay dos tipos de *features* que podrían agregar. Uno es como sumar más líneas al core. Ustedes hoy tienen un mecanismo que detecta o que evalúa PRs. Ustedes podrían sumar más *features* core, digamos, como distintas líneas de negocio, por decirlo así. Creo que no me iría por ese lado, porque van a tener que ir a buscar demos para esas *features* también. Y tienen *features* un poco menos [de core], más higiénicas y más estéticas casi, o como *nice to have*: tener un dashboard que visualice con checks, no sé qué, con cruces, o poder correrlo en cualquier momento sin que sea un PR. Que son como cosas no core: no te generan un producto o una nueva forma de mostrar valor, pero sí hacen que se vea como un producto más consolidado o más bonito. Y creo que, dado que están en un buen lugar y tienen la capacidad, vale la pena explorar esa [vía]. *Demo maxing*: yo creo que de aquí a la noche tengan como casos muy [concretos / buenos]. [Si] tienen otros casos de ese estilo, súper bien. Creo que logran comunicar bien el valor, está bien *frameado* y le tengo harta fe. Creo que es una solución prometedora. Eso, ¿dudas?

**[16:48–17:16]** [Cierre informal: “qué cracks”, un objeto que imprimieron en 3D, “ahora son edición limitada, van saliendo muy a poco, se venden caro”. Saludos.]

**[17:16–18:30] Equipo / Mentor.** [Sigue la charla informal; se oye algo como “capaz podría ser tipo las letras”.] Si le pasan eso al jurado al principio, la rompe. Yo me ocupo del [texto / *demo maxing*] ahora. Cualquier pregunta, dudas, preocupaciones. Yo creo que ya van encaminados, tienen prioridades claras. Hablamos a la noche, tipo 7, 8; voy a estar acá de nuevo, y hablamos de la demo, la presentación. Tengo varias opiniones de cómo armar una presentación clara y buena. [“Todo con Claude”, y se ofrecen a mandar por WhatsApp lo que se les ocurra.] Dale, sí.

**[18:30–18:50] Equipo.** [Ya más entre ellos.] Número. Caso real. Demo. ¿Saben cuánto tiempo tienen para esta? Yo te había preguntado porque cinco minutos me pareció una banda. Me parece que tenemos 3. Creo que tuvimos 3. 3 tuvimos la última vez.
