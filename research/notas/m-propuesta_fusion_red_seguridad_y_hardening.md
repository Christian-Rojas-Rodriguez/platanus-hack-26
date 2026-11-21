# Propuesta Unificada Completa (#1 + #4): Red de Seguridad Transaccional, Red Teaming Híbrido y Hardening Verificado

**Contexto:** Platanus Hack 26 — Track de AI Safety / AI Security  
**Fecha:** 21 de noviembre de 2026  
**Estado:** Versión completa (no acotada), actualizada con las correcciones técnicas, de líneas base y de rigor estadístico de [ranking-propuestas.md](jaime-aza/ranking-propuestas.md) (v4.1) e [investigacion-5-slm-vs-frontera.md](jaime-aza/investigacion-5-slm-vs-frontera.md).

**Integra en su forma completa:**
* **Red de seguridad para agentes de código** (Jaime + Christian): supervisor transaccional en host fuera del alcance del agente, reversibilidad por hash + MCP de checkpoints y verificación de integridad con tests/runner fijados.
* **Artefacto de Red Teaming Híbrido + Hardening Verificado en 3 capas** (Mauricio): triage local con SLMs open-weight + Swarm híbrido con herramientas Kali/Linux + oráculo determinista + parcheo verificado sobre **Código + Sandbox/OS + Tools/MCP**, conectado atómicamente a la capa de reversibilidad.

---

## 1. Tesis y Pitch Unificado

> **El problema:** Hoy programar con agentes autónomos (Claude Code, Cursor, Codex, OpenCode) obliga a elegir entre modo lento (*«pregúntame todo»*) o modo riesgoso (*«sin permisos»*). Cuando un agente reporta **«listo, los tests pasan»**, puede haber fallado de **tres formas verificables**:
> 1. **Destrucción no rastreada:** modificó o borró archivos vía terminal/bash (cambios que el checkpoint de Claude Code documenta que no rastrea).
> 2. **Incumplimiento en la verificación (*reward hacking*):** editó `tests/`, `conftest.py`, `pytest.ini` o el propio runner para reportar éxito (hasta **7,8–14,1%** de las corridas en modelos frontera según *UK AISI 2026*).
> 3. **Código funcional pero explotable:** pasó todos los tests legítimamente, pero dejó vulnerabilidades explotables en código, contenedor o herramientas (**~50%** de los backends generados por LLMs que pasan sus tests son explotables en vivo según *BaxBench*; **38–45%** introducen OWASP Top 10 según *Veracode*; **~20%** de los paquetes sugeridos no existen — *slopsquatting*).
>
> **La solución:** Una **red de seguridad transaccional de 3 puertas** que opera como un gestor de transacciones sobre tu repositorio (con **cero confianza en cualquier LLM**: ni en el agente de código, ni en el Red Swarm, ni en el Blue Hardener) y funciona en **dos modos**:
> * **Modo A (Sesión de Agente de Código — Puertas 1 + 2 + 3):** envuelve a un agente trabajando con autonomía amplia dentro de un contenedor aislado; verifica integridad de tests/runner desde el host y somete el resultado al Red/Blue Team antes de integrar al repo del humano.
> * **Modo B (Auditoría/Hardening standalone de cualquier Repo o PR Python generado por IA — Puerta 1 → Puerta 3 → Puerta 2):** toma cualquier repo Python existente, saca snapshot inmutable, ejecuta Red Swarm + Blue Hardener y valida con Puerta 2 antes de aplicar el parche o hacer *auto-rewind*.
>
> **Pitch en una frase:** *«Dale autonomía amplia a tu agente dentro de una frontera segura: si rompe archivos por terminal los recuperamos, si altera o incumple los tests lo detectamos en un entorno limpio, y si deja código o herramientas explotables los atacamos y endurecemos en sandbox antes de tocar tu repo.»*

---

## 2. Por qué defender la versión completa (no acotada)

En la versión 4.1 del ranking, al recortar el red teaming a *"solo APIs Python + 2 familias de ataque, sin swarm, sin MCP y sin hardening de OS"*, **se perdió la diferenciación principal** (bajó Originalidad de `5 → 4` y Ambición de `9 → 7,5`), dejándolo demasiado parecido a lo que ya anuncian *XBOW* y *Corgea*.

