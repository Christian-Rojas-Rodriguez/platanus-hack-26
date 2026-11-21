# Notas de Jaime: ranking de propuestas

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Los puntajes son mi juicio, no una medición.

Versión 2 (21-11-2026). Suma las ideas nuevas de Tomás (`docs/t/final-ideas/` y `docs/t/project-pitches.md`) y de Christian (`research/notas/christian-rojas/mercado/`, sobre todo los informes 29, 31, 32 y 33), y ajusta los puntajes con mi tercera investigación ([investigacion-3-problemas-mundiales.md](investigacion-3-problemas-mundiales.md)).

Cada propuesta lleva la categoría de la guía de Kairos en la que entra y un puntaje de 0 a 100 según la rúbrica del jurado: aspecto técnico 25 %, ambición 20 %, ejecución 20 %, impacto 20 %, originalidad 15 %. Cuando dos o más propusimos lo mismo, lo dejé en una sola fila con todos los autores.

| # | Propuesta | Autor | Categoría Kairos | Puntos | Cambio | Por qué |
|---|---|---|---|---|---|---|
| 1 | Juez de trayectorias por ejecución (antes «detector de trampas + canarios») | Brief de Juanfe + Jaime + Christian | AI control | **75,5** | 79 → 75,5 | Sigue primera. Baja porque las reglas sobre el diff ya existen en seis repos y montar contenedores es riesgo real. El hueco medido sigue abierto: el mejor juez publicado detecta 44 % cuando el agente no cuenta lo que hizo. Christian llegó a lo mismo por separado (su problema n.º 1) |
| 2 | Preflight de contención para evaluaciones | Jaime (cercana al hueco 2 del informe 29 de Christian) | AI control (cercano a cyber evals) | **67** | nueva | Tiene el mejor villano de 2026 (agentes que salieron a internet desde las evaluaciones de los laboratorios). Débil en la métrica: se mide sobre fallas plantadas por uno mismo |
| 3 | Brecha de salvaguardas en español regional (SafeBench-ES + LatamGPT, LatAm Safety Gate, brecha dialectal y boleta de LatamGPT) | Brief de Juanfe + Tomás + Christian + Jaime | Guardrails y robustez | **66** | 64,5 → 66 | Los tres llegamos a la misma idea. Sube por el diseño con pares y gemelos benignos, que da resultado aunque la brecha sea chica. No sube más porque ya existe LatAm-RT (incluye Chile, 284 prompts, 5 modelos); lo nuevo sería medir guardias, sobre-rechazo, escritura coloquial y LatamGPT |
| 4 | Eval Mirage (antes «eval realism scorer») | Tomás + brief de Juanfe | No encaja limpio (cercano a AI control) | **65,5** | 63,5 → 65,5 | Tomás lo aterrizó en cuatro condiciones pareadas con criterio de corte. La demanda es real (los modelos notan cada vez más que los evalúan). Riesgo: con 8 corridas por condición el resultado puede ser ruido |
| 5 | Complacencia (sycophancy) en conversaciones largas en español | Christian | No encaja limpio (cercano a guardrails) | **63** | nueva | Sale del carril de control, no encontramos versión en español y se arma sobre Petri o Inspect. Lo más frágil es validar el juez automático |
| 6 | Voz sintética con acento chileno (antes «anti-vishing») | Jaime | Defensa (def/acc) | **59,5** | 57,5 → 59,5 | Hay datos listos con acento chileno (HISPASpoof). Se lee como réplica del paper y no hay cifra oficial chilena de fraude con voz clonada |
| 7 | ProbeGate | Jaime | Interpretabilidad pragmática | **58,5** | 65,5 → 58,5 | Baja: las sondas caen a AUC 0,62 cuando no hay razonamiento visible, y un resultado negativo de 2026 muestra que una coincidencia de texto logra lo mismo |
| 7 | Safety Evidence Auditor (con Evidence-to-Experiment Compiler) | Tomás | No encaja limpio (transparencia de laboratorios) | **58,5** | nueva | Fácil de ejecutar y en un carril que el brief da por abierto. Poco técnico, demo abstracta y ya hay rastreadores de compromisos (Watchtower, Seoul Tracker) |
| 9 | Banco de pruebas para agentes de voz en español y portugués | Christian | Defensa (def/acc) | **57,5** | nueva | Hueco real y sin proveedor dedicado. Montar voz de punta a punta en el tiempo que hay es lo más arriesgado de la lista |
| 10 | MCP-Shield + MCP-Arena | Jaime | AI control | **56,5** | = | Aporta un entorno nuevo a ControlArena, pero los gateways MCP ya se vieron |
| 11 | Chile Scam Mutator | Tomás | Defensa (def/acc) | **55** | nueva | Demo clara y rápida. Queda cerca del anti-estafas que descartamos, Agent Zero ya hizo el ciclo ataque y regla, y generar variantes de estafas roza una línea roja del brief |
| 11 | SideEffect Auditor | Tomás | AI control | **55** | nueva | Buena pregunta (qué más cambió el agente además de la tarea), pero SABench ya mide efectos no autorizados |
| 13 | Mandato y expediente de disputa para pagos de agentes, cuenta a cuenta | Christian | AI control | **54,5** | nueva | Es la recomendación de Christian y tiene comprador claro. El núcleo (validación determinista más recibos firmados) es el patrón que más vio el jurado; lo distinto es el ángulo regional de las transferencias instantáneas |
| 14 | Sandbox tripwires | Brief de Juanfe | AI control | **52,5** | = | Ya hay proyectos parecidos (hackbait, Tracebit); sirve como componente de la 1 o la 2 |
| 14 | MCP TimeLock | Tomás | Guardrails y robustez | **52,5** | = | Roxy e Ikarus ya son gateways MCP, y mcp-scan fija herramientas por hash desde 2025 |
| 14 | Agent Escape Lab | Tomás | AI control | **52,5** | = | Más investigación que producto; difícil mostrar resultado en el tiempo |
| 14 | Radar de jailbreaks en español | Jaime | Guardrails y robustez | **52,5** | = | Roza la línea roja del brief y la brecha en español es chica |
| 18 | Radar + harness | Jaime + Mauricio | Guardrails y robustez | **52** | = | Agent Zero ya hizo el mismo ciclo, con 1.176 pruebas |
| 18 | Anti-estafas por WhatsApp (descartada) | Jaime | Defensa (def/acc) | **52** | = | Fácil y clara, pero poco técnica y ya hay filtros |
| 20 | Seguridad multiagente (A2A) con tarjetas firmadas | Christian | AI control | **50,5** | nueva | Vacío de verdad, pero todavía sin comprador y es lo más parecido a otro «agent guard» |
| 21 | Reversión de acciones de agentes («rewind») | Christian | AI control | **49,5** | nueva | El propio Christian la pone tercera: el carril de control en ejecución tiene cientos de proveedores |
| 22 | Qwen + constrained decoding | Reunión con mentor | AI control | **48,5** | = | La técnica no resuelve el incidente que usa de gancho |
| 23 | ScopeProof / mandato y recibo | Tomás / brief de Juanfe | AI control | **48** | = | AP2, borradores IETF, Specter y Roxy ya lo cubren |
| 24 | Harness en cascada | Mauricio | Guardrails y robustez | **47,5** | = | Es el patrón que más vio el jurado en el tour |
| 25 | Scheming radar (observatorio de incidentes) | Brief de Juanfe + Christian | AI control | **46,5** | = | CLTR ya opera un observatorio; demo sin villano |
| 25 | «Hugging Face para evals» | Reunión con mentor | No encaja limpio (cercano a cyber evals) | **46,5** | = | Inspect Evals ya cubre mucho |
| 27 | Prompt-to-Policy Compiler | Tomás | AI control | **45,5** | nueva | Tomás mismo lo ve como componente de ScopeProof, no como proyecto |
| 28 | MemoryLineage / memoria envenenada | Tomás + Christian | AI control | **43,5** | = | Provenance Firewall ya lo hizo en Bogotá |
| 28 | Agente con acceso total sin acciones peligrosas | Reunión con mentor | AI control | **43,5** | = | El mentor dijo que no se metería; difícil de demostrar |
| 30 | Benchmark hardener / auditor de benchmarks hackeables | Brief de Juanfe + Christian | No encaja limpio (cercano a cyber evals) | **42,5** | = | Ya existe con código abierto (harden-v0 y BenchJack, que reporta 219 fallas en 10 benchmarks) |
| 31 | AI kitchen con interpretabilidad | Reunión con mentor | No califica como está | **39** | = | No resuelve un problema de seguridad |

