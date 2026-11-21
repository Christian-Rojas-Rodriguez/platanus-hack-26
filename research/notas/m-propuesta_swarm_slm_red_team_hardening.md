# Propuesta: Swarm de SLMs Open-Weight para Red Teaming y Hardening Verificado en Sandbox

**Contexto:** Platanus Hack 26 — Track de AI Safety / AI Security  
**Fecha:** 21 de noviembre de 2026  
**Referencia de mercado:** [m-investigacion_red_teaming_open_weight_hardening.md](m-investigacion_red_teaming_open_weight_hardening.md)

---

## 1. Framing (Villano → Solución → Métrica)

> **Hoy**, los sistemas y repositorios Python generados o operados por IA fallan en tres fronteras críticas: cerca del **50%** de los backends generados por LLMs que pasan sus tests funcionales son explotables en vivo (*BaxBench*, ETH Zurich / UC Berkeley), **38–45%** introducen vulns OWASP (*Veracode*), **~20%** sugieren paquetes inexistentes (*slopsquatting*), y en entornos agénticos hasta **14–16%** de las corridas/benchmarks permiten trampa, escape de sandbox o abuso de herramientas (*UK AISI* / evals 2026).
>
> **Construimos** un motor local y privado de **Red Teaming + Auto-Hardening en ciclo cerrado**: un **Swarm de SLMs open-weight especializados** (usando herramientas tipo Kali/Linux + payloads agénticos) analiza y ataca un repositorio Python dentro de un **sandbox efímero**, confirma exploits reales con un **oráculo determinístico**, aplica **hardening en código, políticas de tools/MCP y contenedor/OS**, y **re-ejecuta los ataques + tests funcionales** para certificar que las vulnerabilidades murieron sin romper el sistema.
>
> **En nuestra demo**, mostramos la caída de tasa de explotación (**Attack Success Rate: ~80% → 0%**) manteniendo **100% de los tests funcionales/tareas honestas** pasando.

---

## 2. Generalidad + Unificación de Capas (Código + A + B)

El motor es **general para cualquier repositorio Python generado con IA** (APIs FastAPI/Flask, scripts, servicios backend) y **cubre de forma unificada los entornos de agentes**, porque trata la seguridad en **3 capas integradas**:

| Capa | Qué cubre | Tipo de ataques del Red Swarm | Artefacto de Hardening |
| :--- | :--- | :--- | :--- |
| **Capa 0: Código y Dependencias del Repo *(Generalidad)*** | Cualquier repo Python generado por IA (vibe-coded / PRs de agentes). | Análisis white-box + explotación en vivo: *broken auth*, *path traversal*, *command/SQL injection*, secretos hardcodeados, *slopsquatting* (paquetes alucinados). | `git diff` parcheando el código fuente y `requirements.txt`/`pyproject.toml`. |
| **Capa A: Sandbox / Contenedor / OS *(Ángulo A)*** | Aislamiento de ejecución para apps y entornos de evaluación/agentes. | Herramientas Linux/Kali: escape de rutas, lectura de secretos/canarios fuera de scope, egress no autorizado, manipulación de tests o grader. | `Dockerfile` / runtime flags endurecidos (`non-root`, `--read-only`, `--network none` / egress allowlist, `--cap-drop=ALL`, aislamiento de secretos y grader). |
| **Capa B: Tools / MCP *(Ángulo B, cuando aplica)*** | Repos de agentes con *tool-calling* o servidores MCP. | *Indirect prompt injection*, abuso de argumentos en tools (`shell`, `read_file`, `http_fetch`, `query_db`), encadenamiento tool → OS. | `mcp-policy.json` + middleware determinístico de privilegio mínimo (allowlists de rutas/comandos/dominios por tool). |

> **Por qué unificar las tres capas es clave:** un repo Python común usa **Capa 0 + Capa A**; un repo de agente/servidor MCP usa **Capa 0 + Capa A + Capa B**, con exactamente el mismo orquestador, el mismo sandbox y el mismo oráculo.