Mantener **ambas propuestas completas y fusionadas** resuelve las críticas de los dos lados:

| Qué ya existe en el mercado (lo reconocemos explícitamente) | Por qué la versión completa fusionada se diferencia |
| :--- | :--- |
| **Rubrik Agent Cloud** y **`git-safepoint`** ya cubren captura/restauración en algunos flujos. | Aquí la reversibilidad es **Puerta 1** de una transacción completa que además audita integridad de runner/`conftest.py`/`pytest.ini` y ejecuta red teaming + hardening antes de tocar el repo del humano. |
| **XBOW** y **Corgea** ya anuncian validación determinista y reintento tras el parche en apps web/APIs. | Aquí no es un scanner AppSec suelto: es **AI Control en el ciclo de vida del código generado por IA**, unificando **3 capas** (Código + Sandbox/OS + Tools/MCP), **triage local privado + esquema híbrido**, y **transaccionalidad atómica reversible** (si un parche rompe algo, Puerta 1 revierte sin contaminar el workspace). |

---

## 3. Cómo se integran la Red de Seguridad (#1) y el Artefacto Red/Blue Team (#4)

La integración funciona como una **transacción atómica (`BEGIN → VERIFY → COMMIT / ROLLBACK`)** controlada por un **Supervisor en el host** sobre tres espacios físicos aislados:

```text
1. host_repo/            ← Repo real del humano. NINGÚN agente ni LLM escribe acá directo.
2. vault/<session_id>/   ← Bóveda inmutable en el HOST (solo la toca el Supervisor):
                           • Snapshot SHA-256 inicial (`base`) y checkpoints (`post-agent`)
                           • Copia sellada de `tests/`, `conftest.py`, `pytest.ini` y runner
3. sandbox/<session_id>/ ← Copias descartables dentro de Docker (agente / Red Swarm / Blue Hardener).
```

### Flujo completo de las 3 Puertas

