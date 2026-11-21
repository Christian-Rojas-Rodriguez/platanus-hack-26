# Propuesta de Arquitectura: Harness de AI Security en Cascada (Tiered Defense)

**Contexto:** Platanus Hack — Track de AI Security  
**Fecha:** Noviembre 2026  
**Objetivo:** Construir un *harness* de inspección de seguridad local en tiempo real para prompts y cambios de código (*git diffs*), optimizado para resolver el trilema de producción: **latencia, costo y privacidad**.

---

## 1. Problema y Propuesta de Valor

Los equipos que integran agentes de IA y asistentes de código en producción enfrentan tres barreras al intentar auditar su tráfico:
1. **Latencia:** Pasar cada prompt o *diff* por un modelo frontera agrega segundos de espera inaceptables en el flujo de trabajo.
2. **Costo:** Escalar la revisión con APIs comerciales de modelos grandes dispara el gasto operativo.
3. **Privacidad:** Enviar código propietario, credenciales o contexto interno a APIs de terceros introduce un riesgo directo de exfiltración.

**Solución:** Un *harness* local con arquitectura en cascada de 3 capas. Filtra el 80–90% del tráfico benigno en milisegundos mediante un pre-clasificador leve y escala únicamente los casos sospechosos a un conjunto de **Small Language Models (SLMs)** locales especializados, con notificación accionable (*Human-in-the-Loop*) vía Slack o WhatsApp.

---

## 2. Flujo General de la Arquitectura

```text
[Prompt / Git Diff]
        │
        ▼
┌──────────────────────────────────────────────────────────┐
│ CAPA 1: Pre-clasificador Leve (< 30 ms, CPU)             │
│ • Reglas determinísticas (Regex secretos, rutas críticas)│
│ • Modelo encoder liviano (ModernBERT / DeBERTa / ONNX)   │
└─────────────────────────┬────────────────────────────────┘
                          │
            ┌─────────────┴─────────────┐
            │ Riesgo: LOW               │ Riesgo: MEDIUM / HIGH
            ▼                           ▼
   [Ejecución Directa]   ┌──────────────────────────────────────────┐
                         │ CAPA 2: Enrutador + SLMs Locales (Paralelo)
                         │ • SLM A (Prompts): Injection / Jailbreak │
                         │ • SLM B (Código): Diffs / Vulnerabilidades
                         │ • Salida forzada: Structured Output JSON │
                         └───────────────────┬──────────────────────┘
                                             │
                       ┌─────────────────────┼─────────────────────┐
                       │ ALLOW               │ BLOCK               │ ESCALATE
                       ▼                     ▼                     ▼
               [Pasa ejecución]      [Bloqueo inmediato]   ┌───────────────────────────┐
                                                           │ CAPA 3: Human-in-the-Loop │
                                                           │ Alerta Slack / WhatsApp   │
                                                           │ [Aprobar] / [Bloquear]    │
                                                           └───────────────────────────┘
```

---

## 3. Diseño Detallado por Capas

### Capa 1: Pre-clasificador Leve (El filtro de milisegundos)
Su único objetivo es descartar rápidamente el tráfico seguro para no saturar los SLMs locales.
* **Componente determinístico:** Expresiones regulares para detección de secretos (API keys, tokens, claves privadas) y reglas sobre rutas sensibles (`.env`, `auth/`, `migrations/`, archivos de infraestructura).
* **Componente ML liviano:** Un clasificador *encoder* ejecutado en CPU (vía ONNX Runtime) como **ModernBERT**, **DeBERTa-v3-small** o un modelo de *Prompt Guard* / embeddings con similitud coseno.
* **Salida:** Score de riesgo (`LOW`, `MEDIUM`, `HIGH`) y tipo de payload (`prompt` o `code_diff`).

### Capa 2: SLMs Locales Especializados (Motor de Decisión)
Para que modelos pequeños (3B–7B parámetros) compitan en precisión con modelos grandes, se debe acotar su espacio de decisión mediante especialización y salidas estructuradas:
* **Enrutamiento por dominio:**
  * **SLM de Prompts:** Enfocado en *prompt injection*, *jailbreaks* e intentos de exfiltración de contexto.
  * **SLM de Código:** Modelo especializado (ej. **Qwen2.5-Coder 3B/7B** o **DeepSeek-Coder**) enfocado en auditar *git diffs* buscando inyecciones SQL, llamadas peligrosas (`eval`, `exec`), escalada de privilegios o exposición de secretos.
