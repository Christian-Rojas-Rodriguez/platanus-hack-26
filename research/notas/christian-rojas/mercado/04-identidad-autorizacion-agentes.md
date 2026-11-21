# Identidad, autorización y "know your agent" para agentes de IA

Fecha de la investigación: 21-nov-2026. Se agotó el cupo de búsquedas web a mitad de la investigación (límite de la herramienta), por lo que Natoma, Stytch, Visa/Mastercard (montos) y Auth0 quedaron con cobertura parcial. "sin dato" = no verificado con fuente en esta pasada.

Nota sobre ingresos: ninguna de las empresas de abajo publicó ARR confirmado en las fuentes consultadas. Lo que hay son clientes nombrados y rondas.

## 1. Tabla de empresas

| Empresa | País | Qué vende | Última ronda (monto, fecha, inversores) | Evidencia de facturación o clientes | URL |
|---|---|---|---|---|---|
| Oasis Security | EE.UU. (NY), origen israelí | "Agentic Access Management": acceso just-in-time, vaulting, federación y permisos efímeros para identidades no humanas y agentes | Serie B US$120M, 19-mar-2026. Lidera Craft Ventures; Cyberstarts, Sequoia, Accel. Total ~US$195M (SiliconANGLE dice US$190M) | ARR: sin dato. Clientes: sin nombres. El CEO dice solo "lo vemos en nuestra base de clientes" | https://www.securityweek.com/oasis-security-raises-120-million-for-agentic-access-management/ ; https://fintech.global/2026/03/20/oasis-security-lands-120m-to-govern-enterprise-ai-agents/ |
| Astrix Security | Israel | Seguridad de identidades no humanas (service accounts, API keys, agentes) | Serie B US$45M, 10-dic-2024. Lidera Menlo Ventures; Workday Ventures, BVP, CRV, F2. Total ~US$85M (otras fuentes dicen US$95M). Ronda posterior: sin dato | Clientes citados: Workday, NetApp, Priceline, Figma. ARR: no divulgado | https://www.securityweek.com/astrix-security-banks-45m-series-b-to-secure-non-human-identities/ |
| Aembit | EE.UU. | Workload IAM: acceso sin secretos (tokens de corta vida) entre workloads y recursos; posicionado también para agentes | Serie A US$25M, 12-sep-2024. Lidera Acrew; Ballistic, CrowdStrike Falcon Fund, Okta Ventures, Ten Eleven. Total ~US$45M. Serie B: no aparece | Clientes citados (2024): Snowflake, un minorista Fortune 250, una empresa global de property management. ARR: sin dato | https://www.securityweek.com/non-human-iam-provider-aembit-raises-25-million/ |
| Keycard | EE.UU. (SF) | Identidad y acceso para agentes: broker federado, tokens dinámicos por tarea en vez de API keys, revocación con una llamada, soporta MCP/WIMSE/OAuth | US$38M total, 22-oct-2025: semilla US$8M (a16z, Boldstart) + Serie A US$30M (lidera Acrew; Essence, Exceptional, Mantis, otros) | Sin clientes nombrados ni métricas; recién salió de stealth | https://www.securityweek.com/keycard-emerges-from-stealth-mode-with-38-million-in-funding/ ; https://www.biometricupdate.com/202510/agentic-ai-boom-continues-with-funding-for-keycard-protocols-for-payment-giants |
| Skyfire | EE.UU. | Red de pagos para agentes (wallets USDC con límites de gasto), protocolo KYAPay, "Agent Checkout" | Semilla US$8.5M, ago-2024 (Neuberger Berman, Inception, Arrington, otros); extensión con Coinbase Ventures y a16z CSX, total US$9.5M, oct-2024. Ronda posterior: sin dato | Facturación: sin dato. Hay lanzamiento de red y adopción anunciada por nota de prensa (no verificada en profundidad) | https://www.theblock.co/post/322742/coinbase-ventures-and-a16zs-csx-bring-skyfires-total-funding-raised-to-9-5-million ; https://www.businesswire.com/news/home/20241024532897/en/AI-Agents-Race-to-Join-Skyfire-Payments-Network |
| Descope | EE.UU. | CIAM con "Agentic Identity Hub": identidad para agentes y servidores MCP, SSO para agentes, "Envoy" (acceso delegado para agentes personales) | Semilla US$53M, feb-2023 (Lightspeed, GGV). Ronda posterior: sin dato | Clientes de Envoy como socios de diseño: GoFundMe, GoodRx (según su blog, nov-2026). Gartner lo lista como vendor de muestra "CIAM for AI Agents" (ago-2026). ARR: sin dato | https://www.descope.com/blog |
| Auth0 for AI Agents (Okta) | EE.UU. | Autorización fina (FGA) y auditoría para agentes dentro de la plataforma Auth0 | No aplica (producto de Okta) | Estado GA, precios y clientes: sin dato en la página consultada | https://www.auth0.com/ai |
| Stytch | EE.UU. | Auth para apps y agentes | sin dato (no se alcanzó a verificar; no afirmo la adquisición por Twilio sin fuente) | sin dato | sin dato |
| Natoma | EE.UU. | Gobierno de acceso de agentes / MCP | sin dato (búsqueda no completada) | sin dato | sin dato |

