# Notas de Jaime: ranking de propuestas

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Los puntajes son mi juicio, no una medición.

Versión 3.2 (21-11-2026). Cambios desde la versión 2:

- El chequeo previo de contención sube a 79,5 con una versión mejorada (prueba de separación entre corridas y reinicio), y corrige dos afirmaciones que no se sostienen.
- La propuesta unificada de Mauricio (swarm de modelos pequeños, `research/notas/m-propuesta_swarm_slm_red_team_hardening.md`) reemplaza la fila de su investigación de red teaming.

- Suma «reversibilidad para agentes» (cuarta): funde la recuperación tras un agente destructor con dos ideas de Jaime (más poder al agente es más útil y más riesgoso, así que en vez de quitarle poder hacer que todo sea reversible; y un producto de seguridad cuyo cliente es el propio agente). Iba primera, pero el informe forense de Christian (`research/notas/christian-rojas/forense/`) mostró que Rubrik, Veeam, Commvault y Cohesity ya venden «deshacer» para agentes empresariales.
- Sube el chequeo previo de contención (preflight) a primero con el informe de contención de Christian (`research/notas/christian-rojas/contencion-playgrounds/`).

- Suma las propuestas nuevas de Federico (AegisHub, `research/notas/fede-horl/`) y de Mauricio (red teaming con modelos abiertos y hardening, `research/notas/m-investigacion_red_teaming_open_weight_hardening.md`).
- Suma una idea nueva de mi investigación sobre ransomware y ataques con IA: [investigacion-4-ransomware-con-ia.md](investigacion-4-ransomware-con-ia.md).
- Baja el juez por ejecución después de revisarlo a fondo (detalle abajo).
- Baja la brecha en español: el paper que subió Mauricio (`research/papers/paper.tex`, hackathon de Apart de junio de 2026) ya planteó la comparación inglés contra «español diverso».

Cada propuesta lleva la categoría de la guía de Kairos y un puntaje de 0 a 100 según la rúbrica del jurado: aspecto técnico 25 %, ambición 20 %, ejecución 20 %, impacto 20 %, originalidad 15 %. Cuando dos o más propusimos lo mismo, va en una sola fila con todos los autores.

