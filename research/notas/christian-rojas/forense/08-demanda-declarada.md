# 08 — Demanda declarada: ¿los CISOs, los fondos y los analistas dicen que la forense de agentes es un problema?

Fecha: 21-nov-2026. Método: unas 20 búsquedas web y unas 30 lecturas de fuente con WebFetch.

**Hipótesis bajo prueba:** "Cuando un agente ejecuta una acción dañina o no autorizada, nadie puede probar de forma independiente qué autorizó el humano, qué hizo el agente y quién debe pagar. Los registros los firma la parte interesada. Es un problema grande y poco atendido."

**Reglas de lectura**
- "Confirmada": leí la cifra o la frase en la fuente original o en una reproducción literal del comunicado.
- "Parcial": la cifra existe, pero dice otra cosa, tiene otra fecha o viene de otra fuente.
- "Refutada": la fuente original dice algo distinto.
- "No verificado": no pude abrir la fuente original.
- Las citas tienen menos de 15 palabras. Las extrajo WebFetch del texto de la página. Antes de ponerlas en una slide, conviene volver a abrir la URL y verificarlas.
- gartner.com, thehackernews.com e infosecurity-magazine.com devolvieron 403. En esos casos usé reproducciones del comunicado en prensa y lo indico.

---

## (a) Tabla de verificación

### 1. Team8

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| "Cerca de 1 de cada 5 CISOs no puede saber qué hizo un agente con datos sensibles" | Charla de Liran Grinberg (Team8) en la conferencia Tech1, citada por Calcalist. **No es un informe publicado.** | **Parcial** | "One in five CISOs in our CISO Village can't tell whether an agent has touched sensitive data." Dice *si tocó* datos, no *qué hizo* con ellos. No da tamaño de muestra. | https://www.calcalistech.com/ctechnews/article/i1nz7ctbm | 29-oct-2026 |
| "Solo el 2% espera depender de productos comprados" | Misma charla | Confirmada | "Only 2% expect to mostly buy in two years." | idem | 29-oct-2026 |
| "Asegurar agentes es la preocupación n.º 1 (37%)" | Team8 CISO Village Survey **2025** (>110 líderes) | **Parcial**: la cifra existe, pero es de **2025, no de 2026**, y queda casi empatada con el uso de IA por empleados (36%) | "Securing AI agents (37%) and employees' use of AI tools (36%)" | https://team8.vc/ciso-village-survey-2025/ | 17-jul-2025 |
| "67% construye sus agentes in-house" | Team8 CISO Village Survey 2025 | Confirmada, **pero es de 2025** | "67% of these enterprises are building their own agents in-house." | idem | 17-jul-2025 |
| (dato nuevo) Team8 2026 | Encuesta anual Team8 2026, según SecurityWeek. No encontré el informe de Team8. | Confirmada en fuente secundaria | "AI and agent security is by far the biggest pain point (78%)" | https://www.securityweek.com/cisos-race-to-control-ai-agents-without-destroying-their-value/ | 14-sep-2026 |

### 2. Gartner

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| "54% no tiene cómo limitar el acceso de los agentes" | Gartner, "Top Five Actions for CISOs" (encuesta a 297 líderes, Q2-2026) | **Confirmada** con una reproducción literal (CXOToday) y el snippet del buscador de gartner.com. No abrí gartner.com (403). | "no defined approach to limit AI agent access, or rely on predefined human access" | https://www.gartner.com/en/newsroom/press-releases/2026-09-30-gartner-identifies-top-five-actions-for-cisos-to-take-by-end-of-2026 · reproducción: https://cxotoday.com/?p=251986 | 30-sep-2026 |
| Mercado "Securing AI": 2.835M (2026), ~4.800M (2027), ~7.700M (2028) | Gartner forecast. Lo leí en ITBrief porque gartner.com dio 403. | **Confirmada** en fuente secundaria | "almost USD $4.8 billion" (2027), +68,7%. Segmentos: AI app security, usage control, governance platforms, gateways y "otros". **Ningún segmento es auditoría o forense.** | https://itbrief.com.au/story/gartner-sees-securing-ai-market-hit-usd-4-8bn-in-2027 | 27-ago-2026 |

### 3. IBM

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| "13% tuvo brechas de IA" | IBM Cost of a Data Breach 2025 (600 organizaciones; Ponemon) | Confirmada | "13% of organizations reported breaches of AI models or applications" | https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls | 30-jul-2025 |
| "97% sin controles de acceso de IA" | idem | Confirmada. El texto dice "no tener" controles, no "controles inadecuados". El 97% es sobre el 13% que tuvo brechas. | "97% report not having AI access controls in place." | idem | 30-jul-2025 |
| (extra) auditorías | idem | Confirmada | "only 34% perform regular audits for unsanctioned AI." | idem | 30-jul-2025 |

