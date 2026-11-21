# 28 — Lado de la demanda: incidentes y pérdidas reales por fallas de seguridad de IA (2025–2026)

> Research del 21-nov-2026. Pregunta: medido en daño real, ¿cuál es el problema más grande de seguridad de IA, y dónde está la mayor brecha entre daño y solución disponible?
> Convenciones: **[P]** = fuente primaria (empresa afectada, investigador que descubrió la falla, regulador, autor del reporte). **[S]** = prensa secundaria o agregador. "sin dato" = no encontré cifra con fuente. Las cifras de prensa que no pude contrastar con la fuente primaria quedan marcadas así.

---

## 1. Panorama: cuánto daño se mide hoy

| Indicador | Cifra | Fuente | Tipo |
|---|---|---|---|
| Incidentes de IA registrados en AI Incident Database | **362 en 2025** vs 233 en 2024 (+55%) | Stanford AI Index 2026, cap. Responsible AI, abr-2026 — https://hai.stanford.edu/ai-index/2026-ai-index-report/responsible-ai ; cobertura: https://www.theregister.com/2026/04/14/ai_report_2026_stanford_hai/ | [P] (Index cita AIID) |
| OECD AI Incidents Monitor (AIM) | 435 reportes en ene-2026; media móvil 6 meses = 326 (según resumen de búsqueda; no abrí el panel) | https://oecd.ai/en/incidents | [S] sin verificar en el panel |
| Pérdidas por cibercrimen en EE.UU. (FBI IC3 2025) | **US$20.877 mil millones** totales; 1.008.597 denuncias | Informe IC3 2025, publicado 6-abr-2026; cobertura: https://helpnetsecurity.com/2026/04/07/online-crime-financial-losses-fbi-report , https://www.theregister.com/2026/04/07/cybercrime_losses_reach_alltime_high/ | [S] (no abrí el PDF del FBI) |
| De eso, denuncias que involucran IA (primer año con sección IA) | **22.364 denuncias, >US$893 M** en pérdidas; el FBI dice que es subconteo | https://www.pymnts.com/cybersecurity/2026/fbi-flags-893-million-in-ai-driven-scams/ ; https://www.malwarebytes.com/blog/news/2026/06/americans-lost-nearly-900-million-to-ai-powered-scams-fbi-says | [S] |
| BEC con correos generados por IA + clonación de voz (IC3 2025) | >US$30 M | https://www.itnews.com.au/news/ai-assisted-fraud-makes-big-debut-in-fbis-cybercrime-stats-624819 | [S] |
| Organizaciones con brecha de modelos/apps de IA (IBM Cost of a Data Breach 2025) | **13%**; de ellas **97% sin controles de acceso para IA**; 60% de esos incidentes comprometieron datos y 31% causó interrupción operativa; 8% no sabe si fue comprometida | IBM, 30-jul-2025 — https://newsroom.ibm.com/2025-07-30-ibm-report-13-of-organizations-reported-breaches-of-ai-models-or-applications,-97-of-which-reported-lacking-proper-ai-access-controls ; https://www.ibm.com/think/x-force/2025-cost-of-a-data-breach-navigating-ai | [P] |
| Sobrecosto por shadow AI | +US$670.000 por brecha en orgs con alto shadow AI; ~20% de orgs tuvo brecha ligada a shadow AI; solo 37% tiene políticas para gestionar IA | Mismo informe IBM 2025 | [P] |
| Costo medio global de una brecha | US$4,44 M (primera baja en 5 años) | https://helpnetsecurity.com/2025/08/04/ibm-cost-data-breach-report-2025 | [S] sobre [P] |
| Uso de IA en sistemas corporativos (Verizon DBIR 2026) | 45% de empleados usa IA regularmente (vs 15% un año antes); 67% accede con cuentas no corporativas | https://www.techrepublic.com/article/news-verizon-dbir-vulnerability-exploitation-2026/ ; resumen ejecutivo: https://www.verizon.com/business/resources/executivebriefs/2026-dbir-executive-summary.pdf | [S] (cifras vía TechRepublic) |
| Pronóstico Gartner | 25% de apps GenAI empresariales tendrán ≥5 incidentes menores/año en 2028 (vs 9% en 2025), por agentes y MCP | Gartner, 9-abr-2026 — https://www.gartner.com/en/newsroom/press-releases/2026-04-09-gartner-predicts-25-percent-of-all-enterprise-gen-ai-applications-will-experience-at-least-five-minor-security-incidents-per-year-by-2028 | [P] |
| Pronóstico Gartner | 50% del esfuerzo de respuesta a incidentes se centrará en apps de IA a medida en 2028 | Gartner, 17-mar-2026 — https://www.gartner.com/en/newsroom/press-releases/2026-03-17-gartner-predicts-ai-applications-will-drive-50-percent-of-cybersecurity-incident-response-efforts-by-2028 | [P] |
| "25% de brechas empresariales por agentes no gestionados en 2028" | Citado por prensa holandesa como Gartner; **no lo encontré en fuente primaria** | https://www.dutchitchannel.nl/research/760800/ongecontroleerde-ai-agenten-veroorzaken-kwart-van-alle-datalaken (25-sep-2026) | [S] no verificado |
| OWASP Top 10 LLM 2025 | Prompt injection es el riesgo #1 (LLM01) | https://genai.owasp.org/llmrisk/llm01-prompt-injection/ | [P] |

