# 25 · Radar de jailbreaks en español: ¿ya existe?

Fecha: 21-nov-2026. Track AI Security / AI Safety.
Idea evaluada: ingestión continua de técnicas de jailbreak y prompt injection (GitHub, Reddit, arXiv, foros) → adaptación al español de Chile/LatAm → prueba contra guardrails abiertos (Llama Guard, Qwen3Guard…) y uno propio → % que pasa → parche automático.

> Límite metodológico: se agotó el presupuesto compartido de WebSearch a mitad del trabajo (~13 búsquedas propias). Los bloques (3) compradores LatAm y (4) tamaño quedaron **casi sin fuentes**: donde no hay URL dice "sin dato". Haize Labs, Gray Swan Arena, Zenity Labs, HiddenLayer, PyRIT y JailbreakBench **no se verificaron en esta sesión**.

---

## 1. Competidores: la idea ya existe en un 70-80 %

### 1.1 El más cercano: 0DIN (Mozilla). Hace feed + escaneo continuo + reglas de guardrail
- Feed de amenazas por suscripción con jailbreaks verificados, que vienen de su bug bounty de GenAI y de su equipo interno. https://0din.ai/docs/jailbreak-feed/introduction
- Cada hallazgo incluye "detection signatures" (reglas híbridas de keyword, semánticas y LLM) y "guardrail rules to mitigate it". Plan gratis y planes Team/Enterprise; los precios no son públicos. https://www.0din.ai/docs/threat-feed/introduction
- Lanzamiento del 7-jul-2025: lo validado llega al feed "within hours". El *Model Scanner* convierte cada hallazgo en un módulo que se corre contra tu modelo con frecuencia horaria a semanal, y desde el reporte se pueden actualizar los guardrails. https://0din.ai/blog/odin-product-launch-threat-intelligence-feed-model-scanner
- El escáner es open source (Apache 2.0) e incluye 179 probes comunitarios en 35 familias. https://blog.mozilla.org/en/mozilla-new-products/0din-ai-security-scanner/
- Bounties de USD 500 a 15.000 según severidad. https://0din.ai/scope
- **Lo que no dice:** cobertura de idiomas (sin dato) ni ningún foco en español o dialectos.

### 1.2 Cisco: pipeline nocturno de amenaza → firma → despliegue
- Paper de Cisco Systems (arXiv 2509.20639, sep/oct-2025). Cada noche recolectan lo publicado en las últimas 24 h (arXiv cs.AI/cs.CR/cs.CL, blogs, bases de vulnerabilidades, vendors de threat intel) y lo traducen en protecciones. Usan firmas tipo YARA como vía rápida y reentrenan los modelos más lento, con un rollout de "días a semanas". Mencionan "prompt translations into various languages" sin decir cuáles. https://arxiv.org/html/2509.20639v2
- Es exactamente el loop "ingestión → parche" de la idea, ya en producción en un incumbente.

### 1.3 Lakera (adquirida por Check Point, anunciado sep-2025)
- Adquisición: https://blog.checkpoint.com/security/check-point-to-acquire-lakera-redefining-security-for-the-ai-era/
- Afirma cubrir "100+ languages", detectar ~15.000 amenazas al día y aprender en continuo de más de 100K muestras adversariales diarias (vendor claim). https://lakera.ai/risk/multilingual-multimodal-attacks
- Evidencia independiente (GenTel-Safe): Lakera "performs well in Spanish and German" pero falla en otros idiomas. O sea, el español **ya es un idioma fuerte** para el líder. https://arxiv.org/pdf/2409.19521

### 1.4 Open source y repositorios
- **garak (NVIDIA):** 10,1k estrellas. Escanea jailbreaks, prompt injection y fugas de datos. La página no muestra probes multilingües ni generación de parches. https://github.com/NVIDIA/garak
- **Promptfoo:** OpenAI anunció su compra el 9-mar-2026; dicen tener más de 125.000 desarrolladores y más de 30 empresas Fortune 500. https://techcrunch.com/2026/03/09/openai-acquires-promptfoo-to-secure-its-ai-agents/
- **L1B3RT4S (Pliny):** 23,4k estrellas, AGPL-3.0, prompts organizados por proveedor (OPENAI, ANTHROPIC, DEEPSEEK…). No se pudo comprobar si tiene contenido en español. Es la fuente "en vivo" natural para el radar. https://github.com/elder-plinius/L1B3RT4S
- Protect AI → Palo Alto Networks (abr-2025, una sola fuente). https://www.cbinsights.com/compare/lakera-ai-vs-promptfoo

