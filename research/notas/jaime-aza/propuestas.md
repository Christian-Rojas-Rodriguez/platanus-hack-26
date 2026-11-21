# Propuestas de Jaime Aza

> **Notas personales de Jaime para discutir, no una decisión del equipo.** Escritas antes del brief de Juanfe; mi lectura actualizada está en [mapa-ideas-equipo.md](mapa-ideas-equipo.md).

Cinco alternativas para el track AI Security, filtradas con los criterios del mentor y la guía de Kairos (`research/papers/kairos-guia-ai-security.pdf`). El estado del arte que las respalda está en [estado-del-arte.md](estado-del-arte.md).

## Criterios usados

- **Gap:** lo que ya existe cubre el problema en un 20 % como mucho, o lo cubre mal.
- **Wow:** la demo se entiende en 30 s y en vivo se rompe algo o se salva algo.
- **Tiempo:** hay una demo funcional en unas 36 h, con APIs o una GPU.
- **Usuario real:** público víctima de fraudes, gobierno, bancos o empresas que usan agentes.
- **Kairos:** el proyecto ataca, defiende o mide, idealmente las tres cosas.
- **Pitch:** sigue el formato «hoy existe X problema, causa X daño, proponemos X y lo mostramos en vivo».

## Mapa impacto vs dificultad

| # | Propuesta | Gap estimado | Wow | Dificultad | Usuario más claro | Subárea Kairos |
|---|---|---|---|---|---|---|
| 1 | Radar de jailbreaks en español | ~10-15 % | Alto | Media | Gobierno, banca | Guardrails, evals |
| 2 | Escudo anti-estafas por WhatsApp | ~25-35 % | Alto | Baja | Público, PDI | Defensa |
| 3 | MCP-Shield + MCP-Arena | ~10 % | Medio-alto | Media | Empresas con agentes | AI control |
| 4 | ProbeGate | ~15 % | Medio | Alta | Labs, plataformas de agentes | Interpretabilidad |
| 5 | Anti-vishing en español | Claro | Muy alto | Alta | Bancos, call centers | Defensa |

Los porcentajes de gap salen de la búsqueda y son una estimación, no una medición.

**Recomendada: la 1.** Toma la idea del mentor (un scraper de prompt injections y jailbreaks) y la vuelve producto. El hueco está confirmado: no existe un benchmark ni un monitoreo de jailbreaks en español latinoamericano. Cubre lo que pide Kairos: ataca porque recolecta y adapta ataques, mide porque arma un scorecard por modelo y guardrail, y defiende porque genera el parche. **Plan B: la 2**, que tiene la demo más fácil de entender.

---

## 1. Radar de jailbreaks: inteligencia de amenazas para chatbots en español

**Problema y daño.** Cada semana aparecen jailbreaks e inyecciones nuevas en GitHub, Reddit, X y arXiv, casi todas en inglés. Los bancos y los servicios públicos que tienen chatbots en español se enteran cuando ya se los rompieron.

**Solución.** Un radar que recolecta esos ataques de forma automática, los adapta al español de Chile y de LatAm, los prueba contra modelos y guardrails y entrega en minutos la regla que los bloquea.

**Cómo funciona.**
1. Un scraper recorre GitHub, Reddit, arXiv y foros.
2. Normaliza cada ataque y lo clasifica por familia: role-play, Crescendo multi-turno, cifrados, Best-of-N o inyección indirecta.
3. Un mutador lo traduce y lo adapta a modismos, spanglish y contexto local (bonos, ClaveÚnica, banca).
4. La batería lo corre contra Llama Guard 4, Qwen3Guard, gpt-oss-safeguard y 2 o 3 LLMs.
5. Sale un scorecard, más una regla o ejemplos de entrenamiento para el guard.

**Demo en vivo.** «Esta técnica se publicó hace 48 h. En inglés la bloquean los 4 guardrails; en español chileno pasa por 3 de 4.» Se presiona «parchar» y el mismo ataque ya no pasa. Después se lanza un ataque adaptativo que intenta saltarse el parche.

**Usuarios.**
- Gobierno digital y servicios con chatbot ciudadano.
- Bancos y fintech con asistentes.
- Startups que despliegan LLMs en LatAm.
- Equipos de guardrails.

**Por qué es nuevo.** garak y PyRIT traen sondas fijas. JailbreakHub es un dataset estático de 2023. Los estudios en español son de España o de México y también estáticos. Nadie hace monitoreo continuo adaptado a LatAm.

**Métrica para los jueces.**
- Tasa de éxito de ataque por familia y por variante (inglés, español neutro, chileno) en cada guardrail.
- Recall antes y después del parche.
- Tiempo desde que se publica el ataque hasta que existe el parche.

