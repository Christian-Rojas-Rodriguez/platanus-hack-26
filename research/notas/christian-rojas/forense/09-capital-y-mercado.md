# 09 — Seguir la plata: capital y mercado para la forense y atribución de acciones de agentes

Research al 21-nov-2026, hecho para validar o refutar la hipótesis. Usé unas 30 búsquedas y lecturas de páginas.

> **Hipótesis bajo prueba:** "Cuando un agente de IA ejecuta una acción dañina o no autorizada, hoy nadie puede probar de forma independiente qué autorizó el humano, qué hizo realmente el agente y quién debe pagar. Los registros existentes los firma la parte interesada. La forense y atribución de acciones de agentes es un problema grande y poco atendido."

**Convenciones:**
- **Confirmado:** dato publicado por la propia empresa (comunicado, blog oficial, newsroom).
- **Prensa:** dato publicado por un medio y no confirmado por la empresa en lo que leí.
- **No verificado:** no encontré fuente en esta sesión.

Los resúmenes del buscador cuentan como fuente secundaria. Cuando un dato salió solo de un resumen y no abrí la página, lo indico.

**Límites:**
- Varias páginas devolvieron 403 y no pude leerlas: el comunicado de Vorlon en GlobeNewswire, el blog de Rubrik de nov-2026, el comunicado de Gartner del 26-ago-2026 y la página de Mastercard sobre Verifiable Intent. En esos casos los datos vienen de cobertura secundaria o del resumen del buscador.
- No encontré rondas de 2025–2026 de Payman, Basis Theory, Prava, Sardine, Forter, Riskified ni Signifyd. Eso no prueba que no existan.

---

## (a) Rondas y empresas

En la columna "¿Forense?":
- **Sí:** el producto central es registro verificable, forense, atribución, undo o disputa de acciones de agentes.
- **Parcial:** tiene un módulo de registro o auditoría, pero lo central es otra cosa.
- **Adyacente:** prevención, identidad, pagos o DFIR genérico.

### a.1 Startups cuyo producto se acerca a "evidencia o forense de agentes"

| Empresa | País | Qué hace exactamente | Monto | Fecha | Inversores | ¿Forense? | URL |
|---|---|---|---|---|---|---|---|
| **OpenBox AI** | EE. UU. (San Francisco, según un comunicado) | Gobernanza de agentes: aplica identidad, autorización y política en el momento de ejecutar, y genera audit trails con "attestation" criptográfica. El plan base es gratis al lanzar. | USD 5M seed (confirmado en el comunicado de la empresa vía PR Newswire) | 31-mar-2026 | Tykhe Ventures (líder) | **Sí, parcial.** El registro lo produce la plataforma del propio operador; la fuente no dice que haya un verificador independiente. | https://tools.prnewswire.com/en-us/live/20823/release/20260331EN22177 · https://pulse2.com/openbox-ai-5-million-raised-for-enterprise-ai-trust-platform-launch |
| **Neuromorphic Labs** | No verificado | Identidad verificable para modelos, datasets y agentes, con seguimiento de cambios para procedencia y aplicación de políticas en runtime | USD 5,1M seed (prensa) | 17-ago-2026 | Flying Fish (líder) | **Parcial**: procedencia, más que un log por acción | https://www.hpcwire.com/aiwire/2026/08/17/neuromorphic-labs-secures-5-1m-for-production-ai-trust-layer/ |
| **OpenMatter** | EE. UU. (Melbourne, Florida) | "Capa de confianza verificable". Su módulo Datavizor produce "un registro criptográficamente demostrable de la ejecución y la actividad de IA". Incluye cómputo entre organizaciones. | No divulgado | 30-jun-2026 (lanzamiento) | No mencionados | **Sí, parcial.** Es lo más cercano a evidencia entre partes, pero no hay detalle de quién verifica. | https://siliconangle.com/2026/06/30/startup-openmatter-wants-make-enterprises-prove-ai-agents/ |
| **Asymptote Labs** | No verificado | Beacon, una capa de telemetría open source que normaliza la actividad de más de 20 "harnesses" de agentes, más una plataforma paga para bloquear acciones | USD 5,5M seed (prensa) | No verificado (2026 según el contexto) | Tower Research Ventures | **Parcial**: telemetría y observabilidad, no evidencia probatoria | https://thenextweb.com/news/asymptote-labs-5-5m-seed-ai-agent-security · https://securityweek.com/asymptote-labs-lands-5-5-million-seed-for-ai-agent-runtime-security |
| **FriskAI** | No verificado | "Vigilar qué hacen los agentes en producción" | USD 3,6M (prensa, Dealroom) | No verificado | No verificado | **Parcial** | https://dealroom.co/news/144391-friskai-raises-3-6m-to-watch-what-ai-agents-do-in-production/ |
| **Endeem** | No verificado | Registro auditable de la actividad de agentes para equipos de seguridad (dato del resumen del buscador) | USD 2,5M pre-seed (prensa) | No verificado | No verificado | **Parcial** | https://www.citybiz.co/article/934896/endeem-raises-2-5-million-in-pre-seed-funding/ |
| **Glacis** | EE. UU. (Seattle) | Arbiter genera un registro firmado del input, los chequeos de seguridad aplicados y el output de cada inferencia. Plan de USD 49/mes en lista de espera. | No verificado | 2026 (GeekWire) | No verificado | **Sí, parcial**: firma a nivel de inferencia, no de acción del agente | https://www.geekwire.com/2026/seattle-startup-glacis-brings-longtime-microsoft-leader-aboard-to-target-ais-biggest-blind-spot/ |
| **Vorlon** | EE. UU./Israel | Seguridad del ecosistema SaaS. En 2026 lanzó AI Agent Flight Recorder: un audit trail entre aplicaciones con identidades, apps SaaS, endpoints de API, clasificación de datos y sistemas downstream. Lo describe como "registro inmutable" sin decir cómo lo logra. También lanzó Action Center (respuesta) y Guardian (bloqueo). | **Sin ronda en 2025–2026.** La última es una serie A del 17-abr-2024 con Accel (CB Insights y TechCrunch); el monto no lo verifiqué en esta sesión. | Productos: 25-mar-2026 y 30-jun-2026 | Accel (2024) | **Sí, como producto.** Es la primera que dice traer "forense" a los agentes, pero el registro lo guarda el vendor del cliente. | https://securitybrief.co.uk/story/vorlon-launches-tools-for-ai-agent-security-response · https://siliconangle.com/2026/06/30/vorlon-debuts-guardian-block-risky-ai-agent-actions-complete/ · https://www.cbinsights.com/company/vorlon |
| **Above Security** | Israel/EE. UU. | Riesgo interno (insider) que incluye a los agentes de IA como actores, con líneas de tiempo de comportamiento | USD 50M al salir de sigilo (prensa) | ~mar-2026 | Ballistic, Merlin, Norwest, Jump, QPV | **Parcial**: las líneas de tiempo son forense interna | https://www.ynetnews.com/business/article/r1e1xl1swg (dato de la nota 14) |

