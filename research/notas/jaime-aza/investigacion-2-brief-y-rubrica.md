# Notas de Jaime: segunda investigación (brief de Juanfe y rúbrica)

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Los puntajes son mi juicio, no una medición.

Hecha el 21-11-2026 a partir del brief del mentor (`docs/ai-safety-track-brief.md`). Tres preguntas: si las cifras del brief se sostienen, si cada idea de su lista corta ya existe, y qué construyeron los equipos anteriores del tour. Mapa resultante en [mapa-ideas-equipo.md](mapa-ideas-equipo.md).

## Rúbrica de evaluación

| Criterio | Peso |
|---|---|
| Aspecto técnico | 25 % |
| Ambición | 20 % |
| Ejecución | 20 % |
| Impacto | 20 % |
| Originalidad | 15 % |

Lo que más pesa es el aspecto técnico. Un benchmark o un dashboard, aunque sea original, parte con desventaja frente a algo con un mecanismo propio. No encontré la definición oficial de cada criterio: conviene pedirla a los organizadores.

## Puntuación de las ideas con la rúbrica

Cada criterio de 0 a 10. El total pondera con los pesos de arriba (máximo 100).

| Idea | Orig. | Amb. | Ejec. | Téc. | Imp. | Total | Comentario |
|---|---|---|---|---|---|---|---|
| Detector de trampas + canarios | 7 | 8 | 7 | 9 | 8 | **79,0** | Nuevo en el tour, villano en vivo, datos etiquetados y núcleo técnico propio |
| ProbeGate | 6 | 8 | 3 | 9 | 6 | **65,5** | Muy técnico, ejecución arriesgada sin GPU |
| SafeBench-ES + LatamGPT | 8 | 6 | 8 | 5 | 6 | **64,5** | Categoría ausente en el tour y fácil de ejecutar, pero poco técnica y con riesgo de resultado nulo |
| Eval realism scorer | 8 | 7 | 4 | 7 | 6 | **63,5** | Nuevo, pero la métrica es frágil y la demo poco visible |
| Anti-vishing | 4 | 7 | 3 | 7 | 7 | **57,5** | SafeLine ya existió; audio en 10-12 h es arriesgado |
| Sandbox tripwires (solo) | 4 | 5 | 7 | 5 | 5 | **52,5** | Ya hay proyectos parecidos; sirve como componente |
| MCP TimeLock / Shield | 4 | 5 | 7 | 5 | 5 | **52,5** | Roxy e Ikarus ya son gateways MCP |
| Radar + harness | 2 | 6 | 6 | 6 | 5 | **52,0** | Agent Zero ya lo hizo; roza una línea roja |
| Qwen + decoding | 4 | 5 | 6 | 5 | 4 | **48,5** | La técnica no resuelve el incidente |
| Mandato y recibo (ScopeProof) | 2 | 5 | 6 | 6 | 4 | **48,0** | AP2, borradores IETF, Specter y Roxy |
| Harness en cascada | 2 | 4 | 8 | 5 | 4 | **47,5** | El patrón que más vio el jurado |
| Scheming radar | 3 | 5 | 7 | 4 | 4 | **46,5** | CLTR ya opera un observatorio |
| HF para evals | 3 | 5 | 7 | 4 | 4 | **46,5** | Inspect Evals ya cubre mucho |
| MemoryLineage | 2 | 5 | 5 | 5 | 4 | **43,5** | Provenance Firewall ya lo hizo |
| Benchmark hardener | 1 | 6 | 3 | 6 | 4 | **42,5** | El paper citado ya lo implementó |

## Qué ya vio el jurado en el tour

Leídos los README de los repos del tour (unos 20 declaran el track AI Security).