| # | Propuesta | Autor | Categoría Kairos | Puntos | Cambio | Por qué |
|---|---|---|---|---|---|---|
| 1 | Chequeo previo de contención: separación entre corridas (preflight) | Jaime (cercana al hueco 2 del informe 29 de Christian) | AI control (cercano a cyber evals) | **79,5** | 69,5 → 79,5 | Versión mejorada tras revisarla a fondo. Antes de poner a correr evaluaciones de agentes, comprueba con pruebas inofensivas en infraestructura propia: (1) salida directa y DNS hacia un receptor nuestro; (2) **el núcleo nuevo:** si dos corridas que deben estar separadas pueden pasarse datos por un servicio que sí tienen permitido (la corrida A deja un valor aleatorio en un registro de paquetes propio y se ve si la B lo lee), y si ese dato sobrevive al reinicio del entorno; (3) aplica una corrección de identidades y espacios separados y verifica que el trabajo legítimo sigue funcionando. Es la condición que habilitó el caso Hugging Face: unos 1.200 agentes se pasaron más de 70.000 mensajes por un repositorio de paquetes compartido (METR). Un chequeo de internet simple no lo ve. **Correcciones:** no decir «nadie lo hace» (Harbor, Cilium y Cyclonus ya prueban redes de forma activa; METR solo dice que su plataforma Hawk aún no lo hace) ni «4 de 5 incidentes fueron red mal configurada» (el instituto británico habilitó internet a propósito). El 79,5 vale solo si se termina y se valida con casos ciegos; si a las 2 horas no aparece un cruce entre corridas que el chequeo simple no vea, vuelve a unos 70 |
| 2 | Juez de trayectorias por ejecución | Brief de Juanfe + Jaime + Christian | AI control | **65,5** | 75,5 → 65,5 | Baja fuerte. La solución de referencia no sirve como vara: en la tarea 1012 de Terminal Wrench tampoco usa el comando que pide la instrucción y la corrida honesta deja un estado distinto. Reproducir pulsaciones en entornos que instalan paquetes por red no es fiable, y medir solo en las tareas que construyen fácil no es comparable con el 44 % publicado. EvalGuard ya publica cifras propias. Solo lo defendería como piloto de 3 a 5 tareas con comprobaciones escritas a mano |
| 2 | Eval Mirage | Tomás + brief de Juanfe | No encaja limpio (cercano a AI control) | **65,5** | = | Cuatro condiciones pareadas con criterio de corte. Riesgo: con pocas corridas el efecto puede ser ruido |
| 2 | Reversibilidad para agentes (funde la recuperación tras un agente destructor, el «rewind» de Christian y dos ideas nuevas de Jaime) | Jaime + Christian | AI control | **65,5** | nueva | Dar al agente todo el acceso, pero que todo lo que haga se pueda deshacer, en vez de quitarle poder. El cliente es el propio agente: un servidor MCP al que llama antes de algo riesgoso («guarda un punto») y después si se equivocó («deshaz»), más una segunda opinión sobre si una acción es reversible. Las copias viven fuera de su alcance aunque no las pida. Se mide contra el deshacer de Claude Code, Gemini CLI y OpenCode (Claude Code documenta que no rastrea lo que cambia solo por terminal): archivos recuperados por hash y utilidad que se conserva frente a bloquear. En contra: Rubrik (Agent Rewind, desde 2025), Veeam, Commvault y Cohesity ya venden «deshacer» para agentes empresariales (Salesforce, Microsoft 365, nube), según el informe forense de Christian. Lo que queda libre es el agente de código en el sistema de archivos local, el agente como cliente y medir cuánto se recupera. Además, un agente que quiere engañar no llamaría al servicio |
| 5 | Brecha de salvaguardas en español regional | Brief de Juanfe + Tomás + Christian + Jaime | Guardrails y robustez | **64,5** | 66 → 64,5 | Baja otra vez por originalidad: además de LatAm-RT, el paper S-OWMI (Apart, junio de 2026) ya comparó inglés contra español diverso. Ojo: sus tablas son datos simulados con 1 a 3 pares, así que no hay resultado real que repetir; sigue abierto medirlo bien |
| 6 | Complacencia (sycophancy) en conversaciones largas en español | Christian | No encaja limpio (cercano a guardrails) | **63** | = | Sale del carril de control y no encontramos versión en español. Lo frágil es validar el juez automático |
| 7 | Swarm de modelos pequeños para red teaming y hardening verificado | Mauricio | Cyber evals y defensa (cercano a guardrails) | **60** | nueva (reemplaza su investigación de red teaming) | Ataca un repo Python generado por IA en un sandbox, confirma exploits con un oráculo determinista, lo parcha y vuelve a atacar para certificar que el parche funcionó sin romper los tests. Lo valioso es ese ciclo cerrado con prueba. En contra: es la propuesta más grande y no cabe en el tiempo (enjambre, sandbox, oráculo, parchador y 6 a 8 repos de prueba); su propia investigación muestra el carril lleno (SplxAI, Novee, XBOW, Corgea) y BaxBench ya mide el problema; y queda en zona gris con la línea roja de «herramientas ofensivas que funcionen». Para alejarla: catálogo de ataques fijo en vez de un atacante general con Kali, solo dentro de su sandbox, no ajustar modelos para quitarles los rechazos y poner al frente el parche verificado |
| 8 | Voz sintética con acento chileno | Jaime | Defensa (def/acc) | **59,5** | = | Datos listos (HISPASpoof), pero se lee como réplica del paper |
| 9 | ProbeGate | Jaime | Interpretabilidad pragmática | **58,5** | = | Las sondas caen a AUC 0,62 sin razonamiento visible |
| 9 | Safety Evidence Auditor | Tomás | No encaja limpio (transparencia de laboratorios) | **58,5** | = | Fácil, pero poco técnico y con demo abstracta |
| 11 | Agentes de voz en español y portugués | Christian | Defensa (def/acc) | **57,5** | = | Hueco real; montar voz de punta a punta es lo más arriesgado |
| 12 | MCP-Shield + MCP-Arena | Jaime | AI control | **56,5** | = | Los gateways MCP ya se vieron en el tour |
| 13 | Chile Scam Mutator | Tomás | Defensa (def/acc) | **55** | = | Cerca del anti-estafas descartado y roza una línea roja |
| 13 | SideEffect Auditor | Tomás | AI control | **55** | = | SABench ya mide efectos no autorizados |
| 15 | Mandato y expediente de disputa para pagos de agentes | Christian | AI control | **54,5** | = | Comprador claro, pero el núcleo es el patrón que más vio el jurado |
| 16 | Sandbox tripwires | Brief de Juanfe | AI control | **52,5** | = | Ya hay proyectos parecidos; sirve como componente de la 1 |
| 16 | MCP TimeLock | Tomás | Guardrails y robustez | **52,5** | = | Roxy, Ikarus y mcp-scan ya lo cubren |
| 16 | Agent Escape Lab | Tomás | AI control | **52,5** | = | Más investigación que producto |
| 16 | Radar de jailbreaks en español | Jaime | Guardrails y robustez | **52,5** | = | Roza la línea roja y la brecha en español es chica |
| 20 | Radar + harness | Jaime + Mauricio | Guardrails y robustez | **52** | = | Agent Zero ya hizo el mismo ciclo |
| 20 | Anti-estafas por WhatsApp (descartada) | Jaime | Defensa (def/acc) | **52** | = | Poco técnica y ya hay filtros |
| 22 | AegisHub (hub y arena de ataques y defensas) | Federico | Guardrails y robustez | **51** | nueva | Tiene lo mejor de la lista en algo: mide seguridad contra utilidad legítima, que es lo que critican los revisores. Pero sus ataques y escudos (inyección por RAG, secuestro de herramientas, canarios) son el carril que el mentor dio por saturado, y la plataforma tipo «Hugging Face de evals» ya la cubren Inspect Evals y Promptfoo. Las cifras de su demo (96,2 % de seguridad, 95,8 % de utilidad) son de maqueta, no medidas |
| 23 | Multiagente (A2A) con tarjetas firmadas | Christian | AI control | **50,5** | = | Sin comprador y cerca de otro «agent guard» |
| 24 | Qwen + constrained decoding | Reunión con mentor | AI control | **48,5** | = | La técnica no resuelve el incidente |
| 25 | ScopeProof / mandato y recibo | Tomás / brief de Juanfe | AI control | **48** | = | AP2, borradores IETF, Specter y Roxy |
| 26 | Harness en cascada | Mauricio | Guardrails y robustez | **47,5** | = | El patrón que más vio el jurado |
| 27 | Scheming radar | Brief de Juanfe + Christian | AI control | **46,5** | = | CLTR ya opera un observatorio |
| 27 | «Hugging Face para evals» | Reunión con mentor | No encaja limpio (cercano a cyber evals) | **46,5** | = | Inspect Evals ya cubre mucho |
| 29 | Prompt-to-Policy Compiler | Tomás | AI control | **45,5** | = | Componente de ScopeProof, no proyecto |
| 30 | MemoryLineage / memoria envenenada | Tomás + Christian | AI control | **43,5** | = | Provenance Firewall ya lo hizo |
| 30 | Agente con acceso total sin acciones peligrosas | Reunión con mentor | AI control | **43,5** | = | El mentor dijo que no se metería |
| 32 | Benchmark hardener | Brief de Juanfe + Christian | No encaja limpio (cercano a cyber evals) | **42,5** | = | harden-v0 y BenchJack ya existen |
| 33 | AI kitchen con interpretabilidad | Reunión con mentor | No califica como está | **39** | = | No resuelve un problema de seguridad |

