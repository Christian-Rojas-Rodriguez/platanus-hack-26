# Investigación de Mercado: Red Teaming con Modelos Open-Weight Fine-Tuneados en Sandbox + Hardening Automático

**Contexto:** Platanus Hack 26 — Track de AI Security  
**Fecha:** 21 de noviembre de 2026  
**Idea evaluada:** Servicio que realiza *red teaming* usando modelos de pesos abiertos (*open-weight*) fine-tuneados dentro de un *sandbox* aislado y, en función de las vulnerabilidades identificadas, aplica *hardening* automático.

---

## 1. Resumen Ejecutivo

**Sí, ya existen productos comerciales y open-source en este espacio**, y el segmento está en plena consolidación (con adquisiciones recientes como SplxAI por Zscaler y Lakera por Check Point, además de varias startups de Y Combinator 2024–2026).

Sin embargo, el mercado se divide en **dos frentes distintos** según el objetivo del ataque y el *hardening*, y el ciclo cerrado real (**atacar en sandbox → aplicar hardening → re-verificar que el exploit murió sin romper funcionalidad**) todavía presenta brechas donde existe espacio para diferenciarse.

---

## 2. Mapa de Competidores Existentes

### 2.1. Frente A: Red Teaming y Hardening de Software, APIs e Infraestructura (Pentesting Autónomo + Auto-remediación)

| Producto / Startup | Enfoque | Relación con la idea |
| :--- | :--- | :--- |
| **Novee Security** | Pentesting autónomo para web, mobile, APIs y apps de IA | **El más cercano arquitectónicamente:** entrena/fine-tunea modelos ofensivos especializados (*SLMs*, arquitectura *Model, Harness, Gym*) en lugar de depender solo de APIs cerradas. Valida exploits con PoCs y genera remediación. |
| **XBOW** | Pentesting ofensivo totalmente autónomo | Referente en agentes que encadenan exploits reales y validan vulnerabilidades de forma autónoma. |
| **Corgea** *(YC)* | Pentesting agéntico + remediación automática | Analiza contexto de la app, detecta vulnerabilidades complejas y genera parches/PRs. |
| **CodeAnt AI** *(YC)* | Seguridad ofensiva (black/white/gray-box) + defensa | Detecta fugas/vulnerabilidades y asiste en la generación de fixes directos vía PR. |
| **Parameter** *(ex Hex Security, YC)* / **MindFort** *(YC)* / **Terra Security** | Red teaming / pentesting continuo con enjambres de agentes | Pruebas continuas 24/7 sobre apps e infraestructura con pasos reproducibles. |
| **Horizon3.ai (NodeZero)**, **Pentera**, **BreachLock** | Validación continua de exposición (BAS / pentesting empresarial) | Más orientados a infraestructura y redes corporativas; menor foco en hardening automático de código. |

### 2.2. Frente B: Red Teaming y Hardening de Aplicaciones de IA, LLMs y Agentes

| Producto / Herramienta | Enfoque | Relación con la idea |
| :--- | :--- | :--- |
| **SplxAI** *(adquirida por Zscaler)* | Red teaming automatizado + hardening dinámico | Simula miles de ataques (prompt injection, RAG poisoning, MCP) y realiza **hardening dinámico de system prompts** y guardrails en runtime. |
| **Vijil (DART)** | Red teaming adaptativo multi-turno para agentes | Agentes adversarios que prueban memoria, *tool-calling* y servidores MCP en frameworks como LangGraph/CrewAI. |
| **Fabraix / Nyx** *(YC)* | Red teaming de agentes customer-facing | Evalúa inyecciones indirectas vía documentos, páginas web y salidas de herramientas en entornos controlados. |
| **Mindgard**, **Lakera** *(Check Point)*, **Giskard**, **Haize Labs**, **Dreadnode** | Auditoría continua de agentes, evaluación y guardrails inline | Cubren desde escaneo automatizado hasta firewalls de prompts y cumplimiento (OWASP LLM Top 10, NIST AI RMF, EU AI Act). |
| **Promptfoo**, **Garak** *(NVIDIA)*, **PyRIT** *(Microsoft)* | Frameworks open-source | Resuelven gran parte del motor de ataque y orquestación (*Red vs. Blue*), pero requieren construir la capa de sandbox y hardening automático encima. |

---

## 3. Ecosistema de Modelos Open-Weight Fine-Tuneados para Seguridad Ofensiva

El uso de **modelos open-weight pequeños (SLMs de 7B–30B)** fine-tuneados es una tendencia técnica validada por tres razones:
1. **Sin *refusals* artificiales:** Los modelos propietarios frontera bloquean payloads ofensivos legítimos en pruebas autorizadas.
2. **Privacidad y compliance:** Permiten ejecución 100% *on-prem* o en VPC privado sin exponer código fuente, staging ni credenciales a APIs externas.
3. **Costo en bucles continuos:** Correr miles de iteraciones adversarias en CI/CD con APIs cerradas es costoso; SLMs cuantizados reducen drásticamente el costo por corrida.

**Piezas ya disponibles en el ecosistema:**
* **WhiteRabbitNeo** *(mantenido por Kindo)*: Familia de modelos open-weight (bases Llama/Qwen) fine-tuneados para tareas ofensivas y defensivas de DevSecOps.
* **CAI (Cybersecurity AI)** y datasets comunitarios de CTFs/exploits usados para hacer SFT/DPO sobre bases como **Qwen**, **Llama** y **Gemma**.

---

## 4. Retos Técnicos Clave del Sandbox

Ejecutar modelos fine-tuneados con capacidades ofensivas introduce riesgos de contención que el producto debe resolver por diseño:
* **Aislamiento estricto (efímero):** Micro-VMs o contenedores desechables con privilegios mínimos que se destruyen al terminar la corrida.
* **Control de red (*egress*):** Bloqueo de tráfico saliente no autorizado para evitar movimientos laterales o llamadas fuera del target bajo prueba.
* **Integridad de pesos y artefactos:** Uso obligatorio de `safetensors` y verificación de checkpoints para evitar *backdoors* o ejecución arbitraria en modelos descargados.

---

## 5. Brechas del Mercado y Ángulos de Diferenciación

Competir en "red teaming genérico" frente a incumbents (Zscaler/SplxAI, Check Point/Lakera, XBOW, Novee) es difícil. Sin embargo, existen **tres huecos claros** donde la propuesta puede diferenciarse:

1. **Closed-loop verificado (no solo reportes ni PRs ciegos):**  
   Levantar una copia efímera del target en sandbox → explotar la vulnerabilidad con un PoC reproducible → aplicar el hardening real (parche de código, config de contenedor/IaC, política IAM o guardrail/prompt) → **re-ejecutar el ataque + tests funcionales** para demostrar empíricamente que la vulnerabilidad se cerró sin romper el sistema.
2. **Privacidad total (*local / VPC-first*) con SLMs open-weight:**  
   Alternativa *zero-egress* para equipos y empresas reguladas que no pueden enviar repositorios, agentes internos o ambientes de staging a SaaS externos.
3. **Wedge específico de alto dolor:**
   * **Hardening automático de agentes con *tool-calling* y servidores MCP** (privilegio mínimo, validación de parámetros, aislamiento de herramientas).
   * **Hardening empírico de contenedores e IaC** (`Dockerfile`, Kubernetes, Terraform) validado con exploits reales dentro de micro-VMs.
   * **Loop de seguridad a nivel de Pull Request (CI/CD):** desplegar cada PR en sandbox, atacarlo con el modelo fine-tuneado y proponer un commit de hardening ya verificado antes del *merge*.