### 4. IANS

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| 69% | IANS + Artico, Security Budget Benchmark 2026 (>500 ejecutivos), según CSO Online | **Parcial**: la cifra existe, pero dice "IA" sin distinguir IA *para* seguridad de seguridad *de* IA | "AI, named by 69% of CISOs as their top net-new priority." | https://www.csoonline.com/article/4223455/security-spending-is-growing-except-for-the-typical-ciso.html | 17-sep-2026 |
| 24% | idem | Confirmada | "Just 24% track AI as a separate security-budget line or subcategory" | idem | 17-sep-2026 |
| "La seguridad de IA es ~3% del presupuesto" (nota 23) | Atribuida a Infosecurity Magazine | **No verificado.** CSO no lo dice; su único 3% es otro dato (brecha como motivo de aumento). Infosecurity dio 403. | — | https://www.infosecurity-magazine.com/news/ai-top-priority-new-spend-cyber/ | — |

### 5. Fondos

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| Bessemer: "la capa menos construida" | Bessemer Atlas, "Securing AI agents" | **Refutada como frase y como tema.** No dice "least built". Lo más parecido se refiere a la **protección en runtime** (etapa 3), no a la forense. | "where the market is most underdeveloped, and where the clearest infrastructure opportunity lies." | https://bvp.com/atlas/securing-ai-agents-the-defining-cybersecurity-challenge-of-2026 | 24-mar-2026 |
| Bessemer: quién aprobó | idem; cita de Mike Gozzo (Ada), no de Bessemer | Confirmada | "'What can this agent do?' 'On whose behalf'? and Who approved it?" | idem | 24-mar-2026 |
| Insight: atribución y "OAuth no lo resuelve" | Insight Partners, "Securing agentic AI" | **Confirmada** | "a need for tracing from action to identity"; "was the Agent acting under its own agency or responding to a human instruction?"; "isn't well catered for with existing protocols (e.g., OAuth 2.0)" | https://www.insightpartners.com/ideas/securing-agentic-ai | 29-oct-2025 |
| Menlo: forense y "quién autorizó" | Menlo, "Security for Agents and Agents for Security" | **Confirmada** | "making post-incident forensics very difficult"; "Who authorized the action, and who executed it?"; "clear attribution chains back to human auth" | https://menlovc.com/perspective/security-for-agents-and-agents-for-security-the-next-cybersecurity-frontier/ | 29-jul-2025 |
| Lightspeed Cyber60: atribución y rollback | Lightspeed Cyber60 2026-27 (200 CISOs de EE. UU., Wakefield, 4–14 sep-2026) | **Confirmada** | "Attribution that separates agent actions from the human whose credentials it may be using"; "audit trails, and reversibility"; "about one in five named rollback or reversibility." | https://lsvp.com/cyber60-2026-2027/ | sep-2026 |
| Lightspeed: incidentes | idem | Confirmada | "suspected-but-unconfirmed incidents rose from 38% to 63%" (los confirmados bajaron de 37% a 16%) | idem | sep-2026 |
| a16z: encuesta a CISOs | a16z, "The New Security Agenda" (100 CISOs) | **Confirmada para los números; no menciona auditoría, forense ni atribución** | "46% cite agents exceeding their permissions or being compromised"; "45% plan a new purchase or upgrade for internal AI agent security" | https://a16z.com/the-new-security-agenda/ | 28-oct-2026 |
| Cowboy Ventures | "Where we're looking to invest: Securing AI agents" (Rohan Puranik) | **Confirmada** | "propagating and auditing authorization from user to agent to sub-agent"; "no accountability chain"; "struggle to identify the right rollback boundary" | https://cowboy.vc/news/where-were-looking-to-invest-securing-ai-agents | 11-mar-2026 |
| YL Ventures | Feed de insights. Solo titulares; no hay tesis propia legible. | No verificado como tesis | Titular de Bay: "vet agent actions before they run". Es prevención, no forense. | https://www.ylventures.com/news-and-insights/insights/ | 11-nov-2026 |
| Ballistic (Barmak Meftah) | TechCrunch | Confirmada; **no habla de auditoría ni de forense** | "runtime observability and runtime frameworks for safety and risk are going to be absolutely essential" | https://techcrunch.com/2026/01/19/rogue-agents-and-shadow-ai-why-vcs-are-betting-big-on-ai-security | 19-ene-2026 |
| Glilot (Nofar Amikam) | "Why I Invested in Way Security" | Confirmada; **habla de acceso, no de auditoría** | "a consistent way to understand what those agents can access" | https://glilotcapital.com/cyberhubs/why-i-invested-in-way-security/ | 30-jul-2026 |
| Merlin Group (Matt Hartman), sector público | The Register | Confirmada | "an audit trail for actions taken on an agency's behalf"; "prove what one did at 2 AM on a Tuesday" | https://www.theregister.com/a/5297546 | 19-sep-2026 |

