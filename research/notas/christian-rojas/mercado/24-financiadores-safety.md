# 24 — Ecosistema que financia AI safety (no ciberseguridad genérica)

Fecha del research: 21-nov-2026. Fuentes priorizadas 2025–2026. Cada dato lleva su URL; donde no encontré fuente escribo "sin dato".

**Límites de este research.** Se agotó el cupo de búsquedas web antes de cubrir todo. Las páginas de Coefficient Giving (coefficientgiving.org), jaan.info y f4.fund devolvieron 403, y algunas páginas del EA Forum devolvieron 429. Algunas cifras vienen de resúmenes del buscador y no de la página original; esas van marcadas como "(vía buscador, no verificado en la fuente)".

---

## 1. Panorama rápido

- **El dinero de capital de riesgo en safety ya no es marginal.** Goodfire (interpretabilidad) levantó una Serie B de US$150M con valuación de US$1,25B en feb-2026, liderada por B Capital. Fuentes: https://siliconangle.com/2026/02/05/goodfire-raises-150m-funding-enhance-ai-interpretability-platform/ y https://www.bloomberg.com/news/articles/2026-02-05/startup-goodfire-notches-1-25-billion-valuation-to-decode-ai-models
- **Hay muchos fondos chicos dedicados.** La wiki "AI Safety & Entrepreneurship" de LessWrong lista Lionheart, Juniper, Polaris, Mythos, Metaplanet, Anthology Fund, Menlo, Babuschkin Ventures, Safe AI Fund, Shift Grants y la AI Safety Seed Funding Network: https://www.lesswrong.com/w/ai-safety-and-entrepreneurship
- **La filantropía crece.** SFF recomendó US$34,92M en 2025 y US$63,64M en 2026, muy por encima de su propia estimación: https://survivalandflourishing.fund/
- **Los gobiernos ya financian.** La Alignment Project del UK AISI suma £27M (https://www.aisi.gov.uk/blog/funding-60-projects-to-advance-ai-alignment-research). Safeguarded AI de ARIA tiene £59M (https://www.aria.org.uk/safeguarded-ai/).
- **Hay un dato de mercado sin verificar.** Un análisis secundario afirma que el "mercado de AI safety" levantó unos US$439M en 9 rondas hasta mayo-2026, contra unos US$96M en 4 rondas en el mismo período de 2025 (vía buscador, no verificado): https://newmarketpitch.com/blogs/news/ai-safety-funding-trends
- **Patrón general.** Los financiadores convergen en pocos temas:
  - monitoreo y control de agentes en producción;
  - auditoría y certificación independiente (incluido seguro);
  - verificación (hardware, formal, de acuerdos);
  - detección temprana de incidentes y misuse;
  - interpretabilidad aplicada.

---

## 2. Inversores con fines de lucro

### Halcyon Futures / Halcyon Ventures
- **Modelo:** híbrido. Halcyon Futures es la nonprofit/incubadora y Halcyon Ventures el fondo. Fundada en 2023 por Mike McCormick (vía buscador): https://f4.fund/firms/halcyon-futures
- **Portfolio (vía buscador, no verificado en la fuente):**
  - nombrados: Goodfire, Transluce, Fathom, Andon Labs, Archia, Red Queen Bio, DepthFirst, Gray Swan, Confident Security y Hadrian;
  - Workshop Labs, ex-portfolio, fue adquirida por Thinking Machines;
  - fuentes: https://f4.fund/firms/halcyon-futures y https://grantedai.com/grants/halcyon-futures-ai-safety-incubation-seed-funding-program-halcyon-c1d2e3f4
- **2025–2026:** según F4, AIUC (certificación y seguro de agentes) levantó una Serie A de US$40M en sep-2026, liderada por Ribbit Capital y First Harmonic (vía buscador; f4.fund dio 403, no verificado).
- **Otro rol:** es socio fundador de la coalición de la Alignment Project del UK AISI: https://www.aisi.gov.uk/blog/funding-60-projects-to-advance-ai-alignment-research
- **RFP o lista de problemas:** sin dato público. El stream de MATS de Halcyon menciona interpretabilidad, scalable oversight y AI control: https://matsprogram.org/stream/halcyon

### Juniper Ventures
- **Tesis:** fondo exclusivo de "AI assurance". Tickets de US$1M a US$100M. Categorías: energía, hardware, compute, seguridad, auditorías, datos, evals, interpretabilidad, inferencia, guardrails, observabilidad, autenticación, agentes, compliance, seguros y policy: https://juniper.xyz/
- **Portfolio:**
  - investigación de safety y alignment: Goodfire, Apollo Research, Recurrent Research (data poisoning y red-teaming), Softmax, Humanis;
  - verificación y confianza: Lucid Computing, Alien (proof of humanity), AIUC;
  - seguridad y forense: Gray Swan, Asymmetric Security (forense y respuesta a incidentes de IA);
  - evaluación: Kradle, Modaic, Musubi Labs, FutureSearch;
  - otros: Axiom Math;
  - exits: Haize Labs, adquirida por Beacon, y Workshop Labs, adquirida por Thinking Machines;
  - fuente: https://juniper.xyz/
- **2025–2026:**
  - Fund II anunciado el 20-may-2026, con un compromiso de US$2,5M de DNV Ventures; el tamaño total del fondo es sin dato;
  - primeras tres inversiones del Fund II: Apollo Research, Alien Labs y Workshop Labs;
  - fuente: https://www.dnv.com/news/2026/juniper-fund2/
- **Lista de problemas:**
  - publica el "AI Assurance Technology Report", que proyecta un mercado de AIAT de US$276B al 2030 y lo divide en Safeguarding, Auditing, Governing y Verifying;
  - el mapa del reporte muestra 100 startups, 82 de ellas en seed o early stage;
  - el reporte parece de 2024: https://aiat.report/

### Lionheart Ventures
- **Tesis:** "wise development of transformative technologies". Invierte en IA que defiende la agencia y resiliencia humana, y en salud mental de frontera: https://www.lionheart.vc/
- **Portfolio e inversiones 2025–2026:** sin dato. La página de inversiones no cargó.
- **RFP:** sin dato.

### Mythos Ventures
- **Tesis:** pre-seed y seed, tickets de US$500k a US$2M, "prosocial technologies for the transformative AI era", equipos cuya estrategia escale a un mundo post-AGI: https://www.mythos.vc/
- **Portfolio e inversiones 2025–2026:** sin dato.
- **RFP:** sin dato.

### Safe Artificial Intelligence Fund (SAIF, Geoff Ralston)
- **Lanzamiento:** abril de 2025, por el expresidente de YC. Tickets iniciales de US$100k vía SAFE con cap de US$10M, más mentoría y coaching para YC: https://techcrunch.com/2025/04/17/former-y-combinator-president-geoff-ralston-launches-new-ai-safety-fund
- **Portfolio declarado (26 entradas):** https://www.saif.vc/
  - **agentes:** AgentHub (simulación y evaluación), Apollo Research (monitoreo), Archia, AIUC (certificación y seguro), Astha AI (zero-trust para agentes), Fabraix (verificación adversarial), General Analysis (monitoreo de seguridad), Mission Control AI;
  - **seguridad:** Asymmetric Security (forense de IA), Chimera Cybersecurity, Confident Security (inferencia privada), Ulyssean (data centers seguros), Lucid Computing;
  - **interpretabilidad:** Goodfire, Freestyle Research;
  - **verificación formal:** Theorem (verificación de programas);
  - **identidad:** Soliton (proof of human), SureMark Digital (deepfakes);
  - **otros:** CTGT, Futuresearch, NewsGuard, Paper Instruments, Pumpkinseed, Locunity;
  - **fondos:** también invierte en Halcyon Futures y Juniper Ventures.
- **Montos por empresa:** sin dato.
- **Otro rol:** es socio de la Alignment Project del UK AISI (ver la sección 3).

### Metaplanet (Jaan Tallinn)
- **Tesis:** invierte en deep tech y también da grants, incluidos grants sobre riesgo existencial de IA: https://www.lesswrong.com/w/ai-safety-and-entrepreneurship
- **Inversiones 2025–2026:** sin dato. Mi intento de leer jaan.info dio 403.

### Fifty Years (programa 5050 AI)
- **Términos:** gratis, sin equity. Cohorte de San Francisco abr–jul 2026 y cohorte de Londres mar–jun 2026, esta última en alianza con ARIA: https://www.fiftyyears.com/5050/ai
- **Request for Startups (5050 AI):**
  - evaluación, testing y red-teaming de seguridad;
  - plataformas de interpretabilidad para sectores regulados;
  - infraestructura de alignment para developers;
  - gobernanza y compliance;
  - colaboración humano-IA en decisiones críticas;
  - robustez frente a ataques adversariales y distribution shift;
  - bioseguridad y prevención de uso dual;
  - ciberseguridad potenciada con IA.
- **Próxima cohorte 5050:** abril de 2027: https://www.fiftyyears.com/

### Anthology Fund (Menlo Ventures + Anthropic)
- **Términos:** US$100M, desde US$100k, de pre-seed a Serie A: https://menlovc.com/anthology-fund/
- **Foco relevante:** una de sus 5 áreas es "trust and safety tooling" ubicada "at or above the model layer".
- **Inversiones safety 2025–2026:** sin dato en la página.
- **Relacionado:** Menlo lideró la Serie A de US$50M de Goodfire: https://menlovc.com/perspective/leading-goodfires-50m-series-a-to-interpret-how-ai-models-think/

### Entrepreneur First — def/acc
- **Origen:** cohorte en Londres anunciada en mayo de 2024 por Matt Clifford, sobre tecnología defensiva contra pandemias, cibercrimen, IA poderosa y guerra nuclear.
- **Cohorte posterior:** hasta US$350k en créditos de Azure por startup: https://www.microsoft.com/en-us/startups/blog/?p=1999 y https://www.joinef.com/?p=8149
- **Advertencia:** un post del EA Forum señala que no todas las startups de la cohorte son de safety: https://forum.effectivealtruism.org/posts/t5iWspQueSyQDHNwo/hacking-away-at-p-doom
- **Estado 2026 y empresas financiadas:** sin dato.

### Seldon Lab
- **Qué es:** aceleradora de "AI/AGI security" en San Francisco, fundada a comienzos de 2025 por Esben Kran y Finn Metz: https://seldonlab.com/ y https://scet.berkeley.edu/meet-finn-metz-the-founder-tackling-ai-safety/
- **Batch 1:**
  - empresas nombradas: Lucid Computing (CEO Kristian Rönn) y Andon Labs (https://seldonlab.com/);
  - según el buscador, el batch levantó US$1,3M y menciona a Asymmetric Security y Workshop Labs (no verificado: https://www.longtermwiki.com/knowledge-base/organizations/safety-orgs/seldon-lab).
- **Batch 2:**
  - Demo Day el 20-abr-2026 (https://seldonlab.com/);
  - temas: ciberdefensa autónoma para infraestructura crítica, nuevos paradigmas de AI control y observabilidad;
  - equipos citados por el buscador: 0labs.ai, weavemind.ai, gutenberg.ai y luthienresearch.org (no verificado: https://luma.com/qtpr2opi).
- **Términos de inversión:** sin dato.

### Catalyze Impact (incubadora)
- **Cohorte invierno 2024/25** (post del 10-mar-2025): https://lesswrong.com/posts/LLJm97gLDacn8AscB/introducing-11-new-ai-safety-organizations-catalyze-s-winter
  - Wiser Human: límites del AI control. US$400k.
  - Una startup en stealth: agentes que automatizan investigación de safety. PBC, US$400k.
  - TamperSec: hardware anti-manipulación para chips de IA. Hasta US$1,5M de inversión más US$500k para transparencia.
  - Netholabs: emulación cerebral.
  - More Light: protección de whistleblowers de labs. Unos US$700k.
  - Lyra Research: automatización de investigación de safety. US$100k.
  - Luthien: AI Control listo para producción, basado en el trabajo de Redwood. US$500k.
  - Live Theory: US$100–500k.
  - Anchor Research: evals de seguridad en operación de días o semanas. US$50–200k.
  - Aintelope: US$475k.
  - AI Leadership Collective: US$264k para un piloto.
- **Lista de "founding opportunities" (2026):** https://catalyze-impact.org/blog/ai-safety-resilience-founding-opportunities
  1. **Hacer rendir cuentas a las empresas de IA:** firmas de auditoría de modelos y agencias de rating.
  2. **Defenderse de misuse catastrófico:** alerta temprana de patógenos y testing de safeguards en pedidos de ADN.
  3. **Mantener el poder en jaque:** watchdog de IA en gobierno y auditorías de quién puede dirigir una IA.
  4. **Hacer verificables los acuerdos sobre IA:** verificación embebida en chips y toolkit para verificar tratados.
  5. **Detectar incidentes de IA temprano:** detección de ataques impulsados por IA e investigación de reportes de misuse.

### AE Studio
- **Qué hace:** agenda de "neglected approaches" en alignment:
  - pretraining alignment, incluido GRAM con Anthropic, que aísla conocimiento peligroso en módulos que se activan o desactivan;
  - alignment inspirado en neurociencia (self-other overlap);
  - investigación empírica sobre conciencia;
  - policy;
  - fuente: https://www.ae.studio/alignment
- **Papers 2026:** "Modular Pretraining Enables Access Control" (jun-2026) y "Endogenous Steering Resistance" (ene-2026).
- **Inversión en startups:** la página no menciona inversiones. La wiki de LessWrong dice que expresó interés en sembrar ideas de negocio "neglected": https://www.lesswrong.com/w/ai-safety-and-entrepreneurship

### Ángeles: Jaan Tallinn
- **Vía SFF:** canaliza grants a través de SFF; por ejemplo, US$1.305.000 a AI Futures Project en 2026: https://survivalandflourishing.fund/
- **ISPA Inspection Prize:**
  - premio de US$5M–20M de Survival and Flourishing Corp por iniciar inspecciones "Independently Supervised Peer-Assisted" entre labs de frontera;
  - Tallinn pone al menos US$5M, más otros US$5M en matching 1:2;
  - fuente: https://survivalandflourishing.fund/
- **Prioridades declaradas (jaan.info):** sin dato (403).

---

## 3. Filántropos y gobiernos

### Open Philanthropy → Coefficient Giving
- **RFP Technical AI Safety (2025):**
  - US$40M o más; cerró el 15-abr-2025;
  - 21 direcciones de investigación en 5 clusters: https://www.alignmentforum.org/posts/26SHhxK2yYQbh7ors
  - **Adversarial ML:** jailbreaks y misalignment no intencional\*, control evaluations\*, backdoors y stress tests de alignment\*, alternativas a adversarial training\*, robust unlearning.
  - **Mal comportamiento sofisticado:** experimentos de alignment faking\*, razonamiento codificado en CoT y comunicación entre modelos\*, psicología black-box de LLMs, capacidad de ocultar comportamientos peligrosos, reward hacking de la supervisión humana.
  - **Transparencia:** aplicaciones de técnicas white-box\*, activation monitoring, representaciones de features, toy models, benchmarks de interpretabilidad, razonamiento externalizado, arquitecturas más transparentes.
  - **Confianza desde primeros principios:** estimación white-box de mal comportamiento raro\*, inductive biases.
  - **Alternativas:** claridad conceptual y moonshots para alinear superinteligencia.
  - (\*) = áreas prioritarias.
- **Gobernanza:** RFP de AI Governance cerrado el 25-ene-2026 (vía buscador): https://www.effectivealtruism.org/opportunities/recTVSiPgDoRHKJrz
- **RFP técnico 2026:** sin dato (coefficientgiving.org dio 403).
- **Lista personal de "proyectos que me gustaría que existan":** "Ten AI safety projects I'd like people to work on", de Julian Hazell (Open Phil, a título personal), 23-jul-2025: https://www.lesswrong.com/posts/vxA2BnCPTaPfnJjti/ten-ai-safety-projects-i-d-like-people-to-work-on
  1. Formación de ingenieros de seguridad para asegurar sistemas de IA de frontera.
  2. Organización de investigación en technical AI governance.
  3. Rastrear comportamiento sospechoso de agentes "in the wild" con logs, honeypots y casos.
  4. Consultora de comunicación especializada en AI safety.
  5. Monitor de labs con scorecards.
  6. Revisiones de literatura de safety "vivas".
  7. Plan de resiliencia de US$10.000M listo para ejecutar.
  8. Herramientas de fact-checking con IA, auditables, como extensión de navegador o API.
  9. Auditores-IA: agentes que automatizan auditorías de compliance de labs.
  10. Tracker del impacto económico de la IA.

### Survival and Flourishing Fund (SFF)
- **Totales:** 2025: US$34,92M. 2026: US$63,64M en la Main Round, más tres rondas temáticas nuevas (temas: sin dato). Fuente: https://survivalandflourishing.fund/
- **Receptores 2026:** AI Futures Project (US$1,305M), METR (~US$2,2M), PauseAI Global (~US$1,5M), Palisade (~US$1,8M), Atlas Computing (~US$2,8M), CAIS, Epoch, Apollo y CLR.
- **Receptores 2025:** MIRI (US$1,607M), AI Futures Project (US$1,535M + US$0,5M), SecureDNA (US$1,5M), CAIS Action Fund (US$772k), FAR AI, Palisade, METR, Encode (US$516k) y MATS (US$289k).
- **Mecanismos:**
  - rolling application con Matching Pledges;
  - Speculation Grants;
  - ISPA Inspection Prize (ver Jaan Tallinn en la sección 2).

### Schmidt Sciences
- **AI Safety Science (2025):** 27 proyectos, unos US$10M en total: https://www.schmidtsciences.org/new-10-million-ai-safety-science-program-launched-for-foundational-research/
- **Expresión de interés sobre inference-time compute (abr-2025):** hasta US$500k: https://www.lesswrong.com/posts/sup9qzCrdjcAGyrxa/schmidt-sciences-request-for-proposals-on-the-science-of
- **RFP Science of Trustworthy AI (2026):**
  - Tier 1 hasta US$1M; Tier 2 de US$1M a US$5M;
  - deadline 17-may-2026;
  - fuente: https://www.effectivealtruism.org/opportunities/rechTkizyZ4wiBoXP
  - adjudicatarios: sin dato.
- **RFP multi-agent safety:** conjunto con Google DeepMind, ARIA, Cooperative AI Foundation y Google.org: https://www.cooperativeai.com/grants/multi-agent-safety (montos adjudicados: sin dato).

### UK AISI (AI Security Institute)
- **Alignment Project:**
  - £27M en total, incluidos £5,6M de OpenAI; 60 proyectos en la 1ª ronda (feb-2026) sobre más de 800 postulaciones;
  - grants de £50k a £1M;
  - ejemplos: Scientist AI de LawZero (Bengio), mecanismo e information design (Bergemann y Morris), Energy Conserving Descent (Stanford);
  - socios: CIFAR, Schmidt Sciences, AWS, Anthropic, Halcyon Futures, Safe AI Fund, UKRI, ARIA, OpenAI, Microsoft, Australian AISI, AI Safety Tactical Opportunities Fund, Sympatico Ventures y Renaissance Philanthropy;
  - fuente: https://www.aisi.gov.uk/blog/funding-60-projects-to-advance-ai-alignment-research
  - la 2ª ronda se esperaba para el verano boreal de 2026.
- **Challenge Fund:**
  - £5M, lanzado el 5-mar-2025, hasta £200k por proyecto;
  - temas: safeguards, control, alignment y resiliencia social;
  - cerró el 1-ago-2025;
  - fuentes: https://www.aisi.gov.uk/grants y https://gov.uk/government/news/cutting-edge-research-on-ai-security-bolstered-with-new-challenge-fund-to-ramp-up-public-trust-and-adoption
- **Systemic Safety Grants:** 20 proyectos en curso sobre resiliencia de salud, redes eléctricas y mercados.
- **Estado hoy:** la página de grants dice que no hay programas abiertos: https://www.aisi.gov.uk/grants

### ARIA — Safeguarded AI
- **Presupuesto:** £59M: https://www.aria.org.uk/safeguarded-ai/
- **Tesis actualizada (may-2026):**
  - TA1: un toolkit open-source de aseguramiento matemático para que agentes de IA produzcan artefactos verificados formalmente;
  - TA2: aplicarlo a ciberseguridad;
  - ejemplos de problemas: contener agentes de IA y proteger código en millones de dispositivos Android.
- **Financiado:** 8 proyectos de TA2 Cybersecurity con £22M combinados.
- **Llamado abierto (rolling) "Safeguarded AI: Cybersecurity":**
  - £20M con deadline 1-dic-2026 según el buscador;
  - £2M–3,5M por equipo, entre blue teams y un red team;
  - fuentes: https://aria.org.uk/funding-opportunities y https://iuk-business-connect.org.uk/opportunities/aria-safeguarded-ai-cybersecurity-rolling-call/
  - las fechas son contradictorias entre fuentes: verificar.
- **Cancelación:** el TA3 Phase 2 (ciberfísico) se canceló en feb-2026.

### Foresight Institute
- **RFP AI Safety (jun-2025):** unos US$5M al año, con deadlines trimestrales: https://www.lesswrong.com/posts/bSm678CPsSLdDQLEx/foresight-institute-ai-safety-rfps-in-automation-security
  1. **Automatizar investigación y forecasting:** agentes de investigación open-source y forecasting automático.
  2. **Tecnologías de seguridad:** descubrimiento de vulnerabilidades asistido por IA, verificación formal, arquitecturas demostrablemente seguras, criptografía de privacidad, compute descentralizado y auditable.
  3. **Escenarios multi-agente seguros:** IA para negociación y mediación, agentes de coordinación que negocian y hacen cumplir acuerdos.
  4. **Neurotecnología para safety.**
- **Ronda 2026 "AI for Science & Safety Nodes":**
  - US$10k–100k, más oficina y compute en San Francisco y Berlín;
  - temas: coordinación, accountability, empoderamiento humano, alignment descentralizado, seguros de IA y gobernanza abierta;
  - cerró el 31-oct-2026 (vía buscador): https://www2.fundsforngos.org/?p=493890

### Manifund
- **Qué es:** plataforma de crowdfunding y regranting.
- **Proyectos visibles:**
  - "Retroactive funding: agent-glovebox", con US$65,8k recaudados;
  - "How Far Do Instilled Values Generalise?", con US$10k;
  - "EvalScience", que busca US$50k;
  - fuente: https://manifund.org/
- **Presupuestos de regranting 2025–2026:** sin dato.

### LTFF (EA Funds)
- **Cierre del fondo:**
  - el LTFF cierra; de su saldo de unos US$3,7M, unos US$2,8M van a la primera ronda de Lightcone Commons, que prevé repartir US$15M–25M;
  - unos US$0,9M siembran el nuevo **Transformative AI Fund (TAIF)**: grants chicos a individuos y organizaciones tempranas, con postulación abierta y rolling;
  - fuente: https://forum-bots.effectivealtruism.org/posts/dtZ9wbKWjtvGWDRJx/closing-the-ltff-spending-down-funds-and-a-new-ai-fund-at-ea
  - el post dice "Aug 11" sin año visible; por contexto, probablemente 2026.
- **Motivo citado:** los grants a for-profits, a individuos y a trabajo cercano a policy generaban fricción legal para CEA.

---

## 4. Listas públicas útiles

- **Startups de AI safety con fines de lucro.** No existe una lista canónica. Las mejores aproximaciones:
  - los portfolios de SAIF (https://www.saif.vc/) y Juniper (https://juniper.xyz/);
  - la cohorte de Catalyze (link en la sección 2);
  - el mapa de 38 startups europeas de Sifted: https://sifted.eu/articles/ai-safety-startups-mapped-38-companies-building-europes-trust-layer/ (no lo pude leer);
  - "12 AI safety startups to watch": https://sifted.eu/articles/ai-safety-startups-to-watch
- **Listas de ideas:**
  - "List of lists of project ideas in AI safety": https://www.lesswrong.com/posts/mtGpdtDdmkRC3ZBuz/list-of-lists-of-project-ideas-in-ai-safety
  - "Some for-profit AI alignment org ideas": https://www.lesswrong.com/posts/PcTLHamp236afJxxT/some-for-profit-ai-alignment-org-ideas
  - "AI safety needs startups": https://www.lesswrong.com/posts/LH8QtTof7Q7CWmMLF/ai-safety-needs-startups
  - "The case for AGI safety products": https://www.lesswrong.com/posts/iwfdwzJerpC7FqbZG/the-case-for-agi-safety-products
  - "Probably good projects for the AI safety ecosystem": https://www.lesswrong.com/posts/v5z6rDuFPKM5dLpz8/probably-good-projects-for-the-ai-safety-ecosystem
  - (no leí estos posts, solo vi su título en los resultados)
- **Señal de mercado sin verificar:** artículo de Puck (sep-2026), "How the Hugging Face attack sparked an AI safety rush". Solo vi el título; el contenido es sin dato: https://puck.news/ai/2026/9/how-the-hugging-face-attack-sparked-an-ai-safety-rush

---

## 5. Tabla: problema pedido → ¿ya existe? → ¿prototipable en 10–12 h?

| # | Problema pedido por financiadores (fuente) | ¿Existe empresa o proyecto? | ¿Prototipo en 10–12 h? |
|---|---|---|---|
| 1 | Rastrear comportamiento sospechoso o engañoso de agentes desplegados "in the wild", con logs y honeypots (Hazell #3; Catalyze "detectar incidentes temprano") | Parcial. Monitoreo: Apollo Research, General Analysis. Forense post-incidente: Asymmetric Security. No vi un "observatorio público" de agentes | **Sí.** Honeypot (sitio, repo o MCP falso) que registre y clasifique a los agentes que lo visitan, más un dashboard |
| 2 | AI control en producción: monitor o proxy entre el agente y sus herramientas (OP RFP "control evaluations"; Seldon Batch 2; Catalyze → Luthien) | Sí, temprano: Luthien (nonprofit), Fabraix, Astha AI | **Sí.** Proxy que intercepte las tool calls de un agente de código y aplique un monitor LLM y una política |
| 3 | Monitoreo de razonamiento codificado y CoT (OP RFP: encoded reasoning, activation monitoring) | Mayormente investigación académica y de labs; no vi un producto | **Parcial.** Demo de un monitor de CoT con un set de esteganografía sintético; difícil de validar en 12 h |
| 4 | Auditores-IA: agentes que automatizan auditorías de compliance (Hazell #9; Catalyze "audit firm"; Juniper "audits") | Sí, el adyacente AIUC (certificación y seguro). No vi un auditor automatizado de *labs* | **Sí.** Agente que contraste la política publicada de un lab o proveedor con su comportamiento observado y genere un reporte |
| 5 | Monitor de labs o agencia de rating con scorecards (Hazell #5; Catalyze "ratings agency") | Probablemente existen esfuerzos nonprofit (no verificado aquí) | **Sí.** Scorecard automatizado desde documentos públicos, aunque con poco "mar azul" |
| 6 | Verificación de acuerdos y chips: inspecciones ISPA entre labs, verificación en hardware (SFF ISPA Prize; Catalyze #4; Foresight) | Hardware: TamperSec, Lucid Computing. ISPA como servicio: no vi ninguno | **No** en hardware. **Parcial** como prototipo de protocolo o atestación por software |
| 7 | Verificación formal de código generado por IA (ARIA Safeguarded AI; Foresight; Anthology) | Sí: Theorem (SAIF), Axiom Math (Juniper), los equipos TA1 y TA2 de ARIA | **Parcial.** Pipeline LLM → Dafny/Lean para funciones chicas; demo acotada |
| 8 | Ciberdefensa autónoma con IA para infraestructura crítica (Seldon Batch 2; ARIA Cybersecurity; 5050 AI) | Sí: varios equipos de Seldon y ARIA; categoría poblada | **Parcial.** Demo en un entorno simulado (CTF o ICS de juguete) |
| 9 | Fact-checking con IA, transparente y auditable (Hazell #8) | Sí: NewsGuard (portfolio de SAIF), otros | **Sí.** Extensión de navegador con fuentes trazables; poco diferenciado |
| 10 | Identidad de agentes y proof of human (Juniper; SAIF) | Sí: Alien, Soliton, SureMark | Sí, pero mercado saturado |
| 11 | Defensa contra misuse biológico, screening de ADN (Catalyze #2; 5050 AI; SFF) | Sí: SecureDNA (SFF 2025) | **No** (requiere dominio y datos) |
| 12 | Negociación, mediación y coordinación multi-agente segura (Foresight 2025–2026; RFP multi-agent de Schmidt, DeepMind y ARIA) | Pocos productos; mayormente investigación | **Sí.** Agente mediador más un benchmark de "colusión vs. cooperación" entre agentes |
| 13 | Seguros y riesgo de agentes (Foresight 2026 "AI insurance"; Juniper "insurance") | Sí: AIUC (Serie A reportada de US$40M, no verificada) | **Parcial.** Scoring de riesgo de un agente a partir de evals |
| 14 | Evals de seguridad en horizontes largos, de días o semanas (Catalyze → Anchor Research) | Temprano: Anchor Research (nonprofit) | **Parcial.** Arnés con tareas largas simuladas; 12 h no alcanzan para correr días |
| 15 | Watchdog del uso de IA en gobierno / concentración de poder (Catalyze #3) | No vi empresas | **Sí.** Tracker de compras públicas de IA y de su uso en decisiones estatales (aplicable a LATAM) |
| 16 | Revisiones de literatura de safety vivas (Hazell #6) | No vi un producto | **Sí.** Pipeline de agentes que actualice una síntesis desde arXiv; bajo valor comercial |
| 17 | Tracker del impacto económico de la IA (Hazell #10) | Esfuerzos tipo Epoch (no verificado) | **Sí**, como dashboard, aunque tangencial a seguridad |
| 18 | Data poisoning y red-teaming de datos (Juniper → Recurrent Research) | Sí: Recurrent Research | **Parcial.** Detector de envenenamiento en un dataset de fine-tuning |

**Lectura para la hackathon.** Las filas 1, 2, 4, 12 y 15 tienen tres cosas a la vez: pedido explícito de financiadores, pocas empresas o solo nonprofits, y un demo creíble en 12 horas. La fila 1 es la más alineada con lo que piden simultáneamente Open Phil/Coefficient Giving, Catalyze y Seldon.
