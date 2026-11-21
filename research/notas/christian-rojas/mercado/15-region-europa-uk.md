# 15 - Barrido regional: Europa y Reino Unido (seguridad / safety de IA)

Fecha de investigación: 21-nov-2026. Limitación: el presupuesto de búsquedas web se agotó a mitad del trabajo (varias búsquedas devolvieron "too_many_requests"). Por eso Advai, Faculty, Conjecture, Aleph Alpha, Dynamo, Overmind, Trismik, Geordie AI y White Circle NO pudieron verificarse con fuente: figuran como "sin dato". No se usó memoria para cifras.

## 1. Tabla de empresas

| Empresa | País | Qué vende | Última ronda (monto, fecha, inversores) | Evidencia de facturación / clientes | URL |
|---|---|---|---|---|---|
| NeuralTrust | España (Barcelona; una fuente dice también Londres) | Seguridad de agentes de IA: TrustGate (gateway), TrustGuard (runtime), TrustLens (visibilidad) | Seed US$20M (~EUR 17,2M), 17-jun-2026. Lidera Alstin Capital; VentureFriends, Seaya, Kibo Ventures, Banc Sabadell, EA Ventures, Plug and Play Fund, Finaves (IESE). Apoyo público: EIC y AEI. Dealroom lo titula "Series A" (discrepancia) | ARR y clientes: no divulgados (Tech.eu). Dato de la empresa (no verificado): "duplicó su ARR 2025 en un trimestre"; inspecciona millones de interacciones de agentes al día, ~1,2% maliciosas | https://tech.eu/2026/06/17/neuraltrust-closes-20m-to-expand-ai-agent-security-platform/ ; https://dealroom.co/news/134931-neuraltrust-raises-20m-series-a-to-secure-enterprise-ai/ |
| Mindgard | Reino Unido (Londres/Boston; spin-out de Lancaster) | Red teaming automatizado de IA, shadow AI, protección en runtime | Serie A US$30M, 12-ago-2026. Lidera Album VC; Karma Ventures, .406 Ventures, Atlantic Bridge, IQ Capital, Lakestar. Total ~US$42M. (Otra fuente cita ronda previa de US$8M, dic-2024, CB Insights) | Sin ARR ni clientes nombrados. Sectores objetivo: finanzas, gaming, salud, farma, semiconductores. Reclama >150 vulnerabilidades divulgadas. SOC 2 Type 2 | https://www.securityweek.com/mindgard-raises-30-million-to-protect-ai-systems/ ; https://mindgard.ai/blog |
| Trent AI | Reino Unido (Londres) | Plataforma multiagente que escanea código, dependencias, infra y runtime de agentes y parchea/verifica cumplimiento | Seed US$13M, 7-abr-2026 (salida de stealth). LocalGlobe y Cambridge Innovation Capital + ángeles | Sin clientes nombrados | https://www.securityweek.com/trent-ai-emerges-from-stealth-with-13-million-in-funding/ |
| Lakera | Suiza (Zúrich/SF) | Guardrails/firewall de LLM (Lakera Guard), Gandalf red teaming | Serie A US$20M, jul-2024, lidera Atomico (~US$30M total). Adquirida por Check Point, anunciada 16-sep-2025; precio no divulgado (estimación de prensa ~US$300M, no confirmada) | "Fortune 500" (sin nombres); claims propios: >98% detección, <50 ms. Sin ARR | https://www.checkpoint.com/press-releases/check-point-acquires-lakera-to-deliver-end-to-end-ai-security-for-enterprises/ ; https://www.ynetnews.com/business/article/bksoa0dogl |
| Giskard | Francia (París) | Testing / red teaming automatizado de agentes y LLM; open source | Seed: EUR 1,5M (dic-2022, Tech.eu); total ~US$6,6M-8M según fuente (sin reconciliar; Elaia, Bessemer, YC). Oferta de empleo habla de "pasar de Seed a Serie A" (no hay Serie A confirmada) | Clientes en Francia, Bélgica e Italia (según oferta de empleo); sin cifras | https://tech.eu/tag/giskard/ ; https://www.crunchbase.com/organization/giskard-ai |
| Geordie AI | (UK, sin verificar) | Seguridad de agentes de IA | Titular: "salió de stealth con US$6,5M"; inversores y fecha: sin dato | sin dato | (solo titular visto en resultados de https://www.securityweek.com/) |
| Advai, Faculty, Conjecture, Aleph Alpha, Dynamo, Overmind, Trismik, White Circle | UK/FR/DE (sin verificar) | sin dato | sin dato | sin dato | sin dato (no verificados por límite de búsquedas) |

Contexto no europeo (comparable): SplxAI US$7M (mar-2025), General Analysis US$10M seed, Capsule Security US$7M (abr-2026), Ultra Security US$10M (oct-2026). Fuentes: https://www.helpnetsecurity.com/2025/03/26/splxai-funding-7-million/ ; https://www.citybiz.co/article/839605/general-analysis-raises-10-million-seed-round-to-secure-agentic-ai-systems/ ; https://helpnetsecurity.com/2026/04/15/capsule-security-platform/ ; https://fintech.global/2026/10/22/ultra-security-raises-10m-as-ai-agents-outrun-defences/

### Programas públicos
| Programa | Qué financia | Monto | URL |
|---|---|---|---|
| UK AISI - Alignment Project | Investigación de alineamiento | Hasta GBP 1M por proyecto; fondo >GBP 15M; convocatoria cerrada | https://www.aisi.gov.uk/grants |
| UK AISI - Challenge Fund | Investigación de seguridad (académicos/ONG) | Hasta GBP 200.000 por proyecto; abrió 5-mar-2025; cerrada. No es comprador comercial: solo instituciones académicas/sin fines de lucro | https://www.aisi.gov.uk/grants |
| EU: EIC y AEI (España) | Co-financiaron la ronda de NeuralTrust | monto sin dato | https://tech.eu/2026/06/17/neuraltrust-closes-20m-to-expand-ai-agent-security-platform/ |
| ARIA | sin dato (no verificado) | sin dato | sin dato |

## 2. Qué ya está saturado
- Guardrails / firewall de prompts para LLM y red teaming automatizado de modelos: Lakera, Mindgard, Giskard, SplxAI, General Analysis. La consolidación ya empezó: Check Point compró Lakera (sep-2025) y, según prensa, Palo Alto compró Protect AI por ~US$500M en 2025 (https://tech.eu/2026/06/17/neuraltrust-closes-20m-to-expand-ai-agent-security-platform/). Entrar con "otro WAF para prompts" compite contra incumbentes de ciberseguridad.
- Seguridad de agentes en runtime / gateway: muchos seeds de US$5-20M en 2026 (NeuralTrust, Trent AI, Capsule, Asymptote, Ultra). Categoría de moda, aún sin ganador, pero cada vez más concurrida.
- Evidencia de facturación pública casi nula: ninguna de estas rondas publica ARR confirmado. Los ingresos reales son "sin dato".

## 3. Huecos / mar azul
Lo que sigue es inferencia mía sobre las fuentes citadas, no hechos verificados.
1. Cumplimiento operativo del EU AI Act. Fechas vigentes (Comisión): GPAI desde 2-ago-2025; aplicabilidad general y transparencia desde 2-ago-2026; reglas de alto riesgo Anexo III aplazadas a 2-dic-2027 y Anexo I a 2-ago-2028 por el AI Omnibus (en vigor 27-jul-2026); prohibición 9 desde 2-dic-2026. Fuente: https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai . Implicación: demanda de evidencia de conformidad (pruebas, documentación técnica, monitoreo) tiene ventana de ~12-18 meses, y casi ningún jugador de la tabla se vende como "cumplimiento AI Act" (Giskard y Mindgard mencionan compliance, pero no hay datos de ventas). Montos de multas: sin dato verificado.
2. Evaluación de agentes (no solo de modelos) con evidencia auditable, en español y otros idiomas europeos: sin evidencia de oferta en las fuentes revisadas.
3. Financiación pública de safety es casi toda académica (AISI Challenge Fund solo instituciones académicas/ONG), por lo que el comprador comercial queda abierto.
Evidencia de que el problema es grande: rondas crecientes (Mindgard US$30M, NeuralTrust US$20M "mayor seed europeo de ciberseguridad", según la propia empresa) y adquisiciones de Lakera y Protect AI. Evidencia de que no está resuelto: nadie reporta ARR, y NeuralTrust cita ~1,2% de interacciones de agentes maliciosas (dato propio, sin verificar).

## 4. Tres conclusiones
1. Europa ya financia seguridad de agentes y red teaming (rondas de US$13-30M en 2026), pero sin ARR público: hay narrativa de mercado más que prueba de ingresos.
2. La demanda regulatoria es real pero se desplazó: el alto riesgo se aplazó a dic-2027/ago-2028, así que un producto de "evidencia de cumplimiento AI Act" tiene tiempo de construir, no urgencia inmediata.
3. Jugador hispanohablante: NeuralTrust (Barcelona) es el único verificado; no se halló ninguno enfocado en cumplimiento ni en evaluación en español. Pendiente verificar: Advai, Faculty, Conjecture, Aleph Alpha, Dynamo, Overmind, Trismik, Geordie, White Circle, ARIA.