### Protocolos / incumbentes (no son startups, definen el estándar)

| Protocolo | Qué hace | URL |
|---|---|---|
| Google AP2 (16-sep-2025) | "Mandates" firmados con verifiable credentials: Intent Mandate (reglas del usuario para el agente) y Cart Mandate (carrito aprobado). Forman una cadena de auditoría no repudiable. +60 socios (Adyen, AmEx, Coinbase, Mastercard, PayPal, Revolut, Salesforce, Worldpay, etc.). Extensión x402 con Coinbase para cripto | https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol |
| Visa Trusted Agent Protocol (oct-2025) | Señala intención del agente, reconoce al consumidor detrás del agente y transmite credenciales de pago | https://www.biometricupdate.com/202510/agentic-ai-boom-continues-with-funding-for-keycard-protocols-for-payment-giants |
| Mastercard Agent Pay (marco de aceptación para comercios, oct-2025) | Registra y autentica agentes antes de la transacción | misma fuente |
| Cloudflare Web Bot Auth | Base de firma de agentes usada por Visa y Mastercard; AmEx planea adoptarlo | misma fuente |

## 2. Qué ya está saturado

- Identidades no humanas (NHI) para workloads y service accounts, y "agentic access management" para empresas: Oasis (US$120M Serie B en 2026), Astrix, Aembit, Keycard, además de Descope y Auth0 desde el lado CIAM. Hay mucho capital y mensajes casi idénticos ("tokens efímeros por tarea, sin secretos estáticos").
- Estándares de mandato/pago de agentes liderados por incumbentes (AP2, Visa TAP, Mastercard Agent Pay, x402): competir en el protocolo contra Google/Visa/Mastercard no es viable para un equipo de hackathon.
- Inferencia mía: el eje "darle credenciales a un agente con permisos mínimos" ya es mercado de producto con muchas ofertas.

## 3. Huecos / mar azul

La pregunta clave: quién prueba qué autorizó realmente el humano y qué hizo el agente. Lo observado en las fuentes:

- Los productos de IAM (Keycard, Oasis, Descope) se describen en torno a emitir credenciales, aplicar políticas en runtime y "rastrear actividad". Ninguna fuente consultada menciona un recibo verificable de extremo a extremo que ate la instrucción humana original, las decisiones del agente y las acciones reales sobre sistemas.
- AP2 sí define mandatos firmados y cadena no repudiable, pero solo para pagos/carritos. No cubre acciones no financieras (enviar correos, modificar datos, ejecutar código, llamadas a APIs) ni el vínculo entre lo que el agente "razonó" y lo que ejecutó.
- Auth0 menciona auditoría por acción, pero no hay evidencia en lo consultado de un registro independiente verificable por un tercero (aseguradora, auditor, contraparte, juez).
- Candidatos de nicho (hipótesis, sin verificar con fuente): (a) recibos firmados "mandato -> acción -> resultado" para acciones generales de agentes, neutrales al proveedor de identidad; (b) verificación del lado receptor (la contraparte comprueba que el agente de verdad tiene autorización humana vigente y su alcance); (c) disputas y atribución de responsabilidad cuando un agente actúa fuera de mandato; (d) delegación entre agentes (agente que contrata subagentes) con cadena de autoridad atenuada.
- Evidencia de que el tema es grande (indirecta): rondas de US$120M (Oasis, 2026), US$38M (Keycard, 2025) y Gartner clasificando "CIAM for AI Agents" en 2026. Evidencia de que no está resuelto: la proliferación de protocolos paralelos (AP2, TAP, Agent Pay, x402, KYAPay) y el lanzamiento continuo de nuevas versiones (Descope Hub 3.0 en oct-2026) sugieren que no hay estándar dominante. Falta una cifra duro de pérdidas por acciones no autorizadas de agentes: sin dato.

## 4. Tres conclusiones

1. El IAM para agentes (emitir y limitar credenciales) está saturado y bien financiado; entrar ahí es competir con US$195M de Oasis y con Okta/Auth0. No conviene.
2. El hueco más defendible es la prueba, no el permiso: un recibo firmado y verificable por terceros que una la autorización humana original con las acciones reales del agente, más allá de pagos (donde AP2 ya cubre carritos). Es una hipótesis razonada; ninguna fuente confirma que nadie lo venda hoy.
3. Ningún dato de ARR está confirmado en este segmento; hay rondas y logos de clientes, no ingresos. Antes de apostar, validar con 3-5 entrevistas (CISOs, equipos de pagos, aseguradoras) y repetir la búsqueda para Natoma, Stytch y Skyfire (rondas posteriores a 2024), que quedaron sin verificar.
