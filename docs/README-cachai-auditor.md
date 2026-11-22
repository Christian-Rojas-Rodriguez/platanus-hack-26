# Cachai: el auditor de modelos servidos como *token-as-a-service*

> **Slogan: PROVISIONAL, falta pulirlo.** Opciones en §1.

- **Equipo:** Christian (Smoke) y equipo, Platanus Hack 26, track AI Safety.
- **Fecha:** sáb 21/11/2026, ~23:15 (hora de Chile, UTC-3).
- **Estado:** idea **en validación**. Por ahora tenemos una entrevista con un posible comprador (Agus, §3) y una investigación del estado del arte. **Todavía no hay mediciones propias**: los números de la demo están como `N`, `X` e `Y` hasta que los midamos.

---

## 1. Nombre y slogan

**Nombre:** **Cachai**. En chileno, "¿cachai?" es "¿entendés?, ¿te das cuenta?". La idea es darte cuenta de qué modelo te están sirviendo de verdad.

**Opciones de slogan (provisionales):**

1. **"¿Cachai qué modelo te están sirviendo?"**
2. **"Pagás por un modelo. Cachai si te lo dan."**
3. **"Medimos lo que tu proveedor de tokens declara."**
4. **"El auditor de proveedores que paga quien compra tokens."**
5. **"Antes de elegir proveedor, cachai."**

---

## 2. El problema

- Los modelos open-weight (GLM, DeepSeek, Kimi, Qwen…) los sirven **decenas de proveedores** con el mismo nombre de modelo y precios muy distintos.
  - En OpenRouter, consultado hoy ~19:55 por la API pública: **GLM-5.3 tiene 48 endpoints**, **15 no declaran cuantización** y el precio de salida va de **1,4 a 6,6 USD por millón de tokens (4,7×)**.
  - DeepSeek V4.1 Flash: 51 endpoints, 20 sin cuantización declarada.
  - Kimi K3: 29 endpoints, 11 sin cuantización declarada.
- **Qué puede hacer mal un proveedor:**
  1. cuantizar o degradar el modelo;
  2. sustituirlo por otro (siempre o en una fracción del tráfico);
  3. romper las tool calls (parsers, plantillas);
  4. inflar la factura de tokens;
  5. inyectar system prompts propios, o retener datos aunque prometa no hacerlo;
  6. cambiar de versión sin avisar;
  7. reconocer las auditorías y servirles el modelo bueno;
  8. no correr donde ni sobre lo que dice.
- **Evidencia pública de que pasa:**
  - *Model Equality Testing* (Gao et al., 2024): **11 de 31 endpoints de Llama** servían una distribución distinta a la de referencia.
  - Artificial Analysis, *Endpoint Accuracy Index* v1.1 (medido entre el 8/10 y el 4/11/2026): **24 de 103 endpoints** quedaron por debajo de una referencia autohospedada. En GLM-5.3 fueron **10 de 26**.
  - K2 Vendor Verifier (Moonshot): la precisión del esquema de tool calls va de **84,63% a 100%** según el proveedor.
- **Por qué es AI Safety y no solo calidad:** si no podés verificar qué modelo te responde, tampoco podés verificar sus evaluaciones de seguridad ni sus salvaguardas. Se cuelga de *Open Problems in Technical AI Governance* (arXiv 2407.14981):
  - §5.2.2 Q52: verificar cómputo sin TEE;
  - §5.4.1: verificar características declaradas sin acceso completo al modelo;
  - §5.3.2: versionado;
  - §8.4: actores de la cadena de suministro.

---

## 3. Validación de Agus (la sección central)

**Fuente:** audio de ~1 min, transcripto (`/workspace/audio/transcript-2026-11-21-2214.txt`, sáb 21/11 ~22:14, hora de Chile). Es una conversación entre alguien del equipo y Agus.

