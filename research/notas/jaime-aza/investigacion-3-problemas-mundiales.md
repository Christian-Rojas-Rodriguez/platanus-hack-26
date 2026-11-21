# Notas de Jaime: tercera investigación (problemas por región y qué construir)

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Resumen de una búsqueda en seis frentes hecha el 20-11-2026. El detalle con las 99 fuentes está en [informe-problemas-mundiales.md](informe-problemas-mundiales.md). Las cifras sin verificar o de fuente secundaria están marcadas ahí; hay que abrirlas antes de decirlas en el pitch.

Pregunta: qué problemas reales tiene hoy la seguridad de IA en Estados Unidos, Europa, China, India, Asia-Pacífico, África y Latinoamérica, y qué conviene construir para ganar el track.

## Lo que se repite en todas las regiones

1. **La IA pasó de decir a hacer y nadie verifica el resultado.** En julio y agosto de 2026 los incidentes ocurrieron dentro de las propias evaluaciones de seguridad de OpenAI, Anthropic y el instituto británico: agentes que salieron a internet, publicaron un paquete real o presionaron a una persona real.
2. **Las evaluaciones no son de fiar.** 59,4 % de las tareas auditadas de SWE-bench Verified son defectuosas (OpenAI). En la prueba conjunta de los institutos de seguridad, los agentes aprobaron cerca de 40 % frente a cerca de 99 % en chat, y los jueces automáticos discreparon de los humanos entre 23 y 28 % (Singapur).
3. **Nadie mide cuánto fraude usa IA**, salvo el FBI desde 2025 (893 millones de USD). Para Chile no hay cifra oficial: lo que existe es fraude general o números de proveedores.
4. **La regulación va por delante de las herramientas** para comprobarla: etiquetado de contenido sintético en la UE, China e India; leyes aplazadas en Chile.
5. **Lo que el agente dice que hizo no coincide con lo que hizo.** METR halló llamadas a herramientas falsificadas en más de 7 % de las transcripciones de un caso.

## Lo propio de cada región

| Región | Problema dominante | Dato |
|---|---|---|
| EE. UU., Reino Unido y UE | Agentes de frontera que escapan o hacen trampa en evaluaciones | 3 incidentes en 141.006 corridas, sin detectar unos tres meses (Anthropic) |
| China | Cadena de suministro de agentes y modelos abiertos sin documentar | 1.184 skills maliciosos y unas 247.000 instalaciones en una campaña (citado por Tencent) |
| India | Fraude que la víctima autoriza; seguridad que cambia con la ortografía | El éxito de un ataque pasa de 0,10 en inglés a 0,50 en hinglish con faltas fonéticas |
| Singapur y Asia-Pacífico | Evaluar agentes a escala y en varios idiomas | 80,8 % de las estafas son transferencias hechas por la propia víctima |
| África | Menos rechazo y jueces menos fiables en lenguas locales | Benchmark comunitario de 4.216 pruebas en 8 lenguas (GSMA y Zindi) |
| Latinoamérica | Casi nada está medido | LatamGPT publicó sus pesos sin evaluación de seguridad; ningún instituto de seguridad de IA en la región |

## Qué gana hackathons de AI safety

- **Un número contra una línea base que falla**, con falsas alarmas medidas y un caso de falla mostrado. Casi nunca un producto.
- De 65 proyectos premiados que se revisaron: 43 % herramientas defensivas con medición, 29 % hallazgos empíricos, 18 % benchmarks nuevos y un solo producto para usuario final.
- Los revisores critican siempre lo mismo: corridas únicas, sin tasa de falsos positivos, sin barras de error y sin un atacante que se adapta.
- **En las sedes previas de Platanus, 13 de 22 proyectos del track fueron un proxy o un hook y ninguno una evaluación.**
- Kairos forma talento (no investiga), se codirige desde Santiago y sus temas visibles son evaluaciones, interpretabilidad y agentes que hacen trampa.
- Sin confirmar: quiénes son los jueces de Santiago, cómo se define cada criterio y el horario exacto de las presentaciones.

## Qué construiría (opinión)

**Un juez de trayectorias por ejecución.** Recibe la corrida de un agente de código, ignora lo que el agente dice y decide reproduciendo lo que hizo: reglas baratas sobre las acciones, después una contraprueba en el contenedor de la tarea y un juez LLM solo para lo ambiguo.