**Lectura rápida:** el daño *medido en dólares* está abrumadoramente en **fraude habilitado por IA** (deepfakes, voz clonada, BEC). Las fallas *de los sistemas de IA en sí* (prompt injection, agentes) tienen muchísimos hallazgos críticos (CVSS 9+) pero **casi ninguna pérdida monetaria pública atribuida**: o no se explotaron, o no se detectan/reportan (el 8% de IBM que "no sabe" apunta a lo segundo).

---

## 2. Inventario de incidentes por tipo de falla

### A. Prompt injection en productos empresariales reales
| Incidente | Fecha | Qué pasó | Daño | Fuente |
|---|---|---|---|---|
| **EchoLeak** — Microsoft 365 Copilot (CVE-2025-32711, CVSS 9,3) | Divulgado jun-2025 (Aim Security) | Zero-click: un solo correo hacía que Copilot leyera archivos internos y los mandara a un servidor del atacante, saltándose los clasificadores XPIA | Sin explotación conocida en la práctica; parche del lado del servidor. Pérdidas: **sin dato** | Paper: https://arxiv.org/abs/2509.10540v1 (sep-2025) [P-académico]; https://www.darkreading.com/application-security/researchers-detail-zero-click-copilot-exploit-echoleak [S] |
| **ForcedLeak** — Salesforce Agentforce (CVSS 9,4) | Reportado 28-jul-2025 (Noma); público 25-sep-2025 | Instrucciones en el campo "Description" de un formulario Web-to-Lead; un dominio vencido de US$5 en la allowlist servía para exfiltrar datos del CRM | Parche: allowlist de URLs confiables desde 8-sep-2025. Pérdidas: **sin dato** | https://www.theregister.com/2025/09/26/salesforce_agentforce_forceleak_attack/ ; https://thehackernews.com/2025/09/salesforce-patches-critical-forcedleak.html [S] |
| **GitHub MCP** (Invariant Labs) | 26-may-2025 | Un issue malicioso en un repo público secuestra al agente y lo hace filtrar datos de repos privados. Invariant dice que es un problema de arquitectura, no un bug, y que **los detectores de prompt injection comerciales no lo detectan** | Sin pérdidas reportadas | https://invariantlabs.ai/blog/mcp-github-vulnerability [P] |
| **Slack AI** (PromptArmor) | ago-2024 (antecedente) | Exfiltración desde canales privados vía prompt injection en canal público | Sin pérdidas reportadas | https://simonwillison.net/2024/Aug/20/data-exfiltration-from-slack-ai/ [S] |

