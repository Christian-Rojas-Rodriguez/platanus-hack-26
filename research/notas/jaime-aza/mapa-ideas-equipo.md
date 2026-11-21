# Notas de Jaime: mapa de ideas (dificultad vs impacto)

> **Esto es una opinión personal de Jaime, no una decisión del equipo.** Todo lo que hay en `research/notas/jaime-aza/` son mis notas para discutir; la elección de la idea la tomamos juntos.

Versión 5 (21-11-2026). Mueve el juez por ejecución a la zona de alto riesgo tras revisarlo a fondo, suma AegisHub (Federico), el red teaming con modelos abiertos (Mauricio) y la recuperación tras un agente destructor ([investigacion-4-ransomware-con-ia.md](investigacion-4-ransomware-con-ia.md)). La versión 4 sumó las ideas nuevas de Tomás (`docs/t/final-ideas/`, `docs/t/project-pitches.md`) y de Christian (`research/notas/christian-rojas/mercado/`), y mueve los puntos según mi tercera investigación, que miró los problemas por región y qué gana hackathons de AI safety: [investigacion-3-problemas-mundiales.md](investigacion-3-problemas-mundiales.md). El puntaje con la rúbrica del jurado está en [ranking-propuestas.md](ranking-propuestas.md).

![Notas de Jaime: mapa de dificultad vs impacto](mapa-ideas-equipo.svg)

**Cómo leerlo.** Colores por origen: rosado, brief de Juanfe; verde oliva, Jaime; verde azulado, Tomás; morado, Christian; azul, Mauricio; ocre, Federico; naranjo, reunión con el mentor sin autor en el repo. El círculo blanco con borde oscuro es una idea a la que llegamos varios por separado. **Anillo rojo punteado: ya existe o el jurado ya lo vio.** Golden zone: dificultad menor a 5 e impacto mayor a 6. Zona rosada: alto riesgo en el tiempo que hay.

| # | Idea | Origen | Dificultad | Impacto | Por qué está ahí |
|---|---|---|---|---|---|
| 1 | Juez por ejecución | Brief + Jaime + Christian | 7,6 | 7,6 | Antes «detector de trampas + canarios». Se corre a la zona de alto riesgo tras revisarlo a fondo: la solución de referencia no sirve como vara (en la tarea 1012 tampoco usa el comando que pide la instrucción), reproducir pulsaciones en entornos que instalan paquetes por red no es fiable y medir solo en tareas fáciles no es comparable con el 44 % publicado. Solo como piloto acotado. |
| 2 | Brecha en español regional | Brief + Tomás + Christian + Jaime | 3,2 | 7,4 | Fusiona SafeBench-ES + LatamGPT (brief), LatAm Safety Gate (Tomás) y la brecha dialectal con boleta de LatamGPT (Christian). Pares que cambian solo la variante del español y gemelos benignos para medir sobre-rechazo. Ya existen LatAm-RT (incluye Chile) y el paper S-OWMI de Apart (junio de 2026, con datos simulados), así que lo nuevo es medirlo bien: guardias, escritura coloquial y LatamGPT. |
| 3 | Preflight de contención | Jaime | 3,6 | 6,6 | Recortado a dos comprobaciones: salida real a internet desde el entorno del agente y cobertura del monitor con acciones señuelo inofensivas. Primera del ranking por ejecución más segura. Débil en originalidad (EvalGuard se solapa) y en la métrica, que se mide sobre fallas plantadas por nosotros. |
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
| 16 | Recuperación tras agente destructor | Christian + Jaime | 4,6 | 6,5 | Reformula el «rewind» de Christian con la investigación de ransomware. Un agente borra o cifra archivos por terminal; se mide cuánto recupera el deshacer de Claude Code, Gemini CLI y OpenCode contra copias fuera de su alcance. Línea base real con límites documentados. En contra: el remedio son copias de seguridad, técnica conocida. |
| 17 | Radar + harness | Jaime | 4,8 | 2,6 | Mi principal de la primera ronda. Agent Zero (Caracas) ya hizo el ciclo ataque, confirmación y regla, con 1.176 pruebas; y un scraper de jailbreaks roza la línea roja del brief. |
| 18 | Qwen + decoding | Reunión con el mentor | 4,3 | 3,4 | Gancho real (Cohere, oct-2026), pero restringir tokens no frena una URL dentro de un comando. |
| 19 | Harness en cascada | Mauricio | 2,6 | 2,6 | El patrón que más vio el jurado: proxy o hook delante del agente con reglas deterministas (HAWK, Aegis, Hackan't, wardlm, Tranquera). |
| 20 | Scheming radar | Brief de Juanfe | 4,0 | 4,5 | A3 del brief y hueco 4 del informe 29 de Christian. CLTR ya opera un observatorio; demo sin villano en vivo. |
| 21 | HF para evals | Reunión con el mentor | 2,0 | 3,4 | Fácil, pero Inspect Evals y Hugging Face Community Evals ya cubren mucho. |
| 22 | MemoryLineage | Tomás | 6,6 | 2,6 | Provenance Firewall (Bogotá) ya protegió la memoria de agentes con 255 tests. Christian lo confirma en su informe 32. |
| 23 | Benchmark hardener | Brief de Juanfe | 8,0 | 2,0 | A2 del brief y hueco 3 del informe 29. Ya existe con código abierto (harden-v0 y BenchJack). |
| 24 | AegisHub | Federico | 5,2 | 3,5 | Hub y arena de ataques y escudos (Federico). Mide seguridad contra utilidad, que es lo valioso, pero sus ataques y escudos son el carril saturado de inyección y la plataforma ya la cubren Inspect Evals y Promptfoo. Las cifras de la demo son de maqueta. |
| 25 | Red teaming open-weight | Mauricio | 8,6 | 3,0 | Modelos abiertos ajustados para atacar en sandbox y hardening automático (Mauricio). Su propia investigación muestra el carril lleno, ajustar modelos ofensivos roza la línea roja y no cabe en el tiempo. |

Fuera del gráfico: Agent Escape Lab y Prompt-to-Policy Compiler (Tomás), MCP-Shield + MCP-Arena y el radar de jailbreaks solo (Jaime), el agente con acceso total y AI kitchen (reunión con el mentor) y el anti-estafas por WhatsApp, descartado. Todas están en el ranking.

## Mi lectura (opinión)

- **Ninguna se despega.** Las cuatro de arriba (preflight 3, brecha en español 2, recuperación tras agente destructor 16 y Eval Mirage 4) están a 3 puntos en el ranking; lo que las separa es qué podemos tener funcionando de punta a punta el sábado en la mañana.
- **El juez por ejecución (1) bajó:** el impacto sigue alto, pero la dificultad real es mucho mayor de lo que estimé. Solo como piloto acotado.
- **Lo que dejaría:** todo lo que tiene anillo rojo. Es lo que más se construyó en el tour o ya existe como herramienta.

Las posiciones son mi juicio para discutir, no una medición.