### 1.5 Academia: guardrails que se adaptan a jailbreaks nuevos
- AdaptiveGuard (ASE 2025): trata los jailbreaks nuevos como entradas fuera de distribución y actualiza el guardrail con aprendizaje continuo. https://arxiv.org/html/2509.16861v1
- JailbreaksOverTime: detección bajo *distribution shift* con self-labeling y "Active Monitoring". https://ar5iv.labs.arxiv.org/html/2504.19440

### 1.6 Competencia directa en español de LatAm: LatAm-RT (2026)
- Benchmark de red teaming para "Latin American Spanish": 284 prompts en 3 capas (traducción directa, adaptación regional y localización nacional), con 4 países: **México, El Salvador, Costa Rica y Chile**. Usa jerga local ("luca", "pisto", "feria"). 12 anotadores nativos; licencia CC BY-NC 4.0 (no comercial). Paper del First Workshop on Pluralistic AI & NLP (2026). https://huggingface.co/datasets/Latam26/LatAmRT
- Es un dataset estático y no hace ingestión continua. Pero ya ocupa la parte de "adaptar jailbreaks al español de Chile".
- Otros: M-ALERT (15k prompts por idioma, incluye español) https://arxiv.org/pdf/2412.15035v2 ; ALERT_es https://huggingface.co/datasets/felfri/ALERT_es ; SESGO (sesgos en LatAm, más de 4.000 prompts) https://arxiv.org/html/2509.03329v1

**Conclusión del bloque 1:** la ingestión continua con parche ya existe (0DIN, Cisco, Lakera). El red teaming localizado al español chileno también (LatAm-RT, académico). **Nadie verificado combina las dos cosas**: un feed continuo que localice cada técnica nueva a variantes dialectales del español y mida la regresión de guardrails abiertos.

---

## 2. ¿Los guardrails rinden peor en español? Sí, pero la brecha es moderada y no uniforme

### 2.1 Lo mejor que hay: Qwen3Guard Technical Report (arXiv 2510.14276), F1 por idioma
Clasificación de prompts en RTP-LX, inglés vs español:

| Guardrail | EN | ES | Δ |
|---|---|---|---|
| LlamaGuard3-8B | 50,0 | 48,3 | −1,7 |
| **LlamaGuard4-12B** | 37,6 | **29,5** | **−8,1** |
| **WildGuard-7B** | 93,9 | **80,3** | **−13,6** |
| ShieldGemma-27B | 76,1 | 71,8 | −4,3 |
| PolyGuard-Qwen-7B | 91,2 | 89,0 | −2,2 |
| Qwen3Guard-8B-Gen (strict) | 92,1 | 88,9 | −3,2 |

En respuestas (PolyGuard-Response), LlamaGuard4 cae de 66,4 a 55,3 (−11,1). Qwen3Guard prácticamente no cae (78,4 → 77,3).
Fuente: https://arxiv.org/html/2510.14276v1 (tablas 5 y 6). Los números los publica Alibaba, que tiene interés en mostrar que su modelo gana.

### 2.2 Jailbreaks en español vs inglés (arXiv 2511.00689, 10 idiomas)
- La conclusión del paper es que los idiomas de muchos recursos (incluido el español) son más seguros con consultas normales y **más vulnerables a las adversariales**. https://arxiv.org/html/2511.00689v2
- **Caso fuerte:** con el jailbreak de Andriushchenko et al., Claude Sonnet 4 da **0 % de respuestas inseguras en inglés y 14,5 % en español** (HarmBench). Con el ataque "Logic" pasa de 6 % a 19 %. En AdvBench, de 0,38 % a 19,23 %.
- **Contraevidencia (ser honestos):** GPT-4o, Qwen2.5 y Llama3.1-70B dan **menos** respuestas inseguras en español que en inglés con varios ataques (Llama3.1-70B Andrius25: 47,5 % EN vs 23,5 % ES).
- Otro paper multimodal: Claude 11,3 % en en-US vs 11,4 % en es-MX, sin diferencia. https://arxiv.org/pdf/2605.23157
- Un análisis IRT de 1,9M respuestas encuentra que "22 model configurations are more vulnerable in English than in low-resource languages". https://arxiv.org/abs/2605.17173