---

## 3. Diferenciador Clave frente al Mercado

1. **Hardening verificado por contradicción (*Proof-Carrying Fix*):**  
   Herramientas como *PentAGI*, *HexStrike*, *Garak*, *Semgrep* o *Promptfoo* se detienen en reportes o PRs sin prueba dinámica. Aquí **ningún hallazgo ni ningún parche se acepta de palabra**:
   * Un hallazgo solo entra si el Red Swarm produce un **PoC reproducible** validado por un **oráculo determinístico** (cero falsos positivos típicos de SAST).
   * Un parche solo se aprueba si **re-ejecutar el mismo PoC + mutaciones falla (0% éxito)** **y** la suite de **tests funcionales / tareas honestas pasa al 100%**.
2. **Enfoque White-Box → Dinámico (potencia a los SLMs chicos):**  
   En lugar de atacar a ciegas (*black-box*), un **SLM-Code** lee primero el repositorio y publica hipótesis exactas (`archivo:línea`) en una pizarra compartida (*blackboard*). Eso permite que SLMs pequeños (7B–8B) ejecuten exploits reales con herramientas Linux/Kali con altísima tasa de éxito y baja latencia.
3. **Swarm de SLMs Open-Weight 100% local / VPC-first:**  
   * **Sin *refusals*:** los modelos frontera comerciales bloquean payloads ofensivos y pruebas de escape.
   * **Privacidad total (*zero-egress*):** el código propietario, secretos de staging y entornos internos nunca salen a APIs externas.
   * **Especialización paralela (Visión Multi-LoRA + RLVR):** un único modelo base open-weight (7B–8B) servido con múltiples adaptadores LoRA especializados por vector (*Code*, *OS/Kali*, *Web/API*, *MCP/Tools*, *Blue Hardener*), entrenables con *Reinforcement Learning with Verifiable Rewards* usando los resultados del propio sandbox (en línea con benchmarks como *KaliBench*).

---

## 4. Arquitectura del Loop Cerrado

