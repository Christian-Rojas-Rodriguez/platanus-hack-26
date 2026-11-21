# 01 — Bancos y traslado de responsabilidad por acciones de agentes (EE. UU., Reino Unido, UE)

Fecha: 21-nov-2026. Objetivo: verificar en fuente primaria lo que afirmaron las notas `mercado/27` y `mercado/33` y buscar evidencia a favor y en contra de esta hipótesis: *"nadie puede probar de forma independiente qué autorizó el humano, qué hizo el agente y quién paga; los registros los firma la parte interesada"*.

**Método y límites**
- Unas 22 búsquedas y unas 30 lecturas directas. Los contratos en PDF se descargaron y se leyeron con `pdftotext`.
- El cupo de búsquedas se agotó antes de terminar el punto 6 (casos de disputa) y el detalle de Mastercard.
- Mastercard (403/404), The Financial Brand (403) y NerdWallet (403) bloquearon la descarga.
- Convención de veredictos: "confirmada" significa que leí la fuente primaria. "No verificado" significa que no encontré o no pude abrir la fuente primaria.

---

## (a) Tabla de verificación

| # | Afirmación (de notas 27/33 o del encargo) | Veredicto | Cita corta (<15 palabras) | URL | Tipo | Fecha |
|---|---|---|---|---|---|---|
| 1 | **Citi** agregó una sección que hace al cliente responsable de lo que hagan los agentes de IA de terceros | **Confirmada** | "Citi will consider any access and actions taken by the agent as authorized by You." | https://www.citi.com/tandc | Primaria (Citi Online User Agreement, Sección H) | "last updated November 2026" |
| 1b | Citi: el cliente responde por los errores de interpretación del agente y debe vigilarlo él | **Confirmada** | "You are responsible for any actions or errors that result from…incorrect interpretation" / "your responsibility and not Citi's to monitor" | https://www.citi.com/tandc | Primaria | nov-2026 |
| 1c | Citi no investiga la autoridad del agente | **Confirmada** (dato clave para la forense) | "no responsibility…to investigate the authority or validity of any such actions" | https://www.citi.com/tandc | Primaria | nov-2026 |
| 1d | Citi: el cliente responde "incluso si hay hackeo o filtración de credenciales" | **Parcial** | En el texto que leí, la responsabilidad se activa al entregar credenciales ("If you disregard this caution and provide your Online Credentials"). Lo de "hackeo" aparece solo en la paráfrasis de TechCrunch | https://www.citi.com/tandc · https://techcrunch.com/2026/11/18/more-banks-says-customers-using-ai-agents-are-on-their-own-even-if-they-get-hacked/ | Primaria + prensa | 18-nov-2026 |
| 1e | Las herramientas de IA que ofrece Citi quedan excluidas de esa sección | **Confirmada** | No aplica a "any third-party AI Agent…provided by Citi" | https://www.citi.com/tandc | Primaria | nov-2026 |
| 2 | **JPMorgan** cambió sus términos en oct-2026 | **Confirmada, con matices** | "Effective October 27, 2026…third parties — including External AI…are prohibited from using your Login Credentials" | https://www.chase.com/content/dam/legal-agreements/library/en/dsa_la/versions/dsa_la.pdf | Primaria (Digital Services Agreement, "Last updated: November 2026") | 27-oct-2026 |
| 2b | JPMorgan: el cliente indemniza al banco por actos del agente fuera de su mandato | **Confirmada** | Indemniza por "actions that were not within the scope of your agent's authority" | mismo PDF, Sección 17 | Primaria | nov-2026 |
| 2c | Chase: el cliente responde si el agente "excede la autoridad" | **Confirmada** (sin fecha propia) | "if it performs unintended actions or exceeds the authority you gave it" | https://www.chase.com/digital/resources/terms-of-use | Primaria (Terms of Use, sección "AI Agent or Agentic AI Notices"; la página dice "Rev. Aug. 2016" y la sección no tiene fecha) | sin fecha |
| 2d | Chase exige que el tráfico de agentes venga etiquetado | **Confirmada** | "must clearly and deterministically label all agentic traffic" | https://www.chase.com/digital/resources/terms-of-use | Primaria | sin fecha |
| 3 | **Bank of America** "tomó medidas similares" en oct-2026 | **Parcial** | El acuerdo vigente desde el 19-oct-2026 **no menciona IA**. Sí trae la regla general previa: el cliente es responsable "(even if he or she exceeds your authorization), until you notify us" | https://www.bankofamerica.com/content/documents/agreement/OBSAUpdateEN.pdf | Primaria (Online Banking Service Agreement) | ef. 19-oct-2026 |
| 3b | BofA avisó por email que el cliente responde por la actividad de agentes de IA | **No verificado en primaria** | Según un artículo, el email dice que el cliente "will be responsible for activity resulting from such AI access" | https://allaboutcookies.org/bank-of-america-ai-agent-liability (cita un post de Bluesky) | Prensa / blog | 4-nov-2026 (el email sería del 27-oct según CSA) |
| 4 | **PNC** cambió sus términos el 18-nov-2026 | **No verificado** | TechCrunch solo dice que PNC cambió sus términos "today". El Digital Services Agreement público es del 25-jul-2025 y no menciona IA | https://techcrunch.com/2026/11/18/… · https://www.pnc.com/content/dam/digital-assets/en/documents/digital_services_agreement.pdf | Prensa; la primaria no contiene el cambio | 18-nov-2026 |
| 4b | **Citizens** avisó por email a sus clientes | **No verificado** | Solo hay un email que vio TechCrunch, sin texto citado | TechCrunch (arriba) | Prensa | 18-nov-2026 |
| 5 | **Wells Fargo** considera "autorizadas por el cliente" las transacciones de agentes (vigente desde el 24-nov-2026) | **Confirmada** | Se consideran "initiated and authorized directly by you" | https://www.wellsfargo.com/online-banking/online-access-agreement/upcoming (Sección 15(d)) | Primaria (Online Access Agreement, "Version Effective November 24, 2026") | ef. 24-nov-2026 |
| 5b | Wells Fargo: el uso de agentes es "a tu riesgo" y el banco no los monitorea | **Confirmada** | "Your use of any AI Agent is AT YOUR OWN RISK." / "We do not monitor, screen, or review AI Agent activities" | mismo, 15(e) | Primaria | ef. 24-nov-2026 |
| 5c | **Wells Fargo exige que el cliente pruebe que revocó al agente** (no estaba en las notas previas; es lo más relevante para la hipótesis) | **Confirmada** | "You must retain evidence of such revocation and must provide such evidence to us" | mismo, 15(f) · https://www.americanbanker.com/news/wells-fargo-wants-customers-to-prove-theyve-revoked-ai-agents | Primaria + prensa | Primaria ef. 24-nov-2026; American Banker 2-nov-2026 |
| 5d | Nota 27: Wells Fargo aparece en TechCrunch del 18-nov | **Refutada** (error de cita) | TechCrunch no menciona a Wells Fargo | TechCrunch (arriba) | Prensa | 18-nov-2026 |
| 6 | Citi pide públicamente que pague "la empresa del agente" (Skift, 11-nov-2026) | **Confirmada** | "the agent themselves, the company that is actually coming with the agent" | https://skift.com/?p=848354 | Prensa (cita textual de Abhinav Anand, Citi) | 11-nov-2026 |
| 6b | Estudio de Visa sobre más de 75 agentes: 43% cometió errores | **Confirmada solo en prensa** | Según Skift, cerca de la mitad de los que se equivocaron completó la compra igual. El estudio de Visa no lo vi | Skift (arriba) | Prensa | 11-nov-2026 |
| 7 | **Worldpay: "No liability shift exists yet"** | **Confirmada** (la página no muestra fecha) | "No liability shift exists yet." · "a disagreement between agent and shopper becomes a coin flip" | https://worldpay.com/insights/articles/agentic-commerce-liability-is-still-being-written | Vendor (Reshmi Suresh, Head of Agentic Commerce) | sin fecha visible (©2026) |
| 7b | Worldpay: sin mandato firmado no hay prueba; aparece el riesgo de "my agent went rogue" | **Confirmada** | "Without a signed mandate proving what the shopper authorized" | mismo | Vendor | íd. |
| 8 | Hay principios de comercio agéntico publicados por bancos | **Confirmada** | La asignación de responsabilidad es "unclear and inefficient", y las disputas "do not involve all relevant parties" | https://business.bofa.com/content/dam/flagship/gps/building-trust-in-agentic-commerce/building-trust-in-agentic-commerce.pdf | Primaria (ASB, BofA, Capital One, CBA, ING, NatWest; voluntario, "non-binding") | 22-sep-2026 |
| 8b | Los principios piden registros auditables, pero los lleva el proveedor del servicio | **Confirmada** | Principio 3.2: "service providers should maintain auditable records to evidence consumer instructions" | mismo PDF | Primaria | 22-sep-2026 |
| 8c | Los principios piden que la responsabilidad siga al origen del error | **Confirmada** | Principio 2.5: "liability outcomes reflecting where risks and errors are introduced" | mismo PDF | Primaria | 22-sep-2026 |
| 9 | **FCA (Reino Unido)**: "Know Your Agent" | **Parcial** | La Mills Review propone que la FCA "consider leading…a trusted framework for AI agent participation". Es una recomendación, no una regla, y no usa la expresión "KYA" | https://www.fca.org.uk/publication/corporate/the-mills-review.pdf | Primaria (informe encargado por la FCA) | 6-jul-2026 |
| 9b | La Mills Review reconoce el problema de atribución | **Confirmada** | "Responsibility becomes harder to attribute as actions are delegated" | mismo PDF | Primaria | 6-jul-2026 |
| 9c | Según la Mills Review, MCP y similares no tienen estándares de auditoría | **Confirmada** | "MCP and others do not have strong identity guarantees, clear mandate structures and strong audit standards" | mismo PDF | Primaria | 6-jul-2026 |
| 9d | El "Know Your Agent" está en el AI Adoption Plan de HM Treasury | **Confirmada** | Pide "standardised identity and verification frameworks" para agentes; liderado "first…by industry" | https://www.gov.uk/government/publications/ai-adoption-plan-financial-services/financial-services-ai-adoption-plan | Primaria (HMT) | 14-jul-2026 |
| 9e | La consulta de HMT sobre servicios de pago decide la responsabilidad | **Refutada** (solo pregunta) | La pregunta 15 consulta si hay que actualizar la "liability for unauthorised payment transactions" | https://www.gov.uk/government/consultations/modernising-payment-services-regulation/modernising-payment-services-regulation-consultation | Primaria | 14-jul a 6-oct-2026 |
| 9f | **PSR (Reino Unido)** se pronunció sobre agentes | **No verificado** | No encontré nada. El plan de HMT no menciona al PSR | — | — | — |
| 10 | **CFPB** emitió una posición sobre agentes y Reg E | **No verificado / no existe** que yo encontrara | Solo aplica el comentario oficial previo 2(m)-2: el consumidor es "fully liable…unless the consumer has notified" | https://www.consumerfinance.gov/rules-policy/regulations/1005/interp-2/ | Primaria (regla vieja, no específica de IA) | vigente |
| 11 | **Fed** se pronunció | **Confirmada** (discurso, no regla) | Waller: "Who is on the hook if an agent makes the wrong purchase?" | https://www.federalreserve.gov/newsevents/speech/waller20260928a.htm | Primaria (discurso en Sibos) | 29-sep-2026 |
| 11b | Waller: la autenticación pasa a ser "probar la autoridad" del agente | **Confirmada** | "proving that an agent has the authority to pay on the buyer's behalf" | mismo | Primaria | 29-sep-2026 |
| 12 | **OCC** se pronunció | **No verificado** | American Banker dice que los bancos actúan "in the absence of clear rules" | https://www.americanbanker.com/news/banks-navigate-ai-risks-solo-as-regulators-play-catch-up | Prensa | 3-nov-2026 |
| 13 | **EBA** se pronunció sobre la responsabilidad por agentes | **No verificado / no encontrado** | El discurso del director ejecutivo de la EBA sobre fraude y PSD3 **no menciona agentes de IA** | https://www.eba.europa.eu/sites/default/files/2026-10/76bb7c6b-29df-4211-b827-2e6b35225067/Payments%20Tomorrow%20Conference%20speech.pdf | Primaria | 16-oct-2026 |
| 14 | **Visa** tiene reglas para transacciones iniciadas por agentes | **Confirmada** | "A Cardholder is responsible for any actions taken by an Agentic Payment Provider" | https://usa.visa.com/content/dam/VCOM/download/about-visa/visa-rules-public.pdf (§4.1.23) | Primaria (Visa Core Rules, edición 24-oct-2026; sección "Last Updated: Apr 2026") | abr / oct-2026 |
| 14b | Visa obliga al proveedor del agente a guardar el consentimiento, pero él mismo es quien lo guarda | **Confirmada** | El proveedor debe "retain this information…and provide it to the Cardholder or Issuer upon written request" | mismo, §4.1.23.3 | Primaria | abr-2026 |
| 14c | Visa exige que el tarjetahabiente acepte su responsabilidad antes de la compra | **Confirmada** | El proveedor debe "obtain Cardholder acknowledgement that they are responsible" | mismo | Primaria | abr-2026 |
| 14d | Visa creó una condición de disputa específica para agentes | **Refutada** (no la encontré) | Solo encontré un agregado a la evidencia de la condición 10.4: "login IDs for an Agentic Payment Provider" | mismo, tabla 11-29 | Primaria | oct-2026 |
| 15 | **Mastercard** tiene reglas de contracargo para agentes | **No verificado** | Las páginas de Mastercard devolvieron 403/404. Según el buscador, Verifiable Intent ofrece un "audit trail" para disputas, sin regla de responsabilidad | — | — | — |
| 16 | **Amex** cubre errores de agentes registrados | **No verificado en primaria** (la página de Amex falló). Según el buscador, cubre compras que se apartan de la intención autenticada y la especificación de registro "under development" | https://www.businesswire.com/news/home/20260414231355/en/ (no abierta) | Prensa / buscador | 14-abr-2026 |
| 17 | Hay un caso documentado de disputa banco–cliente sobre qué autorizó el cliente a su agente | **No verificado / no encontrado** | El único indicio es un incidente anónimo de USD 100.000 que American Banker cita y CSA retoma, sin verificación independiente | https://labs.cloudsecurityalliance.org/research/csa-research-note-banks-block-personal-ai-agents-20261102-cs/ | Secundaria | 2-nov-2026 |

