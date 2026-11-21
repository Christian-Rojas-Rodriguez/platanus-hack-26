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

1. Toma los tests, `conftest.py`, `pytest.ini` y el runner **de la rama base**, no del PR, y los corre en un contenedor limpio.
2. Marca cualquier cambio del PR a esos archivos.
3. Si el PR es un arreglo de seguridad, corre los ataques reservados contra la versión parchada.
4. Responde aprobado o rechazado con evidencia reproducible. Si se rechaza, no se integra nada.

## Qué se construye y qué se corta

| Se construye | Se corta (queda como visión en el pitch) |
|---|---|
| Verificador en el host: tests y runner sellados desde la rama base, contenedor limpio | Modelos pequeños locales, Kali, multi-LoRA y RLVR |
| Equipo rojo de Mauricio con un modelo de frontera: 2 familias de ataque sobre APIs Python (autorización por recurso, acceso indebido a archivos), varios exploits por falla | Capas de contenedor y MCP |
| Parchador con un modelo de frontera, tratado como no confiable | Modo B separado (queda absorbido: el mismo verificador sirve para cualquier PR) |
| Oráculo determinista y ataques reservados | Swarm paralelo |
| Reversión atómica si algo falla | Dashboard elaborado (basta una vista de PR aprobado o rechazado) |

## Demo de 3 minutos

1. Un fundador le pide a un agente «arregla el endpoint y que pasen los tests». El agente edita `conftest.py`. CI normal: verde. Nuestro verificador: rechazado, con el archivo y la línea.
2. El bot de seguridad parcha un acceso indebido. Su propio exploit ya no funciona y su revisor lo aprueba. Nuestro verificador corre un ataque reservado y todavía entra: rechazado.
3. Segundo intento del parchador: pasa los tests sellados y los reservados. Aprobado y con merge.

## Evaluación

- **Casos con trampa etiquetada:** tareas de ImpossibleBench o EvilGenie, donde pasar los tests solo es posible haciendo trampa, corridas con un agente real.
- **Casos de seguridad:** 3 apps de BaxBench con vulnerabilidad conocida.
- **Líneas base:** CI normal que corre los tests del PR; el parche validado solo con el exploit que vio el parchador.
- **Métricas:** trampas detectadas y falsas alarmas sobre corridas honestas; parches aceptados por la validación propia que fallan con los reservados (la cifra que vende la idea); utilidad conservada.
- Con pocos ataques, reportar intervalos («0 de 10, menos de 26 % con 95 % de confianza»), nunca «cero vulnerable».

## Preguntas del jurado (sección 9 del brief)

- **«¿Claude Security o Codex Security no hacen esto?»** Hallan y parchan. En lo que publican, su parche lo valida el mismo sistema que lo escribió, o un modelo, y lo aprueba un humano. Nosotros somos el tercero independiente y no competimos con ellos: los verificamos.
- **«¿Se puede engañar a tu métrica con el mismo truco?»** El runner y los tests salen de la rama base y corren fuera del alcance del modelo; no hay un LLM que convencer.
- **«¿Quién paga primero?»** Startups con mucho volumen de PRs de IA y bots de seguridad activos, sobre todo si se preparan para SOC 2.
- **«¿Por qué es AI safety y no solo seguridad?»** Es AI control: supone que el agente y el parchador pueden estar haciendo trampa (reward hacking) y pone un monitor confiable que no depende de su cooperación.
- **«¿Qué no probaste?»** Lenguajes distintos de Python, vulnerabilidades fuera de las dos familias y trampas que no tocan los tests (por ejemplo, un verificador débil). Decirlo antes de que lo pregunten.

## Puertas de control

- **Hora 2:** el agente hace trampa con `conftest.py`, el CI normal da verde y el verificador lo rechaza usando solo archivos de la rama base.
- **Hora 6:** un parche que pasa su propia validación falla con un ataque reservado en al menos una app de BaxBench.
- Si la hora 6 no cierra, se presenta solo la parte del agente (que ya es la red de seguridad acotada del ranking).

## Puntaje estimado

| Orig. | Amb. | Ejec. | Téc. | Imp. | Total |
|---|---|---|---|---|---|
| 6,5 | 8 | 7 | 8 | 9 | **77,5** |

Sube frente a la fusión completa (71,5) porque concentra la originalidad en lo único que nadie hace, recupera ejecución al cortar capas y conecta el impacto con lo que los jurados viven cada semana. Es mi juicio, no una medición; vale solo si pasan las dos puertas.
