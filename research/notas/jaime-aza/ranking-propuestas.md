# Notas de Jaime: ranking de propuestas

> **Opinión personal de Jaime para discutir, no una decisión del equipo.** Los puntajes son mi juicio, no una medición.

Versión 4.1 (21-11-2026). Ahora también miro las ideas como producto y pitch: que un mentor se vea reflejado pesa en impacto. Cambios:

- Revisé a fondo la red de seguridad y el swarm, y puntué las versiones acotadas que caben en el tiempo: la red de seguridad sube a 76 y queda primera, el swarm queda en 72, y una combinación mínima de las dos en 73,5. Medio punto de diferencia no es significativo: decide lo que funcione en las primeras 2 horas.

- Suma la «red de seguridad para agentes de código», que funde la reversibilidad con el juez de trampas en vivo.
- La propuesta de Mauricio sube a 71,5: los organizadores confirmaron que el uso ofensivo sobre sistemas propios está permitido, y su pitch de prevención conecta con cualquier startup. La investigación sobre modelos pequeños ([investigacion-5-slm-vs-frontera.md](investigacion-5-slm-vs-frontera.md)) recomienda un esquema híbrido en vez de un swarm de modelos pequeños ajustados.
- El chequeo previo baja a 75,5: técnicamente es la mejor, pero su comprador son laboratorios y ningún mentor vive ese problema.