---

## (b) Noticias y documentos relevantes, en orden cronológico

1. **abr-2026.** Visa incorpora a sus Core Rules la sección 4.1.23, "Agentic Platform Requirements": registro en Visa Intelligent Commerce, consentimiento, reconocimiento de responsabilidad del tarjetahabiente y retención del consentimiento por el proveedor. https://usa.visa.com/content/dam/VCOM/download/about-visa/visa-rules-public.pdf
2. **14-abr-2026.** Amex anuncia "Agent Purchase Protection" (no abierto en primaria). https://www.businesswire.com/news/home/20260414231355/en/
3. **26-may-2026.** Mesa redonda de la industria sobre comercio agéntico en la Fed (mencionada por Waller).
4. **6-jul-2026.** Mills Review de la FCA. La recomendación prioritaria 5 propone un "trusted framework" para agentes, con mandatos verificables y estándares para "evidencing control and auditability". https://www.fca.org.uk/publication/corporate/the-mills-review.pdf
5. **14-jul-2026.** HM Treasury publica el AI Adoption Plan (KYA, marco de confianza liderado por la industria) y abre la consulta de servicios de pago, que cierra el 6-oct. https://www.gov.uk/government/publications/ai-adoption-plan-financial-services/financial-services-ai-adoption-plan · https://www.gov.uk/government/consultations/modernising-payment-services-regulation/modernising-payment-services-regulation-consultation
6. **22-sep-2026.** Seis bancos (BofA, Capital One, ING, NatWest, CBA, ASB) publican "Building Trust in Agentic Commerce". https://business.bofa.com/content/dam/flagship/gps/building-trust-in-agentic-commerce/building-trust-in-agentic-commerce.pdf
7. **29-sep-2026.** Waller (Fed) en Sibos: "Who is on the hook…?". https://www.federalreserve.gov/newsevents/speech/waller20260928a.htm
8. **13-oct-2026.** American Banker: ejecutivos de JPMorgan advierten que quien entregue sus credenciales a un agente podría ser responsable. https://www.americanbanker.com/news/jpmorgan-warns-of-risks-to-consumers-who-rely-on-ai-agents
9. **16-oct-2026.** Discurso de la EBA sobre fraude y PSD3, sin mención a agentes. (URL en la tabla, fila 13)
10. **19-oct-2026.** Entra en vigor el nuevo Online Banking Service Agreement de BofA, sin cláusula de IA. https://www.bankofamerica.com/content/documents/agreement/OBSAUpdateEN.pdf
11. **22-oct-2026.** Axios informa que bancos detectan agentes de terceros en cuentas (vía CSA; no lo verifiqué).
12. **24-oct-2026.** Nueva edición de las Visa Core Rules.
13. **27-oct-2026.** Entra en vigor el cambio de JPMorgan (prohíbe usar credenciales a "External AI" y solo permite APIs aprobadas). Según CSA, ese mismo día BofA envía un email a sus clientes.
14. **2-nov-2026.** American Banker: "Wells Fargo wants customers to prove they've revoked AI agents". https://www.americanbanker.com/news/wells-fargo-wants-customers-to-prove-theyve-revoked-ai-agents
15. **3-nov-2026.** American Banker: los bancos gestionan el riesgo de agentes "solos" porque no hay reglas. https://www.americanbanker.com/news/banks-navigate-ai-risks-solo-as-regulators-play-catch-up
16. **11-nov-2026.** Citi (Skift) pide que paguen las empresas de agentes. https://skift.com/?p=848354
17. **nov-2026.** Citi agrega la Sección H a su Online User Agreement. https://www.citi.com/tandc
18. **18-nov-2026.** TechCrunch informa sobre Citi, PNC y Citizens. https://techcrunch.com/2026/11/18/more-banks-says-customers-using-ai-agents-are-on-their-own-even-if-they-get-hacked/
19. **24-nov-2026.** Entra en vigor la Sección 15 del acuerdo de Wells Fargo. https://www.wellsfargo.com/online-banking/online-access-agreement/upcoming

