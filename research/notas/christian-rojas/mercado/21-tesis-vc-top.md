# 21 — Tesis y portafolio de seguridad de IA de los VCs generalistas top

Research: 21-nov-2026. Fuentes priorizadas de 2025–2026. Regla: cada dato con URL; si no hay fuente, "sin dato".

**Limitaciones:** se agotó el presupuesto de búsquedas web a mitad del trabajo. No se pudo verificar: Goodfire (montos y quién lideró además de B Capital), tesis escritas de Kleiner Perkins, Craft, Scale VP y Redpoint, ni cartera actual de Anthology Fund en seguridad. Los montos marcados "(secundaria)" vienen de prensa o agregadores, no de la página del fondo.

---

## 1. Fondo por fondo

### a16z
- **(a) Inversiones**
  - Keycard: 38M (dato dado por el equipo; existe podcast a16z "Keycard: 2026 is the year of agents", https://a16z.com/podcast/keycard-2026-is-the-year-of-agents/).
  - Neo: a16z invirtió (https://a16z.com/announcement/investing-in-neo/). La Serie A de 100M la lideró Bessemer (https://www.bvp.com/news/neo-security-securing-ai-agents-at-the-endpoint). Neo rastrea agentes, extensiones y servidores MCP en endpoints y aplica políticas en tiempo real.
  - Armadin (ofensiva autónoma): a16z co-lideró la Serie B junto con Kevin Mandia; monto sin dato (https://a16z.com/the-new-security-agenda/).
- **(b) Tesis:** "The New Security Agenda", 28-oct-2026, encuesta a 100 CISOs (https://a16z.com/the-new-security-agenda/).
  - Compras previstas a 12 meses: seguridad de agentes internos 45%, ofensiva 42%, uso y gobernanza de IA 38%.
  - 55% de las empresas ya corre servidores MCP. 46% teme que un agente exceda permisos o sea comprometido.
  - 44% busca primero en su plataforma actual; 21% en vendors nativos de IA.
  - Ensayo previo: "Breaking the cybersecurity kill chain with AI", que propone ordenar el mercado por etapa de la kill chain (https://a16z.com/breaking-the-cybersecurity-kill-chain-with-ai/).
- **(c) Problemas abiertos que nombra**
  - "Fix it with the find it": remediar y re-testear, no solo encontrar.
  - Testing ofensivo continuo en CI/CD.
  - Distinguir acciones de agentes de las del empleado (las herramientas de endpoint y DLP no lo logran).
  - Cuánta autonomía dar al SOC.
  - Seguridad de código a escala.
  - Mercados con hasta 43 vendors, donde el comprador no puede comparar.

### Sequoia
- **(a) Inversiones**
  - AIR Security, firewall de supply chain para agentes: 50M en total, con Sequoia liderando los primeros 10M y Greenoaks los 40M siguientes; 1-sep-2026 (https://dealroom.co/news/148163-air-raises-50m-seed-to-build-a-firewall-for-ai-agents/; https://sequoiacap.com/article/partnering-with-air-securing-the-ai-supply-chain).
  - Cymphony, identidad y datos de agentes como un solo problema: 30M en total (seed + Serie A de 25M co-liderada con SMBC), valuación de más de 100M; sep-2026 (https://theaiinsider.tech/2026/09/09/sequoia-leads-30m-round-for-cymphony-to-secure-enterprise-ai-agents/).
  - Corma, modelo de IA para ciberdefensa: seed de 60M liderado por Sequoia, con Khosla y Coatue; ago-2026 (https://thebridge.jp/2026/08/corma-cyber-defense-ai-60m-seed).
  - Irregular, seguridad de modelos frontera: 80M co-liderado con Redpoint; 17-sep-2025 (https://techcrunch.com/2025/09/17/irregular-raises-80-million-to-secure-frontier-ai-models).
  - Oasis: Sequoia participa como inversor existente en la Serie B de 120M (dato del equipo; https://www.securityweek.com/oasis-security-raises-120-million-for-agentic-access-management/).
- **(b) Tesis:** no hay mapa propio. La tesis está en el post de AIR: la supply chain del agente (skills, plugins, MCP, subagentes) se arma en runtime y "often nobody is inspecting it" (https://sequoiacap.com/article/partnering-with-air-securing-the-ai-supply-chain).
- **(c) Problema abierto:** responder "qué está corriendo el agente, de dónde vino y quién lo revisó". Sequoia busca el system of record de esa respuesta.

### Lightspeed
- **(a) Inversiones**
  - A Security, ofensiva autónoma: 37M liderado por Lightspeed; jun-2026 (https://fortune.com/2026/06/08/lightspeed-wiz-assaf-rappaport-37-million-ai-powered-cyberattacker-a/).
  - Descope, IAM para agentes y servidores MCP: Lightspeed "dobló la apuesta" en sep-2025; monto sin dato (https://lsvp.com/stories/doubling-down-on-lightspeeds-investment-in-descope-the-next-gen-iam-platform-for-customers-partners-and-ai-agents/).
  - Straiker: en portafolio, con tesis publicada (https://www.straiker.ai/blog/investor-thesis-lightspeed); ronda de 64M (https://www.securityweek.com/straiker-raises-64-million-for-ai-security-platform/amp/). Quién lideró: sin dato.
  - Endor Labs, seguridad de código generado por IA (https://lsvp.com/stories/adding-a-security-layer-to-the-ai-coding-stack/).
  - Cylake (https://lsvp.com/stories/our-investment-in-cylake/).
  - Ocean Security, email agéntico (https://lsvp.com/company/ocean-security/).
  - P0 Security y Clutch Security (NHI) aparecen como portafolio en Cyber60.
- **(b) Tesis:** Cyber60 2026-27, encuesta a 200 CISOs hecha el 4–14 de sep-2026 (https://lsvp.com/cyber60-2026-2027/).
  - **6 áreas de oportunidad:** gobernanza de identidad y acceso de agentes; seguridad de agentes en runtime; respuesta autónoma confiable; AppSec para código generado por IA; fuga de datos y control de shadow AI; defensa contra engaño generado por IA.
  - **Datos de la encuesta:**
    - 77% tiene agentes en producción.
    - Solo 20% tiene inventario completo de agentes.
    - 34% usa o planea identidades por agente; 26% usa o usaría credenciales humanas.
    - Incidentes de IA sospechados: 63%, contra 38% el año anterior.
- **(c) Problemas abiertos**
  - Agentes que expanden sus permisos gradualmente.
  - Que un agente comprometido no contagie a otros; autorización en tiempo real de llamadas multi-agente.
  - Trust scores basados en comportamiento.
  - Instrucciones ocultas en documentos, emails y webs.
  - Attestation de pesos, dependencias, datasets de fine-tuning y plugins, incluido OT/SCADA.
  - Respuesta autónoma con precisión probada, auditoría y rollback.

### Accel
- **(a) Inversiones**
  - depthfirst, AppSec con agentes: Serie A de 40M liderada por Accel; 14-ene-2026 (https://techcrunch.com/2026/01/14/ai-security-firm-depthfirst-announces-40-million-series-a).
  - Prophet Security, AI SOC: Serie A de 30M liderada por Accel; ago-2025 (https://builtin.com/articles/prophet-security-raises-30m-series-a-20250804).
  - Armadin, ofensiva nativa de IA: Accel lideró la Serie A (https://www.accel.com/news/leading-armadin-s-series-a-building-the-industry-s-first-ai-native-offensive-cyber-platform). Cobertura secundaria reporta 189,9M en seed + Serie A en mar-2026, con GV, Kleiner, Menlo e In-Q-Tel; URL primaria no verificada.
  - AegisAI, email agéntico (https://www.accel.com/news/ai-native-security-for-the-new-era-of-email-threats-our-investment-in-aegisai).
  - Oasis: inversor existente en la Serie B de 120M (dato del equipo).
- **(b) Tesis:** sin mapa publicado. En el post de Armadin, Accel dice que la defensa con humanos en el loop ya no alcanza y que "the best offense is the best defense".
- **(c) Problema abierto:** la asimetría entre ataques a velocidad de IA y defensa humana, y la falta de una respuesta continua a "¿estamos seguros ahora mismo?".

### Index Ventures
- **(a) Inversiones**
  - 7AI, agentes de seguridad (AI SOC): Serie A de 130M liderada por Index, 166M acumulados; fecha sin dato (https://www.indexventures.com/perspectives/securitys-agentic-era-starts-here-our-investment-in-7ai/).
  - NewCore, identidad para humanos, máquinas y agentes: aparece como portafolio de Index en resultados de búsqueda; URL primaria y monto sin dato.
  - Venice, PAM para la era de IA: 33M (secundaria; https://www.indexventures.com/perspectives).
  - Resistant AI, ML adversarial y fraude (https://www.indexventures.com/companies/resistant-ai/).
- **(b) Tesis:** Shardul Shah en el podcast Equity, "The old cybersecurity model is breaking", resumido el 23-sep-2026 (https://ecosistemastartup.com/index-ventures-el-viejo-modelo-de-ciberseguridad-se-rompio/). Prefiere plataformas multi-caso "a lo Wiz".
- **(c) Problema abierto:** según Index, el capital migra hacia capas que "aún no existen": monitoreo de intención de agentes, permisos dinámicos y respuesta en tiempo real. Contexto: ola de adquisiciones (Cyata, Cyclops y Rotate por Check Point; Astrix por Cisco; SGNL por CrowdStrike; SquareX por Zscaler; misma fuente).

### Greylock
- **(a) Inversiones**
  - Tenzai, hackers IA autónomos: seed de 75M liderado por Greylock (https://greylock.com/portfolio-news/introducing-tenzai-autonomous-ai-hackers/).
  - Cylake, seguridad nativa de IA con soberanía de datos: seed de 45M liderado por Greylock (https://greylock.com/?p=13500).
  - Cogent Security, agentes para gestión de vulnerabilidades: seed de 11M liderado por Greylock en jul-2025 (https://www.axios.com/pro/enterprise-software-deals/2025/07/14/vulnerability-management-cogent-security-11m-seed). Serie A de 42M liderada por Bain Capital Ventures, con Greylock.
  - Fable Security, human risk: seed de 6,5M liderado por Greylock (https://greylock.com/?p=13169).
- **(b) Tesis:** sin mapa publicado. En el post de Cogent dice que la IA es "una superficie nueva y hoy no asegurada" y señala las identidades de agentes como nueva superficie (https://greylock.com/blog/introducing-cogent-ai-agents-for-vulnerability-management/).
- **(c) Problema abierto:** gobernar identidades de agentes. Su patrón es liderar seeds grandes vía el incubador Greylock Edge.

### Menlo Ventures, incluido Anthology Fund
- **(a) Inversiones**
  - Portafolio marcado en su mapa: Semgrep, Strata Identity, Astrix, Cequence, Obsidian y Relyance AI; montos sin dato (https://menlovc.com/perspective/security-for-agents-and-agents-for-security-the-next-cybersecurity-frontier/). Astrix ya fue adquirida por Cisco (ver Index).
  - Armadin: Menlo participó (secundaria, ver Accel).
  - RunSybil, ofensiva: Menlo y **Anthology Fund** participaron en la ronda de 40M que lideró Khosla; 18-mar-2026 (https://fortune.com/2026/03/18/exclusive-ai-cybersecurity-startup-runsybil-founded-by-openais-first-security-hire-raises-40-million-led-by-khosla-ventures/).
  - Anthology Fund: 100M, cheques desde 100k. Su primera cohorte de dic-2024 incluyó a Astrix (https://www.globenewswire.com/news-release/2024/12/18/2999231/0/en/Menlo-Ventures-Announces-Cohort-Backed-by-the-100M-Anthology-Fund-Launched-in-Partnership-with-Anthropic.html). La página actual del fondo no lista cartera de seguridad (https://menlovc.com/menlo-anthology-fund/).
  - Goodfire, interpretabilidad: no verificado en esta sesión.
- **(b) Tesis**
  - "Security for Agents and Agents for Security", 29-jul-2025 (URL de arriba). Mapa en 4 categorías: **Build** (AppSec de código de agentes), **Access/Auth** (IAM de agentes), **Run** (gateways y sandboxing) y **Observe & Govern** (monitoreo, evals y red-team).
  - Follow-up del 20-nov-2025, "Agents for Security" (https://menlovc.com/perspective/agents-for-security-and-the-opportunity-to-disrupt-securitys-giants/).
  - Mapa anterior "Security for AI", feb-2024 (https://menlovc.com/perspective/security-for-ai-genai-risks-and-the-emerging-startup-landscape/).
- **(c) Problemas abiertos**
  - Auditabilidad y forense de razonamiento caja negra.
  - Logging de cadenas multi-paso.
  - **Atribución en tiempo real de quién autorizó y quién ejecutó** una acción.
  - Escribir políticas cuando no se puede predecir qué herramienta usará el agente.
  - Detectar anomalías cuando lo "normal" es variable.

### General Catalyst
- **(a) Inversiones**
  - Geordie, monitoreo y gobernanza de agentes con intervención "Beam": GC co-lideró el seed; 9-sep-2025 (https://www.generalcatalyst.com/stories/seeding-the-future-with-geordie). Monto de 6,5M según BusinessWire (https://www.businesswire.com/news/home/20250909556381/en). Una Serie A de 30M en may-2026 no está verificada.
  - Portia AI, SDK de agentes con supervisión: seed liderado por GC en abr-2025; monto sin dato (https://www.generalcatalyst.com/stories/our-investment-in-portia-ai).
- **(b) Tesis:** "AI adoption moves at the speed of trust". Los agentes necesitan seguridad tan autónoma como ellos. Sin mapa.
- **(c) Problemas abiertos:** no existe un punto medio donde el riesgo de agentes esté bien gestionado; falta remediación autónoma y consciente de contexto a escala.

### Khosla Ventures
- **(a) Inversiones**
  - Runlayer, gobernanza y seguridad de MCP: seed de 11M con Keith Rabois y Felicis; nov-2025 (https://techcrunch.com/2025/11/17/mcp-ai-agent-security-startup-runlayer-launches-with-8-unicorns-11m-from-khoslas-keith-rabois-and-felicis).
  - RunSybil, ofensiva: 40M liderado por Khosla; 18-mar-2026 (Fortune, URL de arriba).
  - Exaforce, AI SOC: Serie A de 75M co-liderada con Mayfield y Thomvest; fecha sin dato (https://www.nasdaq.com/articles/exaforce-lands-75m-bring-ai-agents-security).
  - Corma: participa en el seed de 60M (ver Sequoia).
- **(b) Tesis:** sin dato. No se encontró ensayo propio.
- **(c) Problemas abiertos:** sin dato.

### Kleiner Perkins
- **(a) Inversiones:** Armadin, como participante (secundaria). No se encontró ninguna ronda de seguridad de agentes liderada por Kleiner en 2025–2026.
- **(b) Tesis:** cerró 3,5B en KP22 y KP Select IV en mar-2026, con security entre sus áreas (https://kleinerperkins.com/perspectives/our-new-funds-kp22-select-iv-flex). Sin ensayo específico.
- **(c) Problemas abiertos:** sin dato.

### Bessemer (BVP)
- **(a) Inversiones**
  - Onyx Security, control plane de agentes con modelos pequeños y "Guardian Agents": Serie B de 113M liderada por BVP; 30-jul-2026 (https://www.bvp.com/news/onyx-security-defining-cybersecurity-in-the-agentic-era).
  - Neo: Serie A de 100M liderada por BVP (https://www.bvp.com/news/neo-security-securing-ai-agents-at-the-endpoint).
- **(b) Tesis:** "Securing AI agents: the defining cybersecurity challenge of 2026", 24-mar-2026 (https://bvp.com/atlas/securing-ai-agents-the-defining-cybersecurity-challenge-of-2026).
  - **3 etapas:** Visibilidad (inventario), Configuración (mínimo privilegio y drift) y Protección en runtime.
  - **Superficies:** endpoint (agentes de código), gateway de API y MCP, SaaS e identidad.
  - Versión corta en PDF: https://www.bvp.com/assets/uploads/2026/03/Securing-AI-agents_Building_Differently_Quick_read-.pdf
- **(c) Problemas abiertos**
  - **Enforcement en vuelo: frenar una acción concreta sin romper el workflow.** Bessemer lo llama "la capa menos construida" y "la oportunidad de infraestructura más clara".
  - El inventario como etapa más descuidada.
  - Guardrails a nivel de acción, no solo de acceso.
  - Tracking de drift en tiempo real.

### Insight Partners
- **(a) Inversiones:** su post menciona como portafolio a Teleport, Delinea, Keeper, Keyfactor, Ory, PlainID, Frontegg (identidad), Promptfoo (red-team y evals), E2B (sandboxing), Fiddler y HoneyHive (observabilidad), Reco, Skyflow, Anjuna y Kiteworks (datos). Montos y fechas de rondas de IA 2024–2026: sin dato.
- **(b) Tesis:** "Securing agentic AI", 29-oct-2025 (https://www.insightpartners.com/ideas/securing-agentic-ai). **5 áreas:** identidad y acceso de agentes; gobernanza, observabilidad y monitoreo; seguridad de integraciones (MCP, A2A); amenazas novedosas a agentes; privacidad y seguridad de datos. Hay un mapa previo de jul-2025 (https://www.insightpartners.com/ideas/securing-ai/).
- **(c) Problemas abiertos**
  - **"Credential Zero":** cómo se autentica el agente ante el vault o IdP.
  - Trazar si el agente actuó por su cuenta o por instrucción humana (OAuth 2.0 no lo resuelve).
  - Account takeover de agentes y servidores MCP maliciosos.
  - Agentes maliciosos en sistemas multi-agente.
  - Detectar exceso de scope y corregir tras una subversión.
  - Linaje y residencia de datos que viajan entre agentes de distintas jurisdicciones.

### Redpoint
- **(a) Inversiones**
  - JetStream Security, gobernanza de IA: seed de 34M liderado por Redpoint, con el Falcon Fund de CrowdStrike; mar-2026 (https://siliconangle.com/?p=733000).
  - Irregular: 80M co-liderado con Sequoia; sep-2025 (TechCrunch, URL de arriba).
- **(b) Tesis:** sin dato. Su hub de contenido de IA no tiene un ensayo de seguridad identificado (https://www.redpoint.com/content-hub/category/ai).
- **(c) Problemas abiertos:** sin dato.

### Felicis
- **(a) Inversiones:** Runlayer, seed de 11M (nov-2025) y Serie A de 30M liderada (preempt) por Felicis el 24-jun-2026, 42M acumulados (https://fortune.com/2026/06/24/exclusive-vinod-khosla-felicis-runlayer-nanit-30-million-enterprise-ai/; https://www.felicis.com/blog/runlayer-series-a-how-enterprises-actually-become-ai-native).
- **(b) Tesis:** MCP es el chokepoint donde debe vivir la gobernanza. Ganará quien haga que el camino sancionado sea el más fácil: prohibir no funciona.
- **(c) Problemas abiertos**
  - Seguridad de runtime de MCP "no resuelta".
  - Perder la cuenta de qué agentes corren, a qué acceden y en nombre de quién.
  - MCPs y plugins en la sombra.
  - Competencia: Wiz, Palo Alto y Okta construyen lo mismo (https://dealroom.co/news/135840-runlayer-raises-30m-series-a-led-by-felicis-to-govern-enterprise-ai-agen).

### Craft Ventures
- **(a) Inversiones:** Oasis Security, Serie B de 120M liderada por Craft; 19-mar-2026, 195M acumulados (https://www.securityweek.com/oasis-security-raises-120-million-for-agentic-access-management/; https://www.craftventures.com/articles/our-partnership-with-oasis-security-securing-access-for-the-agentic-era).
- **(b) Tesis:** las identidades no humanas necesitan un modelo de gobernanza propio ("agentic access management"). Sin mapa.
- **(c) Problemas abiertos:** sin dato más allá de lo anterior.

### Madrona
- **(a) Inversiones:** Gray Swan, Serie A de 40M co-liderada con Wing; 28-may-2026 (https://www.madrona.com/gray-swan-series-a/). Tiene tres productos: Arena (red-team continuo contra modelos frontera), Shade (red-team automatizado) y Cygnal (protección en runtime). Sus clientes incluyen Anthropic, OpenAI, Meta y Google DeepMind.
- **(b) Tesis:** resolver la seguridad de IA "primero en la frontera", junto a los labs antes del release. Las superficies de ataque cambian con cada modelo.
- **(c) Problemas abiertos**
  - **No hay un framework acordado de identidad de agentes.**
  - **No hay baseline de protección en runtime.**
  - **No hay un modelo común para hacer red-team de un sistema autónomo** antes de que toque datos de producción.
  - El DLP no sirve ante un modelo que sintetiza información entre contextos.

### Scale Venture Partners
- **(a) Inversiones:** Prime Security, IA agéntica para seguridad: Serie A de 20M co-liderada por Scale; 3-feb-2026 (https://www.scalevp.com/press/exclusive--agentic-ai-startup-prime-security-raises--20m).
- **(b) Tesis:** sin dato.
- **(c) Problemas abiertos:** sin dato.

---

## 2. Síntesis: categoría → nº de fondos (de esta lista) que ya apostaron

Se cuentan los fondos con al menos una inversión verificable 2024–2026 en la categoría, incluida la participación sin liderar. "Tesis" indica cuántas tesis la nombran como oportunidad o problema abierto. Los nombres entre paréntesis son las empresas.

| Categoría | Fondos que apostaron | Nº | Tesis que la nombran | Lectura |
|---|---|---|---|---|
| Identidad/acceso de agentes y NHI | Craft (Oasis), Sequoia (Oasis, Cymphony), Accel (Oasis), a16z (Keycard), Lightspeed (Descope, P0, Clutch), Index (NewCore, Venice), Menlo (Astrix, Strata), Insight (Teleport, Ory, PlainID…) | 8 | Menlo, Insight, Lightspeed, Bessemer, Madrona, Greylock | **Saturada**, con consolidación (Astrix→Cisco, SGNL→CrowdStrike) |
| Control plane / gobernanza / gateway MCP / discovery | Felicis y Khosla (Runlayer), Bessemer (Onyx, Neo), a16z (Neo), GC (Geordie), Redpoint (JetStream), Sequoia (AIR), Menlo (Cequence), Lightspeed (Straiker) | 9 | todas | **Saturada**: 12 rondas y 435M en 5 meses ([Forkast](https://forkast.news/enterprise-ai-agent-funding-surges-to-435m-in-five-months-security-and-governance-lead/)) |
| Ofensiva autónoma / pentest IA | Greylock (Tenzai), Lightspeed (A Security), Accel, a16z, Kleiner y Menlo (Armadin), Khosla y Menlo/Anthology (RunSybil) | 7 | a16z, Lightspeed, Accel | **Saturada** en capital (seeds de más de 40M) |
| AI SOC / agentes para el SOC | Index (7AI), Accel (Prophet), Khosla (Exaforce), Greylock (Cogent), Sequoia (Corma, modelo de ciberdefensa) | 5 | a16z, Lightspeed, Menlo (nov-25) | Muy financiada |
| AppSec de código generado por IA | Accel (depthfirst), Lightspeed (Endor, Semgrep), Menlo (Semgrep), Scale (Prime) | 4 | a16z, Lightspeed, Menlo (Build) | Financiada |
| Red-team y seguridad de modelos frontera / evals | Madrona (Gray Swan), Sequoia y Redpoint (Irregular), Insight (Promptfoo) | 4 | Menlo, Madrona, Lightspeed | Media |
| Email / human risk / deepfakes | Lightspeed (Ocean), Accel (AegisAI), Greylock (Fable) | 3 | a16z, Lightspeed | Media |
| Supply chain del agente (skills, plugins, MCP, attestation de pesos y datasets) | Sequoia (AIR) | 1 | Sequoia, Lightspeed, Insight | **Tesis sin empresas** |
| Sandboxing de ejecución de agentes | Insight (E2B) | 1 | Menlo (Run), Insight | Poco capital específico de seguridad |
| Interpretabilidad / safety técnico | ninguno verificado en esta lista (Goodfire: B Capital, fuera de la lista) | 0 | Madrona, de forma indirecta | Fuera del radar de los generalistas |
| **Atribución y forense de acciones** (cadena humano→agente→subagente, quién autorizó qué) | ninguna dedicada | 0 | Menlo, Insight, Lightspeed, Madrona | **Mar azul: tesis sin empresas** |
| **Seguridad multi-agente / autorización agente-a-agente / blast radius** | ninguna dedicada | 0 | Lightspeed, Insight | **Mar azul** |
| **Detección de comportamiento e intención** (trust score, goal drift, exceso de scope) | parcial: Geordie y Onyx como features | ~0 dedicadas | Menlo, Insight, Lightspeed, Index | **Mar azul parcial** |
| **Respuesta autónoma confiable con rollback y enforcement por acción** | Onyx de forma parcial | 1 | Bessemer ("menos construida"), Lightspeed, a16z, GC | **Subconstruida** según los propios VCs |
| Linaje y residencia de datos en flujos multi-agente | ninguna dedicada | 0 | Insight, Lightspeed (shadow AI) | Hueco |

**Lectura general**
- El capital se apiló en tres categorías: identidad de agentes, control plane/gateway y ofensiva autónoma.
- DataTribe confirma que la seguridad de IA fue cerca de un cuarto de los seeds cyber del Q2-2026, casi todo "securing agentic systems". También reporta la mayor brecha en 8 años entre capital desplegado y empresas que lo reciben ([Help Net Security](https://helpnetsecurity.com/2026/07/31/ai-agents-cybersecurity-seed-funding)).
- Los incumbentes (Palo Alto, Okta, Wiz, CrowdStrike) están comprando o construyendo justamente en esas categorías saturadas.

---

## 3. Los 5 problemas que los VCs dicen querer financiar y todavía no encuentran

1. **Atribución y forense de acciones de agentes.** Responder en tiempo real "¿quién autorizó esto y quién lo ejecutó?" a lo largo de toda la cadena de delegación: humano → agente → subagente → herramienta.
   - Lo nombran Menlo, Insight ("OAuth 2.0 no lo resuelve") y Madrona ("no hay framework acordado").
   - Ninguna empresa dedicada en los portafolios revisados.
   - Fuentes: Menlo, Insight y Madrona (URLs arriba).
2. **Seguridad multi-agente.** Autorización agente-a-agente en tiempo real, contención para que un agente comprometido no contagie a otros, y detección de agentes maliciosos en el sistema.
   - Lo piden Lightspeed (Cyber60 2026-27) e Insight ("rogue agents in multi-agent systems").
   - Cero empresas dedicadas.
3. **Integridad de la supply chain del agente.** Attestation y verificación de skills, plugins, servidores MCP, pesos y datasets de fine-tuning.
   - Sequoia dice que "nadie lo inspecciona" y apostó por una sola empresa (AIR). Lightspeed e Insight lo listan.
   - Es la categoría con mejor relación tesis/empresas.
4. **Detección de comportamiento e intención en sistemas no deterministas.** Trust scores basados en comportamiento real, detección de goal drift, de exceso de scope y de expansión gradual de permisos.
   - Lo nombran Menlo ("¿cómo detectar anomalías si lo normal es variable?"), Insight, Lightspeed e Index ("monitorización de intención: capa que aún no existe").
5. **Enforcement en vuelo y respuesta autónoma confiable.** Detener una acción puntual sin romper el workflow, con precisión probada, logs de auditoría y **rollback**.
   - Bessemer lo llama la capa "menos construida".
   - Lightspeed dice que los CISOs no ampliarán la autonomía sin esto. a16z y GC piden remediación autónoma y "fix with the find" (re-test de la corrección).
   - Hay jugadores como Onyx, pero los VCs lo siguen describiendo como abierto.

**Menciones honorables:**
- "Credential Zero" (Insight).
- Un modelo común para hacer red-team de sistemas autónomos antes de producción (Madrona).
- Linaje de datos entre jurisdicciones en flujos multi-agente (Insight).
- Distinguir acciones del agente de las del empleado en el endpoint (a16z).
