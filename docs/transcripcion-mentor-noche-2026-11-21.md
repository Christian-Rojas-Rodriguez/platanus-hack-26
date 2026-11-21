# Feedback de un mentor (reunión de la noche)

- **Fecha:** 21 de noviembre de 2026, grabación creada a las 19:18 (hora de Chile, UTC−3). El archivo de origen tiene `creation_time` `2026-11-21T22:18:01Z`.
- **Evento:** Platanus Hack 26, track AI Safety.
- **Fuente:** nota de voz de ~4 min 38 s (278,5 s). La grabación **empieza a mitad de conversación** (no se oye el arranque ni una presentación). Transcripción ASR (faster-whisper `medium`, CPU int8, en dos tramos de ~2,5 min con solapamiento, más una pasada de control). Los hablantes se separaron de forma heurística (Mentor / Equipo); no se asignaron nombres propios porque no se oyen con claridad. Puede tener errores, sobre todo en nombres propios, términos en inglés y tramos con crosstalk.
- **No es un duplicado** de la reunión de producto del mediodía (`docs/transcripcion-mentor-producto-2026-11-21.md`, ~18 min 50 s) ni de la 2.ª reunión con el mentor de la tarde (`/workspace/audio/transcript-2026-11-21.txt`, ~22 min 34 s). Duración, hash y tema son distintos. Coincide en *tema* (no en audio) con parte del feedback del 20/11: el equipo vuelve a plantear la idea de un «Hugging Face para AI Safety».

## Quiénes hablan

- **Mentor:** da feedback sobre ideas de research y de producto, cita listas de *open problems*, cuenta que **ganaron con un firewall en Buenos Aires** y comenta cómo cree que va a valorar el jurado. No se pudo confirmar un nombre a partir del audio. No es seguro que sea el mismo mentor de la reunión de producto del mediodía (esta grabación no habla de Cachai, de la demo ni del pitch).
- **Equipo:** al menos una persona del equipo (el planteo del «Hugging Face para AI Safety» encaja con una idea que Christian ya había llevado el 20/11). Preguntan qué se valora más (contribución de research vs. producto vendible) y plantean un producto de alineación para LLMs autoalojados. No se etiquetan con nombres (Jaime, Mauricio, Smoke u otros) porque el ASR no los deja oír con seguridad.

## Decisiones y pedidos

- El equipo retoma la idea de una **plataforma tipo Hugging Face para AI Safety**: papers poco reproducibles, artefactos + repos + código para que alguien pueda levantar desde su casa un experimento visto en un blog, impulsada por la comunidad y por grupos que se dedican a reproducir papers. El mentor responde: **«Puede ser, no me convence del todo»**. Encaja con el veredicto del 20/11 (buen backup, impacto positivo pero no demasiado grande).
- Sobre **interpretación automatizada a escala (autointerp)**, el mentor marca que hay que **encontrar cómo diferenciarse** y que es un área de problemas difícil.
- Lo que más le interesa del track está en **AI Control**: asumir que el modelo [está desalineado y] te va a hacer daño, y asegurar seguridad con monitoreo, intervención, *tripwires* y *honeypots*. Dice que esa variedad está llena de cosas interesantes.
- Al mismo tiempo, **honeypots y firewalls están saturados**: «en muchos equipos son honeypots y firewalls». El mentor (o su equipo) **ganó con un firewall en Buenos Aires**, y ahí también había múltiples equipos con firewalls. No queda claro un comentario posterior sobre «el mejor firewall» y un «servidor» (ASR inseguro).
- Les sugiere, si quieren **[pivotear?]**, **echarle ~20 minutos a revisar listas de *Open Problems***: cita papers/artículos del tipo *Open Problems in…*, en concreto *Open Problems in Mechanistic Interpretability* y *Open Problems in AI Control*. Los describe como posts/papers gigantes, con cientos de áreas de problemas que le gustaría que alguien solucionara. Dice que es **muy útil**.
- Pregunta del equipo: en AI Safety, **¿se valora más una contribución a la investigación o un producto que se pueda vender?** Respuesta del mentor:
  - **Depende del juez.** Lo que más importa es **si sirve o no sirve**, más que si está empaquetado como buen o mal producto.
  - En su caso (Buenos Aires), **terminaron vendiendo un producto**, más que algo muy de research y avanzado. Aun así, **puede ser cualquiera de los dos**.
  - **No descartaría un proyecto solo porque es de research.**
  - **Un buen demo de un resultado experimental puede ser el ganador del track.**
  - **Ganar la hackathon completa es mucho más difícil:** el track de safety te puede valorar eso; el premio general es otra cosa. Sobre quién juzga o cómo se decide eso, dice **«esto es secret, no se sabe»**.
