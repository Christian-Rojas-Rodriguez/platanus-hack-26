# Notas de Jaime: ranking de propuestas

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Los puntajes son mi juicio, no una medición.

Todas las propuestas que hay hasta el 21-11-2026 (repo, reunión con el mentor y brief de Juanfe), con la categoría de la guía de Kairos en la que entran y un puntaje de 0 a 100 según la rúbrica del jurado: aspecto técnico 25 %, ambición 20 %, ejecución 20 %, impacto 20 %, originalidad 15 %. El desglose por criterio de las primeras 15 está en [investigacion-2-brief-y-rubrica.md](investigacion-2-brief-y-rubrica.md).

| # | Propuesta | Autor | Categoría Kairos | Puntos | Por qué |
|---|---|---|---|---|---|
| 1 | Detector de trampas + canarios | Brief de Juanfe | AI control | **79** | Nadie del tour lo hizo, villano en vivo, datos etiquetados y núcleo técnico propio |
| 2 | ProbeGate | Jaime | Interpretabilidad pragmática | **65,5** | Muy técnico, pero ejecución arriesgada sin GPU |
| 3 | SafeBench-ES + LatamGPT | Brief de Juanfe | Guardrails y robustez | **64,5** | Original y fácil de ejecutar; poco técnico y puede dar resultado nulo |
| 4 | Eval realism scorer | Brief de Juanfe | No encaja limpio (cercano a AI control) | **63,5** | Nuevo, pero la métrica es frágil y la demo poco visible |
| 5 | Anti-vishing | Jaime | Defensa (def/acc) | **57,5** | Wow alto; audio en 10-12 h es arriesgado y SafeLine ya existió |
| 6 | MCP-Shield + MCP-Arena | Jaime | AI control | **56,5** | Aporta un entorno nuevo a ControlArena, pero los gateways MCP ya se vieron |
| 7 | Sandbox tripwires | Brief de Juanfe | AI control | **52,5** | Ya hay proyectos parecidos; sirve como componente del detector |
| 7 | MCP TimeLock | Tomás | Guardrails y robustez | **52,5** | Roxy e Ikarus ya son gateways MCP |
| 7 | Agent Escape Lab | Tomás | AI control | **52,5** | Más investigación que producto; difícil mostrar resultado en el tiempo |
| 7 | Radar de jailbreaks en español | Jaime | Guardrails y robustez | **52,5** | Roza la línea roja del brief y la brecha en español es chica |
| 11 | Radar + harness | Jaime + Mauricio | Guardrails y robustez | **52** | Agent Zero ya hizo el mismo ciclo, con 1.176 pruebas |
| 11 | Anti-estafas por WhatsApp (descartada) | Jaime | Defensa (def/acc) | **52** | Fácil y clara, pero poco técnica y ya hay filtros |
| 13 | Qwen + constrained decoding | Reunión con mentor | AI control | **48,5** | La técnica no resuelve el incidente que usa de gancho |
| 14 | ScopeProof / mandato y recibo | Tomás / brief de Juanfe | AI control | **48** | AP2, borradores IETF, Specter y Roxy ya lo cubren |
| 15 | Harness en cascada | Mauricio | Guardrails y robustez | **47,5** | Es el patrón que más vio el jurado en el tour |
| 16 | Scheming radar | Brief de Juanfe | AI control | **46,5** | CLTR ya opera un observatorio; demo sin villano |
| 16 | «Hugging Face para evals» | Reunión con mentor | No encaja limpio (cercano a cyber evals) | **46,5** | Inspect Evals ya cubre mucho |
| 18 | MemoryLineage | Tomás | AI control | **43,5** | Provenance Firewall ya lo hizo en Bogotá |
| 18 | Agente con acceso total sin acciones peligrosas | Reunión con mentor | AI control | **43,5** | El mentor dijo que no se metería; difícil de demostrar |
| 20 | Benchmark hardener | Brief de Juanfe | No encaja limpio (cercano a cyber evals) | **42,5** | El paper citado ya lo implementó con código abierto |
| 21 | AI kitchen con interpretabilidad | Reunión con mentor | No califica como está | **39** | No resuelve un problema de seguridad |

Cómo leerla: la primera se despega por 13 puntos; del 2 al 4 y del 7 al 12 están casi empatadas, así que ahí el orden no significa mucho. Por categoría, 10 propuestas caen en AI control, 5 en guardrails, 2 en defensa, 1 en interpretabilidad y ninguna en cyber evals.
