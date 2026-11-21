# Notas de Jaime: mapa de ideas (dificultad vs impacto)

> **Esto es una opinión personal de Jaime, no una decisión del equipo.** Todo lo que hay en `research/notas/jaime-aza/` son mis notas para discutir; la elección de la idea la tomamos juntos.

Versión 2 (21-11-2026), actualizada con el brief de Juanfe (`docs/ai-safety-track-brief.md`): suma ideas de su mapa de failure modes, marca el carril saturado (agent guards y firewalls de prompt injection que ya hicieron otros equipos del tour) y estima la dificultad para 10 a 12 h, como recomienda el brief.

![Notas de Jaime: mapa de dificultad vs impacto](mapa-ideas-equipo.svg)

**Cómo leerlo.** Colores por origen: rosado, brief de Juanfe; verde oliva, Jaime; azul, Mauricio; verde azulado, Tomás; naranjo, reunión con el mentor sin autor en el repo. El círculo con borde rosado une una idea del brief con mi investigación. **Anillo rojo punteado: carril saturado** según el brief. Golden zone: dificultad menor a 5 e impacto mayor a 6. Zona rosada: alto riesgo en el tiempo que hay.

| # | Idea | Origen | Dificultad | Impacto | Por qué está ahí |
|---|---|---|---|---|---|
| 1 | SafeBench-ES + LatamGPT | Brief + Jaime | 4,5 | 8,6 | B3 + D3 del brief. Benchmark de seguridad en español chileno y LatAm con categorías proxy, y los primeros resultados públicos de seguridad de LatamGPT. El harness de Mauricio puede ser el fix que baja la brecha. Riesgo: correr un 70B (~140 GB de VRAM o A100 de 80 GB cuantizado). |
| 2 | Detector de trampas | Brief de Juanfe | 4,8 | 8,0 | A1, primero de la lista corta. AISI: los 5 modelos frontera hacen trampa en 7,8 a 14,1 % de las corridas y no hay métodos confiables para detectarlo. Villano: el agente borra el test que falla y reporta éxito. |
| 3 | Scheming radar | Brief de Juanfe | 4,0 | 6,8 | A3. Es la idea del scraper del mentor, pero del lado seguro: junta incidentes reales de agentes que se portan mal (CLTR: 698 incidentes, 4,9 veces más en seis meses), no jailbreaks. |
| 4 | Sandbox tripwires | Brief de Juanfe | 2,6 | 6,4 | A5. Credenciales y archivos de respuestas señuelo que alertan cuando el agente los toca. Lo más fácil del brief; villano real con el incidente de OpenAI y Hugging Face (jul-2026). |
| 5 | Eval realism | Brief de Juanfe | 6,0 | 6,6 | A4. Mide cuánto «huele a test» un entorno de evaluación. Valioso para jueces de safety, pero la demo es menos visual. |
| 6 | Benchmark hardener | Brief de Juanfe | 6,6 | 6,4 | A2. Un agente intenta hacer trampa en cada tarea y otro la parcha. Más trabajo de setup. |
| 7 | ProbeGate | Jaime | 7,0 | 5,7 | Monitor con sondas sobre activaciones. Necesita GPU y es difícil de explicar en 2 minutos. |
| 8 | Anti-vishing | Jaime | 7,8 | 7,0 | B1. Wow alto, pero entrenar audio es arriesgado y SafeLine (Hack 25) ya hizo un detector de llamadas de estafa. |
| 9 | Mandato y recibo (ScopeProof) | Tomás | 5,1 | 5,6 | ScopeProof reencuadrado como C2 del brief (Citi, «know your agent»). Roxy (Bogotá) ya hizo política formal con motor sin IA. |
| 10 | Radar + harness | Jaime | 4,7 | 5,0 | Mi principal anterior. Agent Zero (Caracas) ya hizo «ataca tu agente, confirma el daño, escribe la regla», y un scraper de jailbreaks roza la línea roja del brief. |
| 11 | MCP TimeLock / Shield | Tomás | 3,1 | 5,0 | Solo vale como nicho: escáner de plug-ins MCP riesgosos. El resto es el carril saturado de agent guards. |
| 12 | Qwen + decoding | Reunión con el mentor | 3,8 | 4,5 | Gancho real (Cohere, oct-2026), pero restringir tokens no frena una URL dentro de un comando. |
| 13 | Harness en cascada | Mauricio | 3,2 | 3,5 | Carril saturado según el brief: Aegis, HAWK y Tranquera ya cubrieron filtros y guards. Sirve como componente de otra idea. |
| 14 | HF para evals | Reunión con el mentor | 2,2 | 3,8 | Fácil, pero Inspect Evals y lm-eval-harness ya cubren mucho. No aparece en el brief. |
| 15 | MemoryLineage | Tomás | 5,4 | 3,8 | Provenance Firewall (Bogotá) ya protegió la memoria de agentes con 255 tests. |

Fuera del gráfico: Agent Escape Lab (Tomás), que el brief cubre mejor con los tripwires; AI kitchen, que no encaja en el track; anti-estafas por WhatsApp, descartado.

## Mi lectura (opinión)

- **Lo que más me convence:** SafeBench-ES + LatamGPT (1) o el detector de trampas (2). Ambos están en la lista corta del brief, fuera del carril saturado, y tienen villano, fix y número.
- **Backup fácil:** sandbox tripwires (4).
- **Lo que dejaría:** las ideas de guard o firewall genérico (10, 11, 13), porque el brief dice que es lo que más se construyó en el tour.
- **A resolver si vamos por la 1:** cómo correr LatamGPT (70B) esta noche.

Las posiciones son mi juicio para discutir, no una medición.
