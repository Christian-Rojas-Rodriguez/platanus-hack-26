# Feedback del mentor

- **Fecha:** 20 de noviembre de 2026, ~23:40 (hora de Chile)
- **Evento:** Platanus Hack 26, track AI Safety
- **Fuente:** nota de voz de la reunión con el mentor (~15 min). La transcripción es ASR (faster-whisper), sin separar hablantes, y puede tener errores.

## Consejos del mentor

- Buscar problemas que todavía nadie resolvió bien: gaps *blue ocean* o temas cubiertos apenas al 20%. Si algo ya está resuelto al 80%, ir a completar el 20% restante aporta poco y es aburrido para el jurado.
- Ubicar cada idea en dos ejes y armar casi un gráfico: **impacto / factor wow** versus **factibilidad** de armar el producto en **10 a 12 horas** (de las ~36 horas de la hackatón, el resto se va en demo, research y, ojalá, dormir).
- Todo lo que no entre en esas 10 a 12 horas se descarta para esta competencia; se puede retomar después, en tiempo libre.
- Priorizar el *golden zone*: fácil de implementar (y de testear) y con alto impacto. Las ideas de alto impacto pero más difíciles son valiosas, aunque más riesgosas con el tiempo que hay. Lo que no llega al umbral de wow de los jueces, aunque sea fácil, no vale mucho la pena.
- Quedarse con **una idea principal** (la de mayor impacto) y **una de backup** fácil de hacer, que igual genere algo de tracción.

### Cómo armar la demo

La demo se explica en dos o tres frases:

1. **Problema:** hoy existe X problema.
2. **Daño cuantificado:** si se puede, un número concreto (por ejemplo, 600 incidentes al día, que mañana podrían ser 1.200). Ese número es el riesgo que se quiere atacar.
3. **Solución:** el producto que proponen.
4. **Impacto en vivo:** mostrar en la demo cómo baja ese número (a 300, a cero, etc.).
5. **Usuario** (secundario en esta hackatón, pero suma): quién adoptaría la solución y cuál es el *pathway to value* (por ejemplo, un gobierno que reduce el riesgo de perder datos o de un ataque ejecutado por agentes).

El track de AI Safety es de los más difíciles para impresionar: para mucha gente estas cosas son muy *black box*, a diferencia de un hardware que se mueve. Por eso la demo tiene que mostrar en vivo un **failure mode**, por ejemplo un prompt injection u otro caso negativo, con el ambiente ya seteado.

## Feedback sobre las ideas

- **Revisar código y prompts con un SLM en un sandbox.** Le gustó y la ve lograble. Pidió confirmar que sea algo nuevo (que alguien que revise el repo no diga “esto ya existe”, porque eso le quita valor contrafactual), cuantificar el enemigo y el daño si no se implementa, y el *lift* que aporta la solución. Preguntó si un agente malicioso podría infiltrarse en el SLM (“ignora tus reglas”) y si da el tiempo para armar el sandbox y la infraestructura del producto además de la demo.
- **Incidente de exfiltración de un modelo Qwen (datos enviados a un servidor en China) y *constrained decoding* / restricciones sobre lo que el modelo puede generar, en la línea de lo que hacen en Nomenclator.** Dijo que el valor se comunica de forma más tangible que en la idea anterior y que a priori lo ve posible en 10 a 12 horas, aunque la factibilidad la puede evaluar mejor el equipo. Le falta saber si la solución es nueva o el mercado ya la tiene, y cuánto riesgo enfrentan las empresas en plata o en incidentes. Insistió en pensar la demo desde ahora.
- **Agente con acceso total (base de datos, nube, AWS, servidores) pero sin acciones peligrosas, sin intervención humana.** No se metería. Escucha muchas ideas ligadas a *control* / *oversight* y sugirió mirar también otras áreas del track. El impacto es difícil de comunicar en una demo; aunque el tema sea interesante, en el tiempo acotado y con el cómputo que hay es muy difícil demostrar un *lift* grande.
- **“Hugging Face para evals de AI Safety”:** una librería o interfaz para reproducir experimentos con un modelo o una API, con la opción de correrlos en servidores, presupuesto determinístico, y aportes de la comunidad (experimentos, datasets). Pensada para empresas grandes y para académicos. El mentor la ve poco difícil, con impacto positivo pero no demasiado grande: es un **buen backup**; cree que pueden llegar a algo más robusto como idea principal.
- **Idea del mentor: scraper de técnicas nuevas de prompt injection o jailbreak.** Exhaustivo (Reddit y sitios de nicho), las prueba contra un agente en un ambiente controlado, otro agente evalúa si el jailbreak funcionó, y a partir de eso sale una recomendación para un AI lab. No sabe si ya existe.
- **AI kitchen con interpretabilidad mecanicista** (hacer *mechanistic interpretability* sobre neuronas para personalizar un modelo local). El mentor preguntó por qué eso es de safety. Ahí se corta la grabación.