### a.2 Runtime y prevención (el grueso del capital)

| Empresa | País | Qué hace | Monto | Fecha | Inversores | ¿Forense? | URL |
|---|---|---|---|---|---|---|---|
| **AIR Security** | Israel/EE. UU. | Firewall inline para agentes. Evalúa skills, plugins y servidores MCP, intercepta acciones peligrosas y pide aprobación humana si la intención es dudosa. | USD 50M en dos seeds (comunicado de la empresa vía Newswire) | 1-sep-2026 | Sequoia y Greenoaks (líderes), Swish, Netz | **Adyacente**: prevención | https://www.securityweek.com/ai-agent-firewall-startup-air-security-emerges-from-stealth-with-50-million/ · https://www.newswire.com/news/air-emerges-from-stealth-with-50m-to-build-a-firewall-for-agents-22853509 |
| **Rein Security** | EE. UU./Israel | Sidecar de runtime que monitorea y gobierna las acciones de los agentes | USD 25M serie A, USD 35M en total (prensa) | 12-oct-2026 | Glilot, Sienna, Corner, Atlacle, RNP | **Adyacente**, con monitoreo | https://thepaypers.com/fraud-and-fincrime/news/rein-security-raises-usd-25-million-in-series-a-to-secure-ai-agents |
| Straiker, Zenity, Noma, Onyx, Neo, WhiteMatter, Vijil, Tenet, Ultra, Runlayer, NewCore, Oak | EE. UU./Israel | Runtime, inventario, MCP e identidad de agentes | De USD 6M a 125M cada una | nov-2025 a nov-2026 | Ver notas 14 y 17 | **Adyacente** | Ver `mercado/14-region-israel.md` y `mercado/17-eeuu-seed-reciente.md` |

### a.3 Pagos agénticos, "know your agent" (KYA) y disputas

