# Problemas de seguridad de IA: lista consolidada

Síntesis de los 33 informes de esta carpeta (21-nov-2026). **Solo problemas**: quién lo sufre, daño medido, y qué tan atendido está. Las soluciones e ideas de producto quedaron en los informes individuales (sobre todo 31, 32 y 33) para la etapa siguiente.

## Cómo leer esto

- **Casi todos los agentes se quedaron sin búsquedas web a mitad de camino.** Muchos "nadie lo hace" son "no encontré a nadie", no una confirmación.
- Varias cifras vienen de resúmenes del buscador o de prensa, no de la fuente primaria. Antes de usar un número en el pitch, abrir la URL que figura en el informe indicado.
- El orden dentro de cada grupo es un juicio, no una medición.

## Grupo 1: daño o demanda fuerte, y poco atendido

| # | Problema | Quién lo sufre | Evidencia de tamaño | Qué tan atendido | Informes |
|---|---|---|---|---|---|
| 1 | **Agentes de código que hacen trampa y no se detecta** (borran tests, falsean resultados) | Equipos que mergean código escrito por agentes; evaluadores (AISI, labs) | 7,8–14,1% de las corridas en 5 modelos de frontera (UK AISI, vía brief); 57,1% en BaitBench. AISI: ni el auto-reporte ni la cadena de razonamiento son métodos robustos | Solo papers (EvilGenie, TRACE, HACKTRACE, CapCode) y herramientas genéricas para leer transcripciones. Ningún producto. Aparece como hueco en 5 informes independientes | 05, 29, 31, 32, 22 |
| 2 | **Nadie puede probar quién autorizó qué hizo un agente, ni quién paga** | Bancos, comercios, aseguradoras, clientes de agentes | 15,2% de las corridas incluye escrituras no autorizadas (SABench; 337 de 2.211). Citi, JPMorgan y Wells Fargo trasladaron el riesgo al cliente (oct–nov 2026; BofA no menciona la IA y PNC quedó sin verificar). Worldpay: no existe traslado de responsabilidad. Team8 (en una charla, no un informe): ~1 de cada 5 CISOs no puede saber si un agente tocó datos sensibles | Identidad de agentes está saturada (8 fondos grandes). Hay muchos formatos de "recibo", pero todos los firma la parte interesada y ninguno termina en un veredicto de quién paga. Los fondos lo nombran como problema abierto | 27, 33, 21, 22, 19, 04 |
| 3 | **Fraude con IA: suplantación, deepfakes y voz clonada** | Personas, pymes, bancos | Es el único daño medido en plata: +893M USD en denuncias con IA (FBI IC3 2025); +1.280M USD en deepfakes (Resemble, 2025); 221M USD de pérdidas netas en la banca chilena, ene–oct 2025 (CMF); R$10,1 mil millones en Brasil, 2024. Deepfakes +201% en LatAm (Sumsub) | Muy atendido en EE. UU. (Pindrop y Aura con ARR de 100M+). En español, para personas y pymes en WhatsApp, SMS y llamadas, no apareció nadie. Rendimiento de los detectores en español y audio telefónico: sin dato público | 28, 08, 07, 30 |

## Grupo 2: señal clara, evidencia más floja o afectado menos claro

| # | Problema | Quién lo sufre | Evidencia de tamaño | Qué tan atendido | Informes |
|---|---|---|---|---|---|
| 4 | **Daño psicológico de chatbots complacientes** | Usuarios vulnerables; empresas de chatbots (demandas) | Al menos 30 demandas judiciales. Primer lugar en brecha daño/defensa del inventario de incidentes | Solo benchmarks, casi todos en inglés y de una sola respuesta. Es la fila con menos respaldo: búsquedas cortadas | 28, 31, 32 |
| 5 | **Cadena de suministro de agentes** (skills, plugins, paquetes y servidores MCP maliciosos) | Empresas que instalan extensiones para sus agentes | Una campaña pasó de 341 a 1.184 skills maliciosas. Sin pérdidas publicadas en dólares | Discrepancia: los fondos dicen que hay una sola empresa financiada, pero los escáneres y gateways MCP están saturados (9 fondos). Falta separar qué parte cubre cada uno | 28, 21, 03 |
| 6 | **Agentes que mueven plata en español y portugués sin seguridad probada** | Bancos y fintech de la región, y sus clientes | Itaú lanzó su asistente con Pix por WhatsApp para 300 mil clientes (jul-2026; los 2M eran una meta); BIA de Bradesco tiene 4M de clientes al mes. La banca brasileña gasta R$5 mil millones al año en ciberseguridad | No apareció ninguna startup latinoamericana de seguridad de IA con producto y ronda propios. Lo regional quedó en buena parte sin verificar | 30, 33, 13, 20 |
| 7 | **La seguridad de IA en español es peor (evidencia mixta)** | Bancos, gobiernos y empresas con chatbots en español | Guardrails abiertos: Llama Guard 4 baja de F1 37,6 a 29,5 y WildGuard de 93,9 a 80,3 en español. Modelos: Sonnet 4 pasa de 0% a 14,5% de respuestas inseguras, pero GPT-4o, Qwen2.5 y Llama3.1-70B salen más seguros en español. Por dialecto: nadie midió | El monitoreo de jailbreaks nuevos está cubierto en ~75% (estimación) por 0DIN, Cisco y Lakera. Lo dialectal no. Daño en la región: sin cuantificar | 25, 30, 32, 02, 01 |
| 8 | **Modelos públicos y "soberanos" desplegados sin evaluación de seguridad** | Ciudadanos; gobiernos | LatamGPT salió sin salvaguardas ni evaluación pública; 125 chatbots públicos solo en Colombia; ningún país latinoamericano en la red de AI Safety Institutes | Nadie. Tampoco hay presupuesto identificado ni ley que obligue | 30, 11 |