Cambios anteriores (versión 3.x):

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
| 1 | Red de seguridad para agentes de código (versión acotada) | Jaime + Christian (funde la reversibilidad y el juez en vivo) | AI control | **76** | 72,5 → 76 | El problema que cualquier mentor vivió: el agente dice «listo, los tests pasan» y no es cierto, o rompe archivos y no hay cómo volver atrás. **Versión acotada, tras revisarla a fondo:** el agente trabaja en una copia aislada dentro de un contenedor; un supervisor en el host, fuera de su alcance, guarda el estado inicial; al cerrar la sesión corre los tests originales en un entorno limpio con el runner y la configuración fijados (no basta proteger `tests/`: `conftest.py`, `pytest.ini` o el propio código pueden fingir éxito), recupera archivos borrados por terminal y solo integra lo aceptado, sin pisar cambios del humano. Un solo agente, Python, tres repos y unas doce sesiones. **Líneas base reales:** el checkpoint de Claude Code (su documentación dice que no rastrea archivos cambiados solo por Bash), commit previo más restore de Git, y copia aislada más pytest normal. **Correcciones:** no decir que nadie lo hace (Rubrik Agent Cloud muestra el caso de un agente de código; git-safepoint ya captura y restaura archivos), ni «el agente mintió» (se detectan incumplimientos, no intenciones), ni «dale todo el poder» (es poder amplio dentro de una frontera; correos, pushes o datos enviados no se deshacen). **Puerta a las 2 horas:** si solo funciona porque el agente coopera o el validador usa el runner que el agente puede tocar, se descarta |
| 2 | Chequeo previo de contención: separación entre corridas (preflight) | Jaime (cercana al hueco 2 del informe 29 de Christian) | AI control (cercano a cyber evals) | **75,5** | 69,5 → 75,5 | Versión mejorada tras revisarla a fondo. Antes de poner a correr evaluaciones de agentes, comprueba con pruebas inofensivas en infraestructura propia: (1) salida directa y DNS hacia un receptor nuestro; (2) **el núcleo nuevo:** si dos corridas que deben estar separadas pueden pasarse datos por un servicio que sí tienen permitido (la corrida A deja un valor aleatorio en un registro de paquetes propio y se ve si la B lo lee), y si ese dato sobrevive al reinicio del entorno; (3) aplica una corrección de identidades y espacios separados y verifica que el trabajo legítimo sigue funcionando. Es la condición que habilitó el caso Hugging Face: unos 1.200 agentes se pasaron más de 70.000 mensajes por un repositorio de paquetes compartido (METR). Un chequeo de internet simple no lo ve. **Correcciones:** no decir «nadie lo hace» (Harbor, Cilium y Cyclonus ya prueban redes de forma activa; METR solo dice que su plataforma Hawk aún no lo hace) ni «4 de 5 incidentes fueron red mal configurada» (el instituto británico habilitó internet a propósito). Baja de 79,5 a 75,5 al mirarla como producto: el comprador son unos 30 a 50 laboratorios y evaluadores, y ningún mentor fundador de startup vive este problema, así que el pitch no conecta. El 75,5 vale solo si se termina y se valida con casos ciegos; si a las 2 horas no aparece un cruce entre corridas que el chequeo simple no vea, vuelve a unos 70 |
| 3 | Combinación mínima: supervisor de la red de seguridad más una prueba de seguridad existente | Jaime + Christian + Mauricio | AI control y defensa | **73,5** | nueva | Une la 1 y la 2 bajo «el código que escribe tu agente no es confiable»: el supervisor corre la suite protegida y además una prueba de autorización ya escrita sobre una API; si falla, rechaza el cambio y conserva los archivos originales. Mejor relato, pero menos probable de terminar con una evaluación convincente. A la hora 6 debe cerrar el ciclo completo o se vuelve a la red de seguridad sola |
| 4 | Swarm de red teaming y hardening verificado, en esquema híbrido | Mauricio | Cyber evals y defensa | **72** | 60 → 72 | Prevención para startups y pymes: ataca su repo generado por IA dentro de un sandbox propio, confirma cada exploit con un oráculo determinista, lo parcha y vuelve a atacar para certificar que el parche funciona sin romper los tests. Pitch: las empresas no hacen este red teaming y por eso son vulnerables (en Reino Unido solo 10 % de las microempresas y 21 % de las pequeñas hizo un pentest el último año; cerca del 50 % de los backends generados por modelos que pasan sus tests son explotables según BaxBench). Sube porque los organizadores confirmaron que el uso ofensivo sobre sistemas propios está permitido y porque cualquier mentor que programa con IA se ve reflejado. **Cambio de diseño por la investigación:** no un swarm de modelos pequeños ajustados. En ataques de varios pasos el mejor modelo pequeño publicado ronda 15 a 20 % en Cybench frente a 46 % de Claude Sonnet 4.5, en AIxCC ningún finalista parchó con un modelo pequeño, y ajustar uno en 24 horas no es realista. Mejor híbrido: modelos de frontera por API para explotar y parchar, modelos abiertos ya ajustados (`fdtn-ai/Foundation-Sec-8B-Reasoning`, `DeepHat/DeepHat-V1-7B`) para triage local y respaldo cuando la frontera se niegue. Lo diferencial es el oráculo que certifica exploit y parche, no el modelo. En contra: el carril tiene empresas (XBOW, Novee, Corgea, RunSybil) y es la propuesta más grande; hay que recortarla a un catálogo fijo de ataques y 3 a 4 repos **Versión acotada, tras revisarla a fondo:** solo APIs Python de un framework, máximo tres repos tomados de BaxBench (con procedencia) y dos familias de ataque (autorización por recurso y acceso indebido a archivos); un modelo de frontera propone ataques y parches, un controlador determinista levanta una copia limpia por ensayo y decide; sin swarm, sin MCP ni hardening de sistema operativo. **Línea base:** reparación con un agente de frontera sin el ciclo dinámico, evaluada con ataques reservados. **Corrección:** el oráculo determinista con reintento tras el arreglo no es diferencial, XBOW y Corgea ya lo anuncian; y la cifra de 10 % y 21 % de pentest en empresas británicas no se pudo confirmar en la fuente primaria. Con 10 ataques fallidos solo se puede decir que la tasa de éxito es menor a 26 % con 95 % de confianza, no cero |
| 5 | Juez de trayectorias por ejecución | Brief de Juanfe + Jaime + Christian | AI control | **65,5** | 75,5 → 65,5 | Baja fuerte. La solución de referencia no sirve como vara: en la tarea 1012 de Terminal Wrench tampoco usa el comando que pide la instrucción y la corrida honesta deja un estado distinto. Reproducir pulsaciones en entornos que instalan paquetes por red no es fiable, y medir solo en las tareas que construyen fácil no es comparable con el 44 % publicado. EvalGuard ya publica cifras propias. Solo lo defendería como piloto de 3 a 5 tareas con comprobaciones escritas a mano |
| 5 | Eval Mirage | Tomás + brief de Juanfe | No encaja limpio (cercano a AI control) | **65,5** | = | Cuatro condiciones pareadas con criterio de corte. Riesgo: con pocas corridas el efecto puede ser ruido |
| 5 | Reversibilidad para agentes (funde la recuperación tras un agente destructor, el «rewind» de Christian y dos ideas nuevas de Jaime) | Jaime + Christian | AI control | **65,5** | nueva | Dar al agente todo el acceso, pero que todo lo que haga se pueda deshacer, en vez de quitarle poder. El cliente es el propio agente: un servidor MCP al que llama antes de algo riesgoso («guarda un punto») y después si se equivocó («deshaz»), más una segunda opinión sobre si una acción es reversible. Las copias viven fuera de su alcance aunque no las pida. Se mide contra el deshacer de Claude Code, Gemini CLI y OpenCode (Claude Code documenta que no rastrea lo que cambia solo por terminal): archivos recuperados por hash y utilidad que se conserva frente a bloquear. En contra: Rubrik (Agent Rewind, desde 2025), Veeam, Commvault y Cohesity ya venden «deshacer» para agentes empresariales (Salesforce, Microsoft 365, nube), según el informe forense de Christian. Lo que queda libre es el agente de código en el sistema de archivos local, el agente como cliente y medir cuánto se recupera. Además, un agente que quiere engañar no llamaría al servicio |
| 8 | Brecha de salvaguardas en español regional | Brief de Juanfe + Tomás + Christian + Jaime | Guardrails y robustez | **64,5** | 66 → 64,5 | Baja otra vez por originalidad: además de LatAm-RT, el paper S-OWMI (Apart, junio de 2026) ya comparó inglés contra español diverso. Ojo: sus tablas son datos simulados con 1 a 3 pares, así que no hay resultado real que repetir; sigue abierto medirlo bien |
| 9 | Complacencia (sycophancy) en conversaciones largas en español | Christian | No encaja limpio (cercano a guardrails) | **63** | = | Sale del carril de control y no encontramos versión en español. Lo frágil es validar el juez automático |
| 10 | Voz sintética con acento chileno | Jaime | Defensa (def/acc) | **59,5** | = | Datos listos (HISPASpoof), pero se lee como réplica del paper |
| 11 | ProbeGate | Jaime | Interpretabilidad pragmática | **58,5** | = | Las sondas caen a AUC 0,62 sin razonamiento visible |
| 11 | Safety Evidence Auditor | Tomás | No encaja limpio (transparencia de laboratorios) | **58,5** | = | Fácil, pero poco técnico y con demo abstracta |
| 13 | Agentes de voz en español y portugués | Christian | Defensa (def/acc) | **57,5** | = | Hueco real; montar voz de punta a punta es lo más arriesgado |
| 14 | MCP-Shield + MCP-Arena | Jaime | AI control | **56,5** | = | Los gateways MCP ya se vieron en el tour |
| 15 | Chile Scam Mutator | Tomás | Defensa (def/acc) | **55** | = | Cerca del anti-estafas descartado y roza una línea roja |
| 15 | SideEffect Auditor | Tomás | AI control | **55** | = | SABench ya mide efectos no autorizados |
| 17 | Mandato y expediente de disputa para pagos de agentes | Christian | AI control | **54,5** | = | Comprador claro, pero el núcleo es el patrón que más vio el jurado |
| 18 | Sandbox tripwires | Brief de Juanfe | AI control | **52,5** | = | Ya hay proyectos parecidos; sirve como componente de la 1 |
| 18 | MCP TimeLock | Tomás | Guardrails y robustez | **52,5** | = | Roxy, Ikarus y mcp-scan ya lo cubren |
| 18 | Agent Escape Lab | Tomás | AI control | **52,5** | = | Más investigación que producto |
| 18 | Radar de jailbreaks en español | Jaime | Guardrails y robustez | **52,5** | = | Roza la línea roja y la brecha en español es chica |
| 22 | Radar + harness | Jaime + Mauricio | Guardrails y robustez | **52** | = | Agent Zero ya hizo el mismo ciclo |
| 22 | Anti-estafas por WhatsApp (descartada) | Jaime | Defensa (def/acc) | **52** | = | Poco técnica y ya hay filtros |
| 24 | AegisHub (hub y arena de ataques y defensas) | Federico | Guardrails y robustez | **51** | nueva | Tiene lo mejor de la lista en algo: mide seguridad contra utilidad legítima, que es lo que critican los revisores. Pero sus ataques y escudos (inyección por RAG, secuestro de herramientas, canarios) son el carril que el mentor dio por saturado, y la plataforma tipo «Hugging Face de evals» ya la cubren Inspect Evals y Promptfoo. Las cifras de su demo (96,2 % de seguridad, 95,8 % de utilidad) son de maqueta, no medidas |
| 25 | Multiagente (A2A) con tarjetas firmadas | Christian | AI control | **50,5** | = | Sin comprador y cerca de otro «agent guard» |
| 26 | Qwen + constrained decoding | Reunión con mentor | AI control | **48,5** | = | La técnica no resuelve el incidente |
| 27 | ScopeProof / mandato y recibo | Tomás / brief de Juanfe | AI control | **48** | = | AP2, borradores IETF, Specter y Roxy |
| 28 | Harness en cascada | Mauricio | Guardrails y robustez | **47,5** | = | El patrón que más vio el jurado |
| 29 | Scheming radar | Brief de Juanfe + Christian | AI control | **46,5** | = | CLTR ya opera un observatorio |
| 29 | «Hugging Face para evals» | Reunión con mentor | No encaja limpio (cercano a cyber evals) | **46,5** | = | Inspect Evals ya cubre mucho |
| 31 | Prompt-to-Policy Compiler | Tomás | AI control | **45,5** | = | Componente de ScopeProof, no proyecto |
| 32 | MemoryLineage / memoria envenenada | Tomás + Christian | AI control | **43,5** | = | Provenance Firewall ya lo hizo |
| 32 | Agente con acceso total sin acciones peligrosas | Reunión con mentor | AI control | **43,5** | = | El mentor dijo que no se metería |
| 34 | Benchmark hardener | Brief de Juanfe + Christian | No encaja limpio (cercano a cyber evals) | **42,5** | = | harden-v0 y BenchJack ya existen |
| 35 | AI kitchen con interpretabilidad | Reunión con mentor | No califica como está | **39** | = | No resuelve un problema de seguridad |