### 6. Analistas

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| Forrester AEGIS y forense | Blog de Jeff Pollard (Forrester) | **Confirmada** | "Obscured causal provenance, making post-incident forensics nearly impossible." | https://www.forrester.com/blogs/introducing-aegis-the-guardrails-that-cisos-need-for-the-agentic-enterprise/?eblogid=296333 | 12-ago-2026 |
| IDC: "el registro no existe" | Blog de IDC, firmado por Ryan Smith (Content Marketing Director, **no analista**) | Confirmada | "the record of what happened often doesn't exist at all"; "60% of security leaders lack basic agent containment controls"; "35% cannot shut down a rogue agent" | https://www.idc.com/resource-center/blog/the-audit-trail-that-doesnt-exist/ | 8-sep-2026 |
| KuppingerCole | Investigación **pagada por Ping Identity** | Confirmada (resumen del comunicado, no cita textual del analista) | "agent chains become untraceable and break auditability" | https://press.pingidentity.com/2026-04-28-Ping-Identity-Warns-of-Emerging-Authorization-Risks-as-AI-Agents-Scale-Across-Enterprises | 28-abr-2026 |
| Gartner: Market Guide for Guardian Agents | Litan y Plummer, feb-2026. Detrás de paywall. | **No verificado** en la fuente. Vendors que anunciaron estar incluidos: Astrix y Delinea (categoría "Agent Identity"), Orchid, Bigeye, Silverfort. No encontré una categoría de forense. | — | https://www.gartner.com/en/documents/7509053 · https://delinea.com/news/delinea-recognized-in-gartner-market-guide-for-guardian-agents | 24/25-feb-2026 |
| Gartner: tipos de guardian agents | ITPro (Avivah Litan) | Confirmada en fuente secundaria | Tipos: "reviewers", "monitors" (observan y rastrean acciones de agentes) y "protectors". Mercado: "10 to 15% of the broader agentic AI market by 2030". | https://www.itpro.com/technology/artificial-intelligence/enterprises-are-worried-about-agentic-ai-security-risks-gartner-says-the-answer-is-just-adding-more-ai-agents | 12-jun-2025 |
| Gartner: respuesta a incidentes | Predicción de Gartner (Christopher Mixter), leída en ITBrief UK | Confirmada en fuente secundaria | "half of enterprise cybersecurity incident response efforts will focus on incidents involving these systems" (apps de IA a medida, 2028); "Most security teams still lack clear processes for handling AI-related incidents" | https://itbrief.co.uk/story/custom-ai-to-drive-half-of-cyber-incidents-by-2028 | 16-mar-2026 |
| Gartner AI TRiSM | — | **No verificado** (no llegué a leerlo) | — | — | — |
| Software Analyst (Francis Odum) | — | **No encontrado** en 2 búsquedas | — | — | — |
| Latio 2026 AI Security Market Report | Informe con formulario. Categorías tomadas del blog de Lasso, un vendor incluido en el informe. | Parcial | 5 categorías: Endpoint Agent Specialists, Broader AI Security, Platform Providers, DLP/Insider Threat, Developer Governance. **Ninguna es forense o auditoría.** | https://www.lasso.security/blog/lasso-named-a-leader-in-latios-2026-ai-security-market-report | 15-sep-2026 |

### 7. Respuesta a incidentes y encuestas de vendors