| Empresa | País | Qué hace | Monto | Fecha | Inversores | ¿Forense o disputa? | URL |
|---|---|---|---|---|---|---|---|
| **Catena Labs** | EE. UU. | "Banco nativo de IA": infraestructura regulada para que los agentes transaccionen. Pidió una carta de National Trust Bank a la OCC. | USD 30M serie A (prensa y post de a16z) | 20-may-2026 | Acrew Capital y a16z crypto (co-líderes), Breyer, General Catalyst, QED. Seed previo de USD 18M (2025) | **Adyacente**: rieles e identidad, no disputa | https://theblock.co/post/402029/catena-labs-lands-30-million-series-a-files-for-national-trust-bank-charter-to-underpin-agentic-finance · https://a16zcrypto.com/posts/article/investing-in-catena-part-ii |
| **Kite** | EE. UU. | Kite AIR: Agent Passport (identidad verificable con guardrails) y Agent App Store, sobre blockchain | USD 18M serie A, USD 33M en total (**confirmado** en el newsroom de PayPal) | 2-sep-2025 | PayPal Ventures y General Catalyst (co-líderes) | **Adyacente**: identidad y pagos | https://newsroom.paypal-corp.com/2025-09-02-Kite-Raises-18M-in-Series-A-Funding-To-Enforce-Trust-in-the-Agentic-Web |
| **t54 Labs** | EE. UU. (San Francisco) | "Capa de confianza" para finanzas agénticas: KYA, monitoreo de riesgo en tiempo real, crédito para agentes y liquidación. Habla de "accountability" sin un producto de disputas. | USD 5M seed (prensa) | 25-feb-2026 | Anagram, PL Capital y Franklin Templeton (co-líderes), Ripple, Virtuals, otros | **Adyacente**, con KYA | https://www.theblock.co/post/391273/ripple-franklin-templeton-ai-agent-trust-startup-t54-labs |
| **Nekuda** | No verificado | Credenciales de pago y autorización para agentes | USD 5M (prensa) | may-2025 | Madrona (líder), Amex Ventures, Visa Ventures | **Adyacente** | https://www.crowdfundinsider.com/2025/05/239660-fintech-startup-nekuda-secures-funding-led-by-madrona-ventures-to-enable-agentic-payments/ |
| **Skyfire** | EE. UU. | Red de pagos para agentes y protocolo KYA. En oct-2026 integró sus datos KYA con Forter. | USD 8,5M seed en ago-2024. **Sin ronda en 2025–2026 encontrada.** | Ronda: ago-2024. Alianza con Forter: 19-oct-2026 | Neuberger Berman, Inception, Arrington | **Adyacente**: identidad en el checkout | https://techcrunch.com/2024/08/21/skyfire-lets-ai-agents-spend-your-money · https://www.pymnts.com/partnerships/2026/skyfire-and-forter-team-to-strengthen-agentic-commerce-decisioning/ |
| **Natural** | EE. UU. | Rieles de pago para agentes | USD 30M serie A, más de USD 40M en total (prensa) | 20-jul-2026 | Forerunner (líder) | **Adyacente** | https://techcrunch.com/2026/07/20/natural-raises-30m-to-reinvent-payments-for-ai-agents-and-take-on-stripe |
| **Sapiom** | No verificado | Pagos para agentes, y ahora también ruteo de modelos | USD 15,75M seed (feb-2026, Accel) + USD 35M serie A (ago-2026, Dragonfly). USD 51M en total (Dealroom) | feb y ago 2026 | Accel, Dragonfly | **Adyacente** | https://dealroom.co/charts/startup-stack-ai-spending |
| **Chargeflow** | Israel/EE. UU. | Automatización de contracargos: trae la disputa, la enriquece y arma la evidencia (ChargebackOS). Publica contenido sobre la responsabilidad por compras de agentes. | USD 35M serie A, de los cuales USD 10M son deuda. USD 49M en total (**confirmado** en el blog de la empresa). CB Insights dice USD 25M. | nov-2025 | No verificado en lo leído | **Adyacente a disputa**: disputa genérica, no un producto específico para agentes | https://www.chargeflow.io/blog/chargeflow-raises-35m-series-a-to-transform-chargeback-management · https://www.finextra.com/pressarticle/108028/chargeflow-raises-35-million |
| **Justt** | Israel | Disputas de contracargos. Su blog dice que en comercio agéntico la evidencia "en gran parte desaparece". | Sin ronda en 2025–2026 verificada. Un agregador dice USD 100M en 4 rondas (serie C de USD 30M liderada por Zeev, fecha no verificada). | — | Zeev Ventures | **Adyacente a disputa.** No encontré un producto agéntico con nombre propio. | https://justt.ai/blog/solving-agentic-commerce-chargebacks/ |
| Payman, Basis Theory, Prava, Sardine, Forter, Riskified, Signifyd | — | — | **No verificado**: no encontré rondas de 2025–2026 | — | — | Forter y Signifyd tienen funciones agénticas (ver b) | — |