**Qué reutilizamos.** HarmBench y su juez, StrongREJECT, garak o PyRIT, Qwen3Guard y Llama Guard 4.

**Ojo.** Solo atacamos modelos locales o chatbots con permiso. Para el caso «gobierno», la demo usa un asistente ciudadano simulado propio, nunca uno real.

**Plan de 36 h.**
1. **Horas 0-4.** Fijar 3 familias de ataque y 3 guardrails. Armar el asistente simulado que hace de víctima.
2. **Horas 4-14.** Scraper de 2 fuentes (GitHub y Reddit bastan), clasificador de familia con LLM y mutador a español chileno.
3. **Horas 14-24.** Batería de pruebas con juez (HarmBench o StrongREJECT) y scorecard por guardrail e idioma.
4. **Horas 24-30.** Generador del parche (ejemplos para el guard o una regla) y ataque adaptativo contra el parche.
5. **Horas 30-36.** Dashboard, guion de la demo («publicado hace 48 h», rompe, parche) y pitch.

## 2. Escudo anti-estafas por WhatsApp con red team de IA

**Problema y daño.** En Chile, 1 de cada 4 personas ya sufrió una estafa digital, y la suplantación se concentra en WhatsApp. Con IA, cada estafa sale distinta y sin faltas de ortografía.

**Solución.** Un contacto al que se le reenvía el mensaje sospechoso y responde en segundos si es estafa y por qué. Se entrena contra un atacante de IA que genera estafas nuevas todo el tiempo.

**Demo en vivo.** Un juez dicta una estafa. El LLM atacante la reescribe en 10 variantes («falso bono por temporales», «hola mamá, cambié de número», soporte falso del banco). El escudo detecta cada una en el celular y explica por qué.

**Usuarios.** Público general y adultos mayores, bancos, PDI, SERNAC y CSIRT de Gobierno.

**Por qué es nuevo.** Hay filtros genéricos (Google, Truecaller, bancos), pero ninguno evaluado contra estafas reescritas por IA en español chileno. Lo medible es el bucle de rojo contra azul.

**Métrica.** F1 en unos 300 mensajes (alertas reales de PDI y CSIRT más mensajes generados), y cuánto cae y se recupera frente a estafas adaptativas.

**Riesgo.** Es la más «producto» y la menos «AI safety», así que puede pesar menos con Kairos.

## 3. MCP-Shield + MCP-Arena: control de agentes con herramientas envenenadas

**Problema y daño.** Los agentes de código se conectan a servidores MCP de terceros. Una descripción de herramienta envenenada basta para que el agente exfiltre secretos, y ninguno de los 15 settings de ControlArena prueba MCP.

**Solución.** Dos piezas:
- Un proxy que detecta herramientas envenenadas y cambios entre versiones (rug pull).
- El primer setting MCP para ControlArena, con curvas de seguridad contra utilidad.

**Demo en vivo.** Claude Code instala un MCP que parece inocente y manda las llaves a un servidor externo. Con el escudo, la misma acción se bloquea y aparece en el panel.

**Usuarios.** Empresas que usan Claude Code, Cursor o Codex con MCP.

**Riesgo.** Se parece a Tranquera, que ganó la edición anterior. Si la elegimos, hay que presentarla como evolución y poner al frente el aporte de investigación (el setting).

## 4. ProbeGate: monitor barato de agentes que lee sus activaciones

**Problema y daño.** Vigilar cada paso de un agente con otro LLM es caro, y por eso casi nadie lo hace. Anthropic y DeepMind ya filtran con sondas lineales sobre las activaciones a una fracción del costo, pero solo en chat y en sistemas cerrados.

**Solución.** Una cascada abierta para agentes: primero la sonda, y el LLM solo revisa los casos dudosos.

**Métrica.** Recall con 1 % de falsos positivos contra el costo por cada mil pasos, comparando sonda sola, LLM solo y cascada.

**Requisito.** Una GPU de 24 GB con Qwen3-8B. A los jueces de AI safety les gusta, pero al público le cuesta entenderla.

## 5. Anti-vishing: detectar voces clonadas en llamadas en español

**Problema y daño.** El mejor detector público de deepfakes de voz falla un 29 % en español (EER en VoxENES 2026). Corrección del 21-11: ese 29 % es el error global del benchmark, no el del español (lo detectó Christian en su informe 32).

**Solución.** Ajustarlo con audio chileno de llamada telefónica (8 kHz).

**Demo en vivo.** Se clona la voz de un compañero, con su permiso, y el detector la marca durante una llamada.

**Riesgo.** Lograr una mejora real entrenando audio en 36 h es la apuesta más arriesgada.