**Cómo leerla.** La primera se despega por 8,5 puntos. Del 2 al 5 están a cuatro puntos entre sí, así que ahí el orden no significa mucho. Por categoría: 15 propuestas caen en AI control, 5 en guardrails, 4 en defensa, 1 en interpretabilidad, 5 no encajan limpio y 1 no califica. Ninguna entra de lleno en cyber evals.

**Dónde no coincido con mis compañeros, para discutirlo.**

- **Tomás descarta el detector de trampas** por ser una dirección ya cubierta. Mi investigación le da la razón en parte: las reglas sobre el diff ya están hechas. Pero el hueco medido sigue abierto en el caso que importa, cuando la trampa no toca los tests ni se anuncia. Por eso lo reformulo en vez de descartarlo, y el informe 31 de Christian lo deja como el espacio más vacío de su matriz.
- **Christian recomienda el mandato para pagos.** Lo puntúo más bajo porque el mentor avisó que el carril de reglas deterministas más recibos firmados está saturado, y en el tour hubo cuatro proyectos parecidos.
- **Las tres ideas finales de Tomás** quedan entre 55 y 66 en mi tabla. La que mejor puntúa es su LatAm Safety Gate, que fusioné con la fila 3.

**Desglose de las filas nuevas o que cambiaron** (0 a 10 por criterio; total = (15·O + 20·A + 20·E + 25·T + 20·I) / 10).