**Agregado del sector de pagos agénticos (Dealroom, 19-oct-2026):** USD 115M en 14 rondas en lo que va de 2026, contra USD 81M en 10 rondas en todo 2025. Natural y Sapiom suman ~70% del monto de 2026. Metodología: una selección editorial de 112 empresas cuya descripción pone a un agente como pagador o cobrador, con rondas que tienen monto divulgado. "No es un censo." https://dealroom.co/charts/startup-stack-ai-spending

### a.4 DFIR con IA (forense hecha por IA, no forense de la IA)

| Empresa | País | Qué hace | Monto | Fecha | Inversores | ¿Forense de agentes? | URL |
|---|---|---|---|---|---|---|---|
| **Cydelphi** | EE. UU. (Dallas) | Plataforma de DFIR nativa en IA para recuperarse de ransomware y brechas | USD 3M seed (**confirmado** en el blog de Glasswing) | feb-2026 | Glasswing Ventures (líder) | **No**: es DFIR clásico acelerado con IA | https://glasswing.vc/blog/3m-seed-investment-in-cydelphi/ |
| **Asymmetric Security** | No verificado | Usa agentes de IA para hacer DFIR | USD 4,2M pre-seed (prensa) | ene-2026 (Seedtable) | No verificado | **No**: IA como investigador, no como investigado | https://www.securityweek.com/asymmetric-security-emerges-from-stealth-with-4-2-million-in-funding/ |

---

## (b) Adquisiciones y lanzamientos de incumbentes

### b.1 Adquisiciones en forense, IR y registro relacionadas con IA

| Comprada | Comprador | Fecha | Precio | Relación con la hipótesis | URL |
|---|---|---|---|---|---|
| Cado Security (forense cloud) | Darktrace | Anuncio: 9-ene-2025 | No divulgado. "Hasta USD 100M" según prensa | Alimenta al "Cyber AI Analyst". Es DFIR cloud genérico. | https://siliconangle.com/2025/01/09/darktrace-acquire-cado-security-strengthen-cloud-forensic-capabilities/ |
| Cybereason (XDR + DFIR) | LevelBlue | Anuncio: 14-oct-2025 | No verificado | DFIR genérico absorbido por un MSSP | https://www.helpnetsecurity.com/2025/10/14/levelblue-acquires-cybereason-mdr-xdr-threat-response/ |
| Predibase | Rubrik | Cerrada antes del 12-ago-2025 | No verificado | Infraestructura sobre la que corre Agent Rewind: es la compra que habilitó el "undo" de agentes de Rubrik | https://www.rubrik.com/blog/company/25/when-ai-agents-go-awry-introducing-rubrik-agent-rewind-powered-by-predibase-ai-infrastructure |
| Galileo, Langfuse, Securiti, Oasis, Pillar | Cisco, ClickHouse, Veeam, Cyera, Vanta | 2025–2026 | Ver nota 22 | Observabilidad, gobernanza e identidad. Ninguna es forense de agentes. | `mercado/22-adquisiciones.md` |

**No encontré ninguna adquisición de una startup cuyo producto central sea la forense o atribución de acciones de agentes.** Coincide con la nota 22, que revisó unas 45 compras.

### b.2 Lanzamientos de incumbentes (2025–2026) con foco en registro, undo o evidencia de acciones de agentes