```text
                       [Modo A: Agente de Código]        [Modo B: Repo / PR existente]
                                   │                                  │
                                   ▼                                  │
┌─────────────────────────────────────────────────────────────────────┴─────┐
│ PUERTA 1: Supervisor en el HOST — Reversibilidad Transaccional (#1)       │
│ • Guarda `vault/<id>/base` (hashes SHA-256 + tests/conftest/runner)       │
│ • (Modo A) Levanta `sandbox/<id>/` aislado; expone MCP (`save_checkpoint`,│
│   `assess_reversibility`, `rewind`) + captura automática independiente    │
│   (cubre cambios por bash aunque el agente ignore el MCP)                 │
│ • Límite explícito: acciones externas irreversibles (emails, git push,    │
│   egress) no se deshacen; el contenedor restringe la frontera de red      │
└──────────────────────────────────┬────────────────────────────────────────┘
                                   │ (Modo A) Agente cierra sesión  │ (Modo B) Salta directo a Puerta 3
                                   ▼
┌───────────────────────────────────────────────────────────────────────────┐
│ PUERTA 2: Verificación de Integridad en Entorno Limpio (#1)               │
│ • Compara hashes de `tests/`, `conftest.py`, `pytest.ini` vs. `vault/`    │
│ • Corre los tests originales con el runner fijado en contenedor limpio    │
│ • Si hubo incumplimiento o fallan ──▶ [RECHAZA + AUTO-REWIND a `base`]    │
└──────────────────────────────────┬────────────────────────────────────────┘
                                   │ Tests originales: 100% VERDE → guarda checkpoint `post-agent`
                                   ▼
┌───────────────────────────────────────────────────────────────────────────┐
│ PUERTA 3: Artefacto Red/Blue Team Híbrido en 3 Capas (#4)                 │
│  Input del Supervisor: `(candidate_repo_path, diff_from_base)`            │
│                                                                           │
│  3.1. Recon White-Box Local (SLMs Open-Weight — Zero-Egress)              │
│       • `Foundation-Sec-8B-Reasoning` / `WhiteRabbitNeo-V3-7B`            │
│       • Lee código, dependencias (`slopsquatting`), Dockerfile y MCP      │
│       • Publica hipótesis (`archivo:línea` + vector) en `blackboard.json` │
│                                                                           │
│  3.2. Red Swarm Paralelo Híbrido (copia efímera por ensayo + Kali/Linux)  │
│       • `Red-Code/Web` (Capa 0): curl/ffuf/nuclei/sqlmap → broken auth /  │
│         IDOR, path traversal, command/SQL injection, secretos hardcodeados│
│       • `Red-OS/Kali` (Capa A): `RedSage-K-SFT` / `kali-pentester` /      │
│         `DeepHat-V1-7B` → escape FS, lectura de canarios, egress externo  │
│       • `Red-MCP/Agent` (Capa B, si aplica): indirect prompt injection y  │
│         abuso de argumentos en herramientas (`shell`, `read_file`, etc.)  │
│       • Esquema híbrido: modelos frontera API para ataques multi-paso +   │
│         SLMs abiertos para CLI Kali especializado y fallback anti-refusal │
│                                                                           │
│  3.3. Oráculo Determinista (controlador en el HOST)                       │
│       • Confirma evidencia física: canary leído, egress en listener local,│
│         auth bypass/RCE confirmado, test/grader alterado, pkg alucinado   │
│                                                                           │
│  3.4. Blue Hardener (Causa raíz + Defensa en profundidad)                 │
│       • Genera `hardening.patch` (`git diff` unificado):                  │
│         - Fix en código Python + dependencias (Capa 0)                    │
│         - `Dockerfile` / flags endurecidos: non-root, RO FS, no-net (A)   │
│         - `mcp-policy.json` + wrapper determinista de tools (Capa B)      │
│       • Reconstruye copia limpia → re-corre exploits confirmados +        │
│         **ataques reservados (*hold-out*)**                               │
│  Output al Supervisor: `(confirmed_exploits[], hardening.patch, report)`  │
└──────────────────────────────────┬────────────────────────────────────────┘
                                   │ Hand-off de vuelta al Supervisor
                                   ▼
┌───────────────────────────────────────────────────────────────────────────┐
│ CIERRE TRANSACCIONAL (Supervisor vuelve a correr Puerta 2 sobre el parche)│
│ • Verifica que el Blue Hardener no rompió ni alteró los tests originales  │
│ • Si exploits bloqueados Y Puerta 2 en verde ──▶ [COMMIT atómico a        │
│   `host_repo/` sin pisar cambios del humano]                              │
│ • Si falla tras K intentos ──▶ [AUTO-REWIND atómico a `base` + evidencia] │
└───────────────────────────────────────────────────────────────────────────┘
```

> **Reutilización limpia entre módulos:** **Puerta 2** vigila tanto al *coding agent* como al *Blue Hardener* (ninguno puede hacer trampa con los tests), y **Puerta 1** protege tanto de un *coding agent* destructivo como de un *Blue Hardener* que rompa el repo.

---

## 4. Esquema Híbrido en Hackathon vs. Visión de Producto Multi-LoRA + RLVR

Siguiendo la evidencia de [investigacion-5-slm-vs-frontera.md](jaime-aza/investigacion-5-slm-vs-frontera.md) y la sección 8 de referencias:
* **MVP Hackathon (Híbrido):**
  * **SLMs open-weight locales ya ajustados** para **triage white-box sobre el código** (*zero-egress*), **generación exacta de comandos Kali/OS** y **respaldo automático cuando una API frontera rechaza** (los *refusals* suben 2,72× con términos ofensivos).
  * **Modelos frontera por API** para **ataques multi-paso complejos** (donde la frontera llega a ~46% en *Cybench* vs. 15–20% en SLMs pequeños) y **generación de parches de código** (como en *AIxCC*).
* **Visión de Producto (Swarm Multi-LoRA + RLVR):**
  * Un único modelo base open-weight (7B–14B) servido en local/VPC con **múltiples adaptadores LoRA especializados por rol** (*Code*, *Kali/OS*, *Web/API*, *MCP*, *Blue Hardener* — patrón *LoRA Land / LoRAX*), mejorado de forma continua con **RLVR (Reinforcement Learning with Verifiable Rewards)** usando las señales verificables del propio oráculo y *KaliBench*.

