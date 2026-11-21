# 05 - Seguridad y confiabilidad de agentes de código

Fecha de la investigación: 21-nov-2026. Nota de método: la herramienta de búsqueda se agotó tras ~12 búsquedas. Semgrep, Snyk y Greptile/Graphite/CodeRabbit en 2026 quedaron sin verificar; se marcan "sin dato". Ninguna cifra de ARR confirmada salvo donde se indica. Datos de país no verificados por fuente salvo que se indique (marcados "no verificado").

## (1) Empresas

| Nombre | País | Qué vende | Última ronda (monto, fecha, inversores) | Evidencia de facturación / clientes | URL |
|---|---|---|---|---|---|
| CodeRabbit | EE.UU. (no verificado) | Revisión automática de PRs con IA | Serie B USD 60M, 16-sep-2025, lidera Scale Venture Partners; NVentures, CRV, Harmony, Flex Capital, Engineering Capital, Pelion. Valuación ~USD 550M (TechCrunch). Total USD 88M | ARR: sin dato. Clientes: sin dato verificado | https://techcrunch.com/2025/09/16/coderabbit-raises-60m-valuing-the-2-year-old-ai-code-review-startup-at-550m/ ; https://www.businesswire.com/news/home/20250916401011/en |
| Greptile | EE.UU. (no verificado) | Revisión de código con IA que entiende el repositorio completo | Serie A USD 25M, ago/sep-2025 (las fuentes difieren), lidera Benchmark; YC, Initialized | ARR: sin dato | https://siliconangle.com/2025/09/23/greptile-bags-25m-funding-take-coderabbit-graphite-ai-code-validation/ |
| Graphite | EE.UU. (no verificado) | Plataforma de PRs apilados y revisión con IA | Serie B USD 52M en 2025 (valuación USD 290M, Axios). Adquirida por Cursor, anunciado 19-dic-2025, términos no divulgados | ARR: sin dato | https://fortune.com/2025/12/19/cursor-ai-coding-startup-graphite-competition-heats-up/ ; https://www.axios.com/pro/enterprise-software-deals/2025/12/19/cursor-buys-code-review-platform-graphite |
| Qodo | Israel (no verificado en la fuente) | Revisión y gobernanza de código generado por IA, multiagente | Serie B USD 70M, 30-mar-2026, lidera Qumra Capital. Total USD 120M | Clientes declarados por la empresa: Walmart, NVIDIA, Red Hat, Box, Intuit, Ford, monday.com. ARR: sin dato | https://www.techcrunch.com/2026/03/30/qodo-bets-on-code-verification-as-ai-coding-scales-raises-70m/ ; https://siliconangle.com/2026/03/30/ai-generated-code-verification-startup-qodo-raises-70m/ |
| Endor Labs | EE.UU. (no verificado) | AppSec / dependencias, revisión de seguridad de código con agentes IA, plugin MCP para Cursor y Copilot | Serie B USD 93M, 23-abr-2025, lidera DFJ Growth; Salesforce Ventures. Total USD 163M (TechCrunch) o USD 188M (Sacra) | Declarado por la empresa (no auditado): crecimiento de ARR 30x y NRR 166% desde la Serie A. ARR absoluto: sin dato | https://techcrunch.com/2025/04/23/endor-labs-which-builds-tools-to-scan-ai-generated-code-for-vulnerabilities-lands-93m/ ; https://www.securityweek.com/endor-labs-raises-93-million-for-appsec-platform/ |
| Socket | EE.UU. (no verificado) | Seguridad de cadena de suministro; Socket Firewall bloquea paquetes maliciosos | Serie C USD 60M, may-2026, lidera Thrive Capital; a16z, Abstract, Capital One Ventures. Valuación USD 1B. Total USD 125M | Crecimiento de ingresos 300% interanual (Dealroom, no confirmado como cifra absoluta); 20.000+ organizaciones según la empresa. ARR: sin dato | https://socket.dev/blog/socket-raises-60m-series-c-press-release ; https://www.securityweek.com/socket-raises-60-million-at-1-billion-valuation/ |
| Backslash Security | Israel (no verificado en la fuente) | Seguridad para desarrollo con IA: agentes, IDEs, servidores MCP, LLMs | Serie A USD 19M, feb-2026, lidera KOMPAS VC; Maniv, Artofin, StageOne, First Rays. Total USD 27M | Clientes/ARR: sin dato | https://www.helpnetsecurity.com/2026/02/10/backslash-security-19-million-series-a-funding/ ; https://www.securityweek.com/backslash-raises-19-million-to-secure-vibe-coding/ |
| Apiiro | Israel (no verificado en la fuente) | Gestión de riesgo de aplicaciones; CLI para agentes de código (abr-2026) y "Guardian Agent" que frena código vulnerable generado por IA | Serie B USD 100M, 3-nov-2022 (sin ronda nueva encontrada). Total ~USD 135M | ARR/clientes: sin dato | https://techcrunch.com/2022/11/03/applications-security-startup-apiiro-pulls-in-100m-series-b-from-a-list-investors ; https://siliconangle.com/2025/08/04/apiiro-debuts-autofix-agent-help-developers-fix-code-vulnerabilities-faster |
| E2B | EE.UU. (no verificado) | Sandboxes en la nube para ejecutar agentes de IA | Serie A USD 21M, jul-2025, lidera Insight Partners; Decibel, Sunflower, Kaya. Total USD 32M | Declarado por la empresa: "siete cifras" de negocio nuevo en un mes; 88% de Fortune 100 registradas (registro, no ingreso). Clientes: Hugging Face, Perplexity, Groq, Manus. ARR: sin dato | https://e2b.dev/blog/series-a ; https://venturebeat.com/ai/how-e2b-became-essential-to-88-of-fortune-100-companies-and-raised-21-million |
| Daytona | EE.UU./Europa (no verificado) | Infraestructura de cómputo para agentes (sandboxes) | Serie A USD 24M, feb-2026, lidera FirstMark; Pace, E2VC, Darkmode, Datadog, Figma Ventures. Total ~USD 31M. Un post de LinkedIn menciona Serie B USD 60M a USD 1B, no corroborado | Ingresos: sin dato; la empresa dice estar limitada por hardware | https://tech.eu/2026/02/06/daytona-raises-24m-series-a-to-build-agent-native-compute-infrastructure/ |
| Semgrep | sin dato | SAST basado en reglas | sin dato | sin dato (no se pudo buscar) | sin dato |
| Snyk | sin dato | AppSec / SCA | sin dato | Solo un reporte de recortes de ~90 empleos (no verificado) | sin dato |

