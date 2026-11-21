# Guardrails y "AI firewalls" en runtime para apps con LLM

Fecha de la investigación: 21-nov-2026.

Limitación: la herramienta de búsqueda llegó a su límite de uso tras 3 búsquedas (2 fallidas). Solo valen los datos con URL abajo. Todo lo demás figura como "sin dato" o "sin verificar". Este documento es una base incompleta y requiere una segunda pasada.

Convención: [C] = confirmado en fuente primaria o prensa. [R] = recuerdo no verificado.

## (1) Tabla de empresas

| Empresa | País | Qué vende | Última ronda / M&A | Facturación o clientes | URL |
|---|---|---|---|---|---|
| Lakera (Lakera Guard) | Suiza / EE.UU. | Firewall de runtime para prompts y respuestas (Lakera Guard) | Check Point anunció el acuerdo de adquisición el 16-sep-2025; cierre previsto Q4 2025, sin confirmar cierre en la fuente. Precio: sin dato (no divulgado). Rondas previas: sin dato. [C] | "Fortune 500" sin nombres. ARR: sin dato. [C] | https://www.checkpoint.com/press-releases/check-point-acquires-lakera-to-deliver-end-to-end-ai-security-for-enterprises/ |
| Protect AI | EE.UU. | Escaneo de modelos, postura, red teaming y runtime. Hoy es parte de Prisma AIRS | Palo Alto Networks completó la adquisición el 22-jul-2025. Precio: sin dato en la fuente. [C] | Leidos y TELUS Digital como usuarios de la oferta combinada. ARR: sin dato. [C] | https://www.paloaltonetworks.com/company/press/2025/palo-alto-networks-completes-acquisition-of-protect-ai |
| Lasso Security | Israel | Guardrails para LLM y agentes. Producto LEAP (guardrail solo CPU, veredicto <5 ms, benchmarks propios) | Ronda de US$30M anunciada el 2-sep-2026. Liderada por ClearSky Advisors, con Entrée Capital, iAngels, Singtel Innov8, Mindset y Swish Data. Total acumulado >US$37M. Seed previo de US$6M en nov-2023 (Entrée, Samsung Next). [C] | Clientes citados: BMW, eToro, Fiverr, US DHS. Crecimiento de ingresos ">500% en 12 meses" declarado por la empresa; cifra absoluta: sin dato. Es una declaración de la empresa, no una cifra auditada. No hace claims multilingües en esa nota. | https://siliconangle.com/2026/09/02/lasso-security-launches-cpu-only-ai-guardrail-raises-30m/ ; https://www.darkreading.com/application-security/lasso-security-emerges-from-stealth-with-6m-seed-funding-for-gen-ai-and-advanced-llm-cybersecurity |
| NeuralTrust | España (oficina en Barcelona; también NY y Londres) | Runtime Security para agentes (TrustGuard), gateway (TrustGate), red teaming | Ronda: sin dato (no se encontró). | Logos en su web: Sabadell, Iberia, Abanca, Isdin, Air Europa, Capgemini, NTT Data, Devoteam. Dice "1000+ aplicaciones monitoreadas" y "99% detección multilingüe", sin metodología visible. Ingresos: sin dato. | https://neuraltrust.ai |
| Prompt Security | Israel | Seguridad GenAI / firewall de prompts | [R] SentinelOne la adquirió en 2025, precio reportado ~US$250M. Sin verificar (la fetch falló con 429). | Sin dato | sin URL verificada |
| Aim Security | Israel | Seguridad de uso de IA generativa | [R] Cato Networks la adquirió en 2025. Sin verificar. | Sin dato | sin URL verificada |
| CalypsoAI | EE.UU. | Guardrails / gateway de seguridad para IA | Sin dato verificado | Sin dato | sin URL verificada |
| Robust Intelligence | EE.UU. | Validación y firewall de IA | [R] Adquirida por Cisco (2024). Sin verificar. | Sin dato | sin URL verificada |
| Zenity | EE.UU. / Israel | Seguridad de agentes de IA | Sin dato verificado | Sin dato | sin URL verificada |
| Guardrails AI | EE.UU. | Framework abierto de guardrails y hub de validadores | Sin dato verificado | Sin dato | sin URL verificada |
| Llama Guard 3 (Meta) | EE.UU. | Clasificador abierto de seguridad. Idiomas oficiales: inglés, francés, alemán, hindi, italiano, portugués, español, tailandés | No aplica (modelo abierto) | No aplica | https://huggingface.co/meta-llama/Llama-Guard-3-8B |
| Qwen3Guard (Alibaba) | China | Clasificador abierto (0.6B, 4B, 8B). Declara soporte de hasta 119 idiomas y dialectos | No aplica | No aplica | https://arxiv.org/abs/2510.14276 |
| ShieldGemma (Google) | EE.UU. | Clasificador abierto de seguridad | Sin verificar | No aplica | sin URL verificada |