---

## (c) Evidencia en contra de la hipótesis (o que la matiza)

1. **"Quién paga" ya no está abierto entre banco y cliente en EE. UU.: lo resolvió el contrato.**
   - Citi, Wells Fargo, JPMorgan y las reglas de Visa dicen lo mismo: la acción del agente es del cliente. Para agentes que usan credenciales o tokens del cliente, la respuesta hoy es "paga el cliente".
   - Lo que sigue abierto es el tramo **cliente → empresa del agente**: Citi pide que pague el agente, pero ningún mecanismo lo impone.
   - Ninguna corte ni ningún regulador probó estas cláusulas; esto lo dice prensa secundaria y no lo verifiqué en primaria.
2. **No es un régimen nuevo.**
   - El comentario 2(m)-2 de Reg E ya hacía al consumidor "fully liable" si entregaba el acceso a alguien que se excedía, hasta que avisara al banco.
   - BofA aplica la misma regla sin mencionar IA.
   - Los bancos están aplicando a los agentes la lógica vieja de "le prestaste la clave a alguien".
3. **La industria de tarjetas ya está construyendo la capa de evidencia del mandato.**
   - Visa obliga a registrar el consentimiento y la instrucción y a entregarlos al emisor.
   - Mastercard tiene Verifiable Intent (no verificado aquí).
   - Amex condiciona su cobertura a una "intención autenticada" (según el buscador).
   - En el riel de tarjetas, "nadie puede probar" es cada vez menos cierto, aunque el registro lo guarde el proveedor del agente.