## Próximos pasos

- **Mañana a la mañana:** reunión para desbloquear y hablar de producto / solución.
- **Mañana a la tarde:** reunión enfocada en la demo.
- El mentor no se iba a quedar toda la noche; al día siguiente se levantaba temprano y iba a estar conectado. Dijo que avisaría el horario con anticipación para juntarse en ambas instancias.

## Notas sobre la transcripción

Texto corrido generado por ASR, **sin separar hablantes**. Se aplicaron correcciones probables de reconocimiento:

| ASR | Corrección |
|---|---|
| jacatona / jacatones | hackatón / hackatones |
| golden song | golden zone |
| Queen | Qwen |
| open router | OpenRouter |
| AI SIFTY | AI Safety |
| having face | Hugging Face |
| sml / slm | SLM |
| Alime | alignment |
| a WS | AWS |
| mecanistic interpretation | mechanistic interpretability |

Pueden quedar otros errores. Se omitió una oferta de contacto personal.

## Transcripción completa (ASR, sin separar hablantes)

Primer factor, creo que un problema que ya está resuelto o que está casi satisfactoriamente resuelto no agrega valor si lo resuelven ustedes también. Yo iría a buscar gaps que son blue ocean, que nadie los ha tocado o algún gap que no está satisfactoriamente llenado, o sea que está al 20%? Y en verdad ese 80% restante es significativo porque es grande, vale la pena, pero si algo está al 80% y ustedes van a ir a cubrir 20% es muy aburrido. Eso, elijan problemas nuevos. 

Primer factor, después que tengan eso, para cada proyecto van a poner a evaluar dos dimensiones y armar casi que un gráfico. Uno es el factor wow, qué tanto impacto o qué tan impresionante es su idea, y dos qué tan difícil o qué tan factible es hacerlo en 36 horas. Y digo 36 horas porque en verdad tienen más o menos 10 o 12 para armar el producto porque tienen que hacer la demo, tienen que hacer research, ojalá que duerman algo debatible. Y en base a eso, arman un mapa, esto es lo que hago yo. Dificultad, impacto. Más dificultad, más fácil, más impacto, más aburrido. 

Todo lo que no se puede hacer en 10 a 12 horas se ignora, eso muere de las hackatones y lo pueden hacer en su tiempo libre. Y todo lo que está acá es lo que pueden evaluar. Cosas que creo que pueden priorizar son aquellas que tienen facilidad de implementación y que tienen harto impacto. Esto es como el golden zone, acá creen estar, porque es fácil de hacer. Si lo pueden testear muy fácilmente, se van a demorar menos tiempo yo creo y va a generar alto wow. Otras cosas que son valiosas son las de acá, pero son de mayor riesgo porque puede ser que no las hagan bien con el tiempo que tienen. Lo que está acá abajo, cosas que son difíciles o fáciles pero que no logran llegar al threshold de wow de los jueces, creo que no vale mucho la pena hacerla. 

Entonces eso, prioricen en base a impacto y factibilidad técnica de lograr su solución. Entonces con eso van a tener un pool grande de proyectos de problemas que siguió. Lo van a haber priorizado, van a quedar con una idea que les gusta y una de backup que es fácil de hacer y que algo de tracción genere. 

Parten con su idea de mayor impacto y después tienen que armar su demo o tienen que entender cuál va a ser su demo. Su demo son más o menos dos o tres frases. Primero, hoy existe x problema, tienen que definir el problema, lo van a tener listo y esto genera x daño. Si ese daño puede ser un número, por ejemplo, esto genera 600 incidentes al día y el día de mañana podrían ser 1.200. Ese es su número, ese es su daño, eso es su riesgo y eso es lo que quieren ir a atacar. Para eso proponemos solución, que va a ser su producto, al final lo que vivía en su record. En nuestra demo genera x impacto, entonces ustedes tienen que ser capaces de mostrar esto en vivo. Por ejemplo, baja la cantidad de incidentes a 300 al día o lo baja a cero y creo que esto es menos importante para esta hackatón en particular, pero si logran definir un usuario que pueda adoptar su solución y entonces generar cierto valor, creo que eso también es importante. Si es que su usuario es un gobierno que diminuye su riesgo de perder data o defraudar al público porque están evitando seguir ataques que serían llevados a cabo por agentes, entonces ese es su pathway to value. 

Eso, ese es mi dump de información. Ahora los escucho, entiendo que vienen con un par de ideas, así que les voy a preguntar para tenerlo en cuenta porque no sé, las ideas que de pronto llegamos ahorita es sin aderecho el research que por ejemplo recomiendas, entonces pueda que cambien en un momento. 