| Cifra o frase | Fuente original | Veredicto | Texto exacto | URL | Fecha |
|---|---|---|---|---|---|
| Unit 42 sobre ataques con IA | Unit 42, "AI insights" (Andy Piazza) | Confirmada | "has not observed a meaningful shift in capabilities related to AI-enabled attacks"; "nascent and have not had major impacts" | https://unit42.paloaltonetworks.com/ai-insights-incident-response-report/ | 16-jul-2026 |
| Unit 42: investigar incidentes con agentes | — | **Sin dato.** La página no habla de logs faltantes ni de atribuir acciones a agente vs. usuario. | — | idem | — |
| Mandiant M-Trends 2026 | Resumen del buscador; no abrí el PDF | No verificado textual | Según el resumen, 2025 no fue el año de brechas causadas directamente por IA (caso QUIETVAULT con CLI de IA local) | https://cloud.google.com/blog/topics/threat-intelligence/m-trends-2026 | 2026 |
| Verizon DBIR 2026 | Cobertura de prensa | **Sin dato** sobre incidentes con agentes. Solo shadow AI: 3.ª fuente no maliciosa de fuga de datos. | — | https://www.verizon.com/about/news/breach-industry-wide-dbir-finds | may-2026 |
| SANS | Resumen de la AI Survey y la SOC Survey 2026 | **Sin dato** sobre investigar agentes. La Detection & Response Survey 2026 se presenta el 9-dic-2026. | — | https://www.sans.org/webcasts/sans-2026-detection-response-survey-report | — |
| Gravitee (vendor; 900 líderes de EE. UU. y Reino Unido; Opinion Matters) | Comunicado de prensa | Confirmada (dato de **vendor**) | "Only 1 in 8 can fully reconstruct what an agent did 30 days ago."; 52% tuvo un incidente con agentes; menos de 1 de cada 10 tiene un responsable nombrado; 27% define responsables en cadenas de agentes | https://www.cybersecuritydive.com/press-release/20261109-enterprises-have-learned-to-deploy-ai-agents-they-have-not-yet-learned-to-1/ | 9-nov-2026 |
| Okta Global CISO Insights (306 CISOs) | Okta newsroom | Confirmada; **no tiene cifras de auditoría** | "can authorize what agents do": 45%; "can identify all agents": 47% | https://www.okta.com/newsroom/articles/global-ciso-insights-2026/ | 29-jul-2026 |

---

## (b) Lo que dicen fondos y analistas del problema

**Nombran explícitamente la atribución o la forense (fuente leída):**
- **Menlo (jul-2025)** es la formulación más cercana a la hipótesis: "Who authorized the action, and who executed it?". También dice que la forense post-incidente es "very difficult".
- **Insight (oct-2025):** habla de trazar de acción a identidad y de distinguir agencia propia de instrucción humana. Dice que OAuth 2.0 no lo cubre. Pide un "audit or forensics trail" en entornos regulados.
- **Cowboy (mar-2026):** describe la cadena de permisos usuario → agente → subagente como poco modelada, sin "accountability chain". Agrega que nadie sabe dónde cortar un rollback.
- **Lightspeed (sep-2026):** pide atribución que separe al agente del humano cuyas credenciales usa. Pone auditoría y reversibilidad como condición previa para dar más autonomía al SOC.
- **Forrester (ago-2026):** "post-incident forensics nearly impossible" por la procedencia causal oculta.
- **IDC (sep-2026):** "the record of what happened often doesn't exist at all". Recomienda un RACI para que "who approved this" tenga respuesta documentada.
- **KuppingerCole/Ping (abr-2026):** las cadenas de agentes se vuelven "untraceable" y rompen la auditabilidad.
- **Merlin Group (sector público, sep-2026):** pide poder "prove what one did at 2 AM on a Tuesday".

**No lo nombran: hablan de acceso, inventario o runtime:**
- a16z (oct-2026)
- Bessemer: su "oportunidad más clara" es la protección en runtime
- Ballistic
- Glilot
- YL Ventures: su apuesta, Bay, valida acciones *antes* de que ocurran
- Gartner: segmentos del mercado y las 5 acciones para CISOs
- Latio

**Categoría de analista:** no encontré ningún analista que trate "agent forensics" o "agent audit" como categoría de mercado con vendors propios.
- Gartner encuadra la supervisión como "guardian agents". Sus vendors visibles son de identidad (Astrix, Delinea, Silverfort). La función "monitors" es lo más cercano a la auditoría.
- IDC propone como solución las plataformas de los hyperscalers (Agent 365, Agentforce, ServiceNow AI Control Tower, Bedrock AgentCore, Vertex).
- Un vendor, Proofpoint, ya publicó un "Agent Integrity Framework" con pilares de "Identity and Attribution" y "Agent Audit Trails". El dato viene del resumen de búsqueda; no leí el PDF: https://www.proofpoint.com/sites/default/files/white-papers/pfpt-us-wp-agent-integrity-framework.pdf

---

## (c) Evidencia en contra

1. **Ninguna encuesta grande pone la forense como prioridad de compra.**
   - a16z (100 CISOs) no menciona auditoría, forense ni atribución. Las prioridades son seguridad de agentes internos, SOC, ofensiva y código.
   - Las 6 áreas de oportunidad de Lightspeed no incluyen forense. La auditoría aparece solo como requisito dentro de "Trusted Autonomous Response".
   - Los segmentos del mercado de Gartner, las 5 acciones de Gartner y las 5 categorías de Latio no incluyen forense.
   - Okta mide identificar, controlar y autorizar, pero no auditar.