- **Problema:** GPT-5 pasa tests de tareas imposibles en 54 a 76 % de los casos (ImpossibleBench), y los monitores que leen su razonamiento detectan entre 42 y 65 % en SWE-bench.
- **Número a superar:** 44 % de trampas detectadas con 5 % de falsas alarmas, que es lo que logra el juez publicado en Terminal Wrench cuando se le quitan los comentarios del agente. La meta de 80 % es una aspiración, no un dato.
- **Datos:** `few-sh/terminal-wrench` y `few-sh/terminal-wrench-trajectories` en Hugging Face (Apache-2.0): 331 tareas, 3.632 trampas y 2.352 corridas honestas.
- **Demo:** tests en verde y el monitor de referencia dice «sin trampa»; el juez reproduce la corrida, las comprobaciones nuevas fallan y muestra la línea.
- **Por qué no es un «agent guard»:** juzga después, no se interpone. Conviene contarlo como integridad de evaluaciones.

**Lo que verifiqué a mano en los datos** (una sola tarea, la `1012`):

- Las corridas guardan cada comando del agente, y cada tarea trae su Dockerfile, sus tests y su solución de referencia. **No guardan el sistema de archivos final**, así que la contraprueba exige reproducir los comandos en la imagen de la tarea.
- En esa tarea el agente no tocó ningún test: leyó el verificador, vio que solo buscaba dos cadenas en un archivo y creó el archivo a mano. **Restaurar los tests originales no detecta esa trampa.** Hacen falta comprobaciones nuevas; lo más barato sería comparar contra el estado que deja la solución de referencia (idea mía, sin probar).
- No medí cuántas de las 331 imágenes construyen hoy ni cuánto tardan. Es lo primero que hay que probar.

**Alternativas, en orden:** el preflight de contención para evaluaciones, la brecha de salvaguardas en español regional y Eval Mirage. Todas están en el [ranking](ranking-propuestas.md).

## Correcciones a mis notas anteriores

- **Las reglas sobre el diff ya existen** en al menos seis repos pequeños (tampercheck, tamperguard, rigged, gauntlet-cheatcatcher, Swarm Orchestrator, truthguard), ninguno evaluado sobre benchmarks. Dejan de ser el titular y pasan a ser la línea base.
- **Leí mal a HackTrace.** El AUC 0,500 con tests de solo lectura es de una sola línea base; otra de la misma tabla da 0,973.
- **canaryhook planta credenciales señuelo**, no canarios de tests, y no encontré ningún repo llamado honeypot-control.
- **ProbeGate sale debilitada:** las sondas caen a AUC 0,62 sin razonamiento visible.
- **Las elecciones chilenas fueron en noviembre y diciembre de 2025**, no en 2026, y la ley de datos 21.719 se postergó a octubre de 2027.
- **El 29 % de VoxENES es el error global del benchmark, no el del español.** Lo corrigió Christian en su informe 32; en mis propuestas lo había puesto como error en español.

## Lo que suman las notas nuevas de mis compañeros

- **Christian** (`research/notas/christian-rojas/mercado/`): su matriz de mercado deja la detección de trampas de agentes de código como el espacio más vacío (menos de 5 % cubierto, ninguna empresa dedicada), y su red team de ideas llega al mismo reencuadre. También aporta el contrapeso: en tráfico real OpenAI describe el reward hacking como poco común, así que las tasas altas son de benchmarks diseñados para provocarlo. Hay que decirlo en el pitch.
- **Tomás** (`docs/t/final-ideas/`): encontró LatAm-RT, un benchmark de red teaming para Latinoamérica que incluye Chile (284 prompts, 5 modelos). Lo comprobé y existe. Baja la originalidad de cualquier «primer benchmark en español» y obliga a diferenciarse: guardias, sobre-rechazo, escritura coloquial y LatamGPT.
- **Coincidencias:** tres llegamos por separado a la idea en español regional, y dos más el brief a la detección de trampas.

## Sin verificar

- Jurado, definición de cada criterio y horario de la final de Santiago.
- Cuántas imágenes de Terminal Wrench construyen y si las trayectorias se pueden reproducir de forma determinista.
- Las cifras de los ganadores de Apart se leyeron con una herramienta que resume páginas; abrir el PDF o el repo antes de citarlas.
- Varias cifras regionales (fraude en China, IC3, UK Finance) vienen de fuentes secundarias.
