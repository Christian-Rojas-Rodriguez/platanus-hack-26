# ¿Cómo se audita HOY a un proveedor de inferencia de LLM?

Estado del arte al 21/11/2026: certificaciones, procedencia, pruebas criptográficas, métodos estadísticos y servicios.

- **Para:** Christian (Smoke) y el equipo, Platanus Hack 26
- **Fecha:** sáb 21/11/2026, ~22:40 (hora de Chile, UTC-3); actualizado ~22:55 con la validación de un comprador, §8 (OpenRouter) y §9 (borrador de estándar)
- **Pregunta:** ¿existe alguna certificación, auditoría, estándar o servicio que verifique qué modelo corre realmente un proveedor de *token-as-a-service*, y que no haya cambios no declarados (cuantización, cambio de modelo, contexto truncado, tokens inflados)?
- **Base:** amplía `security-compute-2026-11-21.md` (producto "Testigo").
- **Método:** búsqueda web + lectura de las fuentes primarias. Cada link fue abierto hoy (HTTP 200 o título de arXiv), salvo los marcados como ⚠️. Las fechas son las que dice cada fuente.
- **Lo que no hice:** no corrí ninguna auditoría, no contacté a nadie y no consulté APIs pagas.

---

## 0. Resumen

1. **Ninguna certificación de procesos verifica qué modelo sirve un endpoint en tiempo de ejecución.** Esto incluye SOC 2, ISO 27001/42001, NIST AI RMF, CSA STAR for AI y HITRUST AI. Certifican que la organización *tiene controles*, no que el modelo servido sea el declarado (ISO 42001 lo dice explícitamente).
2. **La única evidencia fuerte de identidad es criptográfica y exige que el proveedor coopere.** Las variantes son: TEE con atestación (Tinfoil, Phala, Apple PCC), re-ejecución verificable (TOPLOC, PoSP de Hyperbolic, Verde de Gensyn) o zk-proofs (zkLLM, FlashProve de Anthropic, nov 2026, todavía investigación). La mayoría de los endpoints del mercado no la ofrece.
3. **Sin cooperación, lo que hay es evidencia estadística de caja negra.** Detecta *diferencias contra una referencia* con cierta tasa de error. **No certifica identidad.**
4. **Ya hay servicios que "evalúan endpoints y publican un resultado":**
   - Artificial Analysis: Endpoint Accuracy Index (24 de 103 endpoints por debajo de la referencia).
   - Benchlist: atestaciones firmadas, USD 499/mes, lo paga el proveedor.
   - TrackLLM: monitoreo abierto.
   - K2 Vendor Verifier (Moonshot).
   - OpenRouter Exacto, con señales del tráfico de producción.
5. **Corrección explícita:** antes afirmamos que "todas las auditorías usan prompts fijos o públicos". **Es falso o no está verificado** (ver §3).
6. **Veredicto:** la categoría ya existe, así que **no es 0→1**. Puede haber una cuña (verificación del lado del comprador, sobre su propio tráfico, más auditoría de facturación), pero que sea única **no está probado** y hay que validarlo con clientes.
7. **Comprador (22:14):** pide una certificación de proveedores con 4 propiedades: infraestructura legítima, que las solicitudes lleguen bien, que no miren sus datos y que el modelo sea el declarado. OpenRouter hoy cubre confiabilidad y tool calls (medidos) y ZDR (declarado/contractual), pero no la identidad del modelo. En §9 hay un borrador de estándar por niveles de evidencia (E1 declarado / E2 medido / E3 atestado).

---

## 1. Tres tipos de evidencia (no mezclarlas)