Entonces, ¿cómo son tus horarios aquí? Eso también, ¿qué días, qué horas? Yo hoy día voy a estar hasta las 12 más o menos, ¿qué hora es ahora? Las 12. Un poco más probablemente, un poco más. No voy a estar toda la noche ya, pero mañana me levanto temprano y estoy todo el día conectado al menos. 

Mañana vengo en la mañana y vengo también en la tarde. No tengo demasiado claro el blote pero se lo voy a comunicar con anticipación para que nos vamos juntando en ambas instes para tener reuniones. Yo les diría que la de la mañana sea más como desbloquear, hablar de producto, solución, no sé qué, y después la de la tarde puede ser más de demo, a priori. 

Perfecto. Perdón, ¿querés volver a repetirse la voz? Creo que quedó relativamente claro, ¿no? 

Te diría, me gusta la idea, creo que es lograble, por lo que escucho, me faltaría entender si es que es algo nuevo, si es algo no él y que una gente que te revisa el repo no vaya a decir, esto ya existe, ya se ha hecho, porque creo que eso le quita el valor contrafactual. 

¿Tú me dices que es factible en 12 horas? Sí. Creo que lo que faltaría entonces es explicar muy bien el enemigo, el problema, cuál es el daño que generas si es que no se implementa, y cuál es el contrafactual o el lift positivo que genera la solución. ¿Crees que me pudieras decir eso ahora o tendrías que hacer research igual? 

No, no, pues de hecho ya estuve haciendo research hasta recién, pero sí, no creo que ahí es súper clave que identificar problemas a nivel del código por un lado, es decir, que el modelo haya querido insertar código no visible o lo que sea, tiene un valor muy grande para después evitar un posible bug después que se haya explotado por mismos agentes, entonces ahí hay como un valor bastante grande, y por otro lado la revisión del prompt también, porque perfectamente el humano está equivocándose en lo que está pidiendo y está induciendo un bug y el humano le solicita, entonces como que las dos carazos de esa variación son esas, por eso código y prompt, entonces en principio eso sería como la gracia de lo que disminuirías. 

Haciendo como un poquito de red teaming, ¿crees que un agente malicioso podría infiltrarse en el SLM para decirle ignora tus reglas? Potencialmente sí, pero ahí la idea sería precisamente generar un sandbox para ambos lados, o sea, realidad protegerá los SLM al final, más que el modelo, porque el modelo puede ser un modelo propietario que estés utilizando desde una API, pero claro, ahí tendría que el modelo hackear el sandbox e intervenirlo, también se pueden poner safeguards para eso, poder detectar si el sandbox fue accedido por un camino que no sea exclusivamente el definido, entonces eso sería una mejora. 

¿Y puedes hacer setup el sandbox dentro del tiempo que tienen y además generar la infraestructura para tener el producto? Ya eso tendría que investigarlo, porque esa última idea la viste como si está buena, pero no la avalúe todavía. 

Pensaría para un problema, porque AI Safety ya es como de los tracks más difíciles, creo yo, porque hardware, una mano que se mueve, ok perfecto, todo lo entendemos, pero estas son cosas muy black box para la mayoría de personas. Es más difícil que sea wow también. 

Yo tengo una que se me estuvo ocurriendo y estoy haciendo un poco de research, cada vez las empresas optan más modelos locales a gran escala, corriendo en servidores como OpenRouter o demás, y se encontró una falla que un modelo de Qwen envió todos los datos a un servidor externo de China. Quizás ahí hay una oportunidad en hacer un alignment o ofrecer un servicio de alignment en base a las empresas. 

También el harness a veces no queda flojo, pero hacer una pequeña modificación de la función de distribución final que hace el LLM quizás mejore mucho más. Por ejemplo, yo en mi proyecto, en la startup que estamos haciendo, nosotros predecimos códigos de 8 dígitos, pero no todos los códigos son del 0 al 9, sino que algunos tienen restricciones para que puede ser 0, 4, 3 o 2. Con un LLM o un SLM común suele alucinar. Aunque cumpla bien las reglas, te suele crear códigos que no existen. Entonces nosotros lo que hicimos es modificar la función de distribución para que te dé códigos existentes. O sea, por lo menos resolvimos ese primer problema que es que no alucinen. Así que nada, se me ocurrió esa idea. Hice un poco de research con este incidente, pero no hice mucho más. 

Creo que se logra comunicar el valor de una forma más tangible. Si la fara comparar a esta, creo que el valor es más fácil de identificar. Creo que el impacto no tengo como información suficiente para decir es más o menos entre las ideas. No tengo información suficiente para eso. Factibilidad, a priori, yo lo veo posible dentro de 10 horas, 12 horas. Creo que factibilidad la pueden evaluar mejor ustedes, eso sí. Tendría que entender si es que esto es una solución muy nueva o si el mercado ya tiene una solución para esto y tendría que entender cuál es el impacto o el riesgo que enfrentan las empresas tangiblemente o en número o en plata o en incidentes para entender qué se estaría previendo. 