- **Patrón dominante:** un proxy, hook o gateway delante del agente, con reglas deterministas («el LLM no decide»), procedencia y un log encadenado y firmado. Ejemplos: [HAWK](https://github.com/platanus-hack/platanus-hack-26-ve-team-23), [Roxy](https://github.com/platanus-hack/platanus-hack-26-co-team-3), [Aegis](https://github.com/platanus-hack/platanus-hack-26-co-team-1), [Provenance Firewall](https://github.com/platanus-hack/platanus-hack-26-co-team-13), [Hackan't](https://github.com/platanus-hack/platanus-hack-26-ar-team-13), [wardlm](https://github.com/platanus-hack/platanus-hack-26-ar-team-7), [Specter](https://github.com/platanus-hack/platanus-hack-26-mx-team-37), [Ikarus](https://github.com/platanus-hack/platanus-hack-26-mx-team-2), [Tranquera](https://github.com/platanus-hack/platanus-hack-26-ar-team-22).
- **La vara de ejecución es alta:** [Agent Zero](https://github.com/platanus-hack/platanus-hack-26-ve-team-4) mostró 59/90 a 0/90 violaciones con 1.176 pruebas; HAWK usó hardware aparte; [Stegora](https://github.com/platanus-hack/platanus-hack-26-co-team-12) reportó recuperación de 100 % y 97 % con 0 falsos positivos.
- **Lo que nadie hizo:** evals, benchmarks, observatorios ni detección de trampas. El único de interpretabilidad fue [Verbalize](https://github.com/platanus-hack/platanus-hack-26-ar-team-3).
- **Cercanos a vigilar:** [yieldOS](https://github.com/platanus-hack/platanus-hack-26-ar-team-10) (contratos y oráculos para agentes de código) y [Owliver](https://github.com/platanus-hack/platanus-hack-26-mx-team-16) (pentest de chatbots con nota y canary token).

## Hallazgos por idea

### Detector de trampas en agentes de código (A1)

- **Corrección al brief:** el 7,8 a 14,1 % de AISI viene de evaluaciones de ciberseguridad, no de tareas de código ([AISI](https://www.aisi.gov.uk/blog/cheating-behaviour-in-frontier-model-evaluations)). Para código, la cifra es de ImpossibleBench: GPT-5 hace trampa en 54 % de las tareas imposibles tipo SWE-bench ([arXiv 2510.20270](https://arxiv.org/html/2510.20270v1)).
- **Qué existe:** jueces LLM dentro de benchmarks (ImpossibleBench, EvilGenie), reglas sobre diffs sin evaluar ([hone](https://github.com/kyu1204/hone/pull/24)) y hooks que fuerzan TDD ([TDD Guard](https://github.com/nizos/tdd-guard)). No encontré un hook o check de CI con precisión y recall publicados.
- **El hueco técnico:** la trampa que no toca los tests (código que reconoce el caso de prueba, `__eq__` sobrecargado). Ahí los monitores LLM detectan 42 a 65 % en SWE-bench, y el análisis estático solo cae a AUC 0,500 cuando los tests son de solo lectura ([HackTrace](https://arxiv.org/html/2610.03055v1)).
- **Datos etiquetados:** [ImpossibleBench](https://github.com/safety-research/impossiblebench) (toda corrida que pasa es trampa por construcción) y [Terminal Wrench](https://github.com/few-sh/terminal-wrench) (3.632 trayectorias de trampa y 1.216 legítimas).
- **Diseño posible en 10 a 12 h, tres capas:**
  1. Reglas sobre diff y AST: tests editados o borrados, `skip`, aserciones debilitadas, literales de los tests dentro del código.
  2. Replay causal: restaurar los tests originales desde git, correrlos contra el código del agente y sumar entradas perturbadas. Es el núcleo técnico y da evidencia de comportamiento.
  3. Juez LLM solo para lo ambiguo, con la evidencia de las capas 1 y 2.
  - Más un canal de canarios: valores señuelo en los tests visibles. Si aparecen en el código del agente, la trampa queda probada.
- **Frase del brief:** «Hoy los agentes de código hacen trampa: GPT-5 pasa el 54 % de tareas imposibles manipulando tests o escribiendo la respuesta esperada, y los monitores LLM detectan entre 42 y 65 % de esos casos. Construimos un detector de tres capas. En nuestra demo detecta X de Y corridas con menos de 5 % de falsas alarmas (número por medir). Si los equipos que delegan código a agentes y los institutos de seguridad lo adoptan, un "tests en verde" vuelve a significar algo.»
- **Cuidado:** contarlo como integridad de evaluaciones, no como otro guard delante de Claude Code.

### SafeBench-ES y report card de LatamGPT (B3 + D3)

- **Corrección al brief:** el 79 % de jailbreak no es de español. Viene de un estudio de 2023 con zulú, gaélico escocés, hmong y guaraní ([Yong et al.](https://arxiv.org/html/2310.02446v1)).
- **La brecha es chica con peticiones directas:** GPT-4o 4,0 % en ambos idiomas; solo aparece bajo ataque adversarial ([arXiv 2511.00689](https://arxiv.org/html/2511.00689v2)), que el brief prohíbe construir.
- **Competidor cercano:** [XL-SafetyBench](https://arxiv.org/html/2605.05662) incluye España y ningún país latinoamericano.
- **Lo que sí se sostiene:** LatamGPT no tiene evaluaciones de seguridad publicadas ([mapa del EA Forum](https://forum.effectivealtruism.org/posts/3sL6iB6WzKHJciwta/latin-america-in-search-of-its-stake-in-ai-safety-a-map)), y nadie midió guards en chileno ni coa.
- **No hay evidencia** de que LatamGPT esté desplegado en colegios o gobierno.
- **Se puede correr sin GPU:** [Featherless](https://featherless.ai/models/latam-gpt/Llama-3.1-70B-LatamGPT-SFT-1.0) lo sirve por API a 2,88 USD por millón de tokens (plan desde 50 USD al mes). Falta probar una llamada real.
- **Riesgo:** resultado nulo. Con 60 escenarios solo se defienden brechas de 15 puntos o más.

### Tripwires, hardener, scheming radar y mandato con recibo

- **Tripwires (A5):** ya existen [canaryhook](https://github.com/aiagentflow/canaryhook) y [honeypot-control](https://github.com/nathanpham8/honeypot-control). Sirve como componente del detector.
- **Benchmark hardener (A2):** el paper citado ya lo implementó ([harden-v0](https://github.com/few-sh/harden-v0)).
- **Scheming radar (A3):** la cifra de CLTR es correcta ([arXiv 2604.09104](https://arxiv.org/abs/2604.09104)), pero CLTR ya opera un observatorio con más de 1.600 incidentes y existe el [tracker de Eon](https://www.eon.io/rogue-ai-agent-tracker). Solo quedaría sumar GitHub y español.
- **Mandato y recibo (C2):** el artículo de FIDO citado no menciona a Citi. El prior art es amplio: [AP2](https://ap2-protocol.org/specification), Visa TAP, borradores IETF de recibos firmados, y Specter y Roxy en el tour.

## Mi lectura (opinión)

1. **Primera opción: detector de trampas con canarios.** Es la que mejor puntúa en lo que más pesa (técnico) y tiene villano en vivo: el agente borra el test o escribe la respuesta esperada y reporta éxito.
2. **Segunda opción: SafeBench-ES con LatamGPT.** Más simple y original, pero menos técnica. El titular tendría que ser «primer report card de seguridad de LatamGPT», no «los modelos fallan en español».
3. **Descartaría:** todo lo que sea un guard, proxy o gateway delante del agente.

## Sin verificar

- La definición oficial de cada criterio de la rúbrica.
- Los ganadores de las otras sedes del tour.
- Una llamada real a LatamGPT en Featherless.
- Que `impossiblebench` publique trayectorias listas: puede que haya que generar las corridas.
