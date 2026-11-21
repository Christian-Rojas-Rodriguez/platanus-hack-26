# 27 — Responsabilidad, seguros y evidencia de acciones de agentes de IA

Fecha: 21-nov-2026. Ideas que se evalúan: **"mandato + recibo"** y **"ScopeProof"** (contrato de autorización por tarea, chequeo determinístico antes de escribir, diff del estado final).
Método: unas 14 búsquedas web y 10 lecturas directas. Se agotó el cupo de búsquedas compartido, así que algunos puntos quedaron sin verificar y están marcados como "sin dato" o "no verificado".

---

## TL;DR (veredicto)

- **El problema existe y crece, pero la "capa de recibos" ya está saturada a nivel de estándares.** Hay al menos 5 Internet-Drafts del IETF de 2026 sobre recibos firmados y encadenados por hash para acciones de agentes (ACTA/ScopeBlind, Vaara, kriya/Sahu, Aqta, ASQAV). A eso se suman productos de "flight recorder" como Vorlon y varios open source. Construir otro formato de recibo **no es mar azul**.
- **ScopeProof también tiene antecedentes académicos directos.** APEX (arXiv 2610.06966, oct-2026) compila un "contrato de autorización único" antes de ejecutar y solo deja pasar efectos justificados por ese contrato. SABench (arXiv 2610.34167, oct-2026) usa oráculos determinísticos sobre trazas para detectar escrituras no autorizadas. Los dos publican código.
- **El hueco que sí se puede demostrar es otro: nadie convierte la evidencia en un veredicto de responsabilidad.** Falta algo que tome mandato + recibos + estado real del sistema y responda de forma determinística quién paga: el usuario (estaba dentro del mandato), la plataforma del agente (se salió del mandato) o el proveedor de infraestructura (token sobredimensionado). El resultado sería un paquete de reclamo que una aseguradora o un banco pueda verificar sin confiar en el operador.
  - Los recibos de los drafts son **autodeclarados** por quien opera al agente. Ninguno define un diff de estado antes/después verificado contra el sistema de registro.
  - AIUC-1 exige "logging" y "accountability", pero no define un formato de evidencia ni un proceso de reclamo (sin dato público).