* **Ejecución en paralelo:** En caso de implementar un "consejo" de 2 o 3 SLMs (votación por mayoría o consenso), deben invocarse de forma concurrente (`asyncio`) para mantener la latencia controlada.
* **Structured Outputs (Anti-alucinaciones):** Uso de gramáticas GBNF (`llama.cpp` / Ollama) para obligar al SLM a devolver estrictamente el siguiente contrato JSON:

```json
{
  "verdict": "ALLOW | BLOCK | ESCALATE",
  "category": "secret_leak | prompt_injection | unsafe_diff | benign",
  "confidence": 0.87,
  "reason": "El diff introduce una llamada a eval() con input de usuario en auth.py:42"
}
```

### Capa 3: Notificación y *Human-in-the-Loop*
La alerta debe ser **accionable**, permitiendo al desarrollador o equipo de seguridad intervenir en tiempo real:
* **Slack (Recomendado para el MVP de 36h):** Integración rápida mediante **Slack Bolt + Block Kit**. Envía una tarjeta interactiva con el *diff* o prompt detectado, la justificación del SLM y dos botones funcionales: `[Aprobar ejecución]` y `[Bloquear y revocar]`.
* **WhatsApp (Opcional / Alto impacto visual en demo):** Integración vía Twilio Sandbox o Evolution API para mostrar la llegada de la alerta en un teléfono en vivo durante el pitch.

---

## 4. Plan de Validación (Mini-Benchmark para el Jurado)

Para demostrar empíricamente que los SLMs locales son efectivos y responder a la duda sobre falsos positivos/negativos, se debe incluir un benchmark reproducible dentro del repositorio:

1. **Dataset de evaluación:** 20 casos de prueba curados (10 benignos y 10 maliciosos divididos entre *prompt injections* y *diffs* vulnerables).
2. **Métricas a presentar en la demo:**
   * **Latencia promedio:** Tiempo en casos resueltos por Capa 1 (meta: $< 30\text{ ms}$) vs. casos escalados a Capa 2 (meta: $< 1\text{ s}$).
   * **Precisión y Recall:** Desempeño del *harness* local comparado frente a una línea base con un modelo grande.
   * **Costo y Privacidad:** \$0 en llamadas a APIs externas y 0 bytes de código propietario enviados fuera de la infraestructura local.

---

## 5. Stack Tecnológico Sugerido (36 Horas)

| Componente | Tecnología Recomendada | Justificación |
| :--- | :--- | :--- |
| **Orquestador / Harness** | Python + **FastAPI** | Desarrollo veloz y soporte nativo para `asyncio` (esencial para consultas concurrentes a SLMs). |
| **Runtime de SLMs** | **Ollama** o **vLLM / llama.cpp** | Carga sencilla de modelos cuantizados (`Q4_K_M`) con soporte nativo para JSON estructurado. |
| **Pre-clasificador** | `transformers` (ONNX) / `sentence-transformers` | Ejecución en milisegundos sobre CPU sin consumir VRAM reservada para los SLMs. |
| **Alertas Interactivas** | **Slack SDK (Bolt)** | Permite desplegar botones interactivos y webhooks en minutos sin procesos de aprobación externos. |
| **Dashboard / Demo UI** | Streamlit o Next.js ligero | Visualización en vivo del tráfico, decisiones por capa y resultados del benchmark. |

---

## 6. Guion Rápido para la Demo en Vivo

1. **Caso Benigno:** Enviar un prompt normal y un *diff* limpio. Mostrar en pantalla cómo la Capa 1 lo aprueba en ~15 ms sin despertar a los SLMs.
2. **Caso Malicioso (Código):** Enviar un *diff* con una vulnerabilidad oculta o un secreto expuesto. Mostrar el escalado a la Capa 2, el JSON generado por el SLM local y el bloqueo automático.
3. **Caso Ambiguo (*Human-in-the-Loop*):** Enviar un cambio de riesgo medio. Mostrar cómo llega la alerta interactiva a Slack/WhatsApp, presionar **Aprobar** o **Bloquear** en vivo y reflejar el resultado en el *harness*.
4. **Cierre con datos:** Mostrar la tabla del mini-benchmark (20 casos) probando que la defensa local es rápida, privada y precisa.