Y creo que siempre hay que pensar en cómo hacemos una demo de esto. Yo te preguntaba por Sandbox, porque creo que si tienen que hacer una demo tienen que tener todo el ambiente seteado para poder mostrarlo en vivo y tener como un caso negativo con prompt injection o lo que sea que puedan hacer en esos minutos que tengan en la presentación para demostrar el failure mode. Entonces la valoría, creo que se logra transmitir el valor y me hace sentir la teoría de cambio y valoría de nuevo como cuánto es el riesgo a nivel mundial que se podría disminuir por esto. 

Nosotros hablamos mucho de alignment en la semana pero es como que lo único tranquilo que se me ocurre. 

Yo hay una idea que tenia entre tu más poder le des a una agente un mejor te va a ayudar. Yo con mi empresa y le doy a mi agente acceso a la base de datos, a la nube, AWS, a los servidores a mi información en que más le doy más contexto tiene de mi y me va a ayudar en todo. El problema es que entre más le doy es bueno y es malo porque corro más riesgos de que se ejecuten acciones peligrosas o de que pues por culpa de una agente, de solo una agente que tiene acceso a todo, pues pasen no sé, como se digo, por raridad o algún error, entonces es bueno y malo y bueno hasta ahí vino a mi idea y es como que buscar e investigar e intentar quitar el malo, o sea que tenga todo el acceso posible y disminuir los riesgos de que ejecute cosas que no quiero que ejecute pero sin intervención porque la idea es que yo le doy todo acceso para yo no estar checando y manualmente haciendo todo sino que la gente, yo solamente le diga, le diga, le diga y él haga, haga, haga, pero sin cometer acciones peligrosas. 

Creo que por lo general escucho ideas que van muy ligadas como al subtrack que es control control o como oversight sobre lo que está haciendo una agente, no me acotaría eso, creo que pueden investigar distintas áreas dentro del mismo track. ¿Cómo? Porque sentimos que es muy research y producto. 

Mira, yo creo que es lo más difícil creo que el impacto es difícil de comunicar, creo que como es que uno tiene mucho contexto, es muy interesante, pero creo que lograr en una demo comunicar todo eso para demostrar valor es lo que a mí me hace, es como, yo tendría mucho juego a meterme ahí, si logran encontrar la solución y como de muy gran lift, creo que de nuevo, va a ser muy difícil en el tiempo acotado y con el cómputo que van a tener actualmente pero yo a priori no me metería ahí. 

Yo tenía dos propuestas, una que sería como nosotros en AI y engineering tenemos un problema siempre que es la evaluación de los modelos, entonces y lo difícil que son de reproducir los experimentos cuando alguien con el código solo da un blog post sobre eso y no te libera el código por tal o cual motivo entonces lo que a mí me gustaría hacer sería como un Hugging Face para evals o para AI safety en donde yo pueda reproducir un experimento con un modelo o una API que yo le de a mi librería o a mi interfaz y que tenga la opción también de correrlo en servidores en V, donde yo pueda calcular un presupuesto de manera determinística para todos los usuarios esto estaría, digamos, soportado por la comunidad open source que iría agregando experimentos dataset y cosas para que se vayan mezclando, que sería como un Hugging Face, pero para AI safety. Esto yo lo pensé más que nada para empresas grandes donde capaz no tienen mucha gente que se dedique a esto, pero si tienen la plata como para correr grandes experimentos y también para activados, y mi segunda propuesta perdón que vaya rápido, es flagiote, creo que ese grupo nos está esperando bueno, si, si querés comentar la primera te diría que, encuentro que esto solamente siendo como de mi personal pero creo que no es difícil y si bien el impacto es positivo creo que no es demasiado grande, creo que es una idea que necesita, pero creo que la mantendría creo que es contento un buen backup, creo que pueden llegar a algo más robusto. 

Les dejo una última idea que se me ocurrió que es un scrapper de técnicas de prompt injection o de jailbreaking, esto no sé si existe pero que sea súper exhaustivo, que busque reddit, que busque todas las páginas más nichos y que identifique como las técnicas más nuevas de jailbreaking, que las testee, contra un agente en un ambiente controlado, que un agente me evalúe si es que funcionó o no funcionó el jailbreak y que en base a eso entre una recomendación a un AI lab eso. [Se omite una oferta de contacto personal.] 

Y si quieren, mandame la segunda idea: te la puedo decir ahora en 5 segundos. Un AI kitchen en donde básicamente vos haces mechanistic interpretability en neuronas para personalizar tu propio modelo local 

¿y por qué eso es de safety? Buena pregunta. [Se corta la grabación.]
