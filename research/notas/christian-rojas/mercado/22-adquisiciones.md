# 22 — Mapa de fusiones y adquisiciones en seguridad de IA (2024 – nov 2026)

Research al 21-nov-2026. Cada dato lleva su URL. "sin dato" = no encontré fuente en esta sesión.

**Límites de esta nota:**
- El presupuesto de búsquedas web se agotó antes de terminar. Por eso no pude verificar todo. Faltan la financiación y el año de fundación de SPLX, Apex, Invariant, Lakera, Oasis, Koi y Acuvity, y no revisé si Microsoft o Databricks compraron algo en este espacio.
- No encontré ingresos (ARR) confirmados de **ninguna** de las startups compradas. La columna de ingresos dice "sin dato" en casi todas las filas.

## Cómo leer los precios

- **Confirmado:** lo publicó el comprador, en un comunicado o en un filing ante la SEC.
- **SEC (tracker):** cifra del tracker de Deepak Gupta, que dice basarse en filings de la SEC (https://guptadeepak.com/agent-security/deals/). Es una fuente secundaria y yo solo la verifiqué contra el filing original en un caso: Prompt Security, ver abajo.
- **Reportado:** estimación de prensa (Globes, Calcalist, etc.) que la empresa no confirmó.

---

## Tabla principal (los deals pedidos)

| Comprada | Comprador | Fecha (anuncio → cierre) | Precio | Capital levantado antes | Edad al salir | Ingresos conocidos | Qué capacidad compraron |
|---|---|---|---|---|---|---|---|
| Robust Intelligence | Cisco | 26-ago-2024 → 24-sep-2024 [1] | ~$400M reportado [1][2]. Forrester estimó ~$500M [3] | $44M [4] | ~5 años (fundada en 2019) [4] | sin dato | Validación y testing automático de modelos, red-teaming y validación en runtime [2] |
| Protect AI | Palo Alto Networks | 28-abr-2025 → 22-jul-2025 [1] | $634,5M (SEC, tracker) [1]. Reportado: $500–700M (Globes: $650–700M) [5] | $108,5M. Valuación de $400M en ago-2024 [5] | ~3 años (fundada en 2022) [4b] | sin dato | Escaneo de modelos y supply chain de ML, seguridad de LLM, red-teaming de GenAI. Se integró en Prisma AIRS [5][2] |
| Koi | Palo Alto Networks | 17-feb-2026 → 14-abr-2026 [1] | $231M (SEC, tracker) [1]. ~$400M reportado por Calcalist y Globes [6] | $48M [6] | sin dato | sin dato | "Agentic endpoint security": inventario y control de extensiones, paquetes, modelos y agentes en el endpoint, más un gateway de supply chain para GitHub y Hugging Face [6] |
| Lakera | Check Point | 16-sep-2025 → 22-oct-2025 [1] | $201,8M (SEC, tracker) [1]. ~$300M reportado [7] | sin dato | sin dato | sin dato | Guardrails en runtime contra prompt injection y fuga de datos (Lakera Guard) y red-teaming (Lakera Red, basado en el juego Gandalf) [7] |
| CalypsoAI | F5 | 11-sep-2025 → 26-sep-2025 [1] | **$180M confirmado** [8]. $145,2M fue el pago en efectivo al cierre (SEC, tracker) [1] | >$40M [8] | sin dato | sin dato | Defensas en la capa de inferencia y red-teaming de flujos agénticos. F5 los lanzó como "F5 AI Guardrails" y "F5 AI Red Team" [3][9] |
| Invariant Labs | Snyk | 24-jun-2025 [1] | No divulgado [1] | sin dato | sin dato | sin dato | Inspección del protocolo MCP y de los mensajes entre agentes [2] |
| Prompt Security | SentinelOne | 5-ago-2025 → 5-sep-2025 [1] | **~$160M confirmado en el 10-Q de SentinelOne** (preliminar ~$159M, ajustado a ~$160M) [10]. ~$250M reportado [10][3] | $23M a nov-2024 [10] | sin dato | sin dato | Control del uso de GenAI por empleados, defensa contra prompt injection y DLP granular [2] |
| Aim Security | Cato Networks | 3-sep-2025 [1] | No divulgado. Calcalist estimó $300–350M [10] | $28M ($10M seed en ene-2024 y $18M en jun-2025) [10] | ~3 años (fundada en 2022) [10] | sin dato | Gobernanza de IA dentro de SASE y monitoreo de agentes por tráfico [3][2] |
| SPLX | Zscaler | 3-nov-2025 [1] | $40,6M (SEC, tracker) [1]. Oficialmente no divulgado [11] | sin dato | sin dato | sin dato | Red-teaming automatizado y AI-SPM (la descripción de la capacidad viene del tracker y la cobertura; no la verifiqué) |
| Pangea | CrowdStrike | 16-sep-2025 → 26-sep-2025 [1] | $222,7M (SEC, tracker) [1]. ~$260M reportado [10][3] | ~$51M [10] | ~4 años (fundada en 2021) [10] | sin dato | "AI Detection & Response" (AIDR) para Falcon y control de identidad y roles para IA [10][2] |
| Apex Security | Tenable | 29-may-2025 → 17-jun-2025 [1] | $47,8M (SEC, tracker) [1]. Forrester estimó ~$105M [3] | sin dato | sin dato | sin dato | Superficie de ataque de IA: distinguir mal uso accidental de malicioso [2] |
| Promptfoo | OpenAI | 9-mar-2026 (anunciado; el tracker no registra cierre) [12][1] | No divulgado [12] | $23M. Valuación de $86M en jul-2025 según PitchBook [12][13] | ~2 años (fundada en 2024) [12] | sin dato. La usan >25% de las Fortune 500 [12] | Red-teaming automatizado y evaluación de seguridad de agentes, integrados en OpenAI Frontier. El CLI sigue siendo open source [12][13] |
| Pillar Security | Vanta | 9-nov-2026 (acuerdo definitivo) [14] | No divulgado. Calcalist reportó ~$150M y un vocero lo disputó [14][15] | $9M [14][16] | ~3 años (fundada en 2023) [14] | sin dato (entre 20 y 33 empleados) [14] | Descubrir, testear, asegurar y gobernar agentes. Une el compliance de Vanta con la ejecución de controles en runtime. Testing en primavera de 2027 y runtime en verano de 2027 [14] |
| Oasis Security | Cyera | 28-jul-2026 → 3-sep-2026 [1] | ~$1B reportado [1] | sin dato | sin dato | sin dato | Identidades no humanas (NHI) y de agentes [1] |
| Haize Labs | Beacon Software (holding de Toronto) | 17-sep-2026 [17] | No divulgado [17] | sin dato | sin dato | sin dato | Red-teaming y confiabilidad de agentes. El equipo pasa a ser el "Applied AI Research Group" para 45 empresas de software del portafolio [17] |
| Graphite | Cursor | 19-dic-2025 [18] | No divulgado [18] | sin dato | sin dato | sin dato | Revisión de código y stacked PRs, para verificar código escrito por IA. Seguirá como producto independiente [18] |
| Langfuse | ClickHouse | ene-2026 [19] | No divulgado | sin dato | sin dato | sin dato | Observabilidad, evals y gestión de prompts para LLM (open source, MIT) [19] |
| Galileo | Cisco | ~abr-2026 → cerrado (actualización del 22-may-2026) [20][21] | No divulgado [21] | sin dato | ~5 años (fundada en 2021) [21] | sin dato | Evaluación y observabilidad de agentes y guardrails en producción. Va a Splunk Observability [20][21] |

## Otros deals relevantes encontrados (2025–2026)

| Comprada | Comprador | Fecha | Precio | Capacidad / nota |
|---|---|---|---|---|
| Astrix Security | Cisco | 4-may-2026 → 29-jun-2026 [22] | ~$400M reportado [1] | NHI y agentes: descubrimiento, ciclo de vida, detección de credenciales comprometidas. Fundada "hace cinco años" [22] |
| Acuvity | Proofpoint | 12-feb-2026 [23] | No divulgado [23] | Inspección y enforcement en runtime sobre apps, agentes y servidores MCP, incluido IA local y navegador [23] |
| AllTrue.ai | Varonis | ~feb-2026 [24] | No divulgado [24] | AI-SPM, shadow AI, gateway de runtime, AIDR, testing y compliance [24] |
| Virtue AI | Fortinet | 17/18-ago-2026 [1][25] | "Inmaterial" según Fortinet [25] | Red-teaming con más de 100 algoritmos de ataque y guardrails multimodales que bloquean acciones de agentes. Había levantado $30M [25] |
| Guardrails AI | Harvey | 9-sep-2026 [26] | No divulgado [26] | Framework open source de guardrails (más de 250k descargas al mes) y Snowglobe, una simulación con usuarios sintéticos. Es la 4.ª compra de Harvey en 2026 [26][27] |
| Portkey | Palo Alto Networks | 30-abr-2026 → 29-may-2026 [1] | $117M (SEC, tracker) [1] | AI gateway |
| Natoma | Snowflake | 27-may-2026 → 3-jun-2026 [1] | $128,3M (SEC, tracker) [1] | Identidad y acceso para agentes y MCP (según el tracker) |
| LayerX | Akamai | 14-may-2026 → 2-jul-2026 [1] | $205M (SEC, tracker) [1] | Seguridad en el navegador y shadow AI |
| Entro Security | SailPoint | 15-jun-2026 → 29-jun-2026 [1] | $122,6M (SEC, tracker) [1] | NHI y secretos |
| Permiso Security | Okta | 30-jul-2026 → 26-ago-2026 [1] | No divulgado [1] | Detección de amenazas de identidad |
| Fabrix Security | Silverfort | 28-abr-2026 [1] | No divulgado [1] | Identidad |
| Ryft | Cyera | 23-abr-2026 [1] | No divulgado [1] | (sin dato de capacidad) |
| SGNL | CrowdStrike | 8-ene-2026 → 20-feb-2026 [1] | $637,1M (SEC, tracker) [1] | Autorización continua y acceso just-in-time |
| Veza | ServiceNow | 2-dic-2025 → 2-mar-2026 [1] | $1,20B (SEC, tracker) [1] | Gobernanza de acceso e identidad |
| Securiti AI | Veeam | 21-oct-2025 → 11-dic-2025 [1] | $1,73B reportado [1] | Seguridad de datos y gobernanza de IA |
| Axiom Security | Okta | 26-ago-2025 → 4-sep-2025 [1] | $54M (SEC, tracker) [1] | Acceso privilegiado |
| Stytch | Twilio | 30-oct-2025 → 14-nov-2025 [1] | $104,1M (SEC, tracker) [1] | Autenticación (incluye la autenticación de agentes) |
| Aporia | Coralogix | sin dato | sin dato | Observabilidad de IA en runtime [2] |
| CyberArk | Palo Alto Networks | 30-jul-2025 → 11-feb-2026 [1] | $21,10B (SEC, tracker) [1] | Identidad y privilegios, incluidas identidades de máquina (es contexto: no es una startup de IA) |
| Wiz | Google | 18-mar-2025 → 11-mar-2026 [1] | $29,47B (SEC, tracker) [1] | Seguridad cloud. Es la mayor compra de seguridad de un grande de IA, pero no es seguridad de IA en sentido estricto |

## Laboratorios y plataformas grandes (OpenAI, Anthropic, Google, Microsoft, Nvidia, Databricks)

- **OpenAI:** compró Promptfoo, su única compra de *seguridad de IA* que encontré [12].
- **Anthropic:** no encontré ninguna compra de seguridad. Sus compras fueron Bun (dic-2025), Vercept (computer use, 25-feb-2026; el producto externo se cerró), Coefficient Bio (~$400M reportado, abr-2026) y Stainless (SDKs, may-2026, una sola fuente) [28][29][30].
- **Google:** compró Wiz ($29,47B, seguridad cloud) [1]. No encontré ninguna compra específica de seguridad de IA.
- **Nvidia:** compró Gretel, de datos sintéticos, el 19-mar-2025 por un precio de "nueve cifras" según Wired, no confirmado. Gretel tenía >$67M levantados y una valuación de $320M [31]. Es datos para entrenamiento, no seguridad.
- **Microsoft y Databricks:** sin dato. Una búsqueda no encontró compras de seguridad de IA [32], pero no pude verificar con búsquedas dirigidas porque se agotó el presupuesto.
- **Patrón:** los laboratorios casi no compran seguridad. Quienes compran son los vendors de ciberseguridad (PANW, Cisco, CrowdStrike, Check Point, SentinelOne, Zscaler, F5, Fortinet, Proofpoint, Okta, Varonis, Akamai) y, cada vez más, las empresas de aplicaciones de IA, que compran confiabilidad y evals para uso propio: Harvey (Guardrails), Beacon (Haize), Cursor (Graphite), ClickHouse (Langfuse) y Snowflake (Natoma).

## Volumen

- SecurityWeek contó 13 deals de M&A con empresas de IA en 2025, contra 8 en 2024, sobre 426 deals de ciberseguridad en total. El dato viene del resumen de una búsqueda sobre SecurityWeek y no pude ver la página exacta.
- ISMG dice que Cisco, con Robust Intelligence en 2024, fue la primera compra, que siguieron unas 11 más en 2025 y que los tamaños van de ~$20M a más de $600M [2].
- Según ISMG, en septiembre de 2025 Cato, Check Point, CrowdStrike, F5 y SentinelOne acordaron pagar en conjunto **$1,31B** [2].

---

## Análisis

### (1) Capacidades que ya compraron todos los grandes (categoría consolidada, no entrar)

| Capacidad | Compras | Ya la tienen |
|---|---|---|
| **Guardrails y firewall de prompts en runtime** (prompt injection, jailbreak, fuga de datos) | Lakera, Prompt, Aim, CalypsoAI, Pangea, Acuvity, AllTrue, Virtue, Pillar, Guardrails AI | Check Point, SentinelOne, Cato, F5, CrowdStrike, Proofpoint, Varonis, Fortinet, Vanta, Harvey |
| **Red-teaming automatizado de LLM y agentes** | Robust Intelligence, Promptfoo, SPLX, CalypsoAI, Lakera Red, Haize, Virtue | Cisco, OpenAI, Zscaler, F5, Check Point, Fortinet |
| **Shadow AI, AI-SPM y uso de GenAI por empleados** | Prompt, Aim, AllTrue, Apex, LayerX | |
| **Escaneo de modelos y supply chain de ML** | Protect AI, Koi | |
| **Identidad no humana y de agentes** (NHI, secretos, acceso just-in-time) | Astrix, Oasis (~$1B), Entro, SGNL, Veza, Axiom, Permiso, Natoma, Stytch, CyberArk | Es la categoría con los cheques más grandes |
| **Gateway de IA y MCP** | Portkey, Invariant, Acuvity, Natoma | |
| **Observabilidad y evals de LLM** | Langfuse, Galileo, Aporia | |

Forrester ya en sep-2025 esperaba que el escaneo de modelos, el filtrado de prompts, el sandboxing de agentes y el DLP para IA terminaran como funciones dentro de los firewall, XDR y SASE existentes [3].

**Conclusión:** entrar con "otro firewall de prompts", "otro red-teamer de LLM", "otro descubridor de shadow AI" o "otra plataforma de NHI" es competir contra funciones que vienen gratis en plataformas que el cliente ya paga.

### (2) Capacidades que ningún grande tiene todavía

Esto es inferencia: sale de lo que **no** aparece entre las ~45 compras revisadas, no de una fuente que diga "nadie lo tiene". Hay que validarlo con las otras notas (p. ej. 31-matriz-mar-azul).

- **Seguridad de agentes *después* del incidente: forense, reconstrucción causal y reversión de acciones.** Todo lo comprado es prevención (guardrails), testing previo (red-team) o detección (AIDR). No vi a nadie comprar "qué hizo el agente, por qué y cómo lo deshago".
- **Seguridad entre agentes de distintas organizaciones** (agente↔agente, comercio agéntico, confianza y reputación de agentes externos). Las compras de identidad cubren las identidades *propias* de la empresa (NHI) e Invariant cubre MCP, pero no hay compras sobre agentes de terceros que interactúan entre sí.
- **AI safety propiamente dicho**: monitoreo de engaño, sabotaje o "scheming", evals de capacidades peligrosas (CBRN, ciber ofensivo) y monitoreo de cadenas de razonamiento. Ninguna compra de la lista apunta a eso. Los laboratorios no compran seguridad y los vendors compran seguridad de *aplicación*.
- **Integridad en tiempo de entrenamiento** (envenenamiento de datos y fine-tunes, procedencia de datasets) y seguridad de pesos de modelos. Protect AI y Koi escanean artefactos, pero nadie compró defensa contra el envenenamiento como categoría.
- **Evidencia de cumplimiento verificable para reguladores** (EU AI Act, auditoría de agentes). Vanta–Pillar es el primer movimiento, recién en nov-2026 y con runtime previsto para 2027 [14]. Está temprano, no vacío.
- **Segmentos desatendidos**: pymes, idioma español y LatAm. Todas las compras son de vendors enterprise de EE. UU. o Israel. Ver 13-region-latam.

### (3) Tiempo y múltiplos típicos de fundación a salida

| Startup | Años hasta la salida | Capital levantado | Precio | Precio / capital |
|---|---|---|---|---|
| Robust Intelligence | ~5 | $44M | ~$400M (reportado) | ~9x |
| Protect AI | ~3 | $108,5M | $634,5M (SEC, tracker) | ~5,8x |
| Koi | sin dato | $48M | $231M (SEC) / $400M (reportado) | 4,8x / 8,3x |
| CalypsoAI | sin dato | >$40M | $180M (confirmado) | ≤4,5x |
| Prompt Security | sin dato | $23M (a nov-2024) | ~$160M (10-Q) | ~7x (techo, si no levantó más después) |
| Aim Security | ~3 | $28M | $300–350M (reportado) | ~11–12,5x |
| Pangea | ~4 | ~$51M | $222,7M (SEC) / ~$260M (reportado) | ~4,4–5x |
| Pillar | ~3 | $9M | ~$150M (reportado y disputado) | ~16x |
| Promptfoo | ~2 | $23M | no divulgado (valuación previa $86M) | n/d |

- **Tiempo:** la mediana ronda los **3–4 años** desde la fundación. Hay casos de ~2 años (Promptfoo) y de ~5 (Robust Intelligence, Galileo, Astrix).
- **Múltiplo sobre capital levantado:** típicamente **~4x–12x**. Con los precios del filing ante la SEC queda en ~4,5–7x. Los precios reportados por la prensa israelí suelen ser más altos que los de la SEC, p. ej. Lakera $300M vs $201,8M y Koi $400M vs $231M [1][6][7]. Hay que descontarlos.
- **Tamaño:** las compras de seguridad de IA "pura" van de ~$40M a ~$650M. Los precios de $1B o más aparecen solo en identidad y datos (Oasis, Veza, Securiti) o en plataformas amplias (CyberArk, Wiz) [1].
- **Múltiplo sobre ingresos:** sin dato. Ninguna fuente publicó ARR.
- **Forma de salida:** muchas son acqui-hire o compras tuck-in de productos tempranos. Forrester las describe como empresas chicas, con pocos productos y cloud-native [3]. Fortinet llamó "inmaterial" el precio de Virtue AI [25] y Beacon convirtió a Haize en un grupo de investigación [17].

### (4) Implicancias para elegir un problema nuevo

1. **No construir una feature que ya es SKU de un grande.** Guardrails, red-teaming de LLM, shadow AI, escaneo de modelos y NHI ya están comprados por 10 o más vendors. Un jurado que conozca el mercado lo va a notar.
2. **Ir donde el comprador natural todavía no compró.** Hay tres candidatos:
   - (a) respuesta a incidentes, forense y reversión de acciones de agentes;
   - (b) confianza entre agentes de distintas organizaciones;
   - (c) safety a nivel de comportamiento del modelo (engaño, sabotaje, monitoreo de razonamiento).

   Los tres son extensiones lógicas de las plataformas que compraron guardrails y AIDR, así que tienen comprador futuro.
3. **Los nuevos compradores son las empresas de IA aplicada.** Harvey, Cursor, Beacon, ClickHouse y Snowflake compran confiabilidad y evals para su propio producto. Un problema de "confiabilidad y seguridad de agentes en un dominio vertical" tiene salida por ahí, no solo por los vendors de ciberseguridad.
4. **La ventana es corta.** Si la salida típica llega a los 3–4 años y las categorías se consolidan en 12–18 meses (las 8 compras que contó Forrester ocurrieron en 18 meses [3]), hay que elegir algo que hoy esté en la etapa en que estaban los guardrails en 2023: con dolor real y demostrable, pero sin un líder claro.
5. **Para el demo:** mostrar por qué el problema elegido **no** se resuelve con Prisma AIRS, Cisco AI Defense, Check Point/Lakera o CrowdStrike AIDR. Es la objeción que va a aparecer primero.

---

## Fuentes

- [1] Tracker de consolidación (Deepak Gupta), con precios que dice basados en SEC: https://guptadeepak.com/agent-security/deals/
- [2] ISMG/BankInfoSecurity, 8-oct-2025: https://www.bankinfosecurity.com/blogs/ai-security-goes-mainstream-as-vendors-spend-heavily-on-ma-p-3953
- [3] Forrester, "Securing AI's M&A Feeding Frenzy Is On", 22-sep-2025: https://www.forrester.com/blogs/securing-ais-ma-feeding-frenzy-is-on/
- [4] SecurityWeek sobre Cisco y Robust Intelligence: https://www.securityweek.com/cisco-to-acquire-ai-security-firm-robust-intelligence/ y SiliconANGLE: https://siliconangle.com/2024/08/27/cisco-snaps-ai-model-data-security-startup-robust-intelligence/
- [4b] CB Insights, Protect AI (fundada en 2022): https://www.cbinsights.com/company/robust-intelligence/financials (resultado de búsqueda sobre CB Insights; no abrí la página de Protect AI)
- [5] SecurityWeek, PANW y Protect AI: https://www.securityweek.com/palo-alto-networks-to-acquire-ai-security-firm-protect-ai/ y Series B: https://www.securityweek.com/protect-ai-raises-60-million-in-series-b-funding/
- [6] SecurityWeek, PANW y Koi: https://www.securityweek.com/palo-alto-networks-to-acquire-koi-in-reported-400-million-transaction/
- [7] SecurityWeek, Check Point y Lakera: https://www.securityweek.com/check-point-to-acquire-ai-security-firm-lakera/
- [8] SecurityWeek, "F5 to Acquire CalypsoAI for $180 Million": https://www.securityweek.com/f5-to-acquire-calypsoai-for-180-million/
- [9] F5, AI Guardrails y AI Red Team: https://www.f5.com/company/blog/what-are-ai-guardrails
- [10] SecurityWeek, roundups y notas de Aim y Pangea: https://www.securityweek.com/cato-networks-acquires-ai-security-firm-aim-security/ · https://www.securityweek.com/crowdstrike-to-acquire-pangea-to-launch-ai-detection-and-response-aidr/ · https://www.securityweek.com/prompt-security-raises-18-million-for-gen-ai-security-platform/ · 10-Q de SentinelOne: https://www.sec.gov/Archives/edgar/data/0001583708/000158370826000041/s-20260430.htm
- [11] TechRepublic, Zscaler y SPLX: https://www.techrepublic.com/article/news-zscaler-buys-splx/
- [12] TechCrunch, OpenAI y Promptfoo, 9-mar-2026: https://www.techcrunch.com/2026/03/09/openai-acquires-promptfoo-to-secure-its-ai-agents/
- [13] SecurityWeek, OpenAI y Promptfoo: https://www.securityweek.com/openai-to-acquire-ai-security-startup-promptfoo/
- [14] Vanta y Pillar: https://www.govinfosecurity.com/vanta-buys-pillar-to-tie-ai-governance-to-real-time-controls-a-33367 · https://www.calcalistech.com/ctechnews/article/hkjzjkjrfl
- [15] RuntimeWire, "reported $150M": https://runtimewire.com/article/vanta-acquire-pillar-security-reported-150m-ai-agents
- [16] Unite.AI: https://unite.ai/vanta-signs-deal-to-acquire-ai-security-firm-pillar-security
- [17] Beacon y Haize Labs: https://www.morningstar.com/news/business-wire/20260917239094/beacon-acquires-haize-labs-to-power-ai-for-the-real-economy · https://betakit.com/beacon-buys-new-yorks-haize-labs-to-boost-ai-reliability-across-its-portfolio/
- [18] Cursor y Graphite: https://techcrunch.com/2025/12/19/cursor-continues-acquisition-spree-with-graphite-deal · https://fortune.com/2025/12/19/cursor-ai-coding-startup-graphite-competition-heats-up/ · https://cursor.com/blog/graphite
- [19] ClickHouse y Langfuse: https://clickhouse.com/blog/clickhouse-acquires-langfuse-open-source-llm-observability · https://www.infoworld.com/article/4118621/clickhouse-buys-langfuse-as-data-platforms-race-to-own-the-ai-feedback-loop.html · https://langfuse.com/blog/joining-clickhouse
- [20] Cisco y Galileo: https://blogs.cisco.com/news/cisco-announces-the-intent-to-acquire-galileo · https://www.cisco.com/site/us/en/about/corporate-development/acquisitions/galileo/index.html
- [21] TechTarget, 13-abr-2026: https://www.techtarget.com/it-infrastructure/news/366641600/Cisco-Galileo-buy-reflects-blurring-lines-in-AI-observability
- [22] Cisco y Astrix: https://blogs.cisco.com/news/cisco-announces-intent-to-acquire-astrix-security
- [23] Proofpoint y Acuvity: https://www.proofpoint.com/us/newsroom/press-releases/proofpoint-acquires-acuvity-deliver-ai-security-and-governance-across
- [24] Varonis y AllTrue.ai: https://www.varonis.com/blog/varonis-acquires-alltrue-ai-security
- [25] SecurityWeek, Fortinet y Virtue AI: https://www.securityweek.com/fortinet-acquires-ai-security-company-virtue-ai/
- [26] Harvey y Guardrails AI: https://www.harvey.ai/blog/guardrails-ai-joins-harvey
- [27] Dealroom: https://dealroom.co/news/149921-harvey-acquires-guardrails-ai-in-its-fourth-deal-of-2026/
- [28] Anthropic y Vercept: https://anthropic.com/news/acquires-vercept · https://geekwire.com/2026/anthropic-acquires-vercept-in-early-exit-for-one-of-seattles-standout-ai-startups
- [29] Anthropic y Coefficient Bio (reportado): https://siliconangle.com/2026/04/03/anthropic-reportedly-acquires-medical-ai-startup-coefficient-bio-400m/
- [30] Anthropic y Stainless (una sola fuente): https://yourstory.com/ai-story/anthropic-acquires-dev-tools-startup-used-by-openai
- [31] TechCrunch, Nvidia y Gretel: https://techcrunch.com/2025/03/19/nvidia-reportedly-acquires-synthetic-data-startup-gretel/
- [32] Búsqueda sin resultados para Microsoft y Databricks (no es prueba de que no haya compras).
- Contexto adicional: Bloomberg sobre OpenAI y Promptfoo: https://www.bloomberg.com/news/articles/2026-03-09/openai-buying-ai-security-startup-promptfoo-to-safeguard-ai-agents
