# Notas de Jaime: mapa de ideas (dificultad vs impacto)

> **Esto es una opinión personal de Jaime, no una decisión del equipo.** Todo lo que hay en `research/notas/jaime-aza/` son mis notas para discutir; la elección de la idea la tomamos juntos.

Versión 4 (21-11-2026). Suma las ideas nuevas de Tomás (`docs/t/final-ideas/`, `docs/t/project-pitches.md`) y de Christian (`research/notas/christian-rojas/mercado/`), y mueve los puntos según mi tercera investigación, que miró los problemas por región y qué gana hackathons de AI safety: [investigacion-3-problemas-mundiales.md](investigacion-3-problemas-mundiales.md). El puntaje con la rúbrica del jurado está en [ranking-propuestas.md](ranking-propuestas.md).

![Notas de Jaime: mapa de dificultad vs impacto](mapa-ideas-equipo.svg)

**Cómo leerlo.** Colores por origen: rosado, brief de Juanfe; verde oliva, Jaime; verde azulado, Tomás; morado, Christian; azul, Mauricio; naranjo, reunión con el mentor sin autor en el repo. El círculo blanco con borde oscuro es una idea a la que llegamos varios por separado. **Anillo rojo punteado: ya existe o el jurado ya lo vio.** Golden zone: dificultad menor a 5 e impacto mayor a 6. Zona rosada: alto riesgo en el tiempo que hay.