| Empresa | Producto | Fecha | Qué hace | ¿Registro independiente? | URL |
|---|---|---|---|---|---|
| **Rubrik** | Agent Rewind | 12-ago-2025 | Audit trail y snapshots inmutables. Localiza el momento del error y revierte archivos, BD, configuraciones y repos. IDC lo llamó "la primera oferta que conozco" que une la visibilidad de acciones con el undo. | **No**: lo guarda Rubrik para el cliente | https://www.businesswire.com/news/home/20250812418116/en/Rubrik-Unveils-Agent-Rewind-For-When-AI-Agents-Go-Awry · https://www.computerworld.com/article/4037957/ai-agents-make-mistakes-rubrik-has-figured-out-a-way-to-reverse-them.html |
| **Rubrik** | Agent Cloud | Anuncio: 22-oct-2025 (early access). GA a comienzos de 2026. Extensión a Google Cloud: 22-abr-2026. | Descubre agentes (OpenAI, Copilot Studio, Bedrock), mantiene "audit trails inmutables" de cada prompt y tool call, aplica políticas (SAGE) y hace rewind. Cada rewind queda logueado. | No | https://www.nasdaq.com/press-release/new-rubrik-agent-cloud-accelerates-trusted-enterprise-ai-agent-deployments-2025-10-22 · https://www.rubrik.com/company/newsroom/press-releases/26/rubrik-secures-and-accelerates-ai-agents-on-google-cloud |
| **Rubrik** | Blog "Agent Rewind: undo agent action…" | 17-nov-2026 | Según el resumen del buscador (la página dio 403), cita a Rubrik Zero Labs (2026): 88% de los líderes de IT y seguridad no puede revertir acciones de agentes sin afectar sus sistemas. Es una cifra del vendor. | — | https://www.rubrik.com/blog/company/26/11/agent-rewind-undo-agent-action-keep-everyones-work |
| **Veeam** | Agent Commander | 24-feb-2026 | Detectar riesgo de IA, proteger y "deshacer errores de IA" con recuperación quirúrgica. Después lanzó Intelligent ResOps para M365 (GA, fecha no verificada) con undo a nivel de archivo. | No | https://www.helpnetsecurity.com/2026/02/24/veeam-agent-commander/ · https://futurumgroup.com/insights/veeam-brings-ai-agent-undo-to-microsoft-365-with-intelligent-resops/ |
| **Cohesity** | Agent Resilience | Catalyst 2026 (cobertura de The Register del 10-mar-2026) | Respalda el estado de los agentes, empezando por Bedrock: memoria, vector DB y configuraciones de modelo | No | https://www.theregister.com/2026/03/10/agentic_ai_rollback_recovery_cohesity/ · https://futurumgroup.com/insights/cohesity-extends-cyber-resilience-to-the-ai-agents-themselves |
| **Commvault** | AI Protect ("Ctrl-Z") | 14-abr-2026 | Descubre agentes en AWS, Azure y GCP y revierte sus acciones a nivel de infraestructura | No | https://www.theregister.com/2026/04/14/commvault_has_a_ctrlz_for/ |
| **Vorlon** | AI Agent Flight Recorder + Action Center | 25-mar-2026 (RSAC) | Audit trail entre aplicaciones y respuesta coordinada | No | https://securitybrief.co.uk/story/vorlon-launches-tools-for-ai-agent-security-response |
| **Mastercard** | Verifiable Intent (open source, co-desarrollado con Google) | 5-mar-2026 | Registro "a prueba de manipulación" de **qué autorizó el usuario**. Une identidad, intención y acción, con divulgación selectiva. Se basa en FIDO, EMVCo, IETF y W3C. Spec y código en GitHub y verifiableintent.dev. Se integrará en las intent APIs de Agent Pay "en los próximos meses". Mastercard dice que sirve para resolver disputas. | **Parcial**: es un estándar abierto y verificable por varias partes, pero solo cubre la autorización del pago, no lo que hizo el agente fuera del pago | https://www.mastercard.com/us/en/news-and-trends/stories/2026/verifiable-intent.html |
| **Mastercard** | Servicios de confianza e inteligencia de Agent Pay Trust Framework | 30-sep-2026 | Capa de inteligencia del marco: identidad, intención, controles, ejecución e inteligencia | Parcial | https://www.mastercard.com/europe/en/news-and-trends/press/2026/september/new-trust-and-intelligence-services.html |
| **Visa** | Trusted Agent Protocol | 14-oct-2025 | Verifica agentes para distinguir compradores, agentes legítimos y bots. En lo leído no cubre disputas. | No aplica | (prensa secundaria, editorialge; no abrí la página de Visa) |
| **Forter + Skyfire** | KYA en las decisiones de fraude | 19-oct-2026 | Forter incorpora los datos KYA de Skyfire. Dice que las órdenes agénticas en su red crecieron más de 4x desde agosto. | No aplica | https://www.pymnts.com/partnerships/2026/skyfire-and-forter-team-to-strengthen-agentic-commerce-decisioning/ |
| **Amex** | Cobertura de compras erróneas de agentes registrados | No verificado | Según un resumen del buscador, Amex se comprometió a cubrir esas compras en su red. No vi la fuente primaria. | — | **No verificado** |

**Lectura del analista (Futurum):** un backup "puede restaurar estado, pero no puede deshacer una acción". Revertir acciones en otros sistemas exige pasos compensatorios y socios de identidad, y la mayoría de las ofertas son tempranas o de alcance acotado. https://futurumgroup.com/insights/veeam-brings-ai-agent-undo-to-microsoft-365-with-intelligent-resops/

---

## (c) Tamaños de mercado y proyecciones

Advertencia general: los informes de "market research" (MarketsandMarkets, TechSci, MarketIntelo, etc.) son pagos. Solo vi sus resúmenes de prensa y su metodología no está verificada. Los rangos varían mucho según cómo cada uno define el mercado.

### c.1 Categorías vecinas