| Tipo | Qué prueba | Qué NO prueba | Requiere |
|---|---|---|---|
| **A. Certificación de procesos** (SOC 2, ISO, CSA, HITRUST) | Que la organización tiene políticas y controles, y que un auditor los revisó con una muestra en un período | Que un request concreto lo respondió el modelo X con los pesos Y | Que el proveedor contrate al auditor |
| **B. Evidencia criptográfica** (TEE con atestación, firmas, zk-proofs, compromisos verificables) | Que un binario o unos pesos con hash H corrieron en hardware que firma esa medición, o que una salida se calculó con el modelo comprometido | Que la medición corresponde al modelo "bueno" si nadie publicó qué hash esperar. Tampoco la seguridad del hardware en sí: hay análisis críticos del modo confidencial del H100 ([2507.02770](https://arxiv.org/abs/2507.02770)) | **Que el proveedor coopere** (desplegar TEE o emitir pruebas) |
| **C. Evidencia estadística de caja negra** (tests de igualdad de distribución, benchmarks por endpoint, fingerprinting, re-conteo de tokens) | Que las salidas del endpoint **difieren** (o no hay evidencia de que difieran) de una referencia, con un nivel de significancia | **Identidad**: "no detecté diferencia" ≠ "es el mismo modelo". Un proveedor que reconoce la auditoría puede esquivarla. Si la referencia ya está degradada, la comparación también | Solo acceso a la API y una buena referencia |

Regla para el pitch: **nunca decir "certificamos que el endpoint corre el modelo X"** con evidencia tipo C. Lo honesto es: "medimos desviaciones contra la referencia Z, con tal potencia y tal tasa de falsos positivos".

---

## 2. Qué existe, por categoría, y cómo funciona

### 2.1 Certificaciones y marcos de procesos (evidencia A)

| Qué | Cómo funciona (simple) | ¿Verifica el modelo servido? | Fuente |
|---|---|---|---|
| **SOC 2** (AICPA) | Un contador público revisa los controles de seguridad, disponibilidad, integridad de procesamiento, confidencialidad y privacidad durante un período (Tipo II) y emite un informe | **No.** Sirve como "integridad de procesamiento" genérica y no hay un criterio específico de identidad del modelo | [AICPA SOC 2](https://www.aicpa-cima.com/topic/audit-assurance/audit-and-assurance-greater-than-soc-2) |
| **ISO/IEC 27001** | Certifica un sistema de gestión de seguridad de la información | **No** | — (conocido, no re-verificado) |
| **ISO/IEC 42001:2023** (+ ISO/IEC 42006:2025 para los certificadores) | Certifica un *sistema de gestión de IA*: políticas, riesgos, roles, controles del Anexo A, Declaración de Aplicabilidad | **No.** *"certifies a management system, not a model"* | [Praxora, 27/10/2026](https://praxoralab.com/insights/iso-42001-certifies-a-management-system-not-a-model); [AI Governance Institute](https://aigovernance.institute/frameworks/iso-42001) |
| **NIST AI RMF 1.0** | Marco voluntario (Govern / Map / Measure / Manage). No es una certificación | **No** (no hay certificado) | [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) |
| **EU AI Act: Código de Práctica GPAI (transparencia)** | El proveedor *del modelo* llena un Model Documentation Form, lo mantiene actualizado (también con versiones nuevas) y se lo da a la AI Office y a los proveedores downstream | **Parcial y declarativo.** El campo 1.3 "Model authenticity" pide *"a secure hash if binaries are distributed, or the URL endpoint in the case of a service"*. Obliga al proveedor del modelo, no a un tercero que lo hospeda, y nadie verifica en tiempo de ejecución | [Código de Práctica, transparencia](https://artificialintelligenceact.eu/ai-act-explorer/cop-transparency/); [formulario](https://ingenrieth-online.de/fileadmin/files/regulations/codes/AI_CoP-GPAI_Transparency_Model_Documentation_Form.pdf) |
| **CSA STAR for AI** (lanzado el 23/10/2025; Nivel 2 desde el 20/11/2025) | Basado en el AI Controls Matrix: 18 dominios, 243 objetivos de control. Nivel 1 = autoevaluación AI-CAIQ. Nivel 2 = ISO 27001/42001 + AICM, o SOC 2 + AICM | **No en tiempo de ejecución.** El AICM tiene controles de "model integrity" y "AI supply chain transparency", pero se auditan como controles de proceso | [Lanzamiento](https://cloudsecurityalliance.org/press-releases/2025/10/23/cloud-security-alliance-launches-star-for-ai-establishing-the-global-framework-for-responsible-and-auditable-artificial-intelligence/); [panorama, 17/11/2026](https://cloudsecurityalliance.org/blog/2026/11/17/csa-star-for-ai-certifications-what-are-they) |
| **HITRUST AI Security Assessment** (19/11/2024) | Hasta 44 requisitos de IA (55 según una nota posterior) que se suman a una evaluación e1/i1/r2: inventario y versionado de modelos, testing/red teaming, cadena de suministro | **No.** Pide inventario y control de cambios (proceso), no verificar el endpoint | [Comunicado HITRUST](https://hitrustalliance.net/press-releases/hitrust_launches_ai_security_assessment_and_certification) |

**Conclusión A:** sirven para *procurement* ("¿tenés controles?"), pero no responden "¿este endpoint sirvió fp4 en vez de bf16?". Incertidumbre: un auditor podría incluir pruebas técnicas dentro del alcance, pero no encontré ningún esquema que lo exija.

### 2.2 Procedencia de artefactos (evidencia B, pero sobre el archivo)

| Qué | Cómo funciona | Límite clave | Fuente |
|---|---|---|---|
| **OpenSSF Model Signing (OMS) v1.0** (04/04/2025) / Sigstore `model-transparency` | Hashea todos los archivos del modelo (pesos, config, tokenizer), arma un manifiesto, lo firma (Sigstore keyless, PKI o claves) y lo registra en un log de transparencia. Quien descarga re-hashea y verifica la firma | Prueba que **el archivo descargado** es el publicado. **No prueba qué carga el servidor** | [Blog OpenSSF](https://openssf.org/blog/2025/04/04/launch-of-model-signing-v1-0-openssf-ai-ml-working-group-secures-the-machine-learning-supply-chain/); [repo](https://github.com/sigstore/model-transparency) |
| **NVIDIA NGC firma con OMS** (desde 03/2025); NIM verifica checksums | Igual que arriba, aplicado al catálogo de NVIDIA | Ídem | [NVIDIA](https://developer.nvidia.com/blog/bringing-verifiable-trust-to-ai-models-model-signing-in-ngc/); [NIM](https://docs.nvidia.com/nim/large-language-models/latest/reference/model-signature-verification.html) |
| **Hugging Face** (hash de commit del repo; Inference Providers) | Cada versión de un repo de modelo tiene un SHA de git | Fija los pesos *de referencia*. No encontré que HF verifique lo que sirven sus Inference Providers (⚠️ incertidumbre) | [HF Inference Providers](https://huggingface.co/docs/inference-providers/index) |
| **AI-BOM / ML-BOM**: CycloneDX ML-BOM, perfil AI de SPDX 3.0 | Inventario legible por máquina: componentes, model card, datasets, dependencias | Es una **declaración**. Se vuelve verificable solo si se firma y se ata a algo medido | [Guía CycloneDX ML-BOM](https://www.cyclonedx.org/guides/OWASP_CycloneDX-Authoritative-Guide-to-AI-ML-BOM-en.pdf); [SPDX 3.0.1](https://spdx.dev/wp-content/uploads/sites/31/2024/12/SPDX-3.0.1-1.pdf) |
| **SLSA** (aplicado a ML vía in-toto) | Atestaciones firmadas de *cómo se construyó* un artefacto | Procedencia del build, no de la inferencia | [slsa.dev](https://slsa.dev/) |
| **C2PA** (spec 2.4, guía AI/ML) | Credenciales firmadas sobre *contenido*. Puede listar un modelo como "ingrediente" de una salida | **No verifica qué modelo se ejecutó.** El manifiesto es una afirmación firmada de quien lo emite | [C2PA AI/ML](https://spec.c2pa.org/specifications/specifications/2.4/ai-ml/ai_ml.html) |

**Conclusión B:** resuelve "¿el archivo es auténtico?", no "¿el servidor corre ese archivo?". Para unir las dos cosas hace falta un TEE (2.3).

### 2.3 Verificación criptográfica en ejecución (evidencia B, sobre el servidor)

| Qué | Cómo funciona (simple) | Qué cubre / límites | Fuente |
|---|---|---|---|
| **NVIDIA Confidential Computing** (H100/Blackwell) + atestación (NRAS / SDK local) | La GPU firma un informe (SPDM) con mediciones de su firmware, VBIOS, driver y configuración, más un nonce. El verificador compara contra valores "golden" (RIM) firmados por NVIDIA | Prueba **que la GPU y su software están en modo confidencial y sin alterar**. **No mide los pesos.** Eso lo hace la VM confidencial de CPU (SEV-SNP/TDX) que los carga | [Arquitectura de atestación NVIDIA](https://docs.nvidia.com/attestation/quick-start-guide/latest/architecture.html); [blog H100 CC](https://developer.nvidia.com/blog/confidential-computing-on-h100-gpus-for-secure-and-trustworthy-ai/) |
| **Tinfoil** | VM confidencial (AMD SEV-SNP/TDX) + atestación de la GPU. TLS atado al enclave atestado. "Modelwrap"/dm-verity atan un commit fijado de HF a la medición de arranque | **Lo más cercano a "prueba de qué pesos corren"**, pero solo para sus propios endpoints | [Cómo prueban la identidad del modelo, 03/02/2026](https://tinfoil.sh/blog/2026-02-03-proving-model-identity); [arquitectura](https://docs.tinfoil.sh/verification/attestation-architecture) |
| **Phala / RedPill** | Inferencia en TEE con recibos por respuesta | Según sus propias docs, la procedencia de los pesos en general **no está probada** | [Phala](https://docs.phala.com/phala-cloud/confidential-ai/confidential-model/providers); [RedPill](https://docs.redpill.ai/confidential-ai/providers) |
| **Apple Private Cloud Compute** | Publica la medición de cada imagen de software en un log de transparencia append-only. El iPhone solo habla con nodos cuya atestación coincide con una imagen publicada. Los investigadores pueden inspeccionar las imágenes (VRE) | Es **transparencia verificable del software de un servicio first-party**, no un estándar para terceros | [Apple PCC](https://security.apple.com/blog/private-cloud-compute/); [investigación](https://security.apple.com/blog/pcc-security-research/) |
| **zkML** | El proveedor genera una prueba criptográfica de que la salida es f(entrada; pesos comprometidos), sin revelar los pesos | **EZKL**: práctico solo para modelos chicos. **zkLLM**: LLaMA-2-13B en menos de 15 min por inferencia en GPU. **FlashProve (Anthropic, 02/11/2026)**: ~110 tokens/s de prueba en una H100 para un MoE de 400B, con ~19 MB de prueba cada 1.024 tokens. Es **investigación, no un servicio** | [EZKL](https://github.com/zkonduit/ezkl); [zkLLM 2404.16109](https://arxiv.org/abs/2404.16109); [Anthropic](https://www.anthropic.com/research/provable-inference) |

### 2.4 Verificación por re-ejecución o incentivos (cooperación parcial)

| Qué | Cómo funciona | Límites | Fuente |
|---|---|---|---|
| **TOPLOC** (Prime Intellect, ICML 2025) | El proveedor se compromete con un hash LSH de las activaciones top-k (258 B cada 32 tokens). Un verificador re-ejecuta el prefill (más rápido que generar) y compara con tolerancias | El proveedor tiene que emitir los compromisos y el verificador necesita GPU. No detecta decodificación especulativa | [repo](https://github.com/PrimeIntellect-ai/toploc); [ficha](https://consortiumforverifiedcomputing.org/atlas/toploc) |
| **Token-DiFR** (Karvonen et al., 28/11/2025) | Con la semilla de muestreo fijada, la inferencia es casi determinística (más de 98% de tokens iguales). Se mide cuánto divergen los tokens del proveedor de una re-ejecución de referencia. Sin semilla compartida, también sirve a T=0 | Es **post-hoc sobre cualquier token de producción** (no son prompts fijos), pero **re-ejecuta el modelo**: caro para MoE gigantes | [post](https://adamkarvonen.github.io/machine_learning/2025/11/28/difr.html) |
| **Hyperbolic PoSP / spML** | Con probabilidad p, validadores al azar re-calculan la salida. Si hay discrepancia hay arbitraje y penalidad. La seguridad es económica (equilibrio de Nash) | Asume una función determinística y validadores honestos en promedio | [arXiv 2405.00295](https://arxiv.org/html/2405.00295v3); blog ⚠️ (devolvió 500 hoy) |
| **Gensyn Verde** | Varios proveedores corren lo mismo. Si difieren, un árbitro hace bisección sobre compromisos Merkle hasta la primera operación divergente. RepOps da reproducibilidad bit a bit | Requiere al menos un proveedor honesto y su runtime | [arXiv 2502.19405](https://arxiv.org/abs/2502.19405) |
| Bittensor (subredes) | Validadores puntúan a los mineros | ⚠️ El mecanismo varía por subred y no lo verifiqué hoy | — |

### 2.5 Métodos estadísticos de caja negra (evidencia C)

| Qué | Cómo funciona | Dato clave | Fuente |
|---|---|---|---|
| **Model Equality Testing** (Gao, Liang, Guestrin, ICLR 2025) | Test de dos muestras (MMD con kernel de strings): ¿las salidas de la API vienen de la misma distribución que la referencia? | 77,4% de potencia mediana con ~10 muestras por prompt. **11 de 31 endpoints de Llama** difieren de los pesos de Meta (verano 2024) | [2410.20247](https://arxiv.org/abs/2410.20247) |
| **Are You Getting What You Pay For?** (Cai et al.) | Formaliza la sustitución (cuantizado, más chico, mezcla aleatoria con probabilidad p, **evasión de benchmarks**) y evalúa detectores | Los tests de texto, identidad y benchmarks **no son confiables**. Los logprobs sirven si se exponen. Propone TEE | [2504.04715](https://arxiv.org/abs/2504.04715) |
| **LLMmap** (USENIX Sec 2025) | 8 consultas elegidas + un clasificador identifican la familia y versión del modelo | Más de 95% sobre 42 versiones; no separa cuantizaciones | [2407.15847](https://arxiv.org/abs/2407.15847) |
| **Idiosyncrasies in LLMs** (2025) | Un clasificador de embeddings predice qué LLM escribió un texto | 97,1% entre 5 APIs de chat | [2502.12150](https://arxiv.org/abs/2502.12150) |
| **TrackLLM** | Logprob tracking (LT) cuando hay logprobs; "border inputs" (B3IT) cuando no, con prompts sonda elegidos para ser sensibles | 364 endpoints activos, 338 cambios detectados, datos crudos públicos | [trackllm.net](https://www.trackllm.net/) |
| **Auditoría de tokens**: CoIn (EMNLP Findings 2026), PALACE, Overage | Auditan tokens de razonamiento ocultos (compromisos Merkle + relevancia semántica, o estimación del largo) | **Token Inflation** ([2605.30040](https://arxiv.org/abs/2605.30040)) los rompe: 1.469% de inflación sin detección, y 50,85% solo por ambigüedad de tokenización | [CoIn](https://github.com/CASE-Lab-UMD/LLM-Auditing-CoIn); [PALACE 2508.00912](https://arxiv.org/abs/2508.00912); [Overage](https://github.com/ishrith-gowda/overage) |

### 2.6 Servicios y "sellos" que ya evalúan endpoints

| Qué | Cómo funciona | Quién paga / formato | Fuente |
|---|---|---|---|
| **Artificial Analysis: Endpoint Accuracy Index v1.1** | Corre una suite fija (BFCL-500, HLE-250, AA-LCR-25 de ~100k tokens) contra cada endpoint y contra una **referencia autohospedada** con los pesos oficiales (vLLM/SGLang en B200/B300/GB200), con IC al 95% | Público, foto puntual (medido entre el 8/10 y el 4/11/2026). **24 de 103 endpoints por debajo de la referencia.** GLM-5.3: 10/26 por debajo (rango 67,2-99,3). Causas: topes de salida, menos razonamiento, etc. | [artículo v1.1](https://artificialanalysis.ai/articles/endpoint-accuracy-index-v1-1); [metodología](https://artificialanalysis.ai/methodology/endpoint-accuracy-index) |
| **Benchlist** | "Atestaciones" diarias firmadas (Ed25519) de benchmarks por proveedor contra la API first-party canónica, alertas de drift (más de 2 pp) y **badge** para la web del proveedor | **USD 499/mes, lo paga el proveedor** | [benchlist.ai](https://benchlist.ai/for/inference-providers) |
| **K2 Vendor Verifier** (Moonshot) | ~4.000 requests de tool calling vs. la API oficial: F1 de disparo y validez de esquema | Lo hace el laboratorio y es público. **Solo el 50% del set es público** (el resto se presume privado) | [repo](https://github.com/MoonshotAI/K2-Vendor-Verifier) |
| **OpenRouter Exacto / Auto Exacto** | Enrutamiento según calidad de tool calls, throughput y latencia, **medidos sobre tráfico de producción reciente** | Lo hace el intermediario y está incluido en el servicio | [Exacto](https://openrouter.ai/docs/guides/routing/model-variants/exacto); [blog](https://openrouter.ai/blog/announcements/provider-variance-introducing-exacto/); [routing](https://openrouter.ai/docs/guides/routing/provider-selection) |
| **TrackLLM** | Monitoreo continuo de cambios (2.4) | Gratis y abierto | [trackllm.net](https://www.trackllm.net/) |
| **ModelWatch**, **Decosa**, **InferenceBench** | Drift con specs definidas **por el propio usuario** (ModelWatch); auditor de endpoints (Decosa); benchmarks de inferencia | SaaS | [ModelWatch](https://modelwatch.app/); [Decosa](https://decosa.ai/tools/developer/auditor); [InferenceBench](https://inferencebench.dev/methodology) |
| **Tinfoil** (criptográfico) | Ver 2.3 | Lo paga el usuario de Tinfoil; solo cubre sus endpoints | [Tinfoil](https://tinfoil.sh/blog/2026-02-03-proving-model-identity) |

---

## 3. Corrección explícita: "todas usan prompts fijos o públicos" es FALSO

| Caso | ¿Prompts fijos? | ¿Públicos? |
|---|---|---|
| K2VV | Sí, set fijo | **No del todo**: solo el 50% es público |
| Artificial Analysis | Sí, suite fija | Mezcla de subsets de benchmarks públicos y propios (AA-LCR). ⚠️ No verifiqué qué partes se mantienen privadas |
| Benchlist | "Canonical sample sets" fijos | ⚠️ No queda claro en su página si son públicos |
| TrackLLM | Sondas (B3IT) elegidas por endpoint | Los datos crudos sí son públicos |
| **OpenRouter Exacto** | **No**: señales del **tráfico de producción** | No aplica |
| **ModelWatch** | Specs que **define el cliente** | Privadas del cliente |
| **Token-DiFR, TOPLOC, PoSP, Verde, TEEs** | **No**: auditan **cualquier request de producción** (con cooperación o re-ejecución) | No aplica |

**Lo que sí se sostiene:** los servicios *públicos de benchmark por endpoint* (AA, Benchlist, K2VV) usan suites fijas y, al menos en parte, conocidas. Por eso son vulnerables a la "evasión de benchmarks" que describen Cai et al. Ninguno de ellos publica cómo se defiende de eso (⚠️ que no lo publiquen no prueba que no se defiendan).

**Lo que no se sostiene:** que *nadie* audite tráfico real. OpenRouter lo hace para tool calls, y los métodos con cooperación auditan cualquier request.

---

## 4. Gaps concretos

1. **No hay estándar ni sello de terceros sobre la "identidad del modelo servido".** Las certificaciones son de proceso, y el Código de Práctica de la UE es declarativo y para el proveedor del modelo, no para quien lo hospeda.
2. **La evidencia criptográfica existe, pero solo donde el proveedor coopera.** En OpenRouter, GLM-5.3 tiene 48 endpoints, 15 sin cuantización declarada (medido hoy ~19:55 hora de Chile vía la API pública). No encontré que la mayoría ofrezca atestación.
3. **La evidencia estadística disponible es:**
   - una **foto puntual** (AA);
   - una suite fija que **paga el auditado** (Benchlist, conflicto de interés);
   - específica de un modelo o laboratorio (K2VV);
   - propiedad del intermediario (Exacto).

   **No encontré** una auditoría continua *del lado del comprador*, sobre su propio tráfico, contra la referencia first-party, con informe para procurement. ⚠️ Puede existir y no haberla visto.
4. **Facturación de tokens visibles:** no encontré ningún servicio que re-cuente con el tokenizer público de los modelos open-weight y compare con `usage`. Lo que existe sobre tokens ocultos está en investigación y ya fue roto (Token Inflation).
5. **Truncado de contexto y topes de salida:** AA los detecta en su suite (AA-LCR, topes de 16-32K), pero en forma puntual, no continua.
6. **Límite teórico:** con caja negra **no se puede certificar identidad**, solo detectar diferencias con cierta potencia. Un proveedor adaptativo puede esquivar parte de las pruebas, y si la referencia está degradada (first-party cuantizada), la comparación hereda ese sesgo.

---

## 5. Lo más parecido a "evaluar un endpoint y dar un sello", y en qué difiere de Testigo

| | AA Endpoint Accuracy | Benchlist | K2VV | Tinfoil | **Testigo (propuesta)** |
|---|---|---|---|---|---|
| Tipo de evidencia | C (benchmark) | C (benchmark firmado) | C (tool calls) | **B** (atestación) | C (estadística) |
| Referencia | **Autohospedada**, pesos oficiales en B200 | API first-party | API oficial | Hash de commit de HF | API first-party (sin GPU) |
| Prompts | Suite fija | Suite fija | Fija (50% pública) | Cualquiera | **Tráfico del cliente** + suite propia |
| Frecuencia | Puntual | Diaria | Puntual | Por request | Continua (muestreo) |
| Quién paga | Nadie (público) | El proveedor | El laboratorio | El usuario de Tinfoil | **El comprador** |
| Facturación / inyección | No | No | No | N/A | **Re-conteo con el tokenizer** (propuesto) |
| ¿"Sello" de identidad? | No (score) | Badge de drift | No | **Sí** (criptográfico) | **No**: informe de desviaciones con IC |

**Diferencias reales de Testigo:** lo paga el comprador, corre sobre su tráfico, en forma continua y agrega facturación.

**Debilidades frente a los otros:**
- La referencia de AA (autohospedada) es más fuerte que una API first-party.
- Tinfoil da prueba y Testigo no.
- TrackLLM es gratis.

---

## 6. Veredicto: ¿hay espacio 0→1? ¿Quién pagaría?

- **0→1, no.** La categoría "verificar proveedores de inferencia" existe y crece: AA (gratis, con referencia fuerte), Benchlist (pago), TrackLLM, K2VV, Exacto, Tinfoil, y la investigación de Anthropic sobre pruebas de inferencia.
- **¿1→n o una cuña?** Plausible, **sin probar**: *assurance* continuo del lado del comprador para modelos open-weight multi-proveedor. Incluiría desviaciones contra la referencia, integridad de tool calls, re-conteo de tokens y mapa de la cadena (cuantización declarada vs. estimada). El informe se podría usar como evidencia de "monitoreo de proveedores" en controles de ISO 42001 / CSA AICM. ⚠️ Que esos auditores acepten esa evidencia es una **hipótesis**.
- **Quién pagaría (hipótesis, ordenadas por evidencia):**
  1. **Laboratorios open-weight**, para proteger su marca. Moonshot ya invirtió en K2VV (evidencia fuerte de dolor, pero lo resolvieron in-house).
  2. **Empresas con gasto relevante en inferencia open-weight multi-proveedor** (agentes, fintech). La evidencia de dolor es la varianza medida por AA y K2VV. La disposición a pagar no está validada.
  3. **Compliance/procurement**, para evidencia de proveedores. Débil hasta validarlo.
  4. **Agregadores**: OpenRouter ya lo internaliza (riesgo competitivo más que cliente).
- **Riesgos de la tesis:**
  - AA es gratis y metodológicamente sólido.
  - OpenRouter o AA podrían agregar monitoreo continuo.
  - Si los TEE con atestación de pesos (estilo Tinfoil) se masifican, la capa estadística pierde valor.
  - La evidencia C nunca da "certificado de identidad".
- **Siguiente paso sugerido:** 3-5 entrevistas cortas (un equipo que gaste en DeepSeek/GLM/Kimi vía OpenRouter, un laboratorio, alguien de compliance) antes de afirmar que hay hueco. En el pitch, decir "cuña" y no "nadie lo hace".

---

## 7. Validación de un posible comprador (22:14, hora de Chile)

Fuente: audio transcripto (`/workspace/audio/transcript-2026-11-21-2214.txt`, ~1 min). Va sin nombres.

- **Lo que dijo:** compraría una certificación de proveedores de tokens para elegir cuáles usar. Hoy no confía en ningún proveedor de OpenRouter porque:
  - le roban credenciales;
  - funcionan mal;
  - le cambian el modelo por uno chino más barato.
- **Lo que no sabe:** no conoce ningún certificado. Sabe que OpenRouter verifica algo, pero no qué ni cómo.
- **Su opinión:** una ISO no sirve, hay que inventar un estándar propio.
- **Lo que le importa:**
  1. que la infraestructura sea legítima;
  2. que las solicitudes lleguen bien (latencia y confiabilidad);
  3. que haya infraestructura que garantice que no miran sus datos;
  4. que el modelo sea el declarado.
- **Cómo leerlo:** es **una sola señal cualitativa**, sin precio ni volumen. Valida el dolor, no la disposición a pagar.
- **Ojo con "robo de credenciales":** con OpenRouter, el proveedor de inferencia no recibe la API key del usuario (OpenRouter llama con la suya). El riesgo de credenciales es más bien de **revendedores o proxies no oficiales** y de keys filtradas (⚠️ inferencia mía; no verifiqué incidentes concretos hoy). Hay que repreguntarle qué le pasó.

---

## 8. Qué verifica HOY OpenRouter (fuentes oficiales, leídas hoy)

| Mecanismo | Qué hace | Tipo de evidencia | Qué NO garantiza | Fuente |
|---|---|---|---|---|
| **Alta de proveedores** | Formulario (infraestructura, endpoints, modelos, política de datos). Revisan compatibilidad de API, confiabilidad, precio y performance. NDA + llamada. Cuestionario de seguridad + documentos de seguridad + términos. Tráfico de prueba (latencia, throughput, errores). Requisitos: API compatible con OpenAI que devuelva `usage`, `/models` con **ubicación de los datacenters**, política de datos publicada, email corporativo. **"SOC 2 and zero data retention help, but neither is required."** | A (proceso/contractual) + pruebas funcionales | Que el modelo servido sea el declarado; que la ubicación declarada sea real | [Become a Provider](https://openrouter.ai/providers/apply); [integración](https://openrouter.ai/docs/guides/providers/integration) |
| **Monitoreo de uptime** | Uptime = éxitos / total (excluye errores del usuario), con 100+ requests mínimo. ≥95%: ruteo normal; 80-94%: degradado; <80%: solo fallback. TTFT y throughput públicos por modelo | C (medición sobre tráfico real) | Calidad del contenido | [integración §10-11](https://openrouter.ai/docs/guides/providers/integration) |
| **Exacto / Auto Exacto** | En cada `tool_call` chequean (desde agosto de 2025) si es JSON válido, si el nombre de la tool existe y si el esquema coincide. También la propensión a usar tools. Auto Exacto reordena proveedores en todo request con tools usando throughput, tasa de éxito de tool calls y **benchmarks internos** contra los endpoints | C (tráfico real + evaluaciones internas) | Identidad del modelo. Ellos mismos aclaran: *"should not be viewed as a broader statement on endpoint or provider quality"* | [blog Exacto](https://openrouter.ai/blog/announcements/provider-variance-introducing-exacto/); [integración §12](https://openrouter.ai/docs/guides/providers/integration); [traffic routing](https://openrouter.ai/docs/guides/providers/traffic-routing) |
| **Penalización por calidad** | Un endpoint marcado por tool calls rotas o por *"benchmark accuracy well below what the model should score"* queda muy atrás en el ruteo y recibe solo tráfico de exploración | C | No es público por endpoint en forma de certificado (⚠️ no vi el detalle de los benchmarks) | [traffic routing](https://openrouter.ai/docs/guides/providers/traffic-routing) |
| **Zero Data Retention (ZDR)** | Tres niveles por endpoint: ZDR / Safety Retention / Retention and Training. Se aplica por request (`zdr: true`), por cuenta, por grupo de modelos o con guardrails. Lista pública: `https://openrouter.ai/api/v1/endpoints/zdr`. Si no pueden confirmar la política de un endpoint, asumen que retiene y entrena | **A (política/contrato), no técnica.** *"OpenRouter works with providers to understand each of their data policies … in some cases creates special agreements"* | **Que el proveedor efectivamente no mire ni guarde**: no hay atestación. El tag de data policy *"is not a definitive source of third party data policies, but represents our best knowledge"* | [ZDR](https://openrouter.ai/docs/guides/features/zdr); [blog ZDR](https://openrouter.ai/blog/insights/zero-data-retention/); [provider routing](https://openrouter.ai/docs/guides/routing/provider-selection) |
| **Cuantización por endpoint** | Campo `quantization` en la API de endpoints y filtro `provider.quantizations` | **Declarativo** | Que sea cierto (en GLM-5.3, 15 de 48 endpoints declaran "unknown"; medido hoy ~19:55) | API pública `/api/v1/models/{id}/endpoints` |
| **Residencia regional** | Enrutamiento dentro de la UE o EE. UU. (`eu.openrouter.ai` / `us.openrouter.ai`), solo en planes Business/Enterprise | A (contractual) | Evidencia técnica de ubicación | [provider routing](https://openrouter.ai/docs/guides/routing/provider-selection) |

**En síntesis:** OpenRouter mide bien *confiabilidad y calidad de tool calls sobre tráfico real*, y lleva una **política de datos declarada por endpoint**. **No verifica en forma técnica ni pública** la identidad del modelo, la cuantización real ni la no-retención. Para lo que hacen con benchmarks internos no hay detalle publicado. Por eso el comprador "sabe que verifican algo pero no qué": lo que hacen es real, pero no se ve como certificado por endpoint.

---

## 9. Borrador de estándar de certificación de proveedores de inferencia (v0, para discutir)

**Principios:**

1. Cada propiedad se califica con un **nivel de evidencia** explícito:
   - **E1, declarado:** el proveedor lo afirma o lo firma por contrato.
   - **E2, medido black-box:** lo mide un tercero desde afuera, con IC y fecha.
   - **E3, atestado:** evidencia criptográfica o auditoría con acceso, verificable por el cliente.
2. **Nunca se emite "certificado de privacidad" ni "de identidad" con evidencia E2.** E2 solo dice "no detectamos desviación con esta potencia".
3. Cada resultado se publica con **fecha, método, tamaño de muestra y referencia usada**, y vence (re-medición periódica + monitoreo continuo).
4. Se mide con **tráfico indistinguible del normal** (prompts propios no publicados, rotados, y opcionalmente muestreo del tráfico del cliente) para reducir la evasión. Esto **reduce** el riesgo de evasión, no lo elimina.

### P1. Infraestructura legítima

| Verificable black-box (E2) | Requiere cooperación o atestación (E1/E3) | No verificable |
|---|---|---|
| Que la empresa existe y es quien dice (registro legal, dominio, TLS/certificados, ASN/IP de la API y su jurisdicción de red). Que el endpoint responde con el modelo y los parámetros publicados. Que no aparece en listas de abuso conocidas | Datacenters y ubicación declarados (E1). SOC 2 / ISO 27001 vigentes (E1, auditoría de proceso). Atestación de GPU y VM confidencial que pruebe qué hardware y software corre (E3) | **Dónde está físicamente la GPU** si no hay atestación de ubicación (open problem; NVIDIA y Lucid lo atacan desde el chip). Que no haya subcontratistas no declarados detrás de la API |

### P2. Las solicitudes llegan bien (latencia y confiabilidad)

| Verificable black-box (E2) | Requiere cooperación (E1/E3) | No verificable |
|---|---|---|
| Uptime, tasa de errores (5xx, cortes a mitad de stream), TTFT y throughput (p50/p95) desde varias regiones. Respeto de `max_tokens` y del contexto declarado (prueba de needle-in-haystack para detectar **truncado de contexto**). Topes de salida ocultos. Integridad de tool calls (JSON, nombre, esquema; como Exacto/K2VV). **Re-conteo de tokens** visibles con el tokenizer público vs. `usage` | Logs internos de incidentes y SLA firmado (E1). Métricas propias del proveedor con trazabilidad (E1) | Calidad bajo picos de carga que el auditor no reproduce. Tokens de **razonamiento ocultos**: sin cooperación no se pueden contar (y los auditores existentes fueron rotos) |

### P3. No miran mis datos (privacidad)

| Verificable black-box (E2) | Requiere cooperación o atestación (E1/E3) | No verificable |
|---|---|---|
| **Casi nada.** Como mucho: **canarios** (datos trampa únicos enviados en prompts, para detectar si reaparecen más tarde en salidas o en filtraciones). Esto **solo puede probar una filtración, nunca su ausencia**. También: TLS correcto y que la política ZDR publicada coincida con la que figura en OpenRouter | Política ZDR + contrato (E1; es lo que hace OpenRouter hoy). Auditoría SOC 2 con alcance en retención de logs (E1/A). **TEE con atestación** (VM confidencial + GPU en modo CC, TLS atado al enclave, imagen de software publicada y medida, estilo Tinfoil o Apple PCC) (**E3**: lo único que da garantía técnica razonable, y depende de la seguridad del hardware) | **Que un proveedor sin TEE no mire o no guarde los datos.** Imposible de certificar desde afuera. **No se promete.** |

### P4. El modelo es el declarado (sin cambio, sin cuantización no declarada)

| Verificable black-box (E2) | Requiere cooperación o atestación (E1/E3) | No verificable |
|---|---|---|
| **Desviación contra una referencia** (pesos oficiales autohospedados, estilo AA, o la API first-party): tests de igualdad de distribución (MMD), divergencia a T=0, benchmarks con IC (razonamiento, tool calls, contexto largo), fingerprinting de familia (LLMmap/idiosyncrasies) para detectar **cambio a otro modelo**. Monitoreo continuo para detectar **cambios no declarados** en el tiempo (estilo TrackLLM) | Cuantización y versión declaradas (E1). Compromisos verificables por request (TOPLOC), semilla compartida para auditar con Token-DiFR (E3 parcial; requiere re-ejecución). **TEE que mida los pesos** (hash del commit de HF atado a la atestación) (E3). zk-proofs de inferencia (E3, investigación) | **Identidad exacta** solo con black-box: "no detecté diferencia" ≠ "es el mismo modelo". Sustituciones **en una fracción muy chica del tráfico** o disparadas solo fuera de la auditoría pueden pasar sin detectarse. Si la referencia first-party está cuantizada, la comparación hereda ese sesgo |

### Cómo se vería el "sello"

- **Una ficha por endpoint**, no por empresa. Ejemplo: "GLM-5.3 @ proveedor X". Cada propiedad P1-P4 lleva su nivel de evidencia (E1/E2/E3), el resultado, el IC, la fecha y el vencimiento.
- **Insignias separadas, nunca un "certificado" único:**
  - "Confiabilidad medida" (P2, E2).
  - "Sin desviación detectada vs. referencia" (P4, E2).
  - "Pesos atestados" (P4, E3).
  - "Privacidad atestada (TEE)" (P3, E3).
  - "Política ZDR declarada" (P3, E1).
- **Lo que vende y por qué no es una ISO:** mide el *endpoint* y no el *sistema de gestión*. Es continuo y no anual. Y dice explícitamente qué nivel de evidencia respalda cada afirmación.

**Lo nuevo frente a lo existente** (con la cautela de §6):
- La ficha por endpoint de P1-P4 con niveles de evidencia no la vi publicada así.
- Las piezas sí existen por separado: AA (P4 E2 puntual), OpenRouter (P2 E2 + P3 E1), Tinfoil (P3/P4 E3 propio), Benchlist (P4 E2 pagado por el proveedor).
- El aporte sería **integrar y separar niveles de evidencia**, no inventar una medición nueva.

---

## 10. Fuentes no verificadas hoy (⚠️)

- Medium de Moonshot sobre K2VV: 403 por bloqueo. El dato del 50% está tomado del README del repo.
- Blog de Hyperbolic sobre PoSP: devolvió 500. Se usó el paper de arXiv.
- Reuters sobre la verificación de ubicación de NVIDIA (doc anterior): 401.
- ISO 27001 y Bittensor: descritos de memoria, sin fuente abierta hoy.
