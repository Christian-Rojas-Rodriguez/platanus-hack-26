# Estado del arte de AI Security (a noviembre de 2026)

> **Notas personales de Jaime para discutir, no una decisión del equipo.**

Investigado por Jaime Aza el 20-11-2026 a partir de la guía de Kairos (`research/papers/kairos-guia-ai-security.pdf`). Varias cifras vienen de preprints de arXiv o de reportes de proveedores que nadie ha auditado. Conviene abrir la fuente antes de citarla ante el jurado.

## Resumen por subárea

| Subárea | Dónde está | Hueco aprovechable |
|---|---|---|
| AI control | ControlArena tiene 15 settings y micro-protocolos. En BashArena, Sonnet 4.5 sabotea sin que lo detecten el 26 % de las veces. Ya existe monitoreo asíncrono. | Ningún setting usa MCP ni navegador. Faltan ataques que eligen cuándo atacar. |
| Guardrails | Constitutional Classifiers++ usa sondas y una cascada que cuesta cerca de 1 % de cómputo extra. «The Attacker Moves Second» rompió 12 defensas con ataques adaptativos. | No hay benchmark de jailbreak en español latinoamericano. Los guards abiertos dejan pasar hasta 75 % del contenido inseguro. |
| Cyber evals | Cybench está saturado (100 %). Mythos resuelve el 73 % de los CTF de nivel experto. El RCT de RAND no encontró uplift significativo en novatos. | Evals en español, medir el uplift al defensor, ranges con un defensor activo. |
| Interpretabilidad | Las NLAs de Anthropic (mayo 2026) tienen pesos abiertos. Hay sondas en producción y circuit-tracer funciona con Gemma 3. | Sondas abiertas para agentes y un medidor de eval awareness. |
| Defensa (d/acc) | Los 7 sistemas de AIxCC son open source y Buttercup corre en un laptop. Están Glasswing, Codex Security y XBOW. | Los detectores de deepfake de voz fallan 29 % en español. Las estafas por WhatsApp crecen en Chile. |

## AI control