**Antes de leer las citas:**
- La transcripción es automática y **no separa quién habla**. Atribuí cada frase por contexto (preguntas = equipo, respuestas = Agus); donde no estoy seguro, lo marco.
- Las correcciones van así: **[corregido: original → corrección]**. Lo dudoso lleva **[?]**.

### 3.1 Citas textuales (limpias)

**Compraría el producto:**
> "Efectivamente compraría su producto, me lo banco demasiado."

**Para qué lo usaría (elegir proveedores) y por qué:**
> "Personalmente yo usaría un sistema de certificación de proveedores de tokens para decir qué proveedores de tokens quieres usar, porque me he cagado de susto **[corregido: "me cagado" → "me he cagado"]** con los proveedores de tokens que te roban credenciales **[corregido: "van rancredenciales" → "te roban credenciales"]** o funcionan como el pico o te cambian a modelos chinos más baratos."

(*"Funcionan como el pico"* es chileno por "funcionan pésimo".)

**OpenRouter, desconfianza:**
> "Realmente te entrás **[corregido: "te entras"]** en OpenRouter y no puedo confiar en ningún modelo, o sea, en ningún proveedor."

**Encaje de la idea:**
> "Y algo de este estilo creo que podría tener muchísimo sentido."

**¿Conoce algún certificado?** El equipo le preguntó: *"Y vos que estás en la frontera, ¿hay algún certificado esencial que vos veas y confíes? ¿O sentís que todavía no hay ninguno?"*
> "No conozco ninguno."

**Lo que sabe de OpenRouter:**
> "Sé que OpenRouter hace algún tipo de sistema de verificación de proveedores, pero no sé qué hacen o cómo."

**ISO no; estándar propio.** El equipo le preguntó: *"¿Sería como buscar más que todo las ISOs que se alineen con esto?"*
> "No, no, no. Una ISO **[corregido: "Un iso"]** no tiene sentido, van a tener que inventar su propio estándar de certificación, yo creo."

> "Sí, como que te inventáis tu propio estándar de qué es lo que un proveedor tiene que ser y cómo certificás **[?; corregido: "cómo tú se refugias" → probablemente "cómo certificás"]** a un proveedor."

**Qué le importa (y qué no):**
> "Porque ISO es como seguridad, está como ISO 27001 **[?; corregido: "iso 30,000" → probablemente ISO 27001]**, que es de seguridad, pero eso, bueno, me importa mucho menos. Me importa más cómo verificar la infraestructura del proveedor, que sea legítimo, que los requests pasen bien **[?; corregido: "los soques" → probablemente "los requests"]**, que haya infraestructura que asegure que no mire mis datos…"

(La frase sigue con *"como que mirar algo nuevo"*, que no se entiende; no la interpreto.)

**La ventaja comparativa** (atribución probable a Agus, no segura):
> "Pero eso puede ser tu producto, que te da una ventaja comparativa."

### 3.2 Lo que nos llevamos

**Las 4 propiedades que pide:**

| # | Propiedad | De dónde sale |
|---|---|---|
| **P1** | **Infraestructura legítima** del proveedor | "verificar la infraestructura del proveedor, que sea legítimo" |
| **P2** | **Que las solicitudes lleguen bien** (confiabilidad y latencia) | "que los requests pasen bien" + "funcionan como el pico" |
| **P3** | **Que no miren sus datos** | "que haya infraestructura que asegure que no mire mis datos" |
| **P4** | **Que el modelo sea el declarado** | "te cambian a modelos chinos más baratos" |

*Honestidad:* en la lista explícita del final nombró P1-P3. P4 sale de su queja del principio, no de esa lista.