**Cómo leerla.** Las cuatro primeras están a 4 puntos; medio punto no es significativo y decide lo que funcione en las primeras 2 horas. **Mi lectura:** construir la red de seguridad acotada (1). Si su puerta de 2 horas falla y el chequeo previo (2) sí muestra un cruce entre corridas que el chequeo simple no ve, cambiar al chequeo previo. La combinación (3) cuenta la mejor historia, pero arriesga no terminar. El swarm (4) tiene la demo más potente para fundadores, pero ocupa un carril con empresas (XBOW, Corgea) y depende de una cadena larga (hallar, explotar, parchar, validar). Por categoría: mayoría en AI control, luego guardrails, defensa y cyber evals; solo una en interpretabilidad.

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
| Chequeo previo: separación entre corridas (si se valida) | 7,5 | 8 | 7,5 | 8,5 | 6 | 75,5 |
| Red de seguridad, versión acotada | 6 | 7,5 | 8 | 8 | 8 | 76 |
| Combinación mínima | 5 | 8 | 6,5 | 8 | 8,5 | 73,5 |
| Chequeo previo simple (versión anterior) | 7 | 6 | 8 | 6 | 8 | 69,5 |
| Juez de trayectorias por ejecución | 5 | 8 | 3 | 8 | 8 | 65,5 |
| Reversibilidad para agentes | 4 | 7 | 7 | 7 | 7 | 65,5 |
| Brecha de salvaguardas en español regional | 5 | 6 | 8 | 6 | 7 | 64,5 |
| Swarm de red teaming, versión acotada (Mauricio) | 4 | 7,5 | 6,5 | 8 | 9 | 72 |
| AegisHub | 3 | 7 | 5 | 5 | 5 | 51 |

Las demás filas mantienen el desglose de la versión 2.