- **Marco de Redwood.** Se asume que el modelo puede estar desalineado y se diseñan protocolos que sigan siendo seguros aun así. Se evalúa con un red team (política de ataque) contra un blue team (monitores y protocolos), un modelo no confiable U, uno confiable más débil T y un presupuesto de auditoría humana. [Post](https://blog.redwoodresearch.org/p/the-case-for-ensuring-that-powerful).
- **[ControlArena](https://github.com/UKGovernmentBEIS/control-arena).**
  - Está construido sobre Inspect AI.
  - Trae 15 settings: AgentDojo, Apps, Bash, BashArena, BigCodeBench, Data Poisoning, Eval Sabotage, IAC, Infra, Rogue Eval, SAE Interp Sabotage, SHADE Arena, SWE-bench Django y vLLM.
  - Trae los micro-protocolos trusted monitoring, defer-to-trusted, trusted editing y defer-to-resample.
  - Para crear un setting nuevo se extiende `Setting` y se implementan `get_dataset`, `get_agent_tools`, `get_scorers` y `get_sandbox_config`.
- **[BashArena](https://arxiv.org/abs/2512.15688).** Tiene 637 tareas de administración de Linux y 4 tipos de sabotaje. Sonnet 4.5 consigue un 26 % de sabotajes sin que GPT-4.1-mini lo detecte, con 4 % de falsos positivos.
- **[Monitoreo asíncrono (AISI)](https://arxiv.org/abs/2512.13526).** Es mucho más barato que bloquear cada paso, pero da garantías más débiles.
- **[Menos información para el monitor](https://arxiv.org/abs/2601.21112).** Quitarle información al monitor a menudo mejora la detección: con extract-and-evaluate sube 16,8 pp.
- **Monitorabilidad del CoT.** [Monitoring Monitorability](https://proceedings.mlr.press/v306/guan26h.html) propone 13 evals. Otros trabajos muestran señales en sentidos opuestos sobre si la monitorabilidad sobrevive al aumentar la capacidad del modelo.
- **[TraceGuard](https://arxiv.org/abs/2604.03968).** Salió de un hackathon y terminó en arXiv: puntuar varias dimensiones da 95 % de seguridad, frente a 0 % con un puntaje único.

## Guardrails y robustez adversarial

- **[Constitutional Classifiers++](https://www.anthropic.com/research/next-generation-constitutional-classifiers)** (enero 2026).
  - Usa un exchange classifier que juzga la salida junto con su entrada.
  - Funciona en cascada: una etapa ligera y luego una precisa.
  - Combina sondas lineales sobre las activaciones con un ensemble.
  - El cómputo extra baja de +23,7 % a cerca de +1 % y los rechazos indebidos a 0,05 %.
  - En 1.700 h de red team no apareció ningún jailbreak universal.
- **Sondas de DeepMind.** DeepMind ya usa sondas en producción contra el mal uso cibernético ([2601.11516](https://arxiv.org/abs/2601.11516)). Son frágiles ante cambios de distribución.
- **Prompt injection.**
  - [AgentDojo](https://arxiv.org/abs/2406.13352) es la base de referencia.
  - Las defensas deterministas (CaMeL, FIDES, Progent) casi eliminan los ataques, pero están siendo reevaluadas con ataques adaptativos.
  - **[The Attacker Moves Second](https://arxiv.org/abs/2510.09023):** rompió 12 defensas con un éxito de 71 a 100 %. Por eso toda demo de defensa debe incluir un ataque adaptativo.
- **MCP.**
  - [MCPTox](https://arxiv.org/abs/2508.14925) prueba tool poisoning en 45 servidores reales con 1.312 casos.
  - [MCP-SafetyBench](https://arxiv.org/html/2512.15163) no encontró ningún modelo que rinda bien y a la vez se defienda de forma robusta.
- **Guard models abiertos.**
  - Llama Guard 4.
  - Prompt Guard 2.
  - ShieldGemma.
  - [Qwen3Guard](https://arxiv.org/abs/2510.14276) cubre 119 idiomas; en español obtiene un F1 de 88,9.
  - gpt-oss-safeguard.
  - Según [un estudio de 14 guards](https://arxiv.org/pdf/2605.28830), los más conservadores dejan pasar hasta 75 %.
- **Familias de jailbreak.** Many-shot, Best-of-N, Crescendo multi-turno, cifrados, ataques de reconstrucción y ofuscación de la salida, y ataques adaptativos.
- **Español.**
  - No existe un benchmark latinoamericano.
  - Un [estudio de español mexicano](https://www.emergentmind.com/papers/2605.23157) encontró que el ranking de qué modelo es más seguro cambia según el idioma.
  - [XL-SafetyBench](https://www.alphaxiv.org/abs/2605.05662) incluye España, pero no LatAm.

## Cyber evals

- **[Inspect Cyber](https://inspect.cyber.aisi.org.uk/).**
  - Cada reto es un `eval.yaml` con sandbox en docker o k8s, una flag y `variants` para cambiar las affordances o las pistas.
  - Los datasets se arman con `create_agentic_eval_dataset(root_dir)`.
  - Las buenas prácticas están en el [Evals Playbook de AISI](https://engineering-playbook.aisi.org.uk/evaluate.html).
- **Benchmarks.**
  - [Cybench](https://cybench.github.io/) está saturado.
  - En [CyberGym E2E](https://rdi.berkeley.edu/blog/cybergym-e2e), los mejores modelos llegan a 63-66 %.
  - [ExploitBench](https://arxiv.org/html/2605.14153): los modelos provocan crashes pero no escapan del sandbox de V8.
  - Otros: CyberSecEval, CTIBench, NYU CTF, CVE-Bench y BountyBench.
- **[AISI sobre Mythos Preview](https://www.aisi.gov.uk/blog/our-evaluation-of-claude-mythos-previews-cyber-capabilities).**
  - Resuelve el 73 % de los CTF de nivel experto.
  - Es el primer modelo que completa un cyber range de 32 pasos.
  - Esos ranges no tienen defensores activos.
- **[RCT de uplift de RAND](https://www.rand.org/pubs/research_reports/RRA3892-1.html).**
  - Participaron 157 personas, la mitad con IA, en 3 cadenas de ataque.
  - El uplift en la cadena completa no fue significativo.
  - En el [seguimiento](https://www.rand.org/pubs/research_reports/RRA3892-2.html), un agente autónomo resolvió el mismo reto.
- **Problemas abiertos.** Saturación, brecha de elicitación, contaminación, ranges sin defensor, falta de evals en español y falta de medición del uplift al defensor.

## Interpretabilidad pragmática

- **[A Pragmatic Vision for Interpretability](https://www.alignmentforum.org/posts/StENzDcD3kpfGJssR/a-pragmatic-vision-for-interpretability)** (DeepMind, diciembre 2025).
  - Propone elegir una North Star y una proxy task medible.
  - Antes de complicarse hay que probar métodos simples: prompting, steering, sondas y lectura del CoT.
  - Las SAEs bajan de prioridad.
- **Las «activation NLAs» de la guía.** Son los [Natural Language Autoencoders](https://transformer-circuits.pub/2026/nla/) de Anthropic (mayo 2026).
  - Un verbalizador convierte activación en texto y un reconstructor convierte texto en activación.
  - Detectaron eval awareness que el modelo no verbaliza.
  - Hay pesos para Qwen2.5-7B, Gemma-3 y Llama-3.3-70B ([repo](https://github.com/kitft/natural_language_autoencoders)), y también se pueden usar desde Neuronpedia.
  - Una alternativa son las [Activation Oracles](https://arxiv.org/abs/2512.15674), aunque cuesta usarlas en tareas de seguridad.
- **Circuit tracing.** [circuit-tracer](https://github.com/safety-research/circuit-tracer) funciona con Gemma-2-2B, Llama-3.2-1B y Gemma-3. [Gemma Scope 2](https://deepmind.google/blog/gemma-scope-2-helping-the-ai-safety-community-deepen-understanding-of-complex-language-model-behavior) trae SAEs y transcoders para Gemma 3.
- **Dónde gana.**
  - Las sondas en producción de Anthropic y DeepMind.
  - Las sondas de engaño de Apollo, con AUROC de 0,96 a 0,999.
  - Las sondas contra reward hacking, que superan en 33 pp al monitor LLM en ImpossibleBench.
- **Dónde no gana.**
  - En [AuditBench](https://arxiv.org/abs/2602.22755), la caja negra con andamiaje supera a la caja blanca.
  - Entrenar al modelo contra la sonda le enseña a esquivarla ([Obfuscation Atlas](https://arxiv.org/abs/2602.15515)).
  - Goodfire Ember dejó de ser público en febrero de 2026.

## Defensa (d/acc)

- **[d/acc según Vitalik](https://vitalik.eth.limo/general/2025/01/05/dacc2.html).** Aceleración descentralizada, democrática y diferencialmente defensiva. En ciberseguridad apunta a software verificable y seguro por defecto, con IA que encuentra y arregla bugs antes que el atacante.
- **[AIxCC](https://aicyberchallenge.com/)** (agosto 2025).
  - Ganaron Team Atlanta, Trail of Bits y Theori.
  - Encontraron el 86 % de las vulnerabilidades sintéticas.
  - El costo fue de unos 152 USD por tarea.
  - Los 7 sistemas son open source.
  - [Buttercup](https://github.com/trailofbits/buttercup) corre en un laptop.
  - ATLANTIS fue portado a [OSS-CRS](https://arxiv.org/abs/2603.08566).
- **Después de AIxCC.**
  - Anthropic: Glasswing, con Mythos.
  - OpenAI: Codex Security, antes Aardvark.
  - Google: CodeMender y Big Sleep.
  - XBOW, que lleva más de 1.060 reportes en HackerOne.
- **Ataques con IA.**
  - [Reporte de amenazas de Anthropic, septiembre 2026](https://anthropic.com/threat-intelligence-report-september-2026).
  - [OpenAI](https://openai.com/index/disrupting-malicious-uses-of-ai-scam-operations) documentó redes de estafa dirigidas a LatAm.
  - Para deepfakes de voz: [VoxENES 2026](https://arxiv.org/abs/2607.11706), con un EER de 28,98 % en el mejor detector, y XMAD-Bench.
- **Chile.**
  - Récord de fraudes en 2025, con la suplantación concentrada en WhatsApp ([The Clinic](https://www.theclinic.cl/2026/01/23/fraudes-se-disparan-en-chile-y-la-suplantacion-se-toma-whatsapp-record-en-2025-y-alerta-por-enganos-en-medio-de-tragedia-por-incendios/)).
  - 1 de cada 4 personas ya fue estafada ([G5](https://g5noticias.cl/2026/10/23/1-de-cada-4-chilenos-ya-sufrio-una-estafa-digital-en-la-mitad-de-los-casos-las-perdidas-superaron-los-13-millones/)).
  - Hubo estafas con falsos bonos estatales ([24horas](https://www.24horas.cl/actualidad/nacional/alerta-por-estafas-que-ofrecen-bonos-estatales-tras-los-temporales)).
  - Una filtración ligada a ClaveÚnica ([Emol](https://www.emol.com/noticias/Nacional/2026/05/04/1198990/filtracion-datos-expertos-ciberseguridad-claveunica.html)).