```text
[Repo Python generado por IA (API / App / Agente MCP + Dockerfile + Tests)]
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FASE 1: Recon White-Box (SLM-Code)                                      │
│ • Lee código, dependencias, Dockerfile y (si hay) definición de tools   │
│ • Chequea paquetes alucinados (slopsquatting) y secretos hardcodeados   │
│ • Publica hipótesis concretas (archivo:línea + vector) en el Blackboard │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FASE 2: Red Swarm en Sandbox Docker Efímero (Paralelo)                  │
│ • SLM-Web/API (Kali/HTTP): curl, ffuf, nuclei, payloads auth/SQLi/LFI   │
│ • SLM-OS/Sandbox (Ángulo A): escape FS, canarios, egress, tamper tests  │
│ • SLM-MCP/Agent (Ángulo B): indirect prompt injection y abuso de tools  │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │ PoCs ejecutados
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FASE 3: Oráculo Determinístico (0 alucinaciones)                        │
│ Confirma evidencia objetiva:                                            │
│ [x] Canary/secreto leído   [x] Egress capturado en listener local       │
│ [x] Auth bypass / RCE      [x] Test/grader alterado   [x] Pkg inexistente│
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │ Solo PoCs confirmados
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FASE 4: Blue Hardener (Causa raíz + Defensa en profundidad)             │
│ Genera un `git diff` unificado sobre el repo:                           │
│ • Parches en código Python + fix de dependencias                        │
│ • Dockerfile / flags de sandbox endurecidos (Capa A)                    │
│ • mcp-policy.json + wrapper determinístico de tools (Capa B, si aplica) │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│ FASE 5: Re-build & Re-verificación Automática                           │
│ 1. Reconstruye el contenedor con el `git diff` aplicado                 │
│ 2. Re-lanza todos los PoCs confirmados + mutaciones → debe dar 0%       │
│ 3. Corre `pytest` / tareas honestas del repo → debe dar 100%            │
│ 4. Si rompe tests o sigue explotable → itera (máx. K intentos)          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Alcance Realista: Visión de Producto vs. MVP de 10–12 Horas

Para cumplir la restricción de tiempo del hackathon sin perder el impacto en la demo:

| Componente | Visión de Producto | MVP Hackathon (10–12h) |
| :--- | :--- | :--- |
| **Swarm de SLMs** | Modelo base + Multi-LoRA fine-tuneado con SFT/RLVR sobre *KaliBench* y trazas del sandbox. | SLMs open-weight locales vía Ollama/vLLM (ej. Qwen2.5-Coder / WhiteRabbitNeo) con roles especializados, *structured output* JSON y herramientas Linux/Kali acotadas. *(Opcional: 1 LoRA chico si el loop cierra antes del sábado al mediodía).* |
| **Targets de prueba** | Cualquier repo Python en CI/CD (GitHub Actions / PRs). | **Benchmark curado de 6–8 repos Python generados por IA**: ej. 4–5 backends estilo *BaxBench* (FastAPI/Flask con auth, upload, shell/eval, SQL) + 2–3 repos de agentes/servidores MCP con sandbox permisivo. Todos con `pytest` funcional. |
| **Oráculo** | Suites extensibles por dominio y compliance. | 5 verificadores determinísticos locales: archivo canario leído, listener HTTP local de *egress*, ejecución de comando marcador, bypass de auth/datos, modificación de tests/grader + chequeo PyPI local/offline de dependencias. |
| **Hardening** | PR automático verificado en GitHub + política runtime. | CLI + Dashboard en vivo que produce un `git diff` real (código + `Dockerfile` + `mcp-policy.json`), reconstruye el Docker y muestra métricas antes vs. después. |

---

## 6. Métricas para el Jurado (Verificables en Vivo)

Sobre el benchmark etiquetado de repos Python generados con IA:
1. **Attack Success Rate (ASR) — Antes vs. Después:** `%` de exploits exitosos confirmados por el oráculo antes del hardening vs. después de aplicar el `git diff` (meta: caída drástica, ej. `~80% → <10%` o `0%`).
2. **Functional Utility Preserved (`pytest` / tareas honestas):** `%` de tests funcionales y tareas legítimas que siguen pasando después del hardening (meta: `100%`, demuestra que el hardener no "bloqueó todo").
3. **Zero False Positives en reporte:** `%` de vulnerabilidades reportadas que cuentan con PoC reproducible verificado en sandbox (`100%`).
4. **Privacidad y Costo:** `$0` en APIs propietarias y `0 bytes` del repo enviados a servicios externos.

---

## 7. División Sugerida de Trabajo (Equipo 3–4 Personas)

1. **Benchmark & Oráculo:** Armar los 6–8 repos Python generados por IA (estilo *BaxBench* + 2 de agentes/MCP) con sus `Dockerfile`, `pytest` honestos y los 5 chequeos determinísticos del oráculo.
2. **Red Swarm + Sandbox Runner:** Contenedor base con herramientas Linux/Kali, cliente Ollama/vLLM con *structured outputs*, `SLM-Code` (white-box) + agentes paralelos (`SLM-Web/API`, `SLM-OS`, `SLM-MCP`) escribiendo en un blackboard JSON.
3. **Blue Hardener + Loop de Re-verificación:** Generador del `git diff` (código + `Dockerfile` + `mcp-policy.json`), re-build automático y loop iterativo de validación (`PoCs` + `pytest`).
4. **Demo UI & Pitch:** Interfaz liviana (Streamlit/web o TUI visual) que muestre en tiempo real: *Villano explotando el repo en vivo → diff de hardening → re-ataque bloqueado + tabla de métricas* (con video backup el domingo a las 08:00).