4. **Los bancos empujan hacia APIs con consentimiento, no hacia el uso de credenciales.**
   - JPMorgan permite el acceso "through approved application programming interfaces".
   - Con APIs, el banco ve qué agente actuó y con qué alcance, lo que facilita atribuir. Parte del problema puede ser transitorio: lo causa el screen scraping con credenciales prestadas.
5. **No apareció ningún caso documentado de disputa.**
   - No encontré un solo caso con nombre, ni un fallo, en que banco y cliente discutieran qué autorizó el cliente a su agente.
   - Waller describe el comercio agéntico como "early".
   - El daño en dinero hoy **no está demostrado**. Puede ser un problema futuro más que uno actual.
6. **En el Reino Unido y la UE, el regulador todavía no actuó, pero la Mills Review cree que los marcos actuales (Consumer Duty, SMCR) sirven de base.** La EBA ni siquiera menciona a los agentes en su discurso de octubre. Sin un regulador que exija evidencia, la urgencia de compra en Europa es baja.

---

## (d) Qué significa para la hipótesis

**Lo que la evidencia primaria sostiene:**
- **Atribución difícil y sin estándar.** La FCA/Mills ("harder to attribute"), la Fed ("Who is on the hook…?"), los seis bancos ("unclear and inefficient allocation of liability") y Worldpay ("No liability shift exists yet") lo dicen con distintas palabras.
- **"Los registros los lleva la parte interesada."** Visa (§4.1.23.3) obliga al **proveedor del agente** a retener y entregar el consentimiento. Los seis bancos piden que los "service providers" mantengan los registros. La Mills Review pide que las "firms" evidencien la conducta de sus agentes. En ninguno de los tres casos aparece un testigo independiente.
- **La carga de la prueba cayó sobre el cliente, que no tiene herramientas.**
  - Wells Fargo exige que el cliente **guarde y entregue evidencia de revocación** y no monitorea a los agentes.
  - Citi dice que no investigará la autoridad de las acciones.
  - Es el hallazgo más fuerte y más concreto: el contrato le pide al cliente pruebas que hoy no puede producir de forma confiable. En la nota de American Banker, una consultora pregunta qué pasa si el agente "just went bad".