2. **Pocos piden reversibilidad.** En Lightspeed, solo "about one in five" CISOs nombró rollback o reversibilidad como condición.
3. **Los incidentes reales todavía son pocos o no están documentados.**
   - Unit 42 dice que los ataques con IA son "nascent" y sin impacto mayor.
   - Según el resumen, Mandiant dice que 2025 no fue el año de brechas causadas por IA.
   - El DBIR 2026 no tiene un conteo de incidentes con agentes.
   - En Lightspeed, los incidentes de IA confirmados **bajaron** de 37% a 16%.

   La demanda de forense de agentes es, sobre todo, anticipatoria.
4. **El dinero va a prevención, no a evidencia.**
   - Gartner (54%), IBM (97%), Okta y Glilot apuntan a controles de acceso e identidad.
   - El capital de los fondos se concentra en identidad y control en runtime (ver nota 21).
5. **El presupuesto es chico y viene de reasignar.** IANS: mediana de crecimiento 0% (nota 23) y solo 24% tiene una línea de presupuesto para IA.
6. **El comprador construye en casa.** Team8: solo 2% espera comprar mayormente y 67% construye sus agentes in-house. Esos equipos pueden armar sus propios logs.
7. **Los incumbentes reclaman el espacio.** Proofpoint ya tiene pilares de atribución y audit trail. IDC presenta las plataformas de agentes como la solución.
8. **La parte "independiente / firmada por la parte interesada" no aparece en ninguna fuente de demanda.** Ningún CISO, fondo ni analista revisado pide que los registros los firme un tercero neutral o que tengan no repudio. El problema que declaran es que **no hay registro o no se puede reconstruir** (Gravitee, IDC, Forrester), no que el registro no sea confiable.

---

## (d) Qué significa para la hipótesis

**Respaldado por fuentes:**
- El problema existe y tiene nombre propio entre fondos y analistas: atribución humano vs. agente, quién autorizó, cadena de delegación, forense post-incidente.
- Lo nombran explícitamente Menlo, Insight, Cowboy, Lightspeed, Forrester, IDC y KuppingerCole, más un comprador del sector público (Merlin).
- Hay una cifra cuantitativa de capacidad, pero es de un vendor: "solo 1 de cada 8 puede reconstruir completamente lo que hizo un agente hace 30 días" (Gravitee, n=900).
- La subida de incidentes "sospechados pero no confirmados" (38% → 63%, Lightspeed) es compatible con la falta de capacidad forense. Que esa sea la causa es inferencia nuestra; la fuente no lo dice.

**Débil o no respaldado:**
- **"Grande":** no hay presupuesto declarado ni categoría de analista para esto. Aparece como requisito dentro de identidad, runtime o respuesta autónoma, no como compra propia.
- **"Poco atendido":** es cierto que no hay empresa dedicada (nota 21), pero puede ser porque los incumbentes lo absorben como feature (Proofpoint, plataformas de agentes).
- **"Firmado por la parte interesada / prueba independiente":** cero evidencia de demanda declarada en esta muestra. Es la parte más original de la hipótesis y la menos validada. Hay que buscarla en otro lado: seguros, legal, disputas entre empresas, regulación (EU AI Act art. 12, que no verifiqué aquí).
- **"Quién debe pagar":** ninguna fuente de demanda lo plantea. Las fuentes hablan de *accountability* interna (un responsable nombrado), no de responsabilidad entre partes.

**Cifras a corregir en el pitch**
- Team8 37% y 67% son de 2025, no de 2026.
- La frase de Team8 es "can't tell whether an agent has touched sensitive data", no "qué hizo".
- Bessemer no dice "la capa menos construida". Su "most underdeveloped" se refiere a la protección en runtime, no a la forense.
- El ~3% del presupuesto de IANS no está verificado.
- El 69% de IANS mezcla IA para seguridad con seguridad de IA.

**Reformulación sugerida, que las fuentes sí sostienen:** "Los CISOs no pueden reconstruir ni atribuir lo que hicieron sus agentes (Forrester, IDC, Menlo, Insight). Ponen auditoría y reversibilidad como condición para dar más autonomía (Lightspeed). Pero hoy compran prevención, no evidencia." El ángulo de "evidencia independiente de terceros" queda como apuesta propia que hay que validar con entrevistas a compradores (aseguradoras, legal, sector público), no como demanda declarada.