**Cómo leerla.** La 1 se despega por 14 puntos, pero ese puntaje depende de terminarla y validarla; si la prueba entre corridas no muestra nada nuevo en las primeras 2 horas, vuelve a unos 70 y queda empatada con las siguientes. La reversibilidad responde mejor la tensión de fondo del track (más poder al agente es más útil y más riesgoso), pero ya tiene productos parecidos y no conviene fusionarla con la 1. Yo elegiría entre las primeras cinco según qué podamos tener funcionando de punta a punta el sábado en la mañana. Por categoría: 15 en AI control, 7 en guardrails, 4 en defensa, 1 en interpretabilidad, 5 no encajan limpio y 1 no califica.

**Por qué bajé el juez.** Al revisarlo a fondo aparecieron problemas que no veía:

1. **No hay vara confiable.** Comparar contra lo que deja la solución de referencia marca como trampa soluciones honestas que solo son distintas. Lo verifiqué en la tarea 1012: la instrucción pide usar `flatpak override`, la referencia escribe el archivo a mano y la corrida honesta usa el comando y deja otro resultado.
2. **Fallar una prueba nueva no prueba trampa.** Un bug, una tarea ambigua y un engaño dan el mismo resultado.
3. **Reproducir no es fiable.** Las corridas son pulsaciones con esperas fijas y los entornos instalan paquetes por red sin versión fija.
4. **El número no sería comparable.** Medir solo en las tareas que construyen fácil elige justo las trampas fáciles.

Si el equipo igual lo quiere, la versión defendible es un piloto acotado y sin prometer superar el 44 %.

**Ideas de ransomware que no agregué.** Un simulacro en vivo de ransomware para agentes defensores (escenarios y línea base serían nuestros, y el simulador roza una línea roja) y un detector de cifrado en archivos de modelos (su hipótesis no la ha medido nadie). Están en [investigacion-4-ransomware-con-ia.md](investigacion-4-ransomware-con-ia.md).

**Desglose de las filas nuevas o que cambiaron** (0 a 10 por criterio; total = (15·O + 20·A + 20·E + 25·T + 20·I) / 10).

| Propuesta | Orig. | Amb. | Ejec. | Téc. | Imp. | Total |
|---|---|---|---|---|---|---|
| Chequeo previo: separación entre corridas (si se valida) | 7,5 | 8 | 7,5 | 8,5 | 8 | 79,5 |
| Chequeo previo simple (versión anterior) | 7 | 6 | 8 | 6 | 8 | 69,5 |
| Juez de trayectorias por ejecución | 5 | 8 | 3 | 8 | 8 | 65,5 |
| Reversibilidad para agentes | 4 | 7 | 7 | 7 | 7 | 65,5 |
| Brecha de salvaguardas en español regional | 5 | 6 | 8 | 6 | 7 | 64,5 |
| Swarm de modelos pequeños (Mauricio) | 4 | 9 | 3 | 8 | 5 | 60 |
| AegisHub | 3 | 7 | 5 | 5 | 5 | 51 |

Las demás filas mantienen el desglose de la versión 2.