**Lo que la evidencia no sostiene o hay que reformular:**
- "Nadie sabe quién paga" es **falso entre banco y cliente** en EE. UU.: paga el cliente, por contrato. La versión defendible es: *el cliente paga por defecto y no tiene cómo probar que el agente se salió del mandato, ni cuándo lo revocó, para trasladar la pérdida a la empresa del agente.*
- "Problema grande" **no está demostrado en dinero**: no hay casos públicos documentados ni montos. Lo que sí está demostrado es la tendencia regulatoria y contractual.
- En pagos con tarjeta, la evidencia del mandato ya tiene dueños (Visa, Mastercard, Amex). El hueco más claro está **fuera de tarjetas**: acceso por credenciales a la banca en línea, transferencias, y la revocación del mandato, que ningún esquema registra de forma independiente.

**Implicancias para el producto:**
- La cláusula 15(f) de Wells Fargo define un caso de uso literal: un **registro independiente y verificable de otorgamiento y revocación del mandato, y de lo que hizo el agente**, que el cliente pueda presentar al banco y que el banco o la empresa del agente puedan verificar sin confiar en el otro.
- El comprador natural sigue sin estar validado. El consumidor paga poco. Hay tres candidatos con incentivo:
  - las empresas de agentes que quieren acceso aceptado por los bancos (Chase exige identificación y tráfico etiquetado);
  - los emisores, en las disputas;
  - las aseguradoras.
- Hay que validarlo con conversaciones, no con más desk research.

**Pendiente:**
- Texto primario de PNC, Citizens, Mastercard y Amex.
- Cualquier caso real de disputa.
- La posición de la OCC y del PSR.
- El texto del informe de la Consumer Bankers Association (ene-2026).
- El cupo de búsquedas se agotó: retomar en otra sesión.