| Categoría | Cifra | Fuente y fecha | Metodología y nota |
|---|---|---|---|
| Forense digital (global) | USD 12,94B en 2025 → USD 22,81B en 2030, 12% anual | MarketsandMarkets (resumen de prensa) https://www.marketsandmarkets.com/PressReleases/digital-forensics.asp | Producto + servicio; metodología no verificada. Otra estimación da USD 8,0B en 2025 (Knowledge Sourcing). |
| Servicios de respuesta a incidentes | USD 41,7B en 2025, 18,4% anual a 2031 | TechSci https://www.techsciresearch.com/report/global-incident-response-services-market/31000.html | Incluye MDR. Con una definición estrecha da ~USD 8,3B. |
| Software de gestión de contracargos | USD 2,1–2,7B en 2025, 15–22% anual | MarketIntelo, Intel Market Research, Global Market Statistics (resúmenes) https://marketintelo.com/report/chargeback-management-software-market | Hay una estimación atípica de USD 6,5B (DataHorizzon). El centro razonable es ~USD 2,5B. |
| Volumen de disputas (global) | 324M de disputas por año en 2028, +24% entre 2025 y 2028 | Datos Insights, citado por American Banker y repetido por Justt (actualizado el 11-ago-2026) https://justt.ai/blog/solving-agentic-commerce-chargebacks/ | No vi el informe original de Datos. |
| Observabilidad de IA | USD 1,24B en 2025 → USD 12,75B en 2032, 40% anual | MarketsandMarkets https://www.marketsandmarkets.com/Market-Reports/ai-observability-market-1103999.html | Gartner proyectaría USD 14,3B para toda la observabilidad en 2028 (vía Network World, sin fuente primaria) https://www.networkworld.com/article/4197973/ai-workloads-shake-up-observability-market.html |
| Plataformas de gobernanza de IA | USD 492M en 2026 → más de USD 1B en 2030 | **Gartner, comunicado del 17-feb-2026** https://www.gartner.com/en/newsroom/press-releases/2026-02-17-gartner-global-ai-regulations-fuel-billion-dollar-market-for-ai-governance-platforms | Gasto de usuarios finales. En la tabla de "securing AI" de agosto la misma categoría aparecería con USD 275M en 2026; ese dato es secundario y probablemente usa otro alcance. |
| "Securing AI" (todo el mercado) | ~USD 4,8B en 2027 (+68,7%) y ~USD 7,7B en 2028 | **Gartner, 26-ago-2026** (vía CRN Asia; el comunicado dio 403) https://www.crnasia.com/news/2026/cybersecurity/gartner-predicts-spending-on-securing-ai-to-grow-68-7-in-2027 | Segmentos: control de uso de IA, appsec de IA, gobernanza y gateways. **No hay un segmento de forense ni de respuesta a incidentes de IA.** |
| Seguros de IA (primas globales) | ~USD 4,7B por año en 2032, ~80% anual | **Deloitte Insights** https://www.deloitte.com/us/en/insights/industry/financial-services/risk-insurance-for-ai.html | Modelado sobre el crecimiento del ciberseguro. Algunos medios redondean a USD 4,8B. |

### c.2 Comercio agéntico (volumen)

| Fuente | Proyección | Fecha | Definición | URL |
|---|---|---|---|---|
| McKinsey | Hasta USD 1T de ingresos "orquestados" en el retail B2C de EE. UU. y USD 3–5T a nivel global, para 2030 | 17-oct-2025 | Solo bienes; excluye servicios y B2B. Mide ingresos orquestados o mediados, no ventas pronosticadas. | https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-agentic-commerce-opportunity-how-ai-agents-are-ushering-in-a-new-era-for-consumers-and-merchants |
| Morgan Stanley | USD 190B (base) a 385B (optimista) de gasto e-commerce en EE. UU. en 2030, ~10–20% del retail online | dic-2025 | Basado en la encuesta AlphaWise (53% de usuarios de ChatGPT investigó productos ahí en el último mes) | https://www.morganstanley.com/insights/articles/agentic-commerce-market-impact-outlook · https://www.digitalcommerce360.com/2025/12/09/morgan-stanley-ai-agentic-shoppers-385-billion-online-sales/ |
| Bain | USD 300–500B en EE. UU. en 2030, 15–25% del e-commerce | No verificado (snap chart) | Compras iniciadas, influidas o completadas por agentes; excluye la búsqueda asistida | https://www.bain.com/insights/2030-forecast-how-agentic-ai-will-reshape-us-retail-snap-chart/ |
| Gartner | Más de USD 15T de gasto B2B intermediado por agentes en 2028; 90% de la compra B2B mediada por agentes | 21-oct-2025 | Predicción de Gartner. Advierte que los estándares fragmentados frenarán el crecimiento. | https://gartner.com/en/newsroom/press-releases/2025-10-21-gartner-unveils-top-predictions-for-it-organizations-and-users-in-2026-and-beyond |
| Signifyd | Órdenes referidas por agentes de IA: +1.247% interanual (oct-2025) | 2026 (State of Commerce 2026) | Datos de su propia red. Crecimiento, no volumen absoluto. | https://signifyd.com/blog/agentic-commerce |
| Forter | Órdenes agénticas en su red: más de 4x desde agosto de 2026 | 19-oct-2026 | Datos de su propia red | https://www.pymnts.com/partnerships/2026/skyfire-and-forter-team-to-strengthen-agentic-commerce-decisioning/ |
| Adyen, Visa, Mastercard | **No verificado**: no encontré proyecciones de volumen propias | — | — | — |