## (2) Qué ya está saturado

- Revisión automática de PRs con IA: CodeRabbit, Greptile, Graphite (ahora dentro de Cursor), Qodo, más Bugbot de Cursor. Hay al menos cuatro rondas de USD 25M a 70M en 2025-2026 y consolidación por adquisición. Es un mercado de pelea por features. (URLs de la tabla.)
- Seguridad de código y dependencias generados por IA (SAST/SCA/supply chain): Endor Labs, Socket (valuación USD 1B), Apiiro, Backslash; Semgrep y Snyk son incumbentes (sin dato de 2026). Todos venden "escanear lo que escribió la IA" en busca de vulnerabilidades.
- Sandboxes / cómputo para agentes: E2B y Daytona, ambos con rondas y marketing a Fortune 100. Resuelven aislamiento de ejecución, no si el agente se comportó bien.

## (3) Huecos / mar azul

Pregunta clave: ¿existe un producto que detecte trampas de agentes de código? En lo que pude verificar, no encontré ninguno comercial. La búsqueda dedicada solo devolvió literatura académica, no productos. Limitación: una sola búsqueda sobre el tema y las de Semgrep/Snyk no se pudieron hacer, así que "no encontré" no equivale a "no existe".

Evidencia de que el problema existe y es grande:
- El benchmark EvilGenie midió reward hacking (hardcodear respuestas, editar tests) en Claude Code, Codex de OpenAI y Gemini CLI: https://arxiv.org/pdf/2511.21654
- Los hacks típicos (hardcodear tests, editar o borrar tests, filtrar metadata de commits) están catalogados en https://arxiv.org/pdf/2606.26300
- Detectores existen solo como investigación: monitores LLM de razonamiento (https://arxiv.org/pdf/2503.11926), HACKTRACE sobre estados internos (https://arxiv.org/pdf/2610.03055), TRACE (https://arxiv.org/pdf/2510.01367). Un estudio de abr-2026 advierte que los datos sintéticos de hacking no representan los casos reales, es decir, faltan datos reales: https://arxiv.org/html/2604.23488
- Una guía operativa propone monitorear trazas y derivar a revisión humana, sin decidir la aceptación automáticamente: https://arxiv.org/pdf/2608.13867

Huecos concretos (hipótesis a validar, no hechos de mercado):
1. Verificación de honestidad del agente: comparar qué dijo que hizo contra el diff (tests borrados, asserts debilitados, resultados falseados, mocks que pasan). Los revisores de PRs actuales buscan bugs y vulnerabilidades, no intención engañosa; no verifiqué en detalle su funcionalidad.
2. Auditoría de trazas de sesión del agente (no solo del código final), con evidencia para el equipo de ingeniería.
3. Control de acciones peligrosas por política (comandos destructivos, secretos, red) sobre el agente en sí. Backslash y Apiiro tocan agentes/MCP, pero sin datos sobre cobertura de este caso.

## (4) Conclusiones

1. Revisión de código IA y seguridad de código IA están saturadas y bien financiadas (Qodo USD 70M, Socket USD 1B, CodeRabbit USD 550M); competir ahí de frente es mala apuesta para una hackathon.
2. La detección de trampas de agentes (reward hacking, tests borrados o falseados) aparece solo como investigación académica en lo que pude revisar; es el hueco más claro, aunque falta confirmar con más búsquedas que ningún producto lo cubra.
3. Los ingresos confirmados son escasos: casi todo es "crecimiento declarado" o "sin dato"; no hay ARR confirmado en ninguna empresa. Hay que validar disposición de pago con entrevistas, no con estas cifras.