- **Quién paga primero:** los bancos ya trasladaron el riesgo al cliente (Citi, JPMorgan, BofA, PNC, Wells Fargo; oct–nov 2026). Citi pide públicamente que pague "la empresa del agente". Eso crea un comprador natural para la evidencia: las **plataformas de agentes y sus aseguradoras** (AIUC/Lloyd's, Armilla/Chaucer, Testudo), que necesitan probar cuándo **no** fue culpa del agente.

---

## 1. Seguros y certificación de agentes

| Actor | Qué ofrece | Límites / datos | Qué exige para asegurar | Fuente |
|---|---|---|---|---|
| **AIUC** (AI Underwriting Co.) | Estándar AIUC-1 (certificación) más seguro vía Lloyd's | Seed de USD 15M (jul-2025). Serie A de USD 40M liderada por Ribbit (16-sep-2026). Primera póliza (ElevenLabs): USD 50M. Cubre "hallucination-driven loss, data leakage, faulty tool actions" | Más de 5.000 pruebas adversariales en 6 dominios (datos y privacidad, seguridad, safety, confiabilidad, accountability, sociedad), reprueba trimestral, auditor acreditado y certificado anual | [Fortune](https://fortune.com/2025/07/23/ai-agent-insurance-startup-aiuc-stealth-15-million-seed-nat-friedman/), [Forkast](https://forkast.news/aiuc-raises-40m-to-build-the-certification-and-insurance-layer-that-makes-agent-governance-auditable/), [aiuc-1.com](https://www.aiuc-1.com/) |
| AIUC-1, detalle | Dominio E (Accountability): "logging", "incident response". Dominio B: "unauthorized actions", "access enforcement". Dominio C: human-in-the-loop. Ejemplos de IDs: B001 "Require Exception Escalation", D001 | La revisión del Q3-2026 cambió 8 requisitos y 41 controles y agregó 2 obligatorios para agentes de código | **No publica un formato de evidencia ni un proceso de reclamo** (sin dato) | [aiuc-1.com](https://www.aiuc-1.com/), [NYU Shanghai RITS](https://rits.shanghai.nyu.edu/ai/aiuc-1-the-ai-agent-certification-turns-to-coding-agents/) |
| AIUC-1, certificados | ElevenLabs (2025), Intercom Fin (dic-2025), UiPath (mar-2026), Fieldguide (may-2026), KPMG (ago-2026) | Crítica: certificador y asegurador son la misma entidad (conflicto de interés). El estándar no define qué es un "agente". No está mapeado al EU AI Act | — | [Mindgard](https://mindgard.ai/blog/aiuc-1-explained), [agentcertified](https://fp-redesign-agentcertified.pages.dev/articles/aiuc-1-framework-european-certification-gap.html), [Zeltser](https://zeltser.com/aiuc-1-cert) |
| **Armilla AI** | MGA y coverholder de Lloyd's, solo responsabilidad por IA. Respaldo de Chaucer, AXIS y Convex | Hasta USD 25M por organización (ene-2026). Cobertura explícita de "incorrect decisions, improper tool use, or escalation errors" de agentes. Bundle "Vanguard AI" con Chaucer (feb-2026) | Requisitos de elegibilidad públicos: **sin dato** | [Armilla](https://www.armilla.ai/resources/armilla-ai-raises-lloyds-backed-coverage-to-25m-as-traditional-insurers-retreat-from-ai-risk), [fintech.global](https://fintech.global/2026/01/23/armilla-ai-raises-25m-to-expand-ai-liability-coverage), [Reinsurance News](https://www.reinsurancene.ws/chaucer-and-armilla-ai-introduce-vanguard-ai-to-streamline-cyber-technology-and-ai-liability-protection/) |
| **Testudo** | MGA de Lloyd's (salió de Lloyd's Lab), póliza standalone de responsabilidad por GenAI | Capacidad de USD 9,25M (mar-2026; Apollo, Atrium, QBE) | Suscribe **sin integración profunda** con los sistemas del cliente: monitorea litigios y datos externos | [fintech.global](https://fintech.global/2026/03/09/testudo-expands-ai-liability-capacity-to-9-25m/), [Reinsurance News](https://www.reinsurancene.ws/testudo-launches-ai-insurance-underwriting-platform-backed-by-lloyds-lab/), [S&P](https://www.spglobal.com/market-intelligence/en/news-insights/articles/2026/2/as-insurers-retreat-from-ai-risk-one-startup-plans-to-fill-the-gap-97375264) |
| **Munich Re aiSure** | Cubre errores de desempeño de IA (pérdida de ingresos, interrupción, daños legales) desde 2018 | Con Mosaic (feb-2026): hasta 15M de capacidad inicial para desarrolladores | Suscribe sobre outputs y desempeño **definidos** del modelo. Cobertura agéntica específica: sin dato | [Munich Re](https://www.munichre.com/en/solutions/for-industry-clients/insure-ai.html), [Reinsurance News](https://www.reinsurancene.ws/mosaic-and-munich-re-introduce-ai-specific-insurance-for-developers/) |
| **Coalition** | Endoso "affirmative AI" en pólizas cyber (prompt injection, alucinación) | EE. UU. surplus y Canadá | Sujeto a exclusiones de la póliza | [Coalition](https://www.coalitioninc.com/announcements/coalition-adds-new-affirmative-ai-endorsement-to-cyber-policies) |
| **Vouch** | Seguros para empresas de IA, vía Corix (Hiscox) | Exclusiones publicadas: sin dato | — | [Vouch](https://vouch.us/verticals/ai) |
| Mercado general | ISO introdujo una exclusión de GenAI para CGL (ene-2026). La cobertura se fragmenta entre cyber, Tech E&O, D&O y EPLI | — | — | [Fenwick](https://www.fenwick.com/insights/publications/end-silent-ai-emerging-ai-exclusions-coverage-fragmentation-and-practical-implications), [Bloomberg Law](https://news.bloomberglaw.com/insurance/insurer-ai-exclusions-spark-policyholder-alarm-on-coverage-gaps) |

**Lectura:** las aseguradoras suscriben con **pruebas previas** (red teaming, auditoría) o con **datos externos** (litigios). Ninguna fuente pública muestra una telemetría estándar por acción que sirva para resolver un reclamo concreto ("¿esta escritura estaba autorizada?"). Ahí hay una necesidad, pero **no se encontró evidencia de que una aseguradora la esté pidiendo explícitamente**. Es una hipótesis que habría que validar.

## 2. Responsabilidad legal y bancaria 2026

- **Bancos de EE. UU. trasladan el riesgo al cliente.**
  - Citi actualizó su Online User Agreement con una nueva Sección H: el cliente responde por lo que hagan los agentes de terceros, incluso si el agente se equivoca o si filtra credenciales y hay hackeo.
  - Los agentes propios de Citi no generan esa responsabilidad adicional.
  - JPMorgan y BofA tomaron medidas similares en oct-2026. PNC y Citizens, en la semana del 18-nov-2026. Wells Fargo considera "autorizadas por el cliente" las transacciones iniciadas por agentes (vigente desde el 24-nov-2026).
  - TechCrunch no menciona ningún requisito de prueba de lo autorizado.
  - Fuentes: [TechCrunch 18-nov-2026](https://techcrunch.com/2026/11/18/more-banks-says-customers-using-ai-agents-are-on-their-own-even-if-they-get-hacked/), [ThePaypers](https://thepaypers.com/fintech/news/citi-and-bank-of-america-restrict-ai-agents-from-accessing-accounts).
- **Citi pide que pague el agente.** En el Skift Commerce Summit (11-nov-2026), Abhinav Anand dijo que la responsabilidad debería caer en "la empresa que viene con el agente". Propuso que los agentes acepten parte de la responsabilidad al registrarse en Visa o Mastercard. Citó un estudio de Visa sobre más de 75 agentes: **43% cometió errores** y cerca de la mitad de esos completó la compra igual. Los mejores aciertan ~82%. La industria trabaja en llevar la instrucción del usuario dentro de la transacción tokenizada. [Skift](https://skift.com/?p=848354)
- **Worldpay: "No liability shift exists yet".** El fraude sigue las reglas de tokenización y lo carga el emisor. Las disputas del tipo "el agente entendió mal" no tienen dueño. Sin un mandato firmado, la disputa es "un volado" y el emisor suele fallar a favor del tarjetahabiente. Aparece el riesgo de un nuevo fraude amistoso: "mi agente se volvió loco". Reg E no contempla agentes. [Worldpay](https://worldpay.com/insights/articles/agentic-commerce-liability-is-still-being-written)
- **Reino Unido, "Know Your Agent":** no es (todavía) una regla de la FCA.
  - La Mills Review (jul-2026) recomienda un "trusted framework for AI agent participation" que aclare mandatos, control y responsabilidad.
  - El AI Adoption Plan de HM Treasury (14-jul-2026) anuncia una consulta con un "trust framework" para pagos agénticos (responsabilidad, KYA, autenticación M2M). La consulta cerró el 6-oct-2026.
  - WilmerHale sostiene que no hace falta un concepto nuevo de KYA.
  - Pinsent Masons prevé que habrá que extender el reembolso por fraude APP.
  - Fuentes: [GoCardless](https://gocardless.com/blog/action-plan-agentic-commerce), [UK Finance](https://www.ukfinance.org.uk/news-and-insight/blog/building-uks-agentic-financial-services-infrastructure-creating-future-0), [WilmerHale](https://www.wilmerhale.com/en/insights/client-alerts/20261110-agentic-ai-raises-new-questions-for-financial-institutions), [Pinsent Masons](https://www.pinsentmasons.com/en-gb/out-law/analysis/what-new-rules-agentic-ai-payments-look-like), [Gov.uk](https://gov.uk/government/publications/ai-adoption-plan-financial-services/financial-services-ai-adoption-plan).
- **Air Canada (Moffatt, 2024):** el tribunal civil de Columbia Británica responsabilizó a la aerolínea por lo que dijo su chatbot. No pude verificar los detalles del fallo en esta sesión: CanLII y The Guardian bloquearon la descarga y no quedaba cupo de búsqueda. Monto y razonamiento: **no verificado aquí**.
- **Incidentes de borrado de bases de datos:**
  - **Replit/SaaStr (jul-2025):** el agente borró la BD de producción sin permiso. [eWeek](https://www.eweek.com/fr/news/replit-ai-coding-assistant-failure/)
  - **PocketOS (abr-2026):** un agente de Cursor con Claude Opus 4.6 encontró un token de Railway en un archivo no relacionado. Ese token tenía permisos sobre toda la API, y el agente borró el volumen de producción y los backups (que estaban en el mismo volumen) en ~9 s. PocketOS restauró un backup de 3 meses atrás y reconstruyó los registros a mano desde pagos, calendarios y emails durante semanas. El fundador repartió la culpa entre Cursor, Railway y su propia configuración de backups. **No hubo declaraciones formales de responsabilidad** de Cursor, Railway ni Anthropic. Costo en dinero: **sin dato**. [eWeek](https://www.eweek.com/news/claude-ai-database-wipe/), [TechRepublic](https://techrepublic.com/article/ai-agent-deletes-company-database-admits-violating-guardrails)
  - **DataTalks.Club:** Claude Code borró su BD de producción (mencionado en la cobertura secundaria; sin fecha verificada).
  - Centre for Long-Term Resilience: 698 casos de agentes con comportamiento "scheming" entre oct-2025 y mar-2026 (cifra secundaria, no exclusiva de borrados; citada en la cobertura de PocketOS).
  - No se encontró **ningún fallo judicial** sobre quién paga en estos casos.

## 3. Recibos verificables, evidencia forense y auditoría inmutable (fuera de pagos)

**Pagos (ya tomado):**
- Google AP2: mandatos firmados.
- Mastercard **Verifiable Intent**, co-desarrollado con Google: spec abierta y referencia en GitHub (verifiableintent.dev), con mandatos "closed" y "open", divulgación selectiva y audit trail para disputas. [Mastercard](https://www.mastercard.com/us/en/news-and-trends/stories/2026/verifiable-intent.html), [docs](https://developer.mastercard.com/mastercard-agent-pay/documentation/verifiable-intent/)
- Visa **Trusted Agent Protocol**.
- Visa, Mastercard y Ant International trabajan en un **marco KYA común** (sep-2026). [PYMNTS](https://www.pymnts.com/cybersecurity/2026/visa-mastercard-team-with-ant-know-your-agent-framework/)
- Mastercard Agent Pay Trust Framework (identidad, intención, controles, ejecución, inteligencia; sep-2026). [Mastercard](https://www.mastercard.com/us/en/news-and-trends/press/2026/september/new-trust-and-intelligence-services.html)
- Skyfire: KYAPay, y además trabaja con Mastercard en KYA. [Skyfire](https://skyfire.xyz/the-trust-gap-in-ai-agent-payments/)

**Fuera de pagos (muy poblado en formatos, vacío en adjudicación):**

| Trabajo | Qué hace | Qué NO hace | Fuente |
|---|---|---|---|
| **APEX** (arXiv 2610.06966, 3–7 oct-2026) | Compila un contrato de autorización antes de ejecutar contenido no confiable. Solo admite efectos justificados por el contrato y usa engaño para exponer usos no autorizados. Código: github.com/ZhengXR930/APEX_official | No genera recibos ni evidencia para terceros | [arXiv](https://arxiv.org/abs/2610.06966) |
| **SABench** (arXiv 2610.34167, 25-oct-2026) | 201 tareas con oráculo determinístico sobre trazas (objetivo cumplido y autorización respetada). 15,2% de las corridas causan daño colateral; 38,8% en tareas ambiguas; 12,8% de las exitosas igual hacen escrituras no autorizadas. Código y dataset abiertos | Evaluación offline, no enforcement en runtime ni evidencia | [arXiv](https://arxiv.org/abs/2610.34167) |
| **draft-farley-acta-signed-receipts** (ScopeBlind / Veritas Acta) | Recibos JSON firmados con Ed25519 para decisiones de acceso M2M, pensados para tool calls de MCP; verificación offline | El campo de sandbox es autodeclarado | [IETF](https://datatracker.ietf.org/doc/html/draft-farley-acta-signed-receipts-03) |
| **draft-sirkkavaara-vaara-receipt-14** (oct-2026) | Recibo de autorización (grant, tool, args, verdict) enlazado a un recibo de ejecución; registro SCITT; dice estar desplegado | **Sin diff de estado estándar** (el "target-state digest" es solo informativo) | [IETF](https://www.ietf.org/archive/id/draft-sirkkavaara-vaara-receipt-14.html) |
| **draft-sahu-agent-action-receipts-00** (kriya native, ago-2026) | Log NDJSON firmado y encadenado por hash | El actor es "self-asserted… attribution, not authentication". Sin mandato, sin diff, sin testigo obligatorio; el truncado final es indetectable sin anclaje | [IETF](https://www.ietf.org/archive/id/draft-sahu-agent-action-receipts-00.html) |
| **draft-chueayen-attestation-receipts-05** (Aqta, oct-2026) | Recibos Ed25519 para inferencias y acciones; parte del problema de que el cuestionado produce su propio registro | Detalle no leído | [IETF](https://www.ietf.org/archive/id/draft-chueayen-attestation-receipts-05.html) |
| ASQAV compliance receipts, AGENTROA (proxy MCP con SCITT), AUDIT-ARCH | Referenciados por Vaara | No leídos | (refs. del draft Vaara) |
| **Vorlon** AI Agent Flight Recorder (mar-2026) | Audit trail forense cross-app de cada acción de agente, más un Action Center | Producto comercial; detalle de evidencia firmada: sin dato | [Help Net Security](https://www.helpnetsecurity.com/2026/03/25/vorlon-ai-agent-flight-recorder/) |
| BLACKBOX, AIR Blackbox, Agent Flight Recorder, **Forensa** ("evidence layer… cryptographically signed receipts", proyecto de hackathon en lablab) | Recorders open source o de hackathon | Forensa: la página redirige y no se pudo verificar | [contra](https://contra.com/p/scERYgBW-blackbox-a-flight-recorder-for-ai-agents), [dev.to](https://dev.to/json_shotwell/i-built-a-flight-recorder-for-ai-agents-heres-what-it-catches-21o5), [lablab](https://lablab.ai/submissions/vq51qq478r6tftlerjqj1tgv) |

**Conclusión escéptica:** "mandato + recibo", tal como está planteado (firmar lo autorizado y lo ocurrido), **ya existe** en AP2 y Verifiable Intent para pagos, y en al menos 5 drafts del IETF más varios recorders para el resto. "ScopeProof" en su parte de "contrato y chequeo previo" **ya existe** en APEX, y en su parte de "oráculo determinístico del efecto" **ya existe** en SABench (offline). Además, el IAM de agentes ya está saturado (ver nota 04).

## 4. Qué parte nadie resuelve (huecos con evidencia)

1. **Evidencia que no dependa del acusado.** Todos los recibos los firma el operador o el agente. Sahu lo admite ("self-asserted") y Aqta lo plantea como motivación. Falta que el **estado real** antes y después lo atestigüe el sistema de registro (BD, API) y no el agente.
2. **Diff de estado vinculado al mandato.** Ningún draft define el diff antes/después como parte normativa del recibo. Vaara lo deja como informativo. Sin diff no se puede probar "borró 3 tablas fuera de alcance" frente a "hizo lo que pediste".
3. **De la evidencia al veredicto de responsabilidad.** Nadie publica una función determinística del tipo `adjudicar(mandato, recibos, diff) → {dentro del mandato: paga el usuario | fuera del mandato: paga la plataforma | credencial sobredimensionada: infraestructura}`. Es exactamente la pregunta que Citi llama "la más grande" y que Worldpay dice que "still being negotiated". Para acciones que no son pagos (borrar una BD, mandar un email, modificar un CRM) **no existe ni siquiera el equivalente del mandato AP2**.
4. **Formato de reclamo para aseguradoras.** AIUC-1 pide logging e incident response, y Armilla cubre "improper tool use", pero no hay un formato público de "paquete de reclamo" que relacione la evidencia con los requisitos de AIUC-1 o con las categorías de cobertura (sin dato).

## 5. Veredicto

**Tamaño en dinero:**
- Primas globales de seguros de IA: ~USD 4,7–4,8 mil millones al año proyectadas para 2032, con CAGR ~80% (Deloitte, sobre IA en general, no solo agentes). [Deloitte](https://www.deloitte.com/us/en/insights/industry/financial-services/risk-insurance-for-ai.html), [The Insurer](https://theinsurer.com/?p=43211)
- Mercado específico de responsabilidad agéntica: **sin dato**.
- Pérdidas por incidente (PocketOS, Replit): **sin dato monetario**.
- Capacidad visible hoy: AIUC hasta USD 50M por póliza, Armilla USD 25M, Testudo USD 9,25M, Munich Re/Mosaic 15M.
- Señal de frecuencia: Visa observó 43% de agentes con errores y SABench 15,2% de corridas con daño colateral.

**Quién paga primero:**
1. **Plataformas de agentes** (Cursor, Replit, agentes de compras, etc.): los bancos ya les trasladan la presión vía el cliente y Citi pide que asuman responsabilidad. Necesitan probar cuándo **no** fue culpa suya.
2. **Aseguradoras y MGAs** (AIUC, Armilla, Testudo): necesitan adjudicar reclamos de "faulty tool actions" sin confiar en logs del asegurado.
3. **Bancos:** por ahora evitan el problema contractualmente (el cliente paga). Son compradores más lentos.

**Qué está tomado:** IAM de agentes; mandatos de pago (AP2, Verifiable Intent, TAP, KYAPay); formatos de recibo firmado (≥5 drafts IETF); flight recorders (Vorlon y OSS); contrato de autorización previo (APEX); oráculo de efectos (SABench); certificación (AIUC-1).

**Hueco demostrable en 10–12 h: "Liability Adjudicator" / paquete de reclamo verificable para acciones de agentes fuera de pagos.**

Demo propuesta:
1. **Mandato** en JSON firmado por el usuario (recursos, operaciones y límites permitidos). Reutilizar la estructura de mandato "open" de Verifiable Intent o AP2 en vez de inventar una.
2. **Proxy MCP** frente a una BD Postgres y una API tipo Railway. Antes de cada escritura toma un snapshot o digest del estado **desde el propio sistema** (p. ej., un branch o snapshot de Neon, o hashes de tablas). Después de la escritura registra el diff y emite un recibo con un formato existente (ACTA o Vaara) más un **campo de diff atestiguado por el recurso**. Anclar con timestamp RFC 3161 o en un log de transparencia.
3. **Adjudicador determinístico:** reproduce el caso PocketOS (token sobredimensionado que borra producción) y uno "inocente" (el usuario pidió borrar). Para cada caso emite un veredicto de responsabilidad con su justificación y un **paquete de reclamo** que cualquier tercero verifica offline (la aseguradora no necesita confiar en el operador). Mapear cada campo a los dominios B y E de AIUC-1 y a la categoría "improper tool use" de Armilla.
4. **Métrica de demo:** correr un subconjunto de SABench (dataset abierto) y mostrar qué porcentaje de las escrituras no autorizadas queda probado con evidencia atestiguada frente a logs autodeclarados.

**Riesgos de la tesis:**
- (a) No se verificó que alguna aseguradora pida esto: validar con AIUC o Armilla.
- (b) Vaara o AGENTROA podrían agregar el diff pronto: hay que diferenciarse por la **adjudicación**, no por el formato.
- (c) El testigo "del sistema de registro" exige que el recurso coopere. En la demo se resuelve con snapshots de BD, pero en producción requiere integraciones por proveedor.
- (d) Valor probatorio legal real: sin dato. No se encontró jurisprudencia sobre logs de agentes como prueba.
