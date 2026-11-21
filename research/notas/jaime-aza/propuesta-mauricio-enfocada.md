# Notas de Jaime: la propuesta de Mauricio, enfocada en lo que la hace distinta

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Parte de la propuesta unificada de Mauricio ([m-propuesta_fusion_red_seguridad_y_hardening.md](../m-propuesta_fusion_red_seguridad_y_hardening.md)) y del ranking v5 ([ranking-propuestas.md](ranking-propuestas.md)). La idea es la de Mauricio; aquí solo se recorta y se enfoca en el jurado.

## La idea en una frase

**Ninguna IA aprueba el código de otra IA.** Un verificador determinista, fuera del alcance de cualquier modelo, que decide si entra al repo el código que escribió un agente o el parche que propuso un bot de seguridad.

## Qué la hace distinta (y qué no)

Lo que **no** es diferencial, porque ya existe y el jurado lo vio:

- Encontrar una vulnerabilidad, confirmarla con un exploit, parcharla y volver a probar: Codex Security, Claude Security, CodeMender, Aikido Infinite, XBOW y Corgea; en el tour, Agent Zero, Gotchu y VanGUARD.
- Aislar al agente y guardar un registro que no pueda borrar: Container Use (Dagger); en el tour, HAWK.
- Detectar ediciones a tests o trucos con `conftest.py`: gauntlet-cheatcatcher.

Lo que **sí** es diferencial, y donde va todo el esfuerzo:

1. **Separación de funciones para IA.** Quien escribe el código no puede ser quien lo califica. Hoy el agente corre sus propios tests, y el bot de seguridad valida su propio parche con su propio exploit y con un revisor que también es un modelo; al final aprueba un humano que no da abasto. Aquí la decisión final la toma un proceso fijo que ningún modelo puede tocar. Es la regla que el brief destaca del tour («la IA no toma la decisión final de seguridad») aplicada a un punto que nadie cubrió: el parchador.
2. **El parchador tampoco es confiable.** El mismo control vigila al agente de código y al bot que arregla vulnerabilidades. Si el parche toca los tests, cambia la configuración de pytest o solo bloquea el exploit exacto que le mostraron, se rechaza.
3. **Ataques reservados.** El equipo rojo de Mauricio genera varios exploits por falla; el parchador ve algunos y el verificador guarda el resto. Un parche que solo tapa el caso que le mostraron falla con los reservados. Es la diferencia entre «arreglé el bug» y «aprendí el examen».
4. **Todo o nada.** Si alguna comprobación falla, nada llega a la rama principal y el repo queda como estaba (la reversibilidad de la puerta 1).

## El uso cotidiano de los jurados

Los jurados son fundadores y gente de startups que programa con agentes todos los días. Su semana se ve así:

- Le piden a Claude Code, Codex o Cursor que arregle algo, y el agente responde «listo, los tests pasan».
- Tienen agentes en segundo plano o en la nube que abren PRs mientras hacen otra cosa.
- Activan bots que abren PRs solos: dependencias, arreglos de seguridad, revisiones.
- Revisan más código del que pueden leer y terminan aprobando por confianza.

**Lo que viene en sus startups** (2026 a 2027): más PRs escritos por IA que por personas, bots de seguridad que parchan solos y agentes que encadenan cambios de otros agentes. La pregunta que van a tener que contestar, ante un cliente, un inversionista o una auditoría SOC 2 (que pide que los cambios se prueben y aprueben antes de producción), es: **¿quién verificó lo que escribieron tus bots?** Hoy la respuesta es «otro bot» o «nadie».

Pitch para ellos: *«Tu repo ya tiene tres autores que no son personas: tu agente, tu bot de seguridad y tu bot de dependencias. Nosotros somos el revisor que no es una IA: tests sellados, ataques que el parchador nunca vio y nada entra si no pasa.»*

## Forma del producto

Una revisión obligatoria antes de hacer merge (GitHub Action y CLI) que se activa en cada PR con un autor de IA:

