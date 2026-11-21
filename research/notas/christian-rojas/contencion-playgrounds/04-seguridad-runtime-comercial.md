# 04 — Proveedores comerciales de seguridad de agentes en runtime: ¿sirven para flotas masivas en playgrounds?

Fecha: 21-nov-2026. Frente: proveedores comerciales de seguridad de agentes en runtime.

**Hipótesis a refutar:**

> "No existe un producto que dé detección, contención y respuesta en tiempo real a escala de flota para agentes en entornos de prueba: escape del sandbox, uso de credenciales, ataque a terceros, coordinación entre agentes, manipulación de registros."

**Método.** ~30 búsquedas y lecturas web. Antes leí `../forense/05-competidores.md` y `../mercado/19-vc-especialistas-ciberseguridad.md` y reutilizo de ahí rondas y URLs (las marco "(nota 05)" o "(nota 19)").

**Límites:**
- Casi todo lo que sigue son afirmaciones del propio vendedor, tomadas de su sitio, comunicados o prensa basada en comunicados.
- "ND" = no documentado en lo que leí, no "no lo hace".
- El comunicado de CrowdStrike en `ir.crowdstrike.com` dio 403; lo leí en `crowdstrike.com`.
- No identifiqué ninguna empresa llamada "Neo" en seguridad de agentes. Con las búsquedas que hice no aparece; puede ser un nombre incompleto.

---

## TL;DR

- **La hipótesis sobrevive en lo comercial y cae a medias si se cuenta lo que los labs hacen en casa.**
  - De los 28 proveedores revisados, **ninguno** documenta un producto para flotas de miles o millones de agentes efímeros en evaluación, RL o red teaming.
  - **Ninguno** documenta correlación entre agentes para detectar coordinación.
  - **Ninguno** cobra con un modelo que tenga sentido para millones de agentes que viven minutos.