- El equipo pregunta si vale un **producto que alinee LLMs autoalojados / self-hosted**, porque cada vez más empresas montan o alquilan servidores para bajar costo. El mentor: hay un mercado gigante, **pero ya existe** — mercado de **prompt guards**, herramientas anti-jailbreaking para cuando se exponen LLMs al público. **No lo ve novedoso.**
- Cierre del equipo: **«vamos por [el lado] de la investigación»**, y agradecen. Eso cierra sobre todo el descarte del producto de prompt guards / LLMs autoalojados. **Esta grabación no nombra a Cachai (ex Contraprueba), ni PRs, ni held-out, ni la demo de la noche.** No se puede tomar, solo con este recorte, como un abandono formal de Cachai.

## Cómo impacta el plan del benchmark y el producto

- **No contradice** el consejo de la 2.ª reunión de la tarde (achicar a 1–2 problemas, priorizar detección, evidencia empírica frente a Claude Review): un **demo de un resultado experimental** es, para este mentor, una vía explícita para ganar el **track**. El benchmark de Cachai (Opus vs. Opus+Cachai, con PRs vulnerables reales) sigue siendo compatible con esa lectura, si el equipo se queda en Cachai.
- **Riesgo de pivot:** la invitación a mirar 20 minutos las listas de *Open Problems* (sobre todo AI Control, evitando honeypots/firewalls) es una puerta a cambiar de idea **el sábado a la noche**. Con el tiempo que queda del hack, un pivot real competiría de frente con congelar dataset y correr el benchmark.
- **Descartado en esta charla:** producto de alineación / prompt guards para LLMs self-hosted (mercado ya existente, poco novedoso); honeypots y firewalls genéricos (carril saturado, coherente con el brief del track). La plataforma «Hugging Face para evals» sigue sin convencer del todo al mentor; no aparece como idea principal.
- **«Vamos por la investigación»** no alcanza, por sí solo, para frenar el benchmark: en el audio aparece justo después de descartar el producto de LLMs autoalojados, no después de una discusión de Cachai. Conviene confirmar con el equipo si siguen en Cachai + evidencia empírica, o si de verdad quieren moverse a un *open problem* de control.

## Notas sobre la transcripción

Calidad **aceptable, no literal**. Idioma detectado: español (p=1.0). El archivo dura menos de 5 minutos, así que no se repitió el colapso en puntos del mediodía (~min 12:50). Sí hubo alucinación tipo outro de YouTube en una pasada de control (tramo ~01:24–01:30); se descartó esa pasada y se conservó el texto estable de las otras. Se aplicaron correcciones probables:

| ASR | Corrección (probable) |
|---|---|
| auto inter / auto-inter | autointerp (interpretación automatizada) |
| High-In-Face / high-end base / having face | Hugging Face |
| wall trucks / WorldTrucks | artifacts o workflows (incierto) |
| repost | repo |
| Time-Prize / timefriending / time frame | tripwires (incierto, pero encaja con el marco de AI Control) |
| HoneyBot / honeybots | honeypots |
| Open Problems Den / Open Problems y Mechanics / Mechanics en Preparado de AI | *Open Problems in Mechanistic Interpretability* |
| Open Problems en Area de Control / Neural Control | *Open Problems in AI Control* |
| pirotear | pivotear (incierto) |
| pos gigantes / pose gigantes | posts (o papers) gigantes |
| en ella dices / area safety | en AI Safety |
| SelfieBloid / LMS Auto Selfie | LLMs autoalojados / self-hosted |
| prompt cards / Promp cards | prompt guards |
| heartbreaking / death breaking / gap breaking | jailbreaking |
| tu mujer está en ese laberinto y no te va a usar daño | tu modelo está [desalineado?] y te va a hacer daño (muy inseguro; «mujer» tenía p≈0,04) |
| macón | montón (incierto) |
| Cachai / Contraprueba, Claude, held-out, fuzzing, harness | **no aparecen** en esta grabación |

El audio original (m4a) **no se sube** al repo.

## Transcripción

**Mentor:** Lo que me iría a preguntar es si está en la [orana/arena?; inaudible], hacer zoom y ver como… Todo eso ha estado como en autointerp, como interpretación automatizada a escala. Eso es, puta, eh, que hay que encontrar cómo diferenciarse, eh. Pero hay que [meterse en / interpretar] un área de problemas muy difícil de trabajar.

**Equipo:** Ok. Yo un problema también que había visto en AI Safety y en research es que, por ejemplo, hay como algunas cosas que se publican, o eso, que no son de todos reproducibles, porque la gente no es que como que te deja el repo y te dice: «Mirá, hice esto y esto y esto».

**Mentor:** Sí, pasa todo el rato.

