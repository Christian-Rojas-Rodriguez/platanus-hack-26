# 03 - Seguridad de servidores MCP y herramientas de agentes

Fecha del research: 21-nov-2026. Limite: el presupuesto de busquedas web se agoto tras ~10 busquedas utiles; faltan Cloudflare, Obot (detalle), MintMCP, Zenity, Prompt Security y adquisiciones 2026 (todo "sin dato" abajo). Las cifras vienen de prensa secundaria; ninguna es ingreso/ARR confirmado.

## 1. Tabla de empresas

| Nombre | Pais | Que vende | Ultima ronda (monto, fecha, inversores) | Evidencia de facturacion o clientes | URL |
|---|---|---|---|---|---|
| Runlayer | EEUU (sin dato de sede exacta) | Plataforma MCP: gateway + deteccion de amenazas + observabilidad, en nube propia o del cliente | Serie A US$30M, 25-jun-2026, lidera Felicis, con Khosla Ventures; total US$42M. Seed US$11M, 17-nov-2025 (Khosla, Felicis; anuncia "8 unicornios" como inversores) | Dice estar adoptado por empresas Fortune 500 (sin nombres). Sin ARR/ingresos publicados (reportado, no confirmado) | https://www.securityweek.com/runlayer-raises-30-million-in-series-a-funding/ ; https://techcrunch.com/2025/11/17/mcp-ai-agent-security-startup-runlayer-launches-with-8-unicorns-11m-from-khoslas-keith-rabois-and-felicis |
| Noma Security | Israel / EEUU | Seguridad de IA y agentes (postura, gobernanza, cumplimiento) | Serie B US$100M, 31-jul-2025, lidera Evolution Equity Partners; Ballistic Ventures y Glilot. Valuacion ~US$400M segun fuentes de Globes (rumor). Total ~US$132M | Sin dato de ingresos ni clientes en lo que lei | https://www.securityweek.com/noma-security-raises-100-million-for-ai-security-platform/ ; https://en.globes.co.il/en/article-ai-and-agent-security-co-noma-raises-100m-1001517758 |
| Invariant Labs (adquirida por Snyk) / MCP-Scan | Suiza (spin-off ETH Zurich) | Escaner de servidores MCP (tool poisoning), guardrails y trazado de agentes | Sin fondos externos divulgados; adquirida por Snyk el 24-jun-2025, precio no divulgado | Integrada en la plataforma "AI Trust" de Snyk y en Snyk Labs; ~10 empleados. Sin dato de facturacion propia | https://snyk.io/news/snyk-acquires-invariant-labs-to-accelerate-agentic-ai-security-innovation ; https://siliconangle.com/2025/06/24/snyk-acquires-invariant-labs-expand-ai-agent-security-capabilities/ |
| Lasso Security | Israel | Seguridad LLM/GenAI; MCP Gateway open source (abr-2025); guardrail LEAP | US$30M (reportado 2-sep-2026), lidera ClearSky Advisors. Antes: seed US$6M, nov-2023 (Entree Capital, Samsung Next) | Alianza con Portkey para gateway MCP. Sin dato de ingresos | https://siliconangle.com/?p=837891 ; https://securitybrief.co.uk/story/lasso-launches-ai-guardrail-leap-raises-usd-30m ; https://portkey.ai/blog/securing-mcp-to-deliver-enterprise-grade-agentic-ai-protection/ |
| Operant AI | EEUU | Runtime protection cloud/API/IA; MCP Gateway (jun-2025) dentro de AI Gatekeeper | Serie A US$10M, sep-2024, co-lideran SineWave Ventures y Felicis; total ~US$13-13.5M. Sin ronda posterior hallada | Sin dato de clientes ni ingresos | https://www.securityweek.com/operant-ai-lands-10m-investment-to-boost-runtime-protection-for-cloud-and-ai/ ; https://siliconangle.com/2025/06/16/operant-ai-expands-gatekeeper-platform-mcp-gateway-ai-runtime-security |
| Pillar Security | EEUU (Miami) / Israel | Seguridad del ciclo de vida de software con IA | Seed US$9M, 16-abr-2025, lidera Shield Capital; Golden Ventures, Ground Up Ventures | Sin dato de ingresos ni clientes | https://siliconangle.com/2025/04/16/pillar-security-raises-9m-address-growing-ai-specific-security-risks |
| Obot AI | EEUU (sin verificar) | Plataforma/gateway MCP (adopcion empresarial) | Seed US$3.5M segun titular de HPCwire; fecha e inversores: sin dato (no abri el articulo) | Sin dato | https://www.hpcwire.com/bigdatawire/this-just-in/obot-ai-secures-35m-seed-round-to-drive-adoption-of-model-context-protocol/ |
| Docker (MCP Catalog / Gateway / Enterprise Gateway) | EEUU | Catalogo de servidores MCP "verificados" (imagenes firmadas, SBOM), gateway open source; Enterprise Gateway de pago con auth por usuario, politica por llamada y auditoria | No aplica (empresa establecida) | Producto comercial en venta; sin cifras. Docker admite que la verificacion de terceros es "best effort" y no exhaustiva | https://www.docker.com/products/mcp-enterprise-gateway/ ; https://docs.docker.com/ai/mcp-catalog-and-toolkit/faqs/ |
| Cloudflare | EEUU | Sin dato (no se pudo buscar) | Sin dato | Sin dato | sin dato |