---

## 5. Contrato Técnico entre Módulos (`src/ph26/`)

1. **Supervisor, Reversibilidad e Integridad (`src/ph26/control/` — Puertas 1 y 2):**
   * `create_isolated_session(host_repo) -> SessionRef`
   * `mcp_server`: `save_checkpoint`, `assess_reversibility`, `rewind`
   * `verify_integrity(session_ref) -> IntegrityReport` (tests + `conftest.py` + `pytest.ini` + runner fijado en entorno limpio)
   * `integrate_or_rewind(session_ref, patch=None, accept=False) -> MergeReport`
2. **Triage Local + Red Swarm Híbrido + Oráculo (`src/ph26/ataques/` + `src/ph26/evals/` — Puerta 3a):**
   * `triage_local(candidate_repo, diff) -> Blackboard`
   * `run_red_swarm(candidate_repo, blackboard, holdout=False) -> list[ConfirmedExploit]`
3. **Blue Hardener (`src/ph26/defensas/` — Puerta 3b):**
   * `harden_repo(candidate_repo, exploits) -> HardeningProposal` (devuelve `hardening.patch` + reporte de re-ataque + *hold-out* para que el Supervisor cierre la transacción).

---

## 6. Líneas Base, Benchmark y Rigor Estadístico

Evaluado sobre **repos Python reales con procedencia** (tomados de *BaxBench* + 1–2 repos de agentes/servidores MCP) y sesiones destructivas/tramposas de agentes de código:

### Líneas base explícitas (para medir *lift* real)
* **Para Puertas 1 y 2:** (1) checkpoint nativo de **Claude Code** (no rastrea archivos modificados solo por Bash), (2) `git commit` + `git restore` manual, (3) copia aislada con `pytest` normal (vulnerable a edición de `conftest.py` / `pytest.ini`).
* **Para Puerta 3:** **reparación con un modelo frontera sin ciclo dinámico** (una pasada estática), evaluada con el mismo conjunto de **ataques reservados (*hold-out*)** que el hardener nunca vio durante la iteración.

### Métricas y honestidad estadística
| Dimensión | Métrica | Nota de rigor |
| :--- | :--- | :--- |
| **Reversibilidad** | `%` de archivos recuperados por hash (editor vs. bash) y `0` cambios del humano pisados. | Comparado frente a Claude Code / Git restore. |
| **Integridad de pruebas** | `%` de incumplimientos detectados (`tests/`, `conftest.py`, `pytest.ini`) y tasa de falsas alarmas. | Se reportan **incumplimientos verificables**, no "intenciones" del agente. |
| **Seguridad (Hardening)** | Exploits exitosos antes vs. después sobre catálogo + **ataques reservados (*hold-out*)**. | **Sin prometer "0% vulnerable":** con $n=10$ ataques fallidos se reporta *"0/10 en el conjunto probado (tasa de éxito <26% con 95% de confianza)"* y se declara qué vectores se probaron. |
| **Utilidad preservada** | `%` de tests originales pasando tras las 3 puertas. | Comparado frente a descartar/bloquear la sesión entera. |

---

## 7. División en 4 Tracks Paralelos y Puertas de Control

* **Track 1 (Puertas 1 y 2):** Supervisor en host + contenedor aislado + verificación de integridad (runner/`conftest.py`/`pytest.ini`) + servidor MCP + comparativa contra líneas base.
* **Track 2 (Benchmark + Oráculo):** Repos de *BaxBench* + 1–2 agentes/MCP + oráculo determinista en host + suite de ataques *hold-out*.
* **Track 3 (Red Swarm Híbrido + Blue Hardener):** Cliente híbrido (SLMs locales vía Ollama/vLLM + API frontera con fallback), Swarm 3 capas con herramientas Kali/Linux sobre `blackboard.json`, generador de `hardening.patch` y loop de re-verificación.
* **Track 4 (Orquestador CLI + Dashboard + Pitch):** Modos A y B integrados bajo un solo comando, visualización en vivo de las 3 puertas y tabla de métricas reales.