### 2.3 Dialectos
- **No se encontró ningún benchmark que mida jailbreaks por variante del español** (rioplatense, chileno, mexicano) con tasas de ataque publicadas. LatAm-RT tiene el dataset, pero sus resultados no se recuperaron (sin dato).
- Análogo en chino: con dialectos (wu y cantonés) el ataque llega a **100 % ASR** en GPT-4o y DeepSeek-Reasoner. https://arxiv.org/pdf/2609.31664
- Red teaming manual en España (Universidad de Sevilla, 670 conversaciones): entre 29,5 % (o3-mini) y 50,6 % (ALIA Salamandra) de respuestas sesgadas o inseguras en español y euskera. https://arxiv.org/abs/2503.10192v1

**Conclusión del bloque 2:** el español **no** es un idioma "de pocos recursos", y los mejores guardrails pierden solo 2-4 puntos de F1. La brecha grande está en guardrails populares pero más débiles (LlamaGuard4, WildGuard) y en casos puntuales (Sonnet 4). Lo dialectal está **sin medir**, y ese hueco sí es real.

---

## 3. ¿Quién pagaría en LatAm?
- Incidentes reales de chatbots en español vulnerados con jailbreak: **sin dato**. Se agotó el presupuesto de búsqueda y no se verificó ningún caso. No hay que inventarlo en el pitch.
- OWASP LLM Top 10 2025 pone Prompt Injection en el primer lugar y menciona explícitamente el escenario "Multilingual/Obfuscated Attack". https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- Compradores probables (hipótesis sin fuente en esta nota): bancos y fintech con asistentes en español, gobiernos con chatbots ciudadanos, telcos y retail. Para mapearlos, ver `13-region-latam.md` y `23-quien-factura.md`.
- Señal de que hay disposición a pagar en el segmento (global): compras de Lakera por Check Point, Promptfoo por OpenAI y Protect AI por Palo Alto (fuentes arriba).

## 4. Tamaño: cuántos despliegues de LLM en español
- **Sin dato.** No se encontró ni se pudo buscar una cifra de despliegues de LLM en español o en LatAm.
- Lo único verificable es indirecto: Qwen3Guard dice soportar 119 idiomas y dialectos (https://arxiv.org/html/2510.14276v1) y Lakera más de 100 (vendor). Es decir, la oferta ya declara cobertura del español.

---

## 5. Veredicto

**Cobertura estimada: ~75 % del problema ya resuelto** (es un juicio cualitativo, no una cifra medida):
- Ingestión continua y validación en horas: **0DIN** (cubierto).
- Escaneo programado contra tu modelo y reglas de guardrail: **0DIN Model Scanner, Cisco, Lakera** (cubierto).
- Escáner open source: **garak, 0DIN scanner, Promptfoo** (cubierto).
- Jailbreaks localizados a Chile/LatAm: **LatAm-RT** (cubierto como dataset estático y no comercial).
- Guardrails multilingües sólidos en español: **Qwen3Guard, PolyGuard** (en gran parte cubierto).

**Ángulo realmente nuevo (el ~25 % restante):**
1. **Localización dialectal continua**: cada técnica nueva del feed se reescribe en chileno, rioplatense y mexicano, y se mide el *delta* frente al inglés y al español neutro. Nadie publica esa serie temporal.
2. **Regresión pública de guardrails abiertos en español** (un leaderboard vivo de "qué % de los jailbreaks de esta semana pasa por LlamaGuard4 o Qwen3Guard en chileno"). 0DIN es cerrado y no habla de idioma.
3. Parche automático **para guardrails abiertos y self-hosted**, el caso de la empresa LatAm que no compra Check Point.

Riesgo: si la medición muestra que el chileno no empeora mucho frente al español neutro, la tesis se cae. Hay que medirlo en la hackathon antes de venderlo.

**Número más fuerte y verificable para el pitch:**
> "Llama Guard 4, el guardrail abierto de Meta, detecta prompts dañinos en español con F1 29,5, frente a 37,6 en inglés. WildGuard cae de 93,9 a 80,3." (Qwen3Guard Tech Report, tabla 5: https://arxiv.org/html/2510.14276v1)

Alternativa más llamativa, pero de un solo modelo:
> "El mismo jailbreak que logra 0 % contra Claude Sonnet 4 en inglés logra 14,5 % en español." (arXiv 2511.00689: https://arxiv.org/html/2511.00689v2)

Evitar en el pitch: "los guardrails fallan en español" como afirmación general. La evidencia es mixta (ver 2.2).