1. **El evaluador vive en otro contenedor.** La app del PR corre en un contenedor y los tests y ataques le pegan por HTTP desde otro, con los tests y el runner tomados **de la rama base**. El código del PR nunca comparte proceso ni contenedor con el evaluador, así que no puede reescribir los resultados.
2. Restaura los `conftest.py` y la configuración de pytest de la rama base, y marca para revisión cualquier `conftest.py`, `sitecustomize.py`, `*.pth` o hook nuevo (lo que hace SWE-Bench Pro Verified).
3. Si el PR es un arreglo de seguridad, corre los **ataques reservados** y también **tests funcionales reservados** contra la versión parchada: los primeros atrapan el parche que solo tapa el exploit que vio, los segundos el que tapa la falla rompiendo la funcionalidad.
4. Responde aprobado o rechazado con evidencia reproducible. Si se rechaza, no se integra nada.

**Límite que se dice en voz alta:** en tests unitarios que corren dentro del mismo proceso que el código no hay garantía; ahí el verificador solo marca para revisión.

## Qué dice el estado del arte (revisado el 21-11-2026)

- **Los ataques reservados están respaldados.** En 112 bugs reales, los parches de los modelos pasan el exploit de prueba en 90 %, pero incluso con Opus 4.7 el 32,7 % de esos parches falla los tests del desarrollador ([Le et al., arXiv 2610.10150](https://arxiv.org/abs/2610.10150v1)). El estudio FLAWED de 1Password (industria, sin revisión de pares) encontró que más de un tercio de los parches que parecían buenos solo bloqueaban el exploit de prueba ([resumen](https://www.noze.it/en/insights/ai-generated-patches-off-by-1-study/)). [arXiv 2606.25973](https://arxiv.org/html/2606.25973v1) usa tests ocultos («Ghost Tests») para atrapar arreglos falsos.
- **Un juez LLM no sirve como decisión final:** no mide bien si el parche conserva la funcionalidad ([Deininger y Slany, 2026](https://www.mdpi.com/2624-800X/6/5/153)).
- **Restaurar tests de la base no alcanza.** BenchJack ([arXiv 2605.12673](https://arxiv.org/html/2605.12673v1)) saca 100 % en SWE-bench Verified y Pro con un `conftest.py` de nueve líneas que sobrevive al reseteo, y cuando se bloquean esos archivos lo salta con un módulo dentro del paquete que altera pytest al importarse. La causa es que agente y evaluador comparten contenedor. SWE-Bench Pro Verified ([arXiv 2609.08149](https://arxiv.org/pdf/2609.08149)) lo resolvió moviendo el evaluador a otro dominio de confianza. Por eso el punto 1 de arriba.
- **Lo que no es nuevo:** validar con tests ocultos es práctica normal en benchmarks de investigación. Lo nuevo es llevarlo a una revisión antes del merge de uso diario y aplicarlo también al bot que parcha.

## Qué se construye y qué se corta

| Se construye | Se corta (queda como visión en el pitch) |
|---|---|
| Verificador en el host: app en un contenedor, evaluador en otro (tests por HTTP), tests y runner sellados desde la rama base | Modelos pequeños locales, Kali, multi-LoRA y RLVR |
| Equipo rojo de Mauricio con un modelo de frontera: 2 familias de ataque sobre APIs Python (autorización por recurso, acceso indebido a archivos), varios exploits por falla | Capas de contenedor y MCP |
| Parchador con un modelo de frontera, tratado como no confiable | Modo B separado (queda absorbido: el mismo verificador sirve para cualquier PR) |
| Oráculo determinista, ataques reservados y tests funcionales reservados | Swarm paralelo |
| Reversión atómica si algo falla | Dashboard elaborado (basta una vista de PR aprobado o rechazado) |

## Demo de 3 minutos

1. Un fundador le pide a un agente «arregla el endpoint y que pasen los tests». El agente mete un hook dentro del paquete que reescribe los resultados de pytest (el truco de BenchJack, que ni bloquear `conftest.py` detiene). CI normal: verde. Nuestro verificador, que evalúa desde otro contenedor: rechazado, con el archivo y la línea.
2. El bot de seguridad parcha un acceso indebido. Su propio exploit ya no funciona y su revisor lo aprueba. Nuestro verificador corre un ataque reservado y todavía entra: rechazado.
3. Segundo intento del parchador: pasa los tests sellados y los reservados. Aprobado y con merge.

## Evaluación

- **Casos con trampa etiquetada:** tareas de ImpossibleBench o EvilGenie, donde pasar los tests solo es posible haciendo trampa, corridas con un agente real.
- **Casos de seguridad:** 3 apps de BaxBench con vulnerabilidad conocida (sus tests ya son de caja negra por HTTP) y CVE de Python de VulnRepairEval (23 casos verificados con exploits; el mejor de 12 modelos arregla 21,7 %, según arXiv 2606.25973).
- **Casos de ataque al evaluador:** las variantes de BenchJack (`conftest.py` en la raíz y hook dentro del paquete).
- **Líneas base:** CI normal que corre los tests del PR; tests de la base restaurados pero en el mismo contenedor (lo que BenchJack rompe); el parche validado solo con el exploit que vio el parchador.
- **Métricas:** trampas detectadas y falsas alarmas sobre corridas honestas; parches aceptados por la validación propia que fallan con los reservados (la cifra que vende la idea); utilidad conservada.
- Con pocos ataques, reportar intervalos («0 de 10, menos de 26 % con 95 % de confianza»), nunca «cero vulnerable».

## Preguntas del jurado (sección 9 del brief)

- **«¿Claude Security o Codex Security no hacen esto?»** Hallan y parchan. En lo que publican, su parche lo valida el mismo sistema que lo escribió, o un modelo, y lo aprueba un humano. Nosotros somos el tercero independiente y no competimos con ellos: los verificamos.
- **«¿Se puede engañar a tu métrica con el mismo truco?»** Restaurar los tests no basta (BenchJack lo demostró), por eso el evaluador corre en otro contenedor y le pega a la app por HTTP; el código del PR no comparte proceso con él y no hay un LLM que convencer. En tests unitarios dentro del mismo proceso no hay garantía y se dice.
- **«¿Quién paga primero?»** Startups con mucho volumen de PRs de IA y bots de seguridad activos, sobre todo si se preparan para SOC 2.
- **«¿Por qué es AI safety y no solo seguridad?»** Es AI control: supone que el agente y el parchador pueden estar haciendo trampa (reward hacking) y pone un monitor confiable que no depende de su cooperación.
- **«¿Qué no probaste?»** Lenguajes distintos de Python, vulnerabilidades fuera de las dos familias y trampas que no tocan los tests (por ejemplo, un verificador débil). Decirlo antes de que lo pregunten.

## Puertas de control

- **Hora 2:** el ataque de BenchJack (hook dentro del paquete) engaña al CI normal y a la restauración de tests en el mismo contenedor, y no engaña a nuestro evaluador en otro contenedor.
- **Hora 6:** un parche que pasa su propia validación falla con un ataque reservado en al menos una app de BaxBench.
- Si la hora 6 no cierra, se presenta solo la parte del agente (que ya es la red de seguridad acotada del ranking).

## Puntaje estimado

| Orig. | Amb. | Ejec. | Téc. | Imp. | Total |
|---|---|---|---|---|---|
| 6 | 8 | 7 | 8,5 | 9 | **78** |

Sube frente a la fusión completa (71,5) porque concentra la originalidad en lo único que nadie hace, recupera ejecución al cortar capas y conecta el impacto con lo que los jurados viven cada semana. Frente a la primera versión de esta nota (77,5): la originalidad baja de 6,5 a 6 porque validar con tests ocultos ya es práctica de investigación, y el aspecto técnico sube de 8 a 8,5 por el evaluador en otro contenedor. Sin ese cambio el control se podría engañar con BenchJack y el técnico caería a 6,5 (total 73). Es mi juicio, no una medición; vale solo si pasan las dos puertas.