**Las ideas fuerza:**
- **Estándar propio, no una ISO.** Una ISO de seguridad (tipo 27001) certifica procesos, y eso le importa poco. Quiere un estándar que diga qué tiene que cumplir un proveedor de tokens y cómo se lo certifica.
- **No conoce ningún certificado** que hoy confíe para esto.
- **Sabe que OpenRouter verifica algo, pero no qué ni cómo.** El hueco de transparencia es parte del producto (ver §5).
- **Lo usaría para elegir proveedores.** El caso de uso es procurement y ruteo, no una curiosidad.
- **"Eso puede ser tu producto, que te da una ventaja comparativa"**: el estándar en sí puede ser el diferencial.

**Cómo leerlo:** es **una sola entrevista**. Valida el dolor y el caso de uso, **no** la disposición a pagar ni el tamaño del mercado. Agus es un early adopter técnico, no necesariamente quien firma la compra en una empresa.

### 3.3 Preguntas abiertas para repreguntarle

1. **Credenciales:** ¿qué te pasó exactamente? ¿Con qué proveedor o revendedor? ¿Fue a través de OpenRouter o de una API directa o proxy no oficial?
   - Con OpenRouter, el proveedor de inferencia en principio no recibe tu API key. Si el robo fue ahí, nos interesa mucho; si fue en un revendedor, cambia el alcance de P1.
   - Esto es inferencia nuestra, sin verificar.
2. **Cuánto pagarías**, y con qué modelo de cobro: ¿suscripción mensual, por endpoint auditado, por volumen de tokens? ¿Cuánto gastás hoy en tokens open-weight por mes?
   - Ancla de mercado: Benchlist cobra **USD 499/mes**, pero al proveedor.
3. **¿Quién decide** en tu equipo o empresa qué proveedor se usa? ¿Lo pagarías vos o tendría que pasar por compras o seguridad?
4. **De P1-P4, ¿cuál pagarías primero?** ¿Te alcanza con evidencia estadística ("no detectamos desviación") o necesitás prueba criptográfica?
5. **¿Qué te haría confiar en el sello?** Quién lo emite, cada cuánto, si es público o privado.
6. **"Modelos chinos más baratos":** ¿lo detectaste vos o lo sospechás? ¿Cómo te diste cuenta?

---

## 4. La solución

**Una ficha y un sello por *endpoint*** (por ejemplo, "GLM-5.3 @ proveedor X"), no por empresa:
- se mide **en forma continua**, no una vez al año;
- **lo paga el comprador** de tokens, no el proveedor, para evitar el conflicto de interés de que pague el auditado.

### 4.1 Niveles de evidencia (cada afirmación lleva el suyo)

| Nivel | Qué es | Ejemplo |
|---|---|---|
| **E1, declarado** | El proveedor lo afirma o lo firma por contrato | Política ZDR, cuantización declarada, SOC 2 |
| **E2, medido black-box** | Un tercero lo mide desde afuera, con fecha, método, muestra e intervalo de confianza | Uptime, tool calls válidas, desviación contra una referencia |
| **E3, atestado** | Evidencia criptográfica o auditoría con acceso, verificable por el cliente | TEE con atestación que mide el hash de los pesos |

**Regla de oro:** con E2 **nunca** se emite un certificado de privacidad ni de identidad. E2 solo dice "no detectamos desviación con esta potencia".

### 4.2 Qué se puede verificar en cada propiedad

| | Black-box (E2) | Con cooperación (E1/E3) | No verificable |
|---|---|---|---|
| **P1. Infraestructura legítima** | Que la empresa existe, dominio y TLS, red y jurisdicción (ASN/IP), listas de abuso | Datacenters declarados, SOC 2/ISO, atestación de hardware | Ubicación física de la GPU sin atestación; subcontratistas ocultos |
| **P2. Las solicitudes llegan bien** | Uptime, errores, cortes a mitad de stream, tiempo al primer token y throughput (p50/p95), truncado de contexto, topes de salida ocultos, validez de tool calls, **re-conteo de tokens visibles** con el tokenizer público | SLA, logs de incidentes | Comportamiento en picos que no reproducimos; tokens de razonamiento ocultos |
| **P3. No miran mis datos** | **Casi nada.** Datos trampa ("canarios") pueden probar una filtración, **nunca su ausencia** | Política ZDR + contrato (E1); **TEE con atestación** estilo Tinfoil o Apple PCC (E3) | Que un proveedor sin TEE no mire ni guarde datos |
| **P4. Modelo declarado** | **Desviación contra una referencia:** tests de distribución (MMD), divergencia con temperatura 0, benchmarks con IC, huella de familia, monitoreo en el tiempo | Cuantización declarada (E1); TOPLOC, Token-DiFR, TEE que mida los pesos (E3) | **Identidad exacta**; sustitución en una fracción muy chica del tráfico o fuera de la auditoría |