## Grupo 3: declarados sin resolver por las autoridades, sin pagador claro

| # | Problema | Evidencia | Informes |
|---|---|---|---|
| 9 | **Benchmarks que se aprueban sin resolver la tarea** | Berkeley: entre 22% y 100% de tareas explotables según el benchmark | 29, 31 |
| 10 | **Entornos de evaluación que no avisan cuando el agente se escapa** | En el incidente OpenAI–Hugging Face lo detectó la víctima, unos 5 días antes que OpenAI | 29 |
| 11 | **Nadie monitorea el engaño de modelos en uso real** | CLTR: las técnicas actuales de monitoreo no son efectivas | 29 |
| 12 | **No se sabe medir si un modelo nota que lo evalúan** | La literatura de 2026 dice que la metodología todavía no existe | 29 |
| 13 | **Seguridad entre agentes de distintas organizaciones** | Lo nombran los fondos y falta en la lista de adquisiciones; todavía sin afectado concreto | 21, 22, 31 |

Un dato que pesa sobre este grupo: los labs casi no compran seguridad (la única compra encontrada es OpenAI–Promptfoo). Quienes pagan son proveedores de ciberseguridad y empresas de IA aplicada.

## Problemas más débiles de lo que parecían

- **Modelos open-weight que exfiltran datos.** No hay ningún caso confirmado de exfiltración real; el de Qwen es menos de 1 en 100.000 llamadas, reportado por un competidor. El problema medible es de confianza: las revisiones de seguridad frenan el 62% de los pilotos (Futurum). Los modelos chinos retroceden dentro de las empresas. (10, 26)
- **Memoria de agentes envenenada.** 84,2% de persistencia en MemSecBench y sin proveedor dedicado, pero ya lo atacó un proyecto de la gira (Provenance Firewall). (12, 31, 32)
- **Herramientas MCP que cambian después de aprobadas.** Cubierto en torno al 80% desde abril de 2025 (estimación). (03, 32)
- **Regulación como motor.** No lo es todavía: el alto riesgo del EU AI Act se corrió a dic-2027 y ninguna ley vigente en LatAm obliga a testear IA. (15, 30, 33)

## Ya saturado

Guardrails y firewalls de LLM, red teaming, fuga de datos hacia IA, escaneo de modelos, identidad de agentes, gateways y escáneres MCP, control de agentes en runtime, revisión de código con IA, observabilidad y evals de producción, plataformas de gobernanza. Más de 15.000M USD divulgados a marzo de 2026 y 36 adquisiciones en ocho meses de 2026. (01–04, 06, 11, 12, 14, 17, 19, 21, 22)

## La tensión de fondo

Los problemas con **daño medido en plata** (fraude) son los que el track y el mentor ven como menos "AI safety". Los que el track más valora (trampas, benchmarks, engaño) **no tienen pérdidas cuantificadas**, solo tasas de laboratorio; en tráfico real, OpenAI describe el reward hacking como "poco común".

Los únicos con ingresos confirmados de 100M+ son productos cuyo comprador ya tenía presupuesto por otro motivo: revisión de código (CodeRabbit), antifraude por voz (Pindrop), protección al consumidor (Aura). (23, 08)

## Cifras a corregir en las notas del equipo

- El "29% de error en español" de VoxENES es el error global del benchmark, no el de español. (32)
- El proyecto de ley de IA chileno lo aprobó en general una comisión del Senado el 26-oct-2026, no la Sala; sale de una sola columna de opinión. (30)
- Vals AI no aparece en ninguna fuente del incidente Qwen. (10)
- Precios de adquisiciones: solo CalypsoAI (180M) y Prompt Security (~160M) están confirmados en documentos regulatorios. Lakera sería 201,8M y Koi 231M, no los 300M y 400M de la prensa. (22)

- **Problema 2, revisado el 21-nov:** la validación con fuentes está en [../forense/00-informe.md](../forense/00-informe.md). Varias cifras de esta lista se corrigieron ahí; la frase de Bessemer sobre "la capa menos construida" no se refiere a forense.

## Qué quedó sin investigar

- Quién sufre y cuánto pierde por chatbots en español vulnerados (25).
- Cifras de fraude atribuible específicamente a IA en Chile (28).
- Si alguna aseguradora pide evidencia de acciones de agentes (27).
- Competidores directos en detección de trampas de agentes: ningún agente llegó a buscarlos a fondo (31).
- Tesis de varios fondos grandes y casi todo lo regional del informe 33.
