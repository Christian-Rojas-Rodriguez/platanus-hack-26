# 04 — Seguros: ¿alguien pide evidencia verificable de lo que hizo un agente?

Fecha: 21-nov-2026. Parte de la validación de la hipótesis forense: "cuando un agente hace algo dañino, nadie puede probar de forma independiente qué autorizó el humano, qué hizo el agente y quién paga; los registros los firma la parte interesada".
Método: unas 25 búsquedas y lecturas directas (WebSearch, WebFetch y extracción con `pdftotext` de dos PDF). Fuentes primarias que se leyeron: texto del estándar AIUC-1 (standard.aiuc-1.com), informe de AIUC y otros "Underwriting the Agent Economy" (arXiv 2607.11999, jul-2026), circular de la IUA (mar-2026), Deloitte, páginas de Armilla, Munich Re, Coalition, Vouch y Relm. Lo que no se pudo verificar dice "no verificado".

---

## TL;DR

- **Respuesta directa: no.** Ninguna aseguradora pide públicamente, para suscribir ni para pagar, evidencia de las acciones del agente que un tercero pueda verificar sin confiar en el asegurado. Lo que más se acerca es AIUC-1 (el estándar que exige AIUC para asegurar vía Lloyd's).
  - Sus controles **obligatorios** piden logs de actividad (E015.1), logs de tool calls (D003.3) y flujos de aprobación humana (D003.4).
  - El control que pide logs "tamper-evident and independently verifiable" (E015.4) es **solo suplementario**, o sea opcional.
  - Y en todos los casos el log lo produce y lo guarda el propio asegurado.
- **El problema sí aparece en fuente primaria del sector.** El informe de AIUC, escrito junto a QBE, Aon, Generali, Tysers y Moody's (jul-2026), dice que para reclamos de agentes "the central difficulty is forensic". Advierte que sin logs obligatorios el ajustador queda "with little more than the policyholder's own narrative". También reconoce que las firmas de respuesta a incidentes y forense de IA "don't yet exist".
- **La demanda todavía es teórica.** No se encontró ningún siniestro público pagado ni rechazado por una acción de agente. Las grandes aseguradoras responden **excluyendo** (formularios ISO de enero de 2026, Berkley, AIG y Great American), no pidiendo evidencia. Las especialistas suscriben con pruebas previas (Armilla, AIUC, Munich Re) o con datos externos de litigios (Testudo), no con telemetría por acción.

---

## (a) Aseguradoras y productos

| Empresa | Producto | Límite | Qué exige de registro o evidencia | URL |
|---|---|---|---|---|
| **AIUC** (Artificial Intelligence Underwriting Co.) | Certificación AIUC-1 más seguro respaldado por Lloyd's | Seed de USD 15M (jul-2025). Serie A de USD 40M liderada por Ribbit (16-sep-2026). Primera póliza (ElevenLabs, feb-2026): "$50 million in coverage" según Forkast. El comunicado de prensa de ElevenLabs **no** da el monto | **Suscripción:** certificación AIUC-1 con más de 5.000 simulaciones adversariales y "quarterly retests". **Registro obligatorio:** E015 "Log AI system activity" (configuración de logging y almacenamiento con retención y control de acceso), D003.3 "Tool call log" ("audit logs showing tracked tool calls"), B006.2 monitoreo de acciones de agentes y D003.4 aprobación humana. **Opcional (suplementario):** E015.2, logging de ejecución del agente, y E015.4, logs "tamper-evident and independently verifiable". **Siniestro:** no se publica ningún proceso ni formato de reclamo (no verificado). Forkast: "We have yet to see how these insurance policies will perform" | [standard.aiuc-1.com/accountability](https://standard.aiuc-1.com/accountability), [standard.aiuc-1.com/evidence](https://standard.aiuc-1.com/evidence), [Forkast 16-sep-2026](https://forkast.news/aiuc-raises-40m-to-build-the-certification-and-insurance-layer-that-makes-agent-governance-auditable/), [PR Newswire 11-feb-2026](https://www.prnewswire.com/news-releases/elevenlabs-secures-first-of-its-kind-ai-agent-insurance-302684587.html) |
| **Armilla AI** (MGA y coverholder de Lloyd's) | Affirmative AI Liability. Cobertura de "AI Agent Failures": "incorrect decisions, improper tool use, or escalation errors" | "Up to $25 million per organization" (ene-2026). Un per-model de USD 5M aparece solo en fuente secundaria (no verificado) | **Suscripción:** "independent AI system certification and risk reporting" y evaluación del modelo antes de cubrir. Según la IUA, su garantía de desempeño exige una "invasive evaluation". La cobertura de responsabilidad requiere doble disparador: bajo desempeño de la IA más un reclamo. **Siniestro:** no publica requisitos de evidencia. Su propia página sugiere preguntarle al broker si el asegurador decide qué fue "caused by AI" recién al momento del reclamo | [Armilla ene-2026](https://www.armilla.ai/resources/armilla-ai-raises-lloyds-backed-coverage-to-25m-as-traditional-insurers-retreat-from-ai-risk), [Armilla requisitos](https://www.armilla.ai/ai-insurance-customer-requirement), [IUA mar-2026](https://iua.co.uk/common/Uploaded%20files/IUA%20Circulars%202026/033_IUA%20Clauses%20Committee%20Roundtable_AI%20Insurance_2026.pdf) |
| **Chaucer + Armilla** | Vanguard AI (feb-2026): cyber y Tech E&O de Chaucer más una póliza AI standalone de Armilla. Cubre "AI agent failures" | AI: USD 25M o más de agregado, junto a USD 10M de cyber (prensa) | Nada público sobre logs ni evidencia | [Chaucer](https://www.chaucergroup.com/news/press-release-chaucer-and-armilla-ai-launch-vanguard-ai-coordinated-insurance-structure), [Reinsurance News](https://www.reinsurancene.ws/chaucer-and-armilla-ai-introduce-vanguard-ai-to-streamline-cyber-technology-and-ai-liability-protection/) |
| **Testudo** (coverholder de Lloyd's, salió de Lloyd's Lab) | Responsabilidad standalone por GenAI para empresas que despliegan IA en EE. UU. (lanzada en ene-2026) | Entre USD 8,5M y 9,25M por asegurado (mar-2026; Apollo, Atrium, QBE) | **Ninguna integración:** su suscripción no requiere integraciones "invasive" con los sistemas del cliente. Tarifa con revisión externa y datos de litigios. No cubre a desarrolladores que venden IA como servicio | [Reinsurance News](https://www.reinsurancene.ws/testudo-launches-ai-insurance-underwriting-platform-backed-by-lloyds-lab/), [fintech.global](https://fintech.global/2026/03/09/testudo-expands-ai-liability-capacity-to-9-25m/), [IUA](https://iua.co.uk/common/Uploaded%20files/IUA%20Circulars%202026/033_IUA%20Clauses%20Committee%20Roundtable_AI%20Insurance_2026.pdf) |
| **Munich Re** | aiSure: garantías de desempeño y pérdidas propias por errores de IA (desde 2018) | La página no publica límites. Con Mosaic hay 15M de capacidad inicial (dato de la nota 27, no reverificado) | **Disparador:** "unexpected errors in the ongoing performance of AI models". Con Mosaic usa una estructura "parametric-like" para "fast, objective claims", es decir, se mide contra una métrica pactada, no con forense de acciones. La página **no menciona agentes** | [Munich Re](https://www.munichre.com/en/solutions/for-industry-clients/insure-ai.html) |
| **Coalition** | Endoso Affirmative AI para cyber (26-mar-2024): "AI security event" y fraude de transferencias por deepfake | Según póliza; solo surplus de EE. UU. y Canadá | Nada específico; rige "terms, conditions, limitations" | [Coalition](https://www.coalitioninc.com/announcements/coalition-adds-new-affirmative-ai-endorsement-to-cyber-policies) |
| **Vouch** | Seguros para startups de IA (no nombra un producto AI específico en la página) | No publicado | Advierte que la documentación insuficiente "can result in higher premiums or even coverage denials". Pide un plan para "gathering evidence" al notificar al asegurador. No hay formato definido | [Vouch](https://vouch.us/verticals/ai) |
| **Relm Insurance** | NOVAAI (cyber y Tech E&O para plataformas de IA), PONTAAI (wrap DIC en exceso cuando otras pólizas excluyen IA) y RESCAAI (14-ene-2025) | No publicado | No publicado (no verificado) | [Relm](https://relminsurance.com/relm-insurance-launches-ai-suite/) |
| **Lloyd's** (mercado) | Es el capital detrás de AIUC, Armilla y Testudo | — | La IUA (mar-2026) informa "limited examples of AI specific clauses" en Londres. No hay requisito de evidencia a nivel de mercado (no verificado) | [IUA](https://iua.co.uk/common/Uploaded%20files/IUA%20Circulars%202026/033_IUA%20Clauses%20Committee%20Roundtable_AI%20Insurance_2026.pdf) |

**Lectura de AIUC-1, el punto clave.** El estándar exige que el asegurado **tenga** logs: actividad (E015.1, obligatorio), tool calls con servidor MCP, herramienta, versión, parámetros y timestamp (D003.3, obligatorio), y retención y control de acceso (E015.3, obligatorio). El requisito de que esos logs sean a prueba de manipulación y "independently verifiable" existe, pero como control **suplementario** (E015.4). E015 además se limita con "where permitted". El auditor verifica la **configuración** del logging en la certificación, no el contenido de los logs en un siniestro. Tampoco hay ningún requisito de registrar **qué autorizó el humano** como un mandato verificable. Lo más parecido es D003.4, flujos de aprobación para operaciones sensibles.

## (b) Exclusiones de IA

| Quién | Qué | Alcance | Estado | Fuente |
|---|---|---|---|---|
| **Verisk / ISO** | CG 40 47, CG 40 48 y CG 35 08 (edición de ene-2026) | CG 40 47 excluye daño corporal, daño a la propiedad y daño personal o publicitario "arising out of" GenAI en la CGL. CG 40 48 solo el daño personal o publicitario (Coverage B). CG 35 08 cubre productos y operaciones completadas | Opcionales. Las aseguradoras las presentan ante los reguladores estatales. Una fuente secundaria cuenta 2.369 registros en 49 estados (no verificado) | [Insurance Journal 17-ago-2026](https://www.insurancejournal.com/magazines/mag-features/2026/08/17/881424.htm), [Insurance Business](https://www.insurancebusinessmag.com/us/news/professional-liability/isos-generative-ai-exclusion-is-already-on-thousands-of-cgl-policies-589971.aspx) |
| **W. R. Berkley** | Exclusión "absolute" de IA en D&O, E&O y responsabilidad fiduciaria | "any actual or alleged use, deployment, or development of Artificial Intelligence" | Introducida en 2025. Un abogado (Hunton) cree que quizás "never see the light of day commercially" | [Hunton](https://www.hunton.com/hunton-insurance-recovery-blog/the-continued-proliferation-of-ai-exclusions), [Insurance Journal](https://www.insurancejournal.com/magazines/mag-features/2026/08/17/881424.htm) |
| **AIG, Great American, W. R. Berkley** | Pidieron a los reguladores aprobar exclusiones de IA (chatbots y agentes) | AIG dijo que tenía "no plans to implement" de inmediato | Reportado por el FT (nov-2025); aprobación pendiente según Insurance Business (24-nov-2025). El FT original no se leyó | [Insurance Business 24-nov-2025](https://www.insurancebusinessmag.com/us/news/technology/major-insurers-seek-approval-to-limit-liability-for-airelated-claims--report-557553.aspx), [Tom's Hardware](https://www.tomshardware.com/tech-industry/artificial-intelligence/insurers-move-to-limit-ai-liability-as-multi-billion-dollar-risks-emerge) |
| Mercado | "Más de 60 grupos" de P&C presentaron alguna exclusión de IA | — | Cifra secundaria (no verificado en fuente primaria) | [JD Supra / NatLawReview](https://natlawreview.com/article/continued-proliferation-ai-exclusions) |
| **Marsh** (en contra de las exclusiones amplias) | El CEO John Doyle advierte que una exclusión amplia genera "real confusion and uncertainty" | — | 16-oct-2026 | [Insurance Journal / Reuters](https://www.insurancejournal.com/news/national/2026/10/16/889136.htm) |

**Relevancia para la hipótesis.** Una exclusión del tipo "arising out of AI" solo se puede aplicar si se prueba que la IA causó la pérdida. El informe de AIUC lo dice explícitamente para las exclusiones de fallas del modelo base: sin logs "will simply shift uncertainty from the policy form into the claims process" (arXiv 2607.11999, jul-2026).

## (c) Qué les falta a suscriptores y corredores (citas)

| Quién | Cita (menos de 15 palabras) | Fuente y fecha |
|---|---|---|
| Informe AIUC + QBE, Aon, Generali, Tysers y otros | "For AI agent claims, the central difficulty is forensic" | [arXiv 2607.11999](https://arxiv.org/abs/2607.11999), §II.8.B, jul-2026 |
| Ídem | "adjudicating black-box failures with little more than the policyholder's own narrative" | Ídem, §II.8.B |
| Ídem | "Mandated input-output logs furnish contemporaneous evidence that is difficult to reconstruct" | Ídem, §II.8.B |
| Ídem | Exclusiones "unenforceable without appropriate logs for post-incident forensics" | Ídem, resumen ejecutivo |
| Ídem | "AI incident response and forensics firms don't yet exist" (recomendación §II.8) | Ídem |
| Ídem | Reconstruir la cadena del agente es "forensic reconstruction of agentic decision chains" (nueva capacidad necesaria) | Ídem, §II.8 |
| Ídem (nota al pie 39) | El rastro causal "may not lie entirely within the insured's own systems" | Ídem, §II.8.C |
| Ídem | Los hallazgos se ocultan: "forensic findings are buried to avoid creating evidence of negligence" | Ídem, §II.8.D |
| Nick Studer, CEO de Marsh Risk | Es "impossible to unbundle it from the causal pathways to whatever outcome" | [Insurance Journal 16-oct-2026](https://www.insurancejournal.com/news/national/2026/10/16/889136.htm) |
| Kevin Kalinich, Aon | Pérdidas de IA "aggregated, systemic, correlated" | [Insurance Business 15-jul-2026](https://www.insurancebusinessmag.com/ca/news/technology/insurers-face-hidden-ai-liability-as-agent-risks-multiply-582434.aspx) |
| Deloitte | "lack of historic data on the performance of AI models" | [Deloitte 29-may-2024](https://www.deloitte.com/us/en/insights/industry/financial-services/risk-insurance-for-ai.html) |
| Lockton (Ashley Bennett Jones) | "There is less opportunity for the human in the loop" | [Insurance Business 2-nov-2026](https://www.insurancebusinessmag.com/us/news/breaking-news/ai-agents-are-moving-faster-than-human-oversight--and-insurers-are-taking-notice-595827.aspx) |
| Insurance Business (redacción) | "There's no clear answer yet to how responsibility will be allocated" | Ídem |
| Phil Dawson, Armilla | La IA "challenges some of the fundamental logic of existing insurance coverage" | [AFP / The Star 16-mar-2026](https://www.thestar.com.my/tech/tech-news/2026/03/16/who-covers-ai-business-blunders-some-insurers-cautiously-step-up) |
| IUA (con Testudo) | El caso del chatbot "underscores the complexity of liability attribution" | [IUA mar-2026](https://iua.co.uk/common/Uploaded%20files/IUA%20Circulars%202026/033_IUA%20Clauses%20Committee%20Roundtable_AI%20Insurance_2026.pdf) |

**Patrón:** la falta de **datos de pérdidas** es la queja más repetida (Deloitte, McKinsey, Munich Re). La falta de **registros y atribución** aparece con fuerza en un solo documento primario, el informe de AIUC. Ese informe tiene interés comercial: AIUC vende el estándar que exige esos logs. Marsh e IUA hablan de causalidad y atribución, pero no de logs. **No se encontró ningún texto de Marsh, Aon o WTW que pida evidencia firmada o verificable** de acciones de agentes. La página de WTW de feb-2026 devolvió un error 429 y no se pudo leer (no verificado).

### Deloitte, verificación de la cifra
- Cifra: "around US$4.7 billion" en primas anuales globales de seguros de IA hacia 2032, con un CAGR de ~80%.
- Publicación: Deloitte Center for Financial Services, 29-may-2024.
- Alcance: seguros de IA **en general** (desempeño de modelos, GenAI, sesgo, propiedad intelectual). **No es específico de agentes.**
- Método: analogía con la curva de cyber entre 2009 y 2017 y una tasa de penetración sobre la economía digital. Es una proyección, no datos de mercado.
- AFP y National Mortgage News citan USD 4,8 mil millones, aparentemente por redondeo o una actualización posterior.
- Fuente: [Deloitte](https://www.deloitte.com/us/en/insights/industry/financial-services/risk-insurance-for-ai.html).

### Siniestros reales por acciones de agentes
- **No se encontró ninguno público** pagado o rechazado por una acción de un agente de IA. Forkast lo confirma: todavía no se vio cómo rinden las pólizas de AIUC.
- PocketOS (abr-2026), Replit y SaaStr: hubo daño, pero **no hay resultado de cobertura publicado**.
- Casos cercanos que no son de agentes: Air Canada/Moffatt (chatbot), Arup (deepfake por HK$200M), Wolf River Electric contra Google (AI Overviews, USD 110M o más). Ninguno es un siniestro de seguro resuelto con logs del agente.
- Law360 publicó "Insurer Lessons From 1st Wave Of GenAI Coverage Rulings", pero está detrás de un muro de pago (no verificado).
- Encuesta de Gallagher 2026: 1 de cada 5 profesionales de seguros dice que sus asegurados ya tuvieron pérdidas ligadas a IA. No dice cómo se probaron.
- **¿Cómo se probó?** No hay ningún caso público que lo muestre.

## (d) Evidencia en contra de la hipótesis

1. **El estándar ya contempla logs verificables.** AIUC-1 E015.4 pide logs "tamper-evident and independently verifiable", con detección de huecos y reordenamiento, WORM o hashing. D003.3 obliga a registrar cada tool call. La idea ya está en el estándar líder; solo falta que sea obligatoria y que la verifique alguien distinto del asegurado. Un producto nuevo compite con "cumplir E015.4".
2. **Muchas aseguradoras no necesitan forense por acción.**
   - Testudo suscribe sin integrarse con los sistemas del cliente.
   - Munich Re y Mosaic pagan con disparadores "parametric-like" contra métricas pactadas.
   - Armilla usa evaluaciones previas.
   - El modelo de negocio funciona hoy sin evidencia por acción. Ese hueco podría no ser un dolor de compra.
3. **Las grandes excluyen en vez de medir.** ISO, Berkley y AIG eligieron sacar el riesgo de la póliza. No piden mejor evidencia para cubrirlo.
4. **La "tercera parte independiente" ya tiene candidatos.** El informe de AIUC propone obtener telemetría de los **proveedores de modelos y de nube** (tool calls MCP, trazas de agentes, eventos de aprobación), como la telemática en autos. Ese testigo no es el asegurado, pero tampoco es una startup. Además cita frameworks de "runtime governance" que ya definen el esquema de trazas.
5. **Sin siniestros públicos la demanda no está probada.** La discusión es ex ante (white papers y exclusiones). La prueba de responsabilidad hoy se resuelve en litigio y discovery, no con un paquete de evidencia.
6. **Sesgo de la fuente principal.** El documento que más apoya la hipótesis lo encabeza AIUC, que vende certificación y seguro. Insurance Business recoge críticas de que AIUC tiene "commercial interest" en exagerar el riesgo.

## (e) Qué significa para la hipótesis

**¿Alguna aseguradora pide evidencia verificable de acciones de agentes? No.**
- AIUC (vía AIUC-1) es la única que **exige logs** de actividad y de tool calls para asegurar.
- Los exige como configuración auditada al certificar, generados y guardados por el propio asegurado.
- La verificabilidad independiente (E015.4) es opcional.
- Ninguna aseguradora publica qué evidencia pide para **pagar** un siniestro de un agente.
- Nadie pide registrar de forma verificable **qué autorizó el humano**.

**Qué queda validado:**
- La parte "los registros los firma la parte interesada": el modelo vigente es un log del asegurado más una auditoría de configuración.
- La parte "nadie puede probar quién paga": un informe primario de la industria aseguradora dice que el problema central de los reclamos de agentes es forense y que sin logs se adjudica con el relato del asegurado.
- Que está poco atendido: las firmas de forense de IA "don't yet exist" y no hay ningún formato de reclamo publicado.

**Qué NO queda validado:**
- Que sea un problema **grande en dinero hoy**: no hay siniestros públicos, y la cifra de USD 4,7 mil millones es una proyección de 2024 para toda la IA.
- Que las aseguradoras **paguen** por resolverlo: las especialistas suscriben sin esa evidencia y las grandes excluyen.

**Implicación para el producto:**
- El argumento más defendible con fuentes no es "las aseguradoras lo exigen". Es este: "AIUC-1 E015.4 ya pide logs a prueba de manipulación y verificables de forma independiente, y el informe de AIUC dice que sin eso las exclusiones no se pueden aplicar. Nosotros convertimos E015.4 + D003.3 + D003.4 en un paquete que un ajustador verifica sin confiar en el asegurado".
- El comprador inicial más plausible son las empresas que buscan la certificación AIUC-1 (quieren cumplir controles suplementarios y bajar la prima), más que las aseguradoras mismas.
- Riesgo principal: que los proveedores de modelos o de nube se conviertan en el testigo de telemetría, como propone el propio informe.
