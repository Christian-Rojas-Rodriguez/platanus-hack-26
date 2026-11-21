# Mapa de ideas del equipo: dificultad vs impacto

Las 12 propuestas del repo y de la reunión con el mentor (20-11-2026), ubicadas por dificultad de construir con al menos 15 h y por impacto. Al impacto se le descuenta lo que ya existe, porque el mentor mide el valor contrafactual. El anti-estafas por WhatsApp quedó descartado.

![Mapa de dificultad vs impacto](mapa-ideas-equipo.svg)

Colores: verde oliva, Jaime; azul, Mauricio; verde azulado, Tomás; naranjo, ideas de la reunión con el mentor sin autor en el repo; círculo vacío, la unión propuesta.

- **Golden zone** (fácil y mucho impacto): dificultad menor a 5 e impacto mayor a 6.
- **Umbral wow**: impacto 6. Lo que queda debajo difícilmente impresiona al jurado.
- **Alto riesgo**: dificultad mayor a 7, aun con 15 h.

| # | Idea | Dificultad | Impacto | Razón |
|---|---|---|---|---|
| 1 | Radar + harness de Mauricio | 4,7 | 8,8 | El radar ataca, el harness defiende y el parche se mide en vivo: «pasan 7 de 10, tras el parche 0». Responde la pregunta del mentor de si un agente puede saltarse el SLM. Con 15 h entra en la golden zone. |
| 2 | Radar de jailbreaks en español | 4,1 | 7,8 | Es la idea del mentor. No existe monitoreo de jailbreaks en español LatAm. Le falta una defensa propia para mostrar el número bajando. |
| 3 | MCP TimeLock (Tomás) / MCP-Shield (Jaime) | 3,1 | 6,4 | Coincidimos los dos. MCP envenenado roba llaves en vivo y se bloquea. MCP-Scan cubre parte. Mejor backup. |
| 4 | Qwen exfiltrando + constrained decoding | 3,8 | 5,2 | Gancho real (Cohere, oct-2026), pero restringir tokens no frena una URL dentro de un comando: eso es control de red y de herramientas. Sin evidencia de que fuera deliberado. |
| 5 | Harness en cascada (Mauricio) | 3,2 | 4,3 | Fácil y bien diseñado, pero ya existe: Lakera, Prompt Guard, Constitutional Classifiers y Tranquera, que ganó la edición anterior de Platanus con la misma arquitectura. |
| 6 | «Hugging Face para evals» | 2,2 | 3,8 | El mentor lo dio como backup. Inspect Evals y lm-eval-harness ya cubren mucho. |
| 7 | ScopeProof (Tomás) | 5,1 | 5,4 | Papers verificados, pero APEX ya pone autorización en el límite de ejecución y el mentor pidió salir de control y oversight. |
| 8 | MemoryLineage (Tomás) | 5,4 | 4,6 | Hueco real (MemSecBench: 84 % de persistencia), pero la demo es abstracta. |
| 9 | Agent Escape Lab (Tomás) | 6,1 | 4,2 | Es investigación más que producto. Difícil mostrar un lift aun con más horas. |
| 10 | ProbeGate (Jaime) | 6,8 | 7,0 | Con 15 h se vuelve posible, pero necesita GPU y es difícil de explicar al público. |
| 11 | Anti-vishing (Jaime) | 7,3 | 7,6 | Wow muy alto, pero entrenar audio sigue siendo la apuesta más arriesgada. |
| 12 | AI kitchen con interpretabilidad | 7,1 | 1,8 | El mentor preguntó por qué es de safety. No encaja en el track. |

## Propuesta

- **Principal: radar de jailbreaks + harness de Mauricio.** El radar recolecta jailbreaks nuevos, los adapta a español LatAm y los lanza contra el guardrail local de Mauricio; se mide cuántos pasan, se genera el parche y se vuelve a medir en vivo. Es la fórmula de demo del mentor (problema, daño en número, solución, número bajando) y responde su pregunta sobre si un agente malicioso podría saltarse el SLM.
- **Backup: MCP TimeLock / MCP-Shield.** Un servidor MCP envenenado roba llaves en vivo y el escudo lo bloquea. El incidente de Qwen (Cohere, oct-2026) sirve de gancho.

## Números para el daño

- Los guardrails abiertos dejan pasar hasta 75 % del contenido inseguro ([arXiv 2605.28830](https://arxiv.org/pdf/2605.28830)).
- Los ataques adaptativos rompen 12 defensas publicadas con 71 a 100 % de éxito ([The Attacker Moves Second](https://arxiv.org/abs/2510.09023)).
- El tool poisoning en MCP logra 72,8 % de éxito contra o1-mini ([MCPTox](https://arxiv.org/abs/2508.14925)).
- Incidente de Qwen: [Cyber Magazine](https://cybermagazine.com/news/cohere-alibaba-qwen-model-tried-to-send-data-to-beijing), [Vals AI](https://vals.ai/blogs/qwen-alibaba-requests).

Las posiciones son un juicio para discutir en equipo, no una medición.