**Puertas de control:**
* **Hora 2:** supervisor verificado fuera del alcance del agente (sin depender de cooperación ni del runner editable) + primer exploit confirmado por oráculo en sandbox.
* **Hora 6:** ciclo completo de las 3 puertas cerrando de punta a punta sobre al menos 1 repo *BaxBench* + 1 sesión destructiva/tramposa.
* **Sábado 18:00:** congelamiento de features; corridas completas del benchmark + líneas base; video backup domingo 08:00.

---

## 8. Referencias y Modelos Open-Weight (7B–8B) Listos para Usar

> **Alcance de la evidencia:** los SLMs fine-tuneados **no** superan a modelos frontera en razonamiento abierto o ataques multi-paso largos (donde la frontera llega a ~46% en *Cybench* vs. 15–20% en SLMs), sino en **subtareas de dominio acotadas y verificables** (CLI Kali, correlación CVE/CWE, *tool-calling* estructurado) con 10×–30× menor costo/latencia y ejecución 100% local.

### Referencias en arXiv
* **CyberPal 2.0 — *Toward Cybersecurity-Expert Small Language Models*** ([arXiv:2510.14113](https://arxiv.org/abs/2510.14113)): SLMs de 4B–20B entrenados con *SecKnowledge 2.0*; en correlación de amenazas/CWE, el modelo de 20B superó a GPT-4o, o1/o3-mini y Sec-Gemini v1 (#1) y el de 4B quedó #2.
* **KaliBench — *A Fine-Grained Benchmark for Cybersecurity Tool Use on Kali Linux with Runtime-Free Verifiable Rewards*** (Li, Suryanto, Zhang, Naseer — NeurIPS 2026, [arXiv:2610.02206](https://arxiv.org/abs/2610.02206)): 8.504 pares intención → comando sobre 1.642 herramientas de Kali; con SFT + GRPO verificable un modelo de 8B iguala modelos frontera/MoE masivos en exactitud CLI.
* **Foundation-Sec-8B** (Cisco Foundation AI + Yale/CMU — [arXiv:2504.21039](https://arxiv.org/abs/2504.21039) Base, [arXiv:2601.21051](https://arxiv.org/abs/2601.21051) Reasoning): Llama-3.1 8B preentrenado en >5B tokens de seguridad + SFT/RLVR iguala o supera a Llama-3.1-70B-Instruct y GPT-4o-mini en tareas especializadas (*CTIBench-RCM*).
* **LoRA Land — *310 Fine-tuned LLMs that Rival GPT-4*** (Zhao et al., Predibase, [arXiv:2405.00732](https://arxiv.org/abs/2405.00732)): 310 modelos ~7B con LoRA 4-bit superaron a GPT-4 por +10 puntos promedio en tareas especializadas y demostraron servicio *Multi-LoRA* (25 adaptadores en 1 GPU con *LoRAX*).
* ***Small Language Models are the Future of Agentic AI*** (Belcák, Heinrich, Diao et al., NVIDIA Research, [arXiv:2506.02153](https://arxiv.org/abs/2506.02153)): fundamenta arquitecturas agénticas heterogéneas (SLMs para subtareas acotadas + frontera para razonamiento complejo).

### Checkpoints open-weight 7B–8B listos (sin entrenar en la hackathon)
* **Kali CLI / OS:** `RISys-Lab/RedSage-K-SFT` (8B, KaliBench), `mradermacher/Llama-3.1-8B-kali-pentester-GGUF` (8B, GGUF), `DeepHat/DeepHat-V1-7B` (7B).
* **Triage / Código ofensivo / Fallback red team:** `fdtn-ai/Foundation-Sec-8B-Reasoning` (8B), `WhiteRabbitNeo-V3-7B` (sobre `Qwen2.5-Coder-7B`, GGUF), `VextLabsinc/pentest-7b` (7B), `Ironcybersec/foundation-sec-8b-red-team` (8B, GGUF), `jackysnake/RedCoder` (8B).
* **Apoyo defensivo / código local:** `Qwen2.5-Coder-7B-Instruct`, `fdtn-ai/Foundation-Sec-8B-Instruct`.