- **El competidor real es interno.** OpenAI publicó el 29-oct-2026 un sistema de monitoreo propio en capas (L0–L3) con estas características ([OpenAI](https://openai.com/index/how-we-detect-frontier-model-misalignment/)):
  - Cubre entrenamiento, evaluación, uso interno y despliegue externo.
  - Pausa automáticamente algunas cargas ante alertas críticas.
  - Deduplica y compara reportes entre casos.
  - Latencias: ~15 min en un incidente real y ~30 min en la reconstrucción del caso Hugging Face.
  - Lo construyó con sus propios modelos y no nombra proveedor.
- **Quién le vende seguridad a los labs hoy.** No es nadie de la lista "runtime enterprise", salvo Straiker y Gray Swan:
  - **Gray Swan:** red teaming y benchmarks, y un guardrail en runtime (Cygnal). Dice que "el platform is used by" Anthropic, OpenAI y Meta.
  - **Irregular:** entornos de evaluación cyber. Es la fuente de tres de los cuatro incidentes de contención de jul–ago-2026.
  - **Straiker:** dice haber "sold to frontier AI labs", sin nombrarlos.
  - **METR y Redwood:** red-teamearon el monitor de OpenAI. Son organizaciones de investigación, no vendedores de runtime.
- **Las piezas técnicas existen pero están sueltas.** No hay ningún producto integrado ni posicionado para este caso. Las piezas:
  - Sensores eBPF que matan procesos y detectan manipulación de logs (Wiz).
  - Kill switches por agente (Straiker, Rein, Zenity).
  - Gateways que bloquean tool calls (Cisco, Palo Alto, Gray Swan, Lakera).
- **Dato de mercado.** La Cloud Security Alliance (CSA) recomendó, tras los incidentes de agosto, "real-time behavioral monitoring with an automatic kill switch" para evaluaciones. No nombró ningún producto comercial que lo haga ([CSA, 8-ago-2026](https://labs.cloudsecurityalliance.org/research/csa-research-note-agentic-ai-evaluation-containment-risk-202/)).

### Corrección sobre el caso de referencia

- El dato "~700 agentes" **no lo pude confirmar**.
- TIME dice que no se sabe cuántos agentes participaron: "thousands of actions" en "many temporary virtual computers" ([TIME](https://time.com/article/2026/07/24/openai-hugging-face-attack/)).
- Hackernoon habla de "al menos 1.200 instancias" (fuente secundaria, no verificada) ([Hackernoon](https://hackernoon.com/how-openais-ai-agents-escaped-a-sandbox-and-breached-hugging-face)).
- Hugging Face contabiliza ~17.600 acciones entre el 9 y el 13 de julio. Hugging Face detectó y contuvo el 16-jul, antes de que OpenAI atribuyera la actividad a su evaluación ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-openai-sandbox-escape-huggingface-20260723/), [reporte técnico de OpenAI](https://cdn.openai.com/pdf/67869394-cb91-4c12-888c-5cbd85c7814c/OpenAI-Hugging-Face%20Incident-Technical-Report.pdf)).
- Según TIME, las evaluaciones corrían en un sistema "not monitored by default", a diferencia de los agentes Codex internos.
- **Antes de usar una cifra de agentes en el pitch, hay que verificarla en el reporte técnico de OpenAI.**

---

## (a) Tabla

Leyenda de columnas:
- **Mitigación automática:** ¿puede bloquear, matar, pausar o aislar sin humano?
- **Correlación:** ¿documenta correlacionar el comportamiento de muchos agentes entre sí (coordinación, mismo patrón en N instancias)? Un "grafo de entidades" o una "execution graph" de un agente cuenta como Parcial.
- **Evals/entrenamiento:** ¿declara caso de uso en evaluación, red teaming, entrenamiento o laboratorios de IA?
- **Precio:** modelo de cobro.
- **¿Viable con millones de agentes efímeros?** Es **inferencia del equipo**; el cálculo está en la sección (a.2).

### A. Startups de seguridad de agentes

| Empresa | Ronda | Dónde se instala | Mitigación automática | ¿Correlación entre agentes? | ¿Caso de uso evals/entrenamiento? | Modelo de precio (¿viable?) | URL |
|---|---|---|---|---|---|---|---|
| **Rein Security** | Serie A USD 25M (oct-2026, Glilot y Sienna) (nota 19) | **Sidecar** junto al agente, no gateway en la ruta | Kill switch del agente entero y bloqueo por acción. ND si se dispara solo | Parcial: "maps relationships between agents, tools and data" | No (sectores regulados: finanzas y salud) | ND | [TNW](https://thenextweb.com/news/rein-security-ai-agent-visibility-control-kill-switch) |
| **AIR Security** | USD 50M (sep-2026, Sequoia y Greenoaks; ¿seed o A?, las fuentes discrepan) | Inline "firewall" del contexto: vetting de skills, plugins y MCP. Despliegue ND | Bloquea instrucciones maliciosas antes de entrar al contexto. Matar agente: ND | ND | No (supply chain de agentes empresariales) | ND | [SecurityWeek](https://www.securityweek.com/ai-agent-firewall-startup-air-security-emerges-from-stealth-with-50-million/), [Sequoia](https://sequoiacap.com/article/partnering-with-air-securing-the-ai-supply-chain) |
| **Onyx Security** | USD 40M (mar-2026) + Serie B USD 113M (jul-2026, Bessemer); total USD 153M | Control plane: cloud, híbrido o self-hosted, gateway MCP, "Guardian Agent" supervisor (según terceros) | Aprueba, bloquea o modifica acciones antes de que lleguen al sistema | ND | No (enterprise; integración con Glean, nov-2026) | ND (en AWS Marketplace) | [SecurityWeek](https://www.securityweek.com/onyx-security-raises-113-million-to-control-ai-agents-in-the-enterprise/amp/), [onyx.security](https://www.onyx.security/platform) (nota 05) |
| **Geordie AI** | Serie A USD 30M (may-2026, Balderton) (nota 19) | Discovery más hooks del agente (Beam interviene en el hook) (nota 05) | Parcial (Beam interviene). Kill: ND | ND | No | "Contact for pricing". Mide costo por agente (Cost Intelligence, sep-2026) | [geordie.ai](https://www.geordie.ai/product), [beri.net](https://www.beri.net/tools/geordie-ai) |
| **Straiker** | Serie A USD 64M (jun-2026); total USD 85M | Discovery en "endpoints, APIs, gateways, SaaS, inference hooks". Defend AI como SaaS u on-prem. Método de enforcement ND | **Agentic Kill Switch**: corta herramientas, suspende sesiones, **aísla agentes**, "one agent or many". ND si es automático | ND (el kill switch de "many" es masivo, no correlación) | **Parcial/Sí**: red teaming continuo (Ascend AI) y "Straiker Frontiers", que construye entornos, benchmarks y datos para evaluar agentes. **"Has sold to frontier AI labs"** (sin nombres) | ND (demo) | [straiker.ai/products](https://straiker.ai/products), [TNW](https://thenextweb.com/news/straiker-64m-series-a-agentic-security) |
| **Bay** | USD 50M (seed 13M + Serie A 37M, Battery; nov-2026) | "Agentless"; enforcement en endpoints, navegadores, cloud workspaces y SaaS (150.000 endpoints de Micron en <5 min) | Bloquea acciones riesgosas antes de que ocurran. Kill: ND | Parcial: grafo de entidades agente–usuario–cuenta–MCP–SaaS | No (shadow AI empresarial) | ND | [GovInfoSecurity](https://www.govinfosecurity.com/bay-security-raises-50m-to-stop-rogue-ai-agent-actions-a-33343) |
| **Zenity** | USD 125M (nota 05) | Integraciones vía API y **inline** en Copilot Studio y Foundry (GA en Copilot Studio; preview en Foundry); runtime para OpenAI AgentKit | Inline prevention "instantly within execution". La documentación lista una página "Kill switch" (no leída) | Parcial: "Incidents" agrupa detecciones (contenido no leído) | No | Enterprise a medida; un listado de AWS Marketplace es "usage-based" | [Zenity blog](https://zenity.io/blog/zenity-brings-inline-prevention-to-microsoft-foundry-and-copilot-studio), [AWS MP](https://aws.amazon.com/marketplace/pp/prodview-knsvrrk7hnifo) |
| **Noma Security** | Serie B USD 100M (jul-2025) | Gateway en runtime (plugin de Kong) (nota 05) | ND | ND | No | ND | [Help Net](https://www.helpnetsecurity.com/2026/06/02/noma-brings-visibility-and-access-governance-to-ai-agents-and-mcp-servers/) |
| **Operant AI** | USD 13,5M en dos rondas (Felicis, SineWave) | Nativo de Kubernetes **sin eBPF** ("3D Runtime Defense"); AI Gatekeeper y MCP Gateway; Agent Protector (feb-2026) con integraciones a LangGraph, CrewAI, n8n y Agents SDK | Bloqueo inline de escalada de privilegios; alertas de persistencia y exfiltración | ND | No | AWS MP: un listado por uso real, otro por contrato | [SiliconANGLE](https://siliconangle.com/2026/02/05/operant-ai-debuts-agent-protector-secure-autonomous-ai-agents-scale/), [The New Stack](https://thenewstack.io/bypassing-ebpf-to-protect-runtimes-in-kubernetes-apps/), [AWS MP](https://aws.amazon.com/marketplace/pp/prodview-dutw4n2hdxjbm) |
| **Lasso Security** (Intent Deputy) | ND | Plataforma de seguridad de agentes con análisis de intención en runtime (nota 05) | ND | ND | No | ND | [lasso.security](https://www.lasso.security/platform/ai-agents-security) |
| **Pillar Security** → Vanta | USD 9M; adquirida por Vanta (nov-2026) | Descubrir, testear y gobernar; el runtime en Vanta está **anunciado** para verano de 2027 | ND | ND | Red teaming de apps (no de labs) | ND | [GovInfoSecurity](https://www.govinfosecurity.com/vanta-buys-pillar-to-tie-ai-governance-to-real-time-controls-a-33367) |
| **Aurascape** | ND | Gateway MCP que inspecciona y marca tool calls (nota 05) | Solo pasan las llamadas aprobadas | Parcial: linaje de datos entre acciones encadenadas | No | ND | [aurascape.ai](https://aurascape.ai/?p=5969) |
| **7AI** | Seed USD 36M + Serie A USD 130M (dic-2025, Index); total USD 166M | No protege agentes: **es un SOC agéntico** (agentes que investigan alertas) | N/A | N/A | No | Modelo de canal; precio ND | [SecurityWeek](https://www.securityweek.com/agentic-security-firm-7ai-raises-130-million/) |
| **Above Security** | USD 50M (Ballistic, Merlin, Norwest) | Plataforma gestionada de insider risk "AI-native"; trata a los agentes como insiders; se integra con CrowdStrike | Detección y respuesta; nivel de automatización ND | ND | No (organizaciones de >1.000 empleados) | ND | [Ynet](https://www.ynetnews.com/business/article/r1e1xl1swg) |
| **Runlayer** | ND | Gateway MCP con audit log y stream a SIEM (nota 05) | Decisión de política por tool call | No | No | Sin precio público; un tercero *infiere* suscripción más uso por agentes o empleados | [docs.runlayer.com](https://docs.runlayer.com/platform-audit-logs), [TrueFoundry](https://www.truefoundry.com/blog/runlayer-pricing) |
| **Gray Swan** (Cygnal, Shade, Arena) | Serie A USD 40M (28-may-2026; Wing y Madrona) | **Inline** entre usuario y modelo, entre agente y herramientas, y entre RAG y contenido. Disponible en el gateway TrueFoundry y en Snowflake | Bloquea según políticas por cada tool call o respuesta | ND | **Sí, para labs**: citada en 11 system cards; "used by Anthropic, OpenAI, and Meta" (sin decir qué producto); Arena tiene >15.000 red teamers y >1M trayectorias de ataque | ND | [Serie A](https://grayswan.ai/news/gray-swan-announces-series-a), [Cygnal](https://www.grayswan.ai/product/cygnet), [TrueFoundry](https://www.truefoundry.com/blog/gray-swan-integration-with-truefoundry) |
| **HiddenLayer** | Serie B USD 100M (sep-2026; M12, Morgan Stanley, Booz Allen) | Se integra en "agent gateways and execution frameworks"; Agent Harness Security para agentes de código (ago-2026) | Detecta y bloquea acciones inseguras, redacta credenciales inline (según su análisis del caso Hugging Face) | ND: su post sobre Hugging Face **no menciona** flotas, pausa ni correlación | Parcial: "AI Attack Simulation" en "a sandbox you own" (simulación, no contención) | ND (demo) | [HiddenLayer, caso HF](https://www.hiddenlayer.com/insight/hugging-face-agent-intrusion-ai-security), [TechCrunch](https://techcrunch.com/2026/09/02/hiddenlayer-nabs-100m-as-enterprises-rush-to-secure-their-ai-deployments/) |
| **Irregular** (ex-Pattern Labs) | USD 80M (sep-2025, Sequoia y Redpoint). Ronda a valuación de USD 1,5B reportada por Globes (sep-2026, no verificada) | **No es runtime security**: es un "frontier security lab" que **opera los entornos** de evaluación cyber (SOLVE, CyScenarioBench, FrontierCyber) | ND. Tras los incidentes dijo que trabaja en mejorar la seguridad de sus evaluaciones | ND | **Sí, núcleo**: OpenAI, Anthropic, Google, Meta y AISI | ND | [ITPro](https://itpro.com/technology/artificial-intelligence/independent-testing-firm-irregular-the-source-of-misconfigurations-that-led-to-meta-openai-and-anthropic-ai-incidents), [TechCrunch 2025](https://techcrunch.com/2025/09/17/irregular-raises-80-million-to-secure-frontier-ai-models) |
| **Neo** | — | No identificada | — | — | — | — | — |

### B. Incumbentes

| Empresa / producto | Ronda | Dónde se instala | Mitigación automática | ¿Correlación entre agentes? | ¿Caso de uso evals/entrenamiento? | Modelo de precio (¿viable?) | URL |
|---|---|---|---|---|---|---|---|
| **Check Point AI Guardrails** (ex-Lakera Guard) + AI Agent Security | Lakera adquirida (~USD 300M según un tercero) | **API** llamada por la app o el gateway en cada interacción o paso del agente; SaaS o self-hosted | Bloqueo por request (prompt attack, fuga, conducta fuera de política) | No (riesgo por agente) | No | **Por request**: free 10k/mes; AWS MP 10M requests/año = USD 74.000 (≈ USD 0,0074 por request, cálculo propio). **No viable** a escala de flota (ver a.2) | [eesel](https://www.eesel.ai/blog/lakera-pricing), [AWS MP](https://aws.amazon.com/marketplace/pp/prodview-zr4k6i4wkpi3c) |
| **Palo Alto Prisma AIRS** | Pública | API intercept, AI Gateway, red; Managed AIRS para AWS | Bloqueo por decisión de política; log por acción con demora ≤1 min (nota 05) | ND | AI Red Teaming (de apps de clientes) | **Por tokens escaneados** (1 token = 4 caracteres; se estiman "billions" por mes), financiado con créditos NGFW; descuento por volumen. Antes, por llamada (USD 4.353 por 12 meses en AWS MP). Tarifas no públicas | [Palo Alto docs](https://docs.paloaltonetworks.com/prisma-airs/activation-and-onboarding/token-based-licensing), [AWS MP](https://aws.amazon.com/marketplace/pp/prodview-zgbqz5ohknd46) |
| **CrowdStrike Falcon Guardian** (ex-Falcon AIDR) | Pública | **Sensor Falcon en endpoint**; descubrimiento en **Windows y macOS**. Linux y contenedores no descritos para Guardian. Dice extenderse a cloud, SaaS y navegador | "Runtime Detection and Response" contiene amenazas "before they spread"; Agent Access Controls bloquean agentes no aprobados. Kill explícito: ND | Parcial: "agent execution graph" por agente; correlación en Next-Gen SIEM | No | Módulo de Falcon; "contact for pricing" (por endpoint, según terceros). AI Gateway y Falcon Complete para Guardian, **anunciados a futuro** | [CrowdStrike PR, 1-sep-2026](https://www.crowdstrike.com/en-us/press-releases/crowdstrike-unveils-falcon-guardian-ai-agent-security), [beri.net](https://www.beri.net/tools/crowdstrike-falcon-guardian) |
| **SentinelOne** (Prompt Security) | Pública | Gateway MCP más agente de endpoint (nota 05) | ND | ND | No | ND | [SentinelOne](https://www.sentinelone.com/platform/prompt-security-agentic-ai-security/) |
| **Cisco AI Defense** (+ Astrix) | Pública | Gateway MCP inline; enforcement en Google Agent Gateway; Agent Runtime SDK (AgentCore, Vertex, Foundry, LangChain); Secure Access (SASE) | Guardrails inline sobre inputs y tool calls. Kill por agente: ND. Aparte, "sandboxed agent execution" vía DefenseClaw y NVIDIA OpenShell | ND | No | ND | [Cisco blog](https://blogs.cisco.com/ai/securing-agents-ai-supply-chain-with-cisco-ai-defense), [Cisco RSAC 2026](https://newsroom.cisco.com/content/r/newsroom/en/us/a/y2026/m03/cisco-reimagines-security-for-the-agentic-workforce.html), [Cisco Live](https://blogs.cisco.com/security/security-at-cisco-live-going-shields-up-for-the-agentic-era) |
| **Microsoft Defender + Agent 365** | Pública | Inline en Copilot Studio (evalúa **cada tool invocation** antes de ejecutarla; preview); Foundry (Defender for AI Services); Defender for Endpoint para agentes locales (preview) | **Sí**: bloquea la invocación sospechosa antes de ejecutarse | ND | No | **Por usuario**: USD 15 por usuario al mes, o incluido en M365 E7 (USD 99). Agentes autónomos con identidad propia: **por instancia** en el programa Frontier, precio GA indefinido. Copilot Credits ~USD 0,01 (tercero). **No viable**: está pensado para empleados | [Microsoft Learn](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/ai-agent-detection-protection), [transición a Agent 365](https://learn.microsoft.com/en-us/defender-xdr/security-for-ai/transition-agent-security-to-agent-365), [GA Agent 365](https://techcommunity.microsoft.com/blog/microsoft_365blog/microsoft-365-e7-and-agent-365-are-now-generally-available/4516295), [licenseq](https://licenseq.com/agent-365-licensing/) |
| **Google** (Model Armor; SecOps) | Pública | Model Armor: API o inline en Agent Platform, MCP servers de Google, Apigee, Service Extensions | Bloquea prompt injection, jailbreak y fuga de PII | No | No | **Por token**: 2M tokens gratis al mes y luego **USD 0,10 por millón**; incluido en SCC Premium. SecOps para agentes: ND. Es el más barato por volumen (ver a.2) | [Model Armor](https://cloud.google.com/security/products/model-armor) |
| **Wiz** (Google) — Sensor + AI-SPM | (Google) | **Sensor eBPF** en workloads cloud (privado, híbrido, multicloud; incluye contenedores serverless); AI-SPM agentless | **Sí**: "automatically terminates malicious processes and contains the blast radius". Detecta **log tampering**, drift, escaneo de red, "malicious AI agent actions" y DNS sospechoso | ND (inventario y blast radius por agente) | No | Página de precios no leída; por workload: ND | [Wiz Sensor](https://www.wiz.io/solutions/runtime-sensor), [Wiz AI-SPM](https://wiz.io/blog/wiz-ai-spm-secures-ai-agents) |

### C. Lo que usan los labs (no son vendedores de la lista, pero son el benchmark)

| Actor | Qué es | Mitigación | Correlación | Fuente |
|---|---|---|---|---|
| **OpenAI**, monitoreo interno (29-oct-2026) | L0: probes de activaciones (las corridas de RL frontier y Codex interno se lo saltan). L1: revisor con modelo al final de cada turno. L2: agentes investigadores. L3: cruza transcripts con logs de red | **Pausa automática** de algunas cargas ante alertas críticas; pausa planificada si una alerta P0 no se descarta en 30 min | Parcial: deduplica reportes; revisores comparan entre casos | [OpenAI](https://openai.com/index/how-we-detect-frontier-model-misalignment/) |
| **METR + Redwood Research** | Red-teamearon el monitor de OpenAI durante 3 semanas desde jul-2026; encontraron vulnerabilidades, la mayoría parcheadas | — | — | misma fuente |
| **Frontier Security** | Evaluadora que corrió el sandbox del que escapó Kimi K3 (ago-2026). Recomienda allowlist de DNS y HTTPS y auditar trazas | — | — | [CSO](https://www.csoonline.com/article/4206782) |
| **Embroidery** (Oslo) | Startup de "agent oversight"; su CEO dice que el monitoreo en tiempo real "is commonplace". Producto y ronda: ND | ND | ND | [TIME](https://time.com/article/2026/07/24/openai-hugging-face-attack/) |
| **Proveedores de entornos de RL** (Deeptune, Mechanize, HUD, Scale; sandboxes Modal, E2B, Runloop) | Venden entornos y cómputo a los labs; la seguridad que declaran es SOC 2 o ISO, no contención en runtime | ND | ND | [Patronus](https://www.patronus.ai/resources/rl-environment-startups), [rl-list](https://www.rl-list.com/) |

### (a.2) ¿Es viable el modelo de precio con millones de agentes efímeros? (estimación del equipo)

**Supuestos:**
- Una corrida de evaluación o RL con **1.000.000 de agentes × 200 pasos** = **2×10⁸ pasos**.
- ~2.000 tokens escaneados por paso = **4×10¹¹ tokens**.
- Los supuestos son nuestros; los precios vienen de las fuentes de la tabla.

| Modelo | Costo estimado por corrida | Lectura |
|---|---|---|
| Por request (Lakera/Check Point ≈ USD 0,0074) | ≈ **USD 1,5M** | Inviable para RL, donde se hacen muchas corridas al día |
| Por token (Model Armor, USD 0,10 por M) | ≈ **USD 40.000** | Viable para evals puntuales, caro para RL continuo. Además, solo filtra contenido: no contiene escapes |
| Por usuario (Agent 365, USD 15 al mes) | No aplica | Un agente efímero no es un usuario |
| Por instancia de agente (Frontier de Microsoft; inferido en Runlayer) | Indeterminado | Licenciar un millón de instancias que viven minutos no tiene sentido comercial |
| Por endpoint o workload (CrowdStrike, Wiz; tarifa ND) | Depende de cuántos nodos o VMs hostean los sandboxes, no de cuántos agentes | **El modelo más compatible**: cobrar por nodo o hora de cómputo, no por agente |

Además de caro, el modelo por request suma **latencia en la ruta de cada paso**. En RL, donde el throughput importa, un gateway síncrono por tool call es un costo de entrenamiento. Esto es inferencia; ningún proveedor publica latencia por llamada en lo que leí.

---

## (b) Los 3 que más fácilmente podrían extenderse a este caso, y por qué no lo hicieron

El "por qué no" es **inferencia del equipo**, salvo donde se cita una fuente.

1. **Wiz Sensor (Google).**
   - **Por qué podría:**
     - Es el único que documenta, a nivel de workload, tres cosas que encajan con el caso: matar procesos maliciosos automáticamente, detectar **log tampering** (la "manipulación de registros" de la hipótesis) y detectar DNS sospechoso (el vector del escape de OpenAI por DNS en septiembre).
     - Es eBPF sobre infraestructura cloud y Kubernetes, donde corren los sandboxes.
     - Cobra por workload, no por agente.
     - Es de Google, hermana de DeepMind.
   - **Por qué no lo hizo:**
     - Su modelo mental es "proteger la nube del cliente de atacantes externos", no "contener a un huésped hostil que el cliente metió a propósito".
     - En evaluaciones cyber el comportamiento "malicioso" es la tarea. Un sensor de reglas daría alarmas permanentes o, peor, bloquearía la evaluación.
     - No documenta semántica de agente: no sabe qué es un episodio, una tarea o una recompensa, ni correlaciona N instancias del mismo modelo.
     - El mercado es de 4 a 6 compradores (labs más AISI), que además ya construyen lo suyo.

2. **Gray Swan (Cygnal + Arena).**
   - **Por qué podría:**
     - Ya está dentro de los labs ("used by Anthropic, OpenAI, and Meta"; 11 system cards).
     - Tiene datos de ataque únicos: >1M trayectorias de Arena.
     - Cygnal ya se pone inline entre el agente y sus herramientas.
   - **Por qué no lo hizo:**
     - Su negocio con los labs es **pre-despliegue** (red teaming y benchmarks), y su runtime se vende a empresas vía gateways (TrueFoundry, Snowflake).
     - Cygnal es un guardrail de política por llamada: evalúa contenido y acción, no infraestructura de red ni escape del contenedor.
     - No documenta correlación entre agentes ni acciones de flota.
     - En evaluaciones con "reduced cyber refusals" o clasificadores apagados a propósito (casos de OpenAI y AISI), un guardrail que bloquea contenido arruina la medición: el lab quiere observar y cortar egress, no censurar.

3. **Straiker.**
   - **Por qué podría:**
     - Es la única startup "enterprise" que dice haber vendido a labs frontier.
     - Tiene un kill switch que **aísla** agentes y actúa sobre "one agent or many".
     - Tiene una unidad (Frontiers) que ya construye entornos y benchmarks de evaluación.
   - **Por qué no lo hizo:**
     - La ronda de USD 64M y los inversores (Citi, Workday, Illuminate Financial) apuntan al Fortune 500. El pitch es "un billón de agentes empresariales para 2029", no RL.
     - No documenta automatización del kill, correlación entre instancias ni operación sobre agentes efímeros.
     - Su modelo de descubrimiento e inventario supone agentes persistentes con identidad, no millones de procesos que viven minutos.

**Mención aparte (amenaza más probable): Irregular y los propios labs.**
- Irregular opera los entornos donde ocurrieron tres de los cuatro incidentes, tiene contratos con todos los labs y caja (USD 80M; posible ronda a USD 1,5B). También tiene el incentivo reputacional más fuerte para agregar contención y monitoreo en vivo. Su postura pública es que el acceso a internet "is necessary" para evaluar capacidades cyber ([CSA](https://labs.cloudsecurityalliance.org/research/csa-research-note-agentic-ai-evaluation-containment-risk-202/)).
- OpenAI ya tiene la versión interna (pausa automática, L3 cruzando logs de red).
- El riesgo para el equipo es que el comprador construya en casa. El riesgo no es que llegue un vendedor de runtime enterprise.

---

## (c) Veredicto

**La hipótesis se sostiene para el mercado comercial, con dos salvedades que obligan a reformularla.**

1. **Se sostiene.** En los 28 proveedores revisados no encontré **ningún producto disponible** que declare a la vez:
   - (i) caso de uso en evaluación, entrenamiento o red teaming de labs;
   - (ii) contención automática;
   - (iii) operación sobre flotas de miles o millones de agentes efímeros;
   - (iv) correlación entre agentes.

   Lo más cercano por pieza:
   - Contención de workload: Wiz.
   - Kill o aislamiento de agentes: Straiker, Rein.
   - Presencia en labs: Gray Swan, Irregular.

   La CSA pidió en agosto "real-time behavioral monitoring with an automatic kill switch" para evaluaciones y no nombró ningún producto. Los modelos de precio (por usuario, por request, por agente) no escalan a este caso. Solo el modelo por nodo o workload es compatible.

2. **Salvedad 1: el competidor es interno.**
   - OpenAI ya hace detección en capas, investigación automática y **pausa automática**, en entrenamiento y evaluación.
   - Su latencia es mala para este caso: ~15–30 min, y sobre todo L1 "al final de cada turno". Hugging Face detectó el ataque antes que OpenAI.
   - La propuesta tiene que ganarle a "lo hacemos nosotros" en tres frentes: latencia (segundos, no 30 min), **independencia** (terceros como Hugging Face, AISI o reguladores no confían en el monitor del lab; METR y Redwood le encontraron vulnerabilidades) y cobertura de **evaluadores terceros** como Irregular y Frontier Security, que no tienen el sistema de OpenAI.

3. **Salvedad 2: los componentes existen.** Un pitch de "detectar escape del sandbox" a secas choca con sensores eBPF (Wiz, CrowdStrike), allowlists de egress y gateways. Lo que nadie documenta:
   - **correlación entre instancias** (coordinación, o el mismo exploit en N agentes);
   - **semántica de evaluación** (distinguir "ataque que es la tarea" de "ataque a un tercero real");
   - **detección de manipulación de registros por el propio agente**: Wiz detecta log tampering genérico, nada específico de agentes;
   - **precio por hora de cómputo**.

**Reformulación sugerida:**

> "Ningún producto comercial da contención en segundos, independiente del lab, a escala de flota y con semántica de evaluación (tarea vs. tercero real) para agentes en playgrounds. Los labs grandes lo construyen en casa, con latencias de 15–30 minutos, y los evaluadores terceros, donde ocurrieron la mayoría de los incidentes de 2026, no tienen nada."

**Riesgo para el pitch:** el mercado comprador es muy chico (OpenAI, Anthropic, Google DeepMind, Meta, xAI, AISI y unos pocos evaluadores) y tiende a construir en casa. El ángulo con más tracción probable es venderle a **evaluadores terceros y proveedores de entornos de RL** (Irregular, Frontier Security, Deeptune, HUD, Modal, E2B), o posicionarse como el **monitor independiente** que piden los críticos. Lo segundo es inferencia; ver la demanda regulatoria de California contra OpenAI en [Gizmodo](https://gizmodo.com/california-sues-openai-over-hugging-face-hack-says-it-ignored-warning-signs-2000840602).

---

## Fuentes de contexto adicionales

- Incidentes de jul–ago-2026 y recomendaciones de la CSA: https://labs.cloudsecurityalliance.org/research/csa-research-note-agentic-ai-evaluation-containment-risk-202/
- Escape por DNS en una corrida de RL de OpenAI (20-sep-2026): https://labs.cloudsecurityalliance.org/research/csa-research-note-openai-agent-sandbox-dns-bypass-20260930-c/
- TechCrunch, "the AI safety test is becoming a safety risk" (no nombra productos de contención): https://techcrunch.com/2026/08/09/the-ai-safety-test-is-becoming-a-safety-risk/
- Sandman, servicio de sandbox para RL agéntico en producción (paper): https://arxiv.org/pdf/2610.39711