### c.3 Tasas de disputa en comercio agéntico

- **No encontré ninguna tasa de disputa publicada específica para transacciones de agentes.** Chargebacks911 (15-may-2026) advierte sobre una "brecha de riesgo de disputa", pero no da cifras. https://thepaypers.com/fraud-and-fincrime/news/chargebacks911-warns-of-dispute-risk-gap-in-agentic-payments
- Según las fuentes de la industria leídas, **no existe un reason code de disputa específico para agentes** en Visa ni Mastercard. Las disputas de agentes cuentan para VAMP y ECM como cualquier otra, y Worldpay dice que la responsabilidad "todavía se está escribiendo". https://worldpay.com/insights/articles/agentic-commerce-liability-is-still-being-written
- **Encuesta de Darwinium** a 500 profesionales de fraude y riesgo de EE. UU. y Reino Unido, sobre quién debe responder: proveedor de IA 39%, cliente 20%, comercio 14%, banco o procesador 11%, modelo compartido 15%. Citada por Justt; no vi el original. https://justt.ai/blog/solving-agentic-commerce-chargebacks/

---

## (d) Lectura: ¿el capital ya está entrando o sigue en lo adyacente?

**1. El grueso del capital sigue en lo adyacente.** En 2025–2026, la prevención, el runtime y la identidad de agentes recibieron cientos de millones:
- AIR, 50M
- Zenity, 125M
- Onyx, 113M
- Neo, 100M
- NewCore, 66M
- Straiker, 64M
- Rein, 25M

Los rieles de pago agénticos también levantaron rondas grandes: Catena 30M, Natural 30M, Sapiom 51M y Kite 18M, en un sector que suma ~196M entre 2025 y 2026 según Dealroom.

**2. La "evidencia o forense de agentes" como producto central recibe migajas.** Las startups que la tienen en el centro (OpenBox, Neuromorphic, Asymptote, FriskAI, Endeem, más OpenMatter y Glacis sin monto) suman **~USD 22M visibles**, todo en pre-seed y seed de USD 2,5–5,5M. Comparado con el runtime y la identidad, el capital ahí es uno o dos órdenes de magnitud menor. **No encontré ninguna serie A ni ninguna adquisición cuyo producto central sea la forense o atribución de agentes.**

**3. Los incumbentes se movieron rápido, pero como feature y con registro propio.** Entre ago-2025 y nov-2026 hubo al menos seis lanzamientos de "audit trail + undo" de agentes: Rubrik (dos), Veeam, Cohesity, Commvault y Vorlon. Comparten tres rasgos:
- **El registro lo guarda el vendor del operador.** Lo llaman "inmutable", pero no es verificable por un tercero ni por la contraparte.
- **Cubren el "qué pasó y cómo lo deshago" dentro de la empresa,** no el "quién autorizó y quién paga" entre partes.
- **Los analistas (Futurum) dudan del undo real:** restaurar estado no deshace una acción externa como un pago, un email o una orden.

**4. La excepción importante es Mastercard Verifiable Intent** (5-mar-2026, open source, junto con Google AP2):
- Ataca justo el tramo "qué autorizó el humano" con un registro a prueba de manipulación, multi-parte y pensado para disputas.
- **Contradice en parte la hipótesis,** porque en pagos con tarjeta ya existe un intento serio de prueba independiente de la autorización.
- Su alcance es acotado: cubre la intención de pago, no las acciones no financieras del agente.
- En lo leído estaba anunciado para integrarse "en los próximos meses". No verifiqué si ya está en producción.

**5. Las disputas son un mercado grande, pero sin capital específico.** Chargeflow (35M) y Justt (~100M acumulados) escriben sobre la "brecha de evidencia" en compras de agentes, pero no encontré un producto agéntico con nombre ni una ronda dedicada a eso. La regla de responsabilidad de Visa y Mastercard no existe todavía.