| Propuesta | Orig. | Amb. | Ejec. | Téc. | Imp. | Total |
|---|---|---|---|---|---|---|
| Juez de trayectorias por ejecución | 6 | 8 | 6 | 9 | 8 | 75,5 |
| Preflight de contención | 8 | 6 | 7 | 6 | 7 | 67 |
| Brecha de salvaguardas en español regional | 6 | 6 | 8 | 6 | 7 | 66 |
| Eval Mirage | 8 | 7 | 5 | 7 | 6 | 65,5 |
| Complacencia en español | 7 | 6 | 7 | 5 | 7 | 63 |
| Voz sintética con acento chileno | 4 | 6 | 6 | 7 | 6 | 59,5 |
| ProbeGate | 6 | 7 | 4 | 7 | 5 | 58,5 |
| Safety Evidence Auditor | 7 | 6 | 8 | 4 | 5 | 58,5 |
| Agentes de voz en español y portugués | 7 | 7 | 3 | 6 | 6 | 57,5 |
| Chile Scam Mutator | 3 | 5 | 8 | 5 | 6 | 55 |
| SideEffect Auditor | 4 | 6 | 6 | 6 | 5 | 55 |
| Mandato y disputa para pagos | 4 | 6 | 6 | 5 | 6 | 54,5 |
| Multiagente (A2A) | 5 | 6 | 4 | 6 | 4 | 50,5 |
| Reversión de acciones | 3 | 6 | 5 | 6 | 4 | 49,5 |
| Prompt-to-Policy Compiler | 2 | 4 | 7 | 5 | 4 | 45,5 |