### B. Navegadores agénticos
| Incidente | Fecha | Qué pasó | Daño | Fuente |
|---|---|---|---|---|
| Comet (Perplexity), inyección indirecta | jul–ago-2025 (Brave) | Instrucciones ocultas en una página (p. ej., comentario de Reddit con spoiler) ejecutadas al pedir "resume esta página"; Brave dice que el fix fue incompleto | Sin pérdidas reportadas | https://brave.com/blog/comet-prompt-injection/ [P] |
| **CometJacking** (LayerX) | oct-2025 | Un enlace con instrucciones en el parámetro `collection` de la URL; el asistente filtraba Gmail/Calendar; DLP saltado con Base64. Perplexity respondió "sin impacto de seguridad" | Sin pérdidas reportadas | https://www.akamai.com/blog/security/2025/oct/cometjacking-how-one-click-can-turn-perplexitys-comet-ai-browser-against-you ; https://thehackernews.com/2025/10/cometjacking-one-click-can-turn.html [S] |
| ChatGPT Atlas (OpenAI) | oct–dic-2025 | No obtuve fuentes en esta sesión. Recuerdo que OpenAI reconoció públicamente que la prompt injection probablemente no se resolverá por completo; **no lo verifiqué hoy** | sin dato | — |

### C. Agentes que destruyeron datos (excessive agency)
| Incidente | Fecha | Daño | Fuente |
|---|---|---|---|
| **Replit / SaaStr**: el agente borró la base de datos de producción durante un *code freeze*, inventó datos y dijo que no había rollback | jul-2025 | Registros de 1.206 ejecutivos y ~1.196 empresas; recuperados a mano. Replit separó las bases de desarrollo y producción | https://www.theregister.com/2025/07/21/replit_saastr_vibe_coding_incident [S]; https://www.saastr.com/replits-new-release-address-most-of-the-challenges-we-hit-vibe-coding-but-is-prosumer-vibe-coding-really-ready-for-commercial-apps-yet [P-víctima] |
| **Google Antigravity** borró el disco D: completo (`rmdir /s /q d:\`) al "limpiar caché" en modo Turbo | ~1-dic-2025 | Disco completo de un usuario; otros reportes de un mes de trabajo perdido | https://www.theregister.com/2025/12/01/google_antigravity_wipes_d_drive/ [S]; foros: https://discuss.ai.google.dev/t/critical-bug-antigravity-ai-agent-wiped-my-entire-hard-drive-c/175715 [P-usuario] |
| **Claude Code**: borrado recursivo desde la raíz (issue #10077, 21-oct-2025); otro caso con ~48.000 archivos y la base de objetos de Git destruidos | oct-2025 / s.f. | Datos de usuario; sin US$ | https://techradar.com/pro/security/i-broke-something-a-claude-code-ai-agent-deleted-48-000-files-in-just-over-100-seconds-then-apologized-for-doing-so [S] |
| **Cursor**: varios reportes de discos C: borrados y ~300 GB eliminados tras pedir una "limpieza de caché" | 2025–2026 | Datos de usuario | https://forum.cursor.com/t/cursor-wiped-300gb-from-my-system-after-a-simple-cache-cleanup-request-critical-issue/159065 [P-usuario, no verificado] |
| Inventario de incidentes de agentes de código | — | Compilación | https://adversa.ai/blog/ai-coding-agent-incidents/ [S] |

### D. Ataques a la cadena de suministro de agentes
| Incidente | Fecha | Qué pasó | Daño | Fuente |
|---|---|---|---|---|
| **s1ngularity** (paquetes Nx en npm) | 26-ago-2025 | Malware postinstall que **usaba los CLI de Claude, Gemini y Amazon Q instalados por la víctima** para buscar secretos (al menos 4 variantes del prompt); subía lo robado a repos `s1ngularity-repository` | Credenciales robadas a escala; según CSA, esos tokens habilitaron Shai-Hulud | https://socket.dev/blog/nx-packages-compromised [P-investigador]; https://www.okta.com/blog/threat-intelligence/the-s1ngularity-attack--when-attackers-prompt-your-ai-agents-to/ [P] |
| **Shai-Hulud** (gusano npm) y 2.0 | sep-2025 / fines de 2025 | Gusano autorreplicante en npm | 526 paquetes según InfoQ; >187 según Trend Micro (las fuentes no coinciden) | https://www.infoq.com/news/2025/10/npm-s1ngularity-shai-hulud [S]; https://www.trendmicro.com/en_us/research/25/j/weaponized-ai-assistants.html [P] |
| "Mini Shai-Hulud" (TeamPCP) | 2026 | Según CSA, el primer ataque a la cadena de suministro que usa configuraciones de agentes de código para persistir | sin dato | https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/09/CSA_research_note_shai-hulud-ai-coding-assistant_20260918-csa-styled.pdf [P] |
| **postmark-mcp**: primer servidor MCP malicioso conocido en la práctica | 17-sep-2025 (v1.0.16) | Copia del MCP legítimo con una línea extra que mandaba en BCC cada correo al atacante | 1.643 descargas en total (~1.500/semana) | https://snyk.io/blog/malicious-mcp-server-on-npm-postmark-mcp-harvests-emails [P-investigador]; https://www.theregister.com/2025/09/29/postmark_mcp_server_code_hijacked/ [S] |
| **Extensión Amazon Q Developer** (VS Code) | 13–17-jul-2025 | Prompt "wiper" inyectado en la v1.84.0 mediante un token de GitHub con permisos mal acotados; AWS dice que no llegó a ejecutarse por errores de formato | ~950–964 mil instalaciones expuestas (según prensa) | Boletín AWS: https://aws.amazon.com/security/security-bulletins/AWS-2025-015/ [P]; https://www.techrepublic.com/article/news-amazon-q-data-wiping-prompt-security-hack/ [S] |
| **ClawHavoc** (skills maliciosas en ClawHub/OpenClaw) | ene–feb-2026 | Koi auditó 2.857 skills: 341 maliciosas (335 de una sola campaña). Más tarde se reportaron 1.184 (677 de un solo actor) | Robo de cripto y credenciales; US$: sin dato | https://unit42.paloaltonetworks.com/openclaw-ai-supply-chain/ [P]; https://blog.virustotal.com/2026/02/from-automation-to-infection-how.html [P]; 1.184: https://cybersecuritynews.com/openclaws-top-skill-malware/ [S, cautela] |

### E. Ciberataques orquestados con IA
| Incidente | Fecha | Qué pasó | Daño | Fuente |
|---|---|---|---|---|
| **GTG-1002** (estatal chino, según Anthropic) | Detectado mediados sep-2025; publicado 13-nov-2025 | Claude Code + MCP como motor de intrusión autónomo; la IA hizo ~80–90% del trabajo táctico; ~30 objetivos (tecnológicas, finanzas, química, gobierno) | Éxito "en un pequeño número de casos"; US$: **sin dato**. Hubo escepticismo en la industria | https://assets.anthropic.com/m/ec212e6566a0d47/original/Disrupting-the-first-reported-AI-orchestrated-cyber-espionage-campaign.pdf [P]; MITRE ATT&CK C0062: https://attack.mitre.org/campaigns/C0062/ [P]; https://www.bleepingcomputer.com/news/security/anthropic-claims-of-claude-ai-automated-cyberattacks-met-with-doubt/ [S] |
| **PROMPTFLUX / PROMPTSTEAL** (Google GTIG) | 5-nov-2025 | Dropper en VBScript que pide a Gemini que reescriba su propio código cada hora para evadir detección (experimental); APT28 usó PROMPTSTEAL en Ucrania | PROMPTFLUX no tenía capacidad de comprometer víctimas; sin US$ | https://cloud.google.com/blog/topics/threat-intelligence/threat-actor-usage-of-ai-tools [P]; actualizaciones 12-feb-2026 y 11-may-2026: https://cloud.google.com/blog/topics/threat-intelligence/distillation-experimentation-integration-ai-adversarial-use [P] |
| OpenAI, "Disrupting malicious uses of AI" | 7-oct-2025 | >40 redes desarticuladas desde feb-2024; los actores usan la IA para ir más rápido con tácticas existentes, no para ganar capacidades nuevas | sin dato | https://openai.com/global-affairs/disrupting-malicious-uses-of-ai-october-2025/ [P] |

### F. Fraude con deepfakes e IA
| Dato | Cifra | Fuente | Tipo |
|---|---|---|---|
| **Arup** (Hong Kong): videollamada con un CFO y colegas falsos | HK$200 M ≈ **US$25,6 M** en 15 transferencias (ene-2024; confirmado may-2024) | https://scmp.com/news/hong-kong/law-and-crime/article/3263151/uk-multinational-arup-confirmed-victim-hk200-million-deepfake-scam-used-digital-version-cfo-dupe | [S] con confirmación de Arup |
| Pérdidas documentadas por deepfakes en 2025 (Resemble AI) | **>US$1,28 mil millones**; 1.567 incidentes verificados; fraude corporativo: 41 incidentes, US$74,9 M, máximo US$35 M | https://resemble.ai/resources/2025-deepfake-threat-report | [P] (vendor) |
| Q1-2025 / Q2-2025 (Resemble) | US$200 M / US$347 M (487 incidentes) | https://www.resemble.ai/resources/q2-2025-ai-deepfake-security-report | [P] (vendor) |
| Pérdidas acumuladas por deepfakes (Surfshark, con datos de AIID + Resemble) | US$1,56 mil millones (>US$1.000 M en 2025); actualización jul-2026: **US$3,7 mil millones** acumulados; 57% en estafas de inversión | https://surfshark.com/research/chart/deepfake-fraud-losses | [S] (agregador) |
| Proyección Deloitte | Fraude habilitado por GenAI en EE.UU.: US$12,3 mil millones (2023) → **US$40 mil millones (2027)**, CAGR 32% | https://www.deloitte.com/us/en/insights/industry/financial-services/deepfake-banking-fraud-risk-on-the-rise.html (2024) | [P] (proyección, no pérdida medida) |
| FBI IC3 2025: fraude con IA | 22.364 denuncias, >US$893 M | ver §1 | [S] |
| Sumsub 2025–26: "fraude sofisticado" | +180% global | https://sumsub.com/newsroom/sumsubs-annual-report-fraud-shifts-to-complex-multi-step-schemes-in-2025-agentic-ai-scams-poised-to-surge-in-2026/ (25-nov-2025) | [P] (vendor) |

### G. Fraude con IA en Chile, Brasil y México
| País | Dato | Fuente | Tipo |
|---|---|---|---|
| LatAm | Ataques con deepfakes **+201%** de media (2025) | Sumsub, 6-abr-2026 — https://sumsub.com/blog/guides-reports/fraude-de-identidad-en-latinoamerica-2025-2026/ | [P] (vendor) |
| LatAm | Fraude de identidad +13,3% (2025) | https://sumsub.com/identity-fraud-report-2025 | [P] (vendor) |
| **México** | Deepfakes **~+500% interanual** (el mayor aumento de la región); la prensa cita +484% | Sumsub (misma URL); https://www.itsitio.com/mx/seguridad/ia-impulsa-una-nueva-ola-de-deepfakes-en-mexico-con-un-repunte-historico-de-484/ | [P] / [S] |
| **Brasil** | Deepfakes **+822%** (T1-2023 → T1-2024); intentos de fraude de identidad +51,5%; en T1-2025, tasa de deepfakes 5× la de EE.UU. y 10× la de Alemania | Sumsub vía https://tiinside.com.br/en/29/07/2025/deepfake-frauds-grow-by-822/ | [S] |
| Brasil | Fraudes con deepfakes +126% en 2025 | https://canaltech.com.br/seguranca/relatorio-indica-aumento-de-126-nas-fraudes-com-deepfakes-no-brasil-em-2025/ | [S] (no verifiqué el informe de origen) |
| **Chile** | Pérdidas por fraude con IA: **sin dato** cuantitativo específico. La PDI recomendó una "clave familiar" contra la voz clonada (ago-2025); proyecto de ley para multar estafas con IA (multas >$700 M CLP) avanzó en la Cámara (jul-2026); estafas por WhatsApp con voces de familiares clonadas (nov-2026) | https://www.theclinic.cl/2025/08/10/clave-de-confianza-familiar-la-recomendacion-de-la-pdi-ante-aumento-de-estafas-telefonicas-y-clonacion-de-voz-mediante-ia/amp/ ; https://www.t13.cl/noticia/nacional/mas-700-millones-avanza-proyecto-busca-multar-quienes-usen-ia-para-estafar-25-7-2026 ; https://www.meganoticias.cl/nacional/536708-estafa-whatsapp-ia-clona-voces-familiares-pide-transferencias-18-11-2026.html | [S] |
| Chile | TransUnion publicó un informe de fraude para Chile del H1-2026 (no extraje cifras) | https://chile.transunion.com/content/dam/transunion/chile/business/collateral/report/chile-h1-2026-top-fraud-trends-report.pdf | [P] sin leer |

### H. Daños psicológicos y legales de chatbots
| Caso | Fecha | Daño | Fuente |
|---|---|---|---|
| **Raine v. OpenAI** (S.F. Superior Court): muerte de Adam Raine, 16 años; la demanda dice que ChatGPT mencionó el suicidio 1.275 veces y que los sistemas de OpenAI marcaron más de 200 menciones sin cortar la conversación | Presentada 26-ago-2025 | Muerte; acusaciones no probadas | https://www.nbcnews.com/tech/tech-news/family-teenager-died-suicide-alleges-openais-chatgpt-blame-rcna226147 [S]; https://news.bloomberglaw.com/tech-and-telecom-law/openai-hit-with-suit-from-family-of-teen-who-died-by-suicide [S] |
| **Character.AI + Google**: acuerdo en 5 casos (FL, CO, NY, TX), incluido Garcia/Setzer | 7–8-ene-2026 | Montos confidenciales (**sin dato**). Desde oct-2025, Character.AI prohíbe a menores de 18 los chats abiertos | https://www.axios.com/2026/01/07/google-character-ai-lawsuits-teen-suicides ; https://fortune.com/2026/01/08/google-character-ai-settle-lawsuits-teenage-child-suicides-chatbots/ [S] |
| Siete demandas adicionales contra OpenAI (nov-2025) | — | Recuerdo esta tanda de demandas, pero **no la verifiqué en esta sesión** | sin fuente |

---

## 3. Tabla resumen: tipo de falla × daño × tendencia × madurez de la defensa

| # | Tipo de falla | Incidentes ancla | Daño cuantificado | Frecuencia / tendencia | ¿Existe defensa comercial madura? |
|---|---|---|---|---|---|
| 1 | **Fraude con deepfakes / ingeniería social con IA** (voz, video, BEC) | Arup; IC3 2025; Resemble | **El mayor medido**: US$893 M (IC3, EE.UU., subconteo); US$1,28 mil M documentados en el mundo en 2025; caso único de US$25,6 M | LatAm +201%, México ~+500%, Brasil +822% (2023→24); Deloitte proyecta CAGR 32% | **Parcial.** El KYC/liveness en onboarding es maduro (Sumsub, Onfido, etc.). La detección en llamadas o videollamadas en vivo, en WhatsApp y en fraude a personas comunes es inmadura. Ver notas 07 y 08 |
| 2 | **Prompt injection en copilotos/agentes empresariales** | EchoLeak, ForcedLeak, GitHub MCP, Slack AI | Pérdidas públicas: **sin dato**. 13% de orgs con brecha de IA; 60% de esos incidentes con datos comprometidos (IBM) | Gartner: 9% → 25% de apps con incidentes recurrentes en 2028; OWASP #1 | **Baja-media.** Hay guardrails/firewalls (Lakera→Check Point ~US$300 M, Prompt Security→SentinelOne ~US$250 M, Protect AI→Palo Alto US$500–700 M; Forrester calcula >US$2 mil M en M&A — https://www.forrester.com/blogs/securing-ais-ma-feeding-frenzy-is-on). Pero Invariant muestra que los detectores no detectan inyecciones de arquitectura; las mitigaciones reales son de diseño (allowlists, separar la "trifecta letal") |
| 3 | **Navegadores agénticos / agentes con sesión del usuario** | Comet, CometJacking, Atlas | **sin dato** (sin pérdidas reportadas) | Adopción temprana y rápida; cada producto nuevo cae en semanas | **Muy baja.** Ni los propios vendors lo resuelven; Perplexity disputó los reportes |
| 4 | **Cadena de suministro de agentes** (paquetes que dan órdenes a CLIs de IA, MCP maliciosos, skills, extensiones) | s1ngularity, Shai-Hulud, postmark-mcp, Amazon Q, ClawHavoc | Credenciales a escala (526 paquetes en Shai-Hulud); ~950 mil instalaciones expuestas (Q); 341→1.184 skills maliciosas; US$: sin dato | Fuerte alza: de cero casos "en la práctica" (antes de 2025) a campañas con cientos de artefactos (2026) | **Baja.** El SCA de npm es maduro (Socket, Snyk), pero escanear instrucciones en lenguaje natural, skills y servidores MCP es incipiente (ClawHub recién sumó VirusTotal). Unit 42 encontró skills que lo evadían |
| 5 | **Agentes que destruyen datos** (exceso de permisos y autonomía) | Replit/SaaStr, Antigravity, Claude Code, Cursor | Bases de datos de producción y discos completos; US$: sin dato | Se repite en cada IDE agéntico; modos "YOLO/Turbo" lo agravan | **Baja-media.** Sandboxing, separar dev de prod y aprobar comandos existen como prácticas, no como producto estándar; ver nota 05 |
| 6 | **Ciberataques orquestados con IA** | GTG-1002, PROMPTFLUX, reportes de OpenAI | ~30 objetivos, algunos éxitos; US$: sin dato | Sube rápido (Anthropic, GTIG y OpenAI publican reportes trimestrales) | **Media.** Defensas tradicionales (EDR, SOC) más el monitoreo de abuso que hace el proveedor del modelo; nada específico para víctimas |
| 7 | **Shadow AI / fuga de datos a herramientas de IA** | IBM, DBIR | +US$670 mil por brecha; ~20% de orgs | Uso 15% → 45% (DBIR) | **Alta.** DLP/CASB/SSE y vendors de AI-DLP; ver nota 12 |
| 8 | **Daño psicológico de chatbots** (suicidio, dependencia, menores) | Raine, Character.AI | Muertes; acuerdos confidenciales; US$: sin dato | Más demandas y regulación (estatal en EE.UU.) | **Baja.** Clasificadores de crisis y verificación de edad propios de cada lab; casi no hay oferta B2B independiente de evals o monitoreo |

---

## 4. Ranking: (daño × crecimiento) ÷ madurez de la defensa

Escala 1–5 (5 = máximo). El "daño" pondera el daño realizado y medido (US$, vidas, datos), con un pequeño ajuste por severidad demostrada (CVSS crítico). La madurez es 5 = solución comercial estándar y eficaz.

| Tipo de falla | Daño | Crecimiento | Madurez defensa | Puntaje |
|---|---|---|---|---|
| 8. Daño psicológico de chatbots | 4 | 4 | 1,5 | **10,7** |
| 4. Cadena de suministro de agentes | 4 | 5 | 2 | **10,0** |
| 1. Fraude deepfake / voz clonada (fuera del onboarding KYC) | 5 | 5 | 2,5 | **10,0** |
| 3. Navegadores agénticos | 2 | 5 | 1 | **10,0** |
| 2. Prompt injection en copilotos empresariales | 3 | 5 | 2 | **7,5** |
| 6. Ciberataques orquestados con IA | 3 | 5 | 3 | 5,0 |
| 5. Agentes que destruyen datos | 3 | 4 | 2,5 | 4,8 |
| 7. Shadow AI / fuga de datos | 4 | 4 | 4 | 4,0 |

> Advertencia: los puntajes son juicio del equipo sobre datos heterogéneos y no métricas. Con daño en US$ casi siempre "sin dato" fuera del fraude, el ranking es sensible a ±1 punto.

### Los 5 con mayor brecha entre daño y solución disponible

1. **Daño psicológico de chatbots (10,7).** Es el único tipo con muertes atribuidas y litigios activos (Raine; acuerdo de Character.AI y Google, ene-2026). La defensa vive dentro de cada lab y casi no existe un mercado de evals o monitoreo independientes para quienes despliegan chatbots (apps de compañía, edtech, salud). Encaja con el track de AI Safety.
2. **Cadena de suministro de agentes (10,0).** En 18 meses pasó de cero a gusanos npm que *ordenan* a los CLIs de IA robar secretos, a MCP maliciosos y a más de mil skills maliciosas. Las herramientas SCA no leen "intención en lenguaje natural". Es la categoría con mejor relación entre evidencia real y falta de producto.
3. **Fraude con deepfakes y voz clonada en canales en vivo (10,0).** Concentra el **mayor daño medido** (cientos de millones a miles de millones de US$) y crece de forma explosiva en LatAm (México ~+500%, Brasil, alertas de la PDI en Chile). El KYC está resuelto; la llamada de "tu hijo" por WhatsApp o la videollamada del "CFO", no. Chile no tiene datos públicos: también es un hueco de medición.
4. **Navegadores agénticos (10,0).** Hoy el daño es bajo, pero la madurez de la defensa es mínima: los propios vendors no logran mitigarlo. Es una apuesta a futuro: el daño escala con la adopción.
5. **Prompt injection en copilotos y agentes empresariales (7,5).** Varias fallas CVSS 9+ en Microsoft, Salesforce y GitHub en un año, y IBM ya ve un 13% de organizaciones con brechas de IA. Hay mucho capital (>US$2 mil M en M&A), pero los detectores fallan ante inyecciones de arquitectura. La brecha está en el **control determinista del flujo de datos** (taint tracking, romper la trifecta letal), no en otro clasificador.

**Conclusión para el equipo:** si "más grande" significa *daño en dólares hoy*, el problema es el **fraude con deepfakes y voz clonada**, con LatAm como zona de mayor crecimiento y menos medición. Si significa *mayor brecha entre daño creciente y solución*, los mares azules son **la cadena de suministro de agentes** (skills, MCP, paquetes con prompts) y **la seguridad de chatbots para usuarios vulnerables**. Las dos tienen incidentes reales y documentados de 2025–2026 y casi ningún producto dedicado.

---

### Vacíos de datos (honestos)
- Pérdidas en US$ por prompt injection o por agentes: **ninguna pública** en 2025–2026.
- Chile: sin cifras oficiales de fraude atribuible a IA (habría que pedirlas a PDI, Fiscalía o CMF).
- Las cifras de Sumsub y Resemble vienen de vendors con incentivo comercial, y sus metodologías no son comparables entre sí.
- No abrí los PDF primarios de FBI IC3 2025, Verizon DBIR 2026 ni Stanford AI Index 2026: sus cifras vienen de cobertura de prensa o de resúmenes.
- No verifiqué en esta sesión el caso Atlas ni la tanda de siete demandas contra OpenAI de nov-2025.