**Equipo:** Sí. Por ejemplo, como si fuese un Hugging Face para AI Safety, más focuseado en eso, donde se puedan subir [artifacts/workflows?; ASR: «wall trucks»] con repositorios, con códigos, más los sources a los que se indican, que se puedan reproducir, y que vos, desde tu casita, puedas levantar un experimento de los que viste en el blog o [que se] subió… Como la idea es que la plataforma te permite tomar un paper, que la plataforma ya tenga cargado el código. Obviamente sería impulsado por la comunidad, porque es un laburo enorme, pero… Hay [gente que] se especializa en el sector, no es que sea más [«second-look research»; inseguro], pero un grupo que se dedica solamente a reproducir papers de ese tipo. Son la gente. Claro, sería potenciado por organismos así.

**Mentor:** Puede ser, no me convence del todo.

*[Tramo informal, alguien bosteza.]*

**Mentor?:** ¿Qué, [primo?], vas a bostezar acá de sueño?

**Equipo?:** Ya vengo a hablar por horas.

**Mentor:** Creo que quizás las cosas más entretenidas están en [AI] Control, que es como: asume que tu [modelo?; ASR inseguro: «mujer»] está [desalineado? / ASR: «en ese laberinto»] y te va a hacer daño. ¿Cómo te aseguras de que, [con] monitoreo, intervención, [tripwires?] o honeypots, como que toda esa variedad está muy llena de cosas interesantes?

**Equipo:** Bueno, honeypots lo habíamos visto como…

**Equipo?:** [inaudible; el ASR oscila entre «o sea, honeypots, parece que vas [por] el mismo [camino]» y otras lecturas].

**Mentor:** No, las dos [ramas/trampas] que en verdad hay, en muchos equipos, son honeypots y firewalls, que por alguna razón han sido… Nosotros ganamos con un firewall en Buenos Aires. En Buenos Aires también había múltiples equipos con firewalls, si no [me equivoco], perdón. [Hagan? / Ya ven?] el mejor firewall. [Hagan?] el mejor, porque no ha llegado a este [servidor?; inseguro].

Hay una… Si ustedes [buscan / en esa lista], hay una serie de papers y artículos que se llaman *Open Problems in…*, como *Open Problems in Mechanistic Interpretability*, *Open Problems in AI Control*, que básicamente es duro: son posts gigantes, cientos de áreas de problemas que me gustaría que alguien solucionara. Y es una opción muy… bueno, si quieren [pivotear?], quizás échenle veinte minutos a revisar estas listas y ver si hay algo que les llama la atención. Pero es muy útil.

**Equipo:** Ok. Y pregunta: en AI Safety, ¿qué se valora más, capaz, una ayuda, una contribución a esa investigación, o un producto que pueda venderse?

**Mentor:** Todo va a depender del juez, pero yo creo que lo más probable es que este juez va a valorar [el resultado / ambas; frase incompleta]. Y lo que más importa es si sirve o no sirve, más que si es un buen producto o un mal producto. A nosotros nos pasó que, finalmente, terminamos vendiendo un producto, más que algo muy de research y algo tan avanzado. Yo creo que puede ser cualquiera de los dos. Definitivamente no descartaría un proyecto solo porque es como [de] research. Yo creo que un buen demo de un resultado experimental puede ser el ganador del track.

**Equipo:** Ok. ¿Y el ganador de la hackathon?

**Mentor:** Sí, es mucho más difícil. El problema es que, claro, puedes tener el track de safety que te va a valorar mucho eso, pero [para el premio general]…

**Equipo?:** Ah, pensé que ibas a estar vos. / [otra lectura: «pensé que ibas a aceptar vos»]

**Mentor?:** Esto es secret, no se sabe.

**Equipo:** Ok. Ok, bueno, es una buena… Sé que es un [montón?], pero bueno, vamos a tener que hacer algo. Pero dale, si todavía queda…

**Mentor?:** Pregunta, pregunta.

**Equipo:** ¿Qué tan viable es un producto que… porque hoy en día, yo lo que pensaba, hoy en día cada vez más empresas se animan a montar sus propios servidores o alquilar servidores y montar sus LLMs para reducir el costo. ¿Hay un gran valor en hacer un producto que alinee eso…?

**Mentor:** ¿Alinee qué? ¿LLMs auto[alojados], como self-hosted?

**Equipo:** Sí. ¿Como producto? ¿Hay algún producto que lo haga, que sea muy famoso?

**Mentor:** Hay un mercado gigante de esto, ¿no? Pero ya existe, hay todo un mercado de prompt guards, que son como distintos tipos de herramientas anti-jailbreaking, para cuando tú [exponés / desplegás] LLMs al público. No sé qué tan novedoso [sea] hacer [eso].

**Equipo:** Ok. Bueno, vamos por [el lado] de la investigación. Bueno, gracias.