Nota: no pude verificar Cloudflare, MintMCP, Zenity ni Prompt Security por limite de busquedas.

## 2. Que ya esta saturado

- Gateways/proxies MCP con autenticacion, politicas y logs: Runlayer, Lasso (open source), Operant, Obot, Docker (gratuito y enterprise), mas integraciones tipo Portkey. Hay al menos 5-6 actores, y varios con rondas de US$10-30M.
- Escaneres estaticos de servidores MCP / deteccion de tool poisoning: MCP-Scan de Invariant ya fue absorbido por Snyk; es un nicho con duenio grande.
- Plataformas generalistas de "seguridad de IA y agentes": Noma (US$100M Serie B), Pillar, Lasso. Competir de frente con ellas no tiene sentido en un hackathon.
- Catalogos "verificados" de servidores: Docker ya ofrece firma + SBOM + procedencia.
- Mitigacion basica de rug pull por hash/pinning de manifiesto: ya existe en gateways (p. ej. Pipelock, segun una fuente de blog) y en articulos practicos.

## 3. Huecos / mar azul

Evidencia de que el problema existe: el rug pull y el tool poisoning estan documentados como categorias de ataque (CSA, mayo y julio de 2026; OWASP MCP03:2025 segun un blog secundario). Fuentes: https://labs.cloudsecurityalliance.org/wp-content/uploads/2026/05/CSA_whitepaper_mcp_security_tool_poisoning_20260506-csa-styled.pdf ; https://reversinglabs.com/blog/mcp-rug-pull-attack-worries . Un blog cita 2.000+ instancias MCP expuestas filtrando claves (Shodan, ene-2026); no verificado en fuente primaria: https://dev.to/luckypipewrench/your-mcp-servers-tool-descriptions-are-an-attack-surface-37pj . ReversingLabs cuenta que publicar una herramienta MCP capaz de manipular a un agente toma ~10 minutos.

Huecos candidatos (mi inferencia a partir de lo hallado; no demostrado que "no exista" producto):

1. Diff semantico entre versiones de herramientas. Lo que encontre es hash/pinning (cambia un byte, alerta) y diff textual. Una fuente senala que el hash no detecta una herramienta envenenada desde el primer `tools/list` (no hay referencia previa) ni el payload dentro de la llamada. No hallé producto que juzgue si un cambio de descripcion altera el significado/intencion (p. ej. agrega instruccion oculta) y lo clasifique por riesgo. Fuente: https://dev.to/alex_spinov/mcp-tool-drift-pin-the-manifest-block-rug-pulls-in-40-lines-4mlp ; https://dev.to/node9_ai/the-mcp-rug-pull-when-the-tool-you-trusted-yesterday-becomes-malicious-today-4om
2. Medicion empirica: la busqueda no hallo ningun estudio de 2026 que mida cuantos servidores MCP cambian sus definiciones o carecen de pinning. Hueco de datos y de benchmark.
3. Benchmarks de control/seguridad con MCP (evaluar si un agente resiste herramientas envenenadas o respeta politicas): no encontre uno establecido en estas busquedas; "sin dato" sobre su inexistencia total, hay que verificarlo.
4. Verificacion de terceros en registros: Docker admite que es best effort; ETDI (propuesta academica, jun-2025) apunta a firmar definiciones de herramientas pero no vi adopcion comercial.
5. Rug pull en el eje del tiempo: monitoreo continuo de servidores remotos de terceros (no solo los del catalogo propio).

## 4. Tres conclusiones

1. El segmento "gateway MCP / plataforma de seguridad de agentes" esta lleno y financiado (Runlayer US$42M en total, Noma US$100M, Lasso US$30M); un gateway nuevo en un hackathon no diferencia. Ninguna de estas cifras es ingreso confirmado: no hay ARR publico en ninguna fuente revisada.
2. La oportunidad mas defendible es detectar cambios de significado en herramientas MCP entre versiones (diff semantico + clasificacion de riesgo), porque lo existente es hash/pinning y no cubre cambios sutiles ni el primer listado. Es una inferencia a validar.
3. Un benchmark abierto + dataset de drift de herramientas MCP (medir que tan seguido y como cambian los servidores publicos, y si agentes/gateways detectan los cambios maliciosos) aprovecha la falta de datos hallada y es factible en 48 horas; antes de comprometerse, verificar con una busqueda extra que no exista ya.