**Respuesta corta:** el capital está entrando **alrededor** del problema (prevenir, identificar, pagar) y los incumbentes lo están convirtiendo en una **feature** de backup y SaaS-security. La forense y atribución **verificable por terceros** sigue poco financiada: no encontré una serie A ni una salida.

---

## (e) Qué significa para la hipótesis

| Parte de la hipótesis | Veredicto con lo encontrado |
|---|---|
| "Nadie puede probar de forma independiente **qué autorizó el humano**" | **Parcialmente refutada para pagos con tarjeta.** Mastercard Verifiable Intent, AP2 y los mandatos firmados de Visa, Mastercard y Google apuntan a eso desde 2025–2026. Fuera de pagos (acciones en SaaS, código, emails, infra) se sostiene: no encontré nada equivalente. |
| "Nadie puede probar **qué hizo realmente el agente**" | **Se sostiene en su versión fuerte.** Hay muchos registros (Rubrik, Vorlon, Veeam, OpenBox), pero todos los genera el operador o su vendor. OpenBox y OpenMatter hablan de pruebas criptográficas, sin evidencia de verificación independiente. |
| "Nadie sabe **quién debe pagar**" | **Se sostiene.** No hay regla de responsabilidad de las redes ni reason code para agentes. La industria dice que se "está escribiendo", hay encuestas divididas (39% dice que el proveedor de IA) y el único compromiso reportado (Amex) no está verificado. |
| "Los registros los firma la parte interesada" | **Se sostiene** para todos los productos de incumbentes revisados. Verifiable Intent es la excepción parcial. |
| "Problema **grande**" | **Plausible pero indirecto.** No hay un tamaño de mercado de la "forense de agentes" en sí. Las proxies sí son grandes: DFIR ~USD 8–13B, contracargos ~USD 2,5B de software y 324M de disputas por año en 2028, comercio agéntico de USD 0,2–1T solo en EE. UU. en 2030, y seguros de IA de USD 4,7B en 2032. No hay datos de tasa de disputa agéntica: el pitch no debe inventarla. |
| "**Poco atendido**" | **Se sostiene para el capital de riesgo, se debilita a nivel de features.** Seis incumbentes ya venden "audit + undo" de agentes y Gartner no tiene un segmento de forense en "securing AI". El riesgo es que el problema termine absorbido como feature de Rubrik, Veeam o las redes de pago, no que esté saturado de startups. |

**Reformulación sugerida, más defendible ante un jurado:**

> "Ya existen registros y 'undo' de agentes, pero los guarda la parte interesada y solo sirven dentro de una empresa. Falta **evidencia neutral y verificable por todas las partes** (usuario, operador del agente, comercio o tercero, aseguradora) sobre la cadena *autorización → acción → efecto*, fuera del caso acotado de los pagos con tarjeta. Eso es lo que hace falta para asignar responsabilidad."

**Implicancias prácticas:**
1. No posicionarse como "otro audit log ni otro undo", porque compite con Rubrik, Veeam, Commvault, Cohesity y Vorlon.
2. Diferenciarse en tres cosas: **verificable por terceros, entre organizaciones, y que cubre acciones no financieras.**
3. Componer con Verifiable Intent y AP2 en lugar de competir con ellos: usarlos como el eslabón de "autorización" y aportar el eslabón de "acción y efecto".
4. El comprador natural podría ser quien paga la pérdida: aseguradoras de IA, el área de disputas de los comercios o los emisores. No necesariamente el CISO, que ya recibe la feature de su vendor de backup.

---

## Fuentes principales (además de las URL en las tablas)

- Dealroom, pagos agénticos, 19-oct-2026: https://dealroom.co/charts/startup-stack-ai-spending
- Futurum sobre el undo de Veeam y Cohesity: https://futurumgroup.com/insights/veeam-brings-ai-agent-undo-to-microsoft-365-with-intelligent-resops/ · https://futurumgroup.com/insights/cohesity-extends-cyber-resilience-to-the-ai-agents-themselves
- Worldpay sobre responsabilidad agéntica: https://worldpay.com/insights/articles/agentic-commerce-liability-is-still-being-written
- Bloomberg Law sobre responsabilidad de los agentes de compra: https://news.bloomberglaw.com/banking-law/ai-shopping-agents-pose-novel-liability-authorization-risks (no la abrí)
- Notas previas del equipo: `../mercado/22-adquisiciones.md`, `../mercado/17-eeuu-seed-reciente.md`, `../mercado/14-region-israel.md`