### 4.3 Insignias separadas, nunca un certificado único

- **"Confiabilidad medida"** (P2, E2)
- **"Sin desviación detectada vs. referencia"** (P4, E2)
- **"Pesos atestados"** (P4, E3)
- **"Privacidad atestada (TEE)"** (P3, E3)
- **"Política ZDR declarada"** (P3, E1)

### 4.4 Cómo mide (diseño heredado de Testigo)

Es un proxy o SDK compatible con la API de OpenAI que se pone delante de OpenRouter o de cualquier proveedor:
- toma una **muestra del tráfico real** (1-5%), mezclada y sin marca, más una suite propia rotada y no publicada;
- la duplica contra la **API first-party del laboratorio** como referencia de caja negra, sin GPU propia;
- arma una **score card por proveedor**:
  1. equivalencia con el oficial (divergencia con T=0 + MMD);
  2. integridad de tool calls;
  3. **factura**: tokens cobrados vs. re-contados con el tokenizer público;
  4. **inyección**: tokens de prompt de sobra;
  5. cuantización declarada vs. estimada;
- si algo se desvía, manda una alerta y puede sacar al proveedor de la rotación (`provider.ignore`).

Muestrear el tráfico del cliente **reduce** el riesgo de que el proveedor reconozca la auditoría, pero **no lo elimina**.

---

## 5. Qué verifica hoy OpenRouter, y qué no

Fuentes oficiales, leídas hoy:

| Mecanismo | Qué hace | Tipo | Qué no garantiza |
|---|---|---|---|
| **Alta de proveedores** ([apply](https://openrouter.ai/providers/apply)) | Piden API compatible con OpenAI que devuelva el uso de tokens, `/models` con ubicación de los datacenters, política de datos publicada y email corporativo. Siguen NDA, llamada, cuestionario y documentos de seguridad, y tráfico de prueba. Textual: *"SOC 2 and zero data retention help, but neither is required."* | E1 + pruebas funcionales | Que el modelo o la ubicación sean los declarados |
| **Uptime** ([integración](https://openrouter.ai/docs/guides/providers/integration)) | Éxitos sobre total, con 100 requests como mínimo. Con 95% o más el ruteo es normal; entre 80% y 94%, degradado; bajo 80%, solo fallback. Publican tiempo al primer token y throughput | E2 sobre tráfico real | Calidad del contenido |
| **Exacto / Auto Exacto** ([blog](https://openrouter.ai/blog/announcements/provider-variance-introducing-exacto/)) | Desde agosto de 2025 revisan cada tool call: JSON válido, que la tool exista, que el esquema coincida. Auto Exacto suma benchmarks internos | E2 | Identidad del modelo. Ellos mismos dicen que **no** es *"a broader statement on endpoint or provider quality"* |
| **Penalización por calidad** ([traffic routing](https://openrouter.ai/docs/guides/providers/traffic-routing)) | Un endpoint con tool calls rotas o con *"benchmark accuracy well below what the model should score"* recibe solo tráfico de exploración | E2 | No se publica como certificado por endpoint |
| **Zero Data Retention** ([ZDR](https://openrouter.ai/docs/guides/features/zdr), [blog](https://openrouter.ai/blog/insights/zero-data-retention/)) | Tres niveles por endpoint, exigible por request (`zdr: true`), lista pública. Si no conocen la política de un endpoint, asumen que guarda y entrena | **E1, política o contrato** | **Que el proveedor efectivamente no mire ni guarde.** Su etiqueta de datos *"is not a definitive source… best knowledge"* |
| **Cuantización** | Campo `quantization` por endpoint | E1 | Que sea cierta (15 de 48 dicen "unknown" en GLM-5.3) |

**En síntesis:** OpenRouter mide bien la confiabilidad y las tool calls sobre tráfico real, y mantiene una política de datos declarada. **No verifica pública ni técnicamente** la identidad del modelo, la cuantización real ni la no retención. Por eso Agus "sabe que verifican algo, pero no qué": lo que hacen es real, pero no se publica como ficha o sello por endpoint.

---

## 6. Competencia y diferenciación honesta

**No es 0→1.** La categoría "verificar proveedores de inferencia" ya existe:

| Quién | Qué hace | Límite frente a Cachai |
|---|---|---|
| **Artificial Analysis**, Endpoint Accuracy Index | Benchmarks contra una referencia autohospedada (pesos oficiales); público y gratis | Foto puntual; su referencia es **más fuerte** que nuestra API first-party |
| **Benchlist** | Atestación firmada de benchmarks y alertas de drift; **USD 499/mes** | **Lo paga el proveedor**; suite fija |
| **TrackLLM** | Monitoreo abierto de cambios en cientos de endpoints | Gratis y amplio; no mira factura ni inyección |
| **K2 Vendor Verifier** (Moonshot) | Tool calls de Kimi contra la API oficial | Un solo modelo |
| **OpenRouter Exacto** | Calidad de tool calls sobre tráfico de producción | Es del intermediario y no es un sello |
| **Tinfoil / Phala** (TEE) | Prueba criptográfica de los pesos | Solo en sus propios endpoints; nosotros **no** damos prueba |
| **Papers:** Model Equality Testing, Token-DiFR, TOPLOC, LLMmap, Cai et al. | Métodos de detección | Investigación, o requieren cooperación o re-ejecutar el modelo |

**La cuña (plausible, sin probar):**
- assurance **continuo**, **del lado del comprador**, sobre **su propio tráfico**, contra la referencia first-party;
- **re-conteo de tokens** para detectar sobrecobro e inyección;
- un **estándar con niveles de evidencia E1/E2/E3** por endpoint, que es lo que pidió Agus.

Las piezas existen por separado; el aporte es **integrarlas y separar los niveles de evidencia**.

**Corrección explícita:** antes dijimos que "todas las auditorías usan prompts fijos o públicos". **Es falso.**
- K2VV mantiene privado el 50% de su set.
- Exacto usa tráfico de producción.
- ModelWatch usa specs que define el cliente.
- Token-DiFR, TOPLOC y los TEE auditan cualquier request.

Lo que sí se sostiene: los servicios públicos de benchmark por endpoint (AA, Benchlist, K2VV) usan suites fijas y al menos en parte conocidas, y por eso son vulnerables a la "evasión de benchmarks" que describen Cai et al. Que no publiquen cómo se defienden no prueba que no lo hagan.

**En el pitch:** decir **"cuña"**, nunca "nadie lo hace".

---

## 7. Lo que NO prometemos

- **No certificamos privacidad black-box.** Desde afuera no se puede probar que un proveedor no mire ni guarde tus datos. Para eso hace falta un TEE con atestación (E3) o confiar en un contrato (E1), y lo decimos con esa etiqueta.
- **No certificamos la identidad exacta del modelo** con evidencia estadística. "No detectamos desviación" ≠ "es el mismo modelo".
- **No acusamos de fraude.** Publicamos mediciones con IC y causas posibles (parser, plantilla, cuantización).
- **No geolocalizamos GPUs.** A través de OpenRouter no se puede; la jurisdicción que mostramos es la declarada más la red de la API.
- **No contamos tokens de razonamiento ocultos.** Los auditores que existen fueron rotos (Token Inflation).
- **La referencia first-party puede estar cuantizada.** Hablamos de "equivalencia con el oficial", no "con los pesos".

---

## 8. MVP para la hackatón y la demo

**Objetivo:** **un failure mode en vivo y un número.**

**Regla:** solo contra cuentas y sistemas propios.
- El "proveedor tramposo" es **un proxy local nuestro**.
- Los proveedores reales se consultan solo con **uso normal de la API** desde nuestra propia cuenta.
- No hay ataques contra terceros.
- El token del proxy Platanus no va en código ni en logs (enmascarar `/t/***/`, buscar el prefijo del token con `rg` antes de cada commit).

### 8.1 Qué construir

1. **`cachai scan`**: para un modelo open-weight (DeepSeek V4.1 Flash por costo, o GLM-5.3 por titular), consulta unos 10 proveedores fijados (`provider: {only: [...], allow_fallbacks: false}`) y la API oficial. Llena una tabla con:
   - divergencia contra el oficial;
   - % de tool calls válidas;
   - Δ de tokens cobrados vs. re-contados;
   - cuantización declarada.
2. **Proveedor tramposo propio:** un proxy local que:
   - desvía una fracción *p* del tráfico a una variante más barata;
   - reconoce los prompts de auditoría públicos y les sirve el modelo honesto.
3. **Auditoría ciega:** muestra del tráfico "del cliente" (simulado por nosotros) contra el oficial, con test estadístico calibrado (oficial vs. oficial como piso de ruido).
4. **Ficha por endpoint** con P2 y P4 en E2, y P3 mostrado como E1 (ZDR declarado), para que se vea la honestidad del estándar.

### 8.2 La demo (≈1 min)

1. `cachai scan` en vivo: la tabla se llena.
2. Switch al proveedor tramposo: la auditoría de prompts fijos marca ✅ y la auditoría ciega de Cachai marca ❌, con su p-valor.
3. Cierre: *"Esto lo paga quien compra tokens, no quien los vende. Y te decimos qué está medido, qué está declarado y qué está atestado."*

### 8.3 El número titular (completar con mediciones; NO inventar)

> "GLM-5.3 tiene 48 proveedores en OpenRouter; 15 no declaran cuantización y el precio varía 4,7× *(dato real de hoy)*. Un proveedor tramposo que desvía el `p`% del tráfico pasa una auditoría de prompts fijos; Cachai lo detecta en **`N`** requests. De 10 proveedores reales, **`X`** se apartan del oficial y **`Y`** cobran tokens de más."

### 8.4 Riesgos y chequeos previos

- **Acceso y costo:** confirmar con un request que el proxy deja pasar `provider` y devuelve `usage` y el proveedor que respondió, y a qué cuenta va el costo.
- **Presupuesto estimado:** ≲ USD 60, sin GPU (estimación del diseño, no un gasto medido).
- **No determinismo con T=0** entre hardware: calibrar oficial vs. oficial y usar umbrales con IC.
- **Re-conteo:** hay diferencias legítimas de plantilla (pocos tokens). Calibrar con el oficial.
- **Pre-registrar** los umbrales antes de la corrida real.
- **Backup:** si el escaneo en vivo falla, mostrar datos cacheados más el tramposo local, que no depende de terceros. El video de backup se entrega a las 08:00 (hora de Chile).

---

## 9. Cómo llegamos acá

1. **Cachai, revisor de PRs.** Empezamos con Cachai como revisor de seguridad de pull requests (`cachai check`: ataques y tests reservados, todo o nada).
2. **Feedback de los mentores:**
   - El mentor de la reunión de producto (mediodía) pidió **branding mínimo, una metáfora y una muy buena demo**: "nosotros creamos un producto, el producto se llama X y funciona de esta forma".
   - El mentor de la noche dijo que **honeypots y firewalls están saturados**, que los prompt guards para LLMs autoalojados "ya existen" y que no los ve novedosos. Sugirió **dedicar ~20 minutos a listas de *Open Problems***. Agregó que **un buen demo de un resultado experimental puede ganar el track** y que lo que importa es "si sirve o no sirve".
3. **Open problems.** Leímos *Open Problems in Technical AI Governance* (arXiv 2407.14981). No es la lista de AI Control que nombró el mentor, pero tiene la sección de Compute y Security. Smoke dejó de lado el Cachai revisor de PRs y pidió un **producto vendible** que salga de esos open problems.
4. **Del "Testigo" a Cachai auditor.** La intuición de Smoke (cada vez más proveedores sirven modelos chinos open-weight) se convirtió en "Testigo", un auditor ciego de proveedores. Investigamos el estado del arte, corregimos el claim de los prompts fijos y armamos un borrador de estándar con niveles de evidencia.
5. **Agus (22:14)** validó el dolor: compraría una certificación de proveedores de tokens con un estándar propio, no una ISO. Ahí renombramos el producto a **Cachai, el auditor de modelos servidos en token-as-a-service**.

---

## 10. Fuentes

**Internas (en el box del equipo):**
- `/workspace/audio/transcript-2026-11-21-2214.txt`: entrevista con Agus.
- `auditoria-proveedores-inferencia-2026-11-21.md`: estado del arte, OpenRouter y borrador del estándar.
- `security-compute-2026-11-21.md`: open problems de Compute y Security, y diseño de Testigo.
- `transcripcion-mentor-noche-2026-11-21.md` y `transcripcion-mentor-producto-2026-11-21.md`: feedback de los mentores.

**Paper base:**
- Reuel, Bucknall et al., *Open Problems in Technical AI Governance*, TMLR 2025, [arXiv 2407.14981](https://arxiv.org/abs/2407.14981).

**Verificación de proveedores:**
- Gao, Liang, Guestrin, *Model Equality Testing*, [arXiv 2410.20247](https://arxiv.org/abs/2410.20247).
- Cai et al., *Are You Getting What You Pay For?*, [arXiv 2504.04715](https://arxiv.org/abs/2504.04715).
- Karvonen et al., [Token-DiFR](https://adamkarvonen.github.io/machine_learning/2025/11/28/difr.html).
- Prime Intellect, [TOPLOC](https://github.com/PrimeIntellect-ai/toploc).
- Pasquini et al., *LLMmap*, [arXiv 2407.15847](https://arxiv.org/abs/2407.15847).
- *Token Inflation*, [arXiv 2605.30040](https://arxiv.org/abs/2605.30040).
- Moonshot, [K2 Vendor Verifier](https://github.com/MoonshotAI/K2-Vendor-Verifier).
- [TrackLLM](https://www.trackllm.net/).
- [Benchlist](https://benchlist.ai/for/inference-providers).
- [ModelWatch](https://modelwatch.app/).
- Artificial Analysis, *Endpoint Accuracy Index* (detalle y fechas en el doc de auditoría).

**OpenRouter:**
- [Become a Provider](https://openrouter.ai/providers/apply)
- [Integración de proveedores](https://openrouter.ai/docs/guides/providers/integration)
- [Traffic routing](https://openrouter.ai/docs/guides/providers/traffic-routing)
- [Exacto](https://openrouter.ai/blog/announcements/provider-variance-introducing-exacto/)
- [ZDR](https://openrouter.ai/docs/guides/features/zdr)
- [Blog ZDR](https://openrouter.ai/blog/insights/zero-data-retention/)
- [Provider routing](https://openrouter.ai/docs/guides/routing/provider-selection)

**Datos medidos hoy:**
- API pública de endpoints de OpenRouter, sin clave, ~19:55 (hora de Chile).