| # | Idea | Origen | Dificultad | Impacto | Por qué está ahí |
|---|---|---|---|---|---|
| 1 | Juez por ejecución | Brief + Jaime + Christian | 5,6 | 8,6 | Antes «detector de trampas + canarios» (brief, Jaime y, por separado, Christian). Decide reproduciendo los comandos del agente y corriendo comprobaciones nuevas, sin leer su relato. El hueco medido: el mejor juez publicado detecta 44 % cuando no hay razonamiento visible. Sube en dificultad porque hay que montar los contenedores de las tareas, y las reglas sobre el diff ya existen en seis repos. |
| 2 | Brecha en español regional | Brief + Tomás + Christian + Jaime | 3,6 | 7,0 | Fusiona SafeBench-ES + LatamGPT (brief), LatAm Safety Gate (Tomás) y la brecha dialectal con boleta de LatamGPT (Christian). Pares que cambian solo la variante del español y gemelos benignos para medir sobre-rechazo. Ya existe LatAm-RT (incluye Chile), así que lo nuevo es medir guardias, escritura coloquial y LatamGPT. |
| 3 | Preflight de contención | Jaime | 4,0 | 6,4 | Nueva, de la tercera investigación. Antes de correr una evaluación de agentes comprueba salida a internet, choque de nombres ficticios con dominios o paquetes reales, que la tarea se pueda resolver y que el monitor vea las acciones. Débil en la métrica: se mide sobre fallas plantadas por uno mismo. |
| 4 | Eval Mirage | Brief + Tomás | 5,8 | 7,0 | A4 del brief, aterrizado por Tomás: misma tarea en cuatro condiciones pareadas (lenguaje de benchmark o natural, tests visibles u ocultos). Demanda real, pero con pocas corridas el resultado puede ser ruido. |
| 5 | Complacencia en español | Christian | 4,6 | 5,8 | Sycophancy en conversaciones largas (Christian). Curva turno a turno de cuándo el bot deja de contradecir, en registro chileno, con una intervención medida. Lo frágil es validar el juez automático. |
| 6 | Voz sintética chilena | Jaime | 7,6 | 6,6 | Antes «anti-vishing». Hay datos listos con acento chileno (HISPASpoof), pero se lee como réplica del paper y no hay cifra oficial chilena de fraude con voz clonada. |
| 7 | ProbeGate | Jaime | 7,2 | 5,2 | Baja: las sondas sobre activaciones caen a AUC 0,62 cuando no hay razonamiento visible. Necesita pesos abiertos y GPU. |
| 8 | Safety Evidence Auditor | Tomás | 2,8 | 4,9 | Convierte afirmaciones de seguridad de un laboratorio en verificaciones y marca las que no tienen evidencia reproducible (Tomás, con su Evidence-to-Experiment Compiler). Fácil, pero poco técnico y con demo abstracta. |
| 9 | Agentes de voz ES/PT | Christian | 8,6 | 5,6 | Banco de llamadas adversarias contra un agente de voz bancario de prueba (Christian). Hueco real; montar voz de punta a punta es lo más arriesgado. |
| 10 | Chile Scam Mutator | Tomás | 2,4 | 4,3 | Genera variantes de una estafa y mide si el detector sobrevive (Tomás). Cerca del anti-estafas descartado; Agent Zero ya hizo el ciclo ataque y regla, y generar estafas roza una línea roja del brief. |
| 11 | SideEffect Auditor | Tomás | 5,0 | 5,0 | Mide qué más cambió el agente además de la tarea (Tomás). SABench ya mide efectos no autorizados. |
| 12 | Mandato y recibo (pagos) | Tomás + brief + Christian | 5,9 | 4,4 | ScopeProof (Tomás), C2 del brief y la tesis de pagos cuenta a cuenta de Christian. Lo más repetido: AP2, Visa TAP, borradores IETF, y en el tour Specter, Roxy y HAWK. Lo distinto sería el ángulo de transferencias instantáneas. |
| 13 | Sandbox tripwires | Brief de Juanfe | 3,4 | 5,5 | A5 del brief. Ya hay proyectos parecidos (hackbait, Tracebit) y Owliver y Agent Zero usaron canarios en el tour. Mejor como componente de la 1 o la 3. |
| 14 | MCP TimeLock / Shield | Tomás | 3,3 | 4,0 | Roxy e Ikarus ya son gateways MCP, y mcp-scan fija herramientas por hash desde 2025. |
| 15 | Multiagente A2A | Christian | 6,9 | 3,7 | Tarjetas de agente firmadas y procedencia entre saltos (Christian). Vacío, pero sin comprador y cerca de otro «agent guard». |
| 16 | Rewind de acciones | Christian | 6,0 | 3,2 | Revertir cadenas de acciones de agentes (Christian, su tercera tesis). El carril de control en ejecución tiene cientos de proveedores. |
| 17 | Radar + harness | Jaime | 4,8 | 2,6 | Mi principal de la primera ronda. Agent Zero (Caracas) ya hizo el ciclo ataque, confirmación y regla, con 1.176 pruebas; y un scraper de jailbreaks roza la línea roja del brief. |
| 18 | Qwen + decoding | Reunión con el mentor | 4,3 | 3,4 | Gancho real (Cohere, oct-2026), pero restringir tokens no frena una URL dentro de un comando. |
| 19 | Harness en cascada | Mauricio | 2,6 | 2,6 | El patrón que más vio el jurado: proxy o hook delante del agente con reglas deterministas (HAWK, Aegis, Hackan't, wardlm, Tranquera). |
| 20 | Scheming radar | Brief de Juanfe | 4,0 | 4,5 | A3 del brief y hueco 4 del informe 29 de Christian. CLTR ya opera un observatorio; demo sin villano en vivo. |
| 21 | HF para evals | Reunión con el mentor | 2,0 | 3,4 | Fácil, pero Inspect Evals y Hugging Face Community Evals ya cubren mucho. |
| 22 | MemoryLineage | Tomás | 6,6 | 2,6 | Provenance Firewall (Bogotá) ya protegió la memoria de agentes con 255 tests. Christian lo confirma en su informe 32. |
| 23 | Benchmark hardener | Brief de Juanfe | 8,0 | 2,0 | A2 del brief y hueco 3 del informe 29. Ya existe con código abierto (harden-v0 y BenchJack). |

Fuera del gráfico: Agent Escape Lab y Prompt-to-Policy Compiler (Tomás), MCP-Shield + MCP-Arena y el radar de jailbreaks solo (Jaime), el agente con acceso total y AI kitchen (reunión con el mentor) y el anti-estafas por WhatsApp, descartado. Todas están en el ranking.

## Mi lectura (opinión)

- **Lo que más me convence:** el juez por ejecución (1). Es la única idea a la que llegamos tres por separado (brief, mis notas y el informe 31 de Christian), tiene datos etiquetados y una línea base pública que falla. Salió de la golden zone porque ahora sé que hay que reproducir los comandos del agente en el contenedor de cada tarea.
- **Segunda opción:** la brecha en español regional (2), que también propusimos tres. Es la más fácil de ejecutar; el riesgo es que la brecha salga chica, y por eso el diseño con gemelos benignos.
- **Tercera:** el preflight de contención (3), con el mejor villano del año pero una métrica más débil.
- **Lo que dejaría:** todo lo que tiene anillo rojo. Es lo que más se construyó en el tour o ya existe como herramienta.
- **Donde no coincido con Tomás:** él descarta la 1 por estar cubierta. Las reglas sobre el diff sí lo están; el caso sin razonamiento visible y sin tocar tests, no. Lo dejo para discutir.

Las posiciones son mi juicio para discutir, no una medición.