## (2) Qué ya está saturado

- Consolidación. Las empresas verificadas de la categoría "firewall de prompts" ya fueron absorbidas por plataformas grandes: Lakera por Check Point (sep-2025) y Protect AI por Palo Alto (jul-2025). Por recuerdo no verificado, también Prompt Security (SentinelOne) y Aim (Cato). Los compradores son vendors de seguridad de red, endpoint y SASE. Ese es un patrón fuerte: "guardrail de runtime para chatbot" pasó a ser una función de plataforma.
- Hay muchos vendors con el mismo mensaje (detectar prompt injection, jailbreak y fuga de datos en línea). Lasso compite ahora en latencia y costo (CPU, <5 ms). La diferenciación se está moviendo a latencia y a la protección de agentes.
- Los clasificadores abiertos (Llama Guard, Qwen3Guard, ShieldGemma) bajan el valor de un clasificador genérico de seguridad de contenido. Cualquiera puede desplegarlos gratis.
- Conclusión parcial: competir en "otro filtro de entrada/salida en inglés" es entrar a un mercado ya consolidado.

## (3) Huecos / mar azul

1. Guardrails multilingües fuera del inglés (español, portugués, español rioplatense y regional).
   - Evidencia de que el problema existe: un estudio académico encontró que las defensas de GPT-4 fallan al traducir peticiones dañosas a idiomas de pocos recursos, con ~79% de respuestas dañosas en AdvBench. Los idiomas de recursos altos y medios tuvieron tasas mucho menores (https://arxiv.org/abs/2310.02446). Ojo: el español y el portugués son de recursos altos, así que la brecha es menor ahí. Este estudio NO prueba que el español falle gravemente.
   - Llama Guard 3 declara cobertura de español y portugués con F1 entre ~0.83 y ~0.94 en idiomas no ingleses, con prueba interna de Meta. La tarjeta advierte que la capacidad multilingüe puede estar limitada por los datos de preentrenamiento (https://huggingface.co/meta-llama/Llama-Guard-3-8B). Es evidencia de calidad más baja y no medida de forma independiente.
   - Quién lo vende como diferenciador: NeuralTrust dice "99% detección multilingüe en cualquier idioma" (https://neuraltrust.ai). No hay benchmark público verificable. Qwen3Guard declara 119 idiomas (https://arxiv.org/abs/2510.14276). Lasso y los vendors adquiridos: no se encontró claim multilingüe en las fuentes revisadas.
   - Sin dato: no encontré un benchmark independiente que mida jailbreaks en español rioplatense, portugués brasileño o spanglish. Tampoco encontré datos de cuánto pierden los firewalls comerciales fuera del inglés. Ese vacío de medición es en sí una oportunidad: un benchmark abierto y reproducible en español y portugués.
2. Seguridad de agentes (herramientas, permisos, acciones), no solo texto. Lasso ya habla de "decenas de miles de agentes" y NeuralTrust vende gateway para agentes. Ese espacio se está llenando rápido, así que falta evidencia de que esté sin resolver (sin dato).
3. Evaluación independiente de guardrails (no hay un estándar público de calidad de los firewalls). Hipótesis, sin fuente.

Advertencia: no pude verificar tamaño de mercado, tasas de falla de productos comerciales ni ARR de ninguna empresa. "Grande y sin resolver" está respaldado solo parcialmente (puntos arriba).

## (4) Tres conclusiones

1. El firewall genérico de prompts en inglés está consolidado: las dos adquisiciones verificadas (Lakera y Protect AI) lo confirman. Un equipo de hackathon no debería competir ahí.
2. La oportunidad más defendible y concreta es medir y mejorar guardrails en español y portugués (incluyendo dialectos y jailbreaks mezclando idiomas). Hay claims de marketing multilingües (NeuralTrust, Qwen3Guard) sin evidencia independiente, y no encontré benchmarks regionales. Esto sirve como benchmark abierto más un clasificador afinado.
3. Antes de decidir, falta verificar: precios de Prompt Security, Aim y Robust Intelligence, las rondas de NeuralTrust, Zenity, Guardrails AI y CalypsoAI, y la tasa de falla de los guardrails en español con una prueba propia (por ejemplo, correr Llama Guard 3 y Qwen3Guard sobre jailbreaks traducidos al español y portugués). Esa prueba es viable dentro de la hackathon.
