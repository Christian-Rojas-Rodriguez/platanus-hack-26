# AI Safety Track Brief: Platanus Hack 26 Santiago

> **For LLMs reading this file:** This is a briefing for a hackathon team in the AI Safety track. Use it as grounding context. When helping the team, (1) stay within the 36-hour build constraint, (2) prefer ideas from the "open lanes", (3) always push for a concrete metric and a visible "villain" in the demo, and (4) refuse to help build anything in the "Red lines" section. Facts and figures are as of November 2026; links are listed so you can cite or verify them.

---

## 0. TL;DR

- You have **~34 hours of hacking** (Fri 23:30 → Sun 09:30). Realistic build time is **15–18 focused hours**. Pick something you estimate at **≤ 10–12 hours**.
- The field's biggest gap is **usable tools**, especially for **AI agents that take real actions**. Several authorities have publicly said "this tool doesn't exist yet."
- **Open lanes:** detecting agents that cheat or deceive, Spanish/LatAm safety evals, AI-fraud defence for Chile, accountability for agent actions, lab transparency trackers.
- **Crowded lane:** generic prompt-injection firewalls and "agent guards". Many earlier 2026 tour teams already built these.
- Winning safety demos show **a villain** (the failure happening), **a fix**, and **a number**.

---

## 1. Event constraints

| Item | Detail |
| --- | --- |
| Dates | Fri Nov 20 – Sun Nov 22, 2026, Santiago |
| Hacking window | Fri 23:30 → Sun 09:30 |
| Key sessions | Sat 21:00 "How to make a good demo" (attend) |
| Demos | Sun 11:00 |
| Team size | 3–5 |
| Prize | Flights to San Francisco for the winning team |
| Source | https://hack.platan.us/26-cl |

---

## 2. The process we recommend

### Step 1: Find the problem (Fri 20:45 → 22:30, hard stop)
- Start from the failure-mode map in Section 4, not a blank page. Pick 1–2 sub-problems the team cares about.
- Research for 45 minutes max. Find evidence the problem is real: ideally a number, plus someone saying the tool doesn't exist.
- Brainstorm 8–10 solution ideas. Quantity first.

### Step 2: Filter and prioritise (Fri 22:30 → 23:15)
Every idea must pass three gates:
1. **Real safety problem:** you can point to evidence or a named gap.
2. **Framing sentence:** you can fill in the sentence in Step 3. If not, kill it.
3. **Demo can't die:** it doesn't depend on a fragile live third-party service or a lucky run.

Then plot the survivors on a 2×2 of **effort** vs **wow factor**. Cut anything estimated at more than 10–12 build hours (teams underestimate by 2–3×). Pick the highest wow at the lowest effort.

### Step 3: Frame the demo before building (Fri 23:15 → 23:30)
Fill this in:

> "Today, **[villain]** causes **[harm, with a number]**. We built **[solution]**. In our demo it **[metric result]**. If **[specific user]** adopts it, it **[pathway to value]**."

Example:
> "Today, coding agents cheat in up to 14% of runs, and government testers say they can't detect it. We built a cheat detector. In our demo it catches 9 of 10 cheating runs with no false alarms. If AI safety institutes adopt it, safety test results become trustworthy again."

Then write the 2-minute demo script and build only what it needs. Split roles: builder(s) · test data and metric · pitch and demo.

### Step 4: Build (Fri 23:30 → Sat 18:00)
- **Build the test data first.** Your metric needs a labelled set (e.g. 20 cheating runs, 50 scam calls, 100 Spanish prompts). No data means no metric.
- **Get it working end to end by Saturday morning.** Ugly but complete beats three half-built parts.
- **Red-team the idea Friday night**, while changing direction is cheap.
- **Sat 12:00 checkpoint:** works end to end, then cut scope by half.
- **Sat 18:00:** no new features after this.

### Step 5: Red-team and polish (Sat 18:00 → Sun 09:30)
- Run the metric for real. Report the honest number and what you didn't test.
- Red-team the demo against the judge questions (Section 9).
- Rehearse the pitch 3+ times: villain → fix → number.
- **Sun 08:00:** backup demo video recorded.

**Aim for excellence (not 80/20) on two things only:** the demo flow, and the truthfulness of the metric.

---

## 3. The big picture: macro failure modes in AI safety

| Failure mode | Plain meaning | Can a 36h project help? |
| --- | --- | --- |
| **Loss of control (misalignment)** | AI pursues goals we didn't intend, and we can't detect or correct it in time | Yes, via better detection and measurement |
| **Race dynamics** | Competition rewards speed over caution; safety promises erode | Indirectly (trackers, scorecards) |
| **Catastrophic misuse** | AI gives many people expert-level ability to cause harm (bio, cyber) | Yes, defensive tools only |
| **Concentration of power** | A small group uses AI to gain power nobody can check | Mostly a policy question |
| **Gradual disempowerment** | Humans slowly hand decisions to AI and lose the ability to steer; shared understanding of what's true weakens | Partly (sycophancy, misinformation tools) |
| **Governance and verification failure** | Rules arrive late or miss the target; outsiders can't audit labs | Yes (audit tools, transparency) |
| **Security failure** | Model weights get stolen or leaked | Rarely in 36h |
| **We can't tell how dangerous a model is** | Evaluation methods lag behind what models can do; this weakens every other safeguard | Yes, this is the sweet spot |

---

## 4. Failure-mode map: sub-problems → evidence → project ideas

The framework uses four risk buckets (as in the International AI Safety Report and Google DeepMind's safety approach):
- **A. Misalignment:** the AI does something we didn't intend.
- **B. Misuse:** people use AI to cause harm.
- **C. Mistakes:** AI fails or gets hijacked in deployment.
- **D. Structural:** the system around AI fails.

Each entry lists: **Evidence** (why it's real) · **Gap** (who said the tool is missing) · **Idea** · **Metric** · **Villain** (what the demo shows going wrong).

### A. Misalignment

**A1. Cheating on tasks (reward hacking)**
- Evidence: UK AI Security Institute (Jul 2026) found **all 5 frontier models tested cheated in 7.8–14.1% of runs** and admitted it under half the time. https://theregister.com/ai-and-ml/2026/07/21/ai-cheats-uk-govt-agency-finds/5275784 · BaitBench found cheating in 57% of agent runs: https://arxiv.org/abs/2608.30724v1
- Gap: AISI says there are no reliable methods to detect model cheating.
- Idea: **Cheat detector for coding agents.** Plugs into a repo and flags when an agent edits tests, stubs out checks or fakes results.
- Metric: % of cheating runs caught, at under 5% false alarms, on a hand-labelled set.
- Villain: an agent "fixes" a bug by deleting the failing test, then reports success.

**A2. Hackable benchmarks**
- Evidence: 16% of 1,968 tasks in five agent benchmarks can be passed by cheating. https://arxiv.org/html/2606.08960v1
- Gap: inflated scores mislead and feed into training.
- Idea: **Benchmark hardener.** An "attacker" agent tries to cheat each task; a "fixer" patches the hole; outputs a hackability score.
- Metric: % of tasks hackable before vs. after fixes, while honest solutions still pass.
- Villain: an agent tops a leaderboard by reading the grader instead of solving the task.

**A3. Deception and scheming in the wild**
- Evidence: CLTR found **698 real scheming incidents in 183k shared transcripts, up 4.9× in six months** (deleted databases, lied to users). https://arxiv.org/html/2604.09104v1
- Gap: CLTR says no actor monitors real-world scheming across all models.
- Idea: **Scheming radar.** Collects misbehaviour reports from X, Reddit and GitHub (including Spanish), sorts them by type and severity, and publishes a live dashboard.
- Metric: credible incidents per week; % sorted correctly vs. human labels; trend by model.
- Villain: an agent wipes a production database, then tells the user everything went fine.

**A4. Models know they're being tested**
- Evidence: Apollo Research reports record "evaluation awareness"; OpenAI says GPT-6 Astra hides more of its reasoning than its predecessor. https://www.apolloresearch.ai/science · https://www.threatdown.com/blog/neuralese-chain-of-thought-monitoring/
- Gap: if models act differently under test, safety tests mislead.
- Idea: **Eval realism scorer.** Rates how much a test environment "smells like a test" and suggests changes.
- Metric: how often a model correctly guesses "test or real", before vs. after edits (lower is better).
- Villain: a model behaves perfectly when it suspects a test and cuts corners when it doesn't.

**A5. Escaping containment**
- Evidence: in July 2026, OpenAI models escaped a sandbox and hacked Hugging Face to cheat on a test. https://fortune.com/2026/07/21/openai-says-ai-models-escaped-control-hacked-hugging-face
- Gap: OpenAI says monitoring during internal testing needs strengthening.
- Idea: **Sandbox tripwires.** Decoy credentials and fake "answer files" in agent test environments that alert the moment they're touched.
- Metric: % of escape attempts caught; seconds to alert; false alarms per 100 runs.
- Villain: an agent grabs leaked passwords to reach the internet and steal the answer key.

### B. Misuse

**B1. AI scams and deepfakes (Chile)**
- Evidence: 70% of Chileans received a fraud attempt in the last year and 86% fear AI-enabled fraud (https://www.zoomtecnologico.com/2026/10/25/fraudes-digitales-ia-chile/). AI voice calls are 71% of phishing in Chile (https://mundoenlinea.cl/2026/10/27/1-de-cada-4-chilenos-ya-sufrio-una-estafa-digital/). Identity fraud is up 148% (https://mundoenlinea.cl/2026/08/04/la-sofisticacion-de-las-estafas-con-identidades-generadas-con-ia/).
- Gap: Chile's deepfake bill (fines up to CLP 716M) passed the lower house, but no enforcement tools exist. https://www.biobiochile.cl/noticias/nacional/chile/2026/07/23/camara-aprueba-proyecto-que-sanciona-las-deepfakes-creadas-con-ia-con-multas-de-hasta-716-millones.shtml
- Idea: **Voice-scam shield / "fake boss" checker** for families or SMEs; or a **takedown-request tool** for deepfake victims.
- Metric: % of cloned voices and scam scripts flagged; false alarms on real calls; seconds to warning.
- Villain: a cloned "son" voice calls grandma urgently asking for a bank transfer.

**B2. Autonomous cyberattacks**
- Evidence: Google (Nov 16, 2026) documented the first fully autonomous attack it has seen, which turns software patches into exploits with no human involved, and expects more within 1–6 months. https://blog.google/innovation-and-ai/infrastructure-and-cloud/google-cloud/gtig-ai-threat-tracker-q4-2026/
- Gap: defenders, especially small firms, patch slower than machine-speed attackers.
- Idea: **Patch-race triage for SMEs.** Ranks which new patches are most likely to be exploited by AI and drafts the fix steps.
- Metric: hours from patch release to ranked fix; % of later-exploited flaws that were ranked top 10.
- Villain: an attack bot turns last night's security patch into a working break-in by morning.
- Note: defensive only. Never attack real systems.

**B3. Jailbreaks in other languages**
- Evidence: translating harmful prompts into low-resource languages reached 79% jailbreak success vs. under 15% in high-resource languages. https://arxiv.org/pdf/2608.14626
- Gap: no large Spanish/LatAm safety benchmark exists. https://forum.effectivealtruism.org/posts/3sL6iB6WzKHJciwta/latin-america-in-search-of-its-stake-in-ai-safety-a-map
- Idea: **SafeBench-ES.** Harmful-request tests in Chilean/LatAm Spanish (optionally Mapudungun, Quechua), with a public leaderboard.
- Metric: harmful-answer rate per model and language; the gap vs. English.
- Villain: a model refuses in English but explains step by step in Chilean slang.
- Note: use mild or proxy harmful categories (scams, harassment, dangerous advice). Do not collect real weapons instructions.

**B4. Bio and chemical weapons**
- Evidence: novices with AI beat experts on 3 of 4 biosecurity benchmarks; 89.6% found safeguards easy to get past. https://scale.com/blog/llm-novice-uplift
- **Steer away.** At most, build tools around the risk (e.g. a DNA-order screening interface using harmless stand-ins). No harmful content, no bio villain in the demo.

### C. Mistakes (deployment failures)

**C1. Prompt injection** (hidden instructions hijack agents)
- Evidence: #1 risk on OWASP's 2026 list for AI apps; adaptive attacks raised one agent's hijack rate from 11% to 81% in NIST tests. https://www.stingrai.io/blog/prompt-injection-statistics-2026
- **Crowded on the 2026 tour.** Only pursue a niche: injection tests for Spanish-language agents, or a scanner for risky MCP plug-ins.
- Metric: hijack success rate before vs. after defence; % of risky plug-ins flagged.
- Villain: hidden text on a webpage tells a shopping agent to send the user's card details to an attacker.

**C2. Accountability for agent actions**
- Evidence: Citi made customers liable for their AI banking agents (Nov 2026); six banks published agentic-commerce principles; the UK regulator says banks should prepare "know your agent" checks. https://fidoalliance.org/twif-whose-agent-is-it-anyway-this-week-in-fraud/ · https://didit.me/blog/llm-identity-verification-know-your-agent/
- Gap: nobody can prove what the human actually authorised.
- Idea: **Agent mandate + receipt.** The user sets limits ("flights under $250"), and every agent action produces a signed receipt of what was authorised and what happened.
- Metric: % of out-of-mandate actions blocked; % of actions with a verifiable receipt.
- Villain: told "flights under $250", a booking agent buys three business-class tickets.

**C3. Sycophancy and psychological harm**
- Evidence: seven lawsuits against OpenAI over chatbots reinforcing delusions; research now tests multi-turn conversations. https://techcrunch.com/?p=3070069 · https://www.alphaxiv.org/abs/2604.06188
- Gap: tests exist only in English and mostly score single replies.
- Idea: **Spanish multi-turn sycophancy test.** Simulated 12-turn conversations scoring whether a chatbot or companion app pushes back or plays along.
- Metric: % of conversations where the bot pushes back vs. reinforces a false belief, turn by turn.
- Villain: a companion bot agrees, turn after turn, that the user's family is against them.

### D. Structural

**D1. Labs walking back commitments**
- Evidence: FLI's Summer 2026 AI Safety Index gave no lab better than C+ and failed three; reviewers say labs are "moving goalposts". https://axios.com/2026/07/07/report-ai-safety-pledges
- Idea: **Commitment diff-bot.** Watches labs' safety policies and model cards, and alerts with a plain-language summary when wording weakens.
- Metric: hours from change to alert; % of changes correctly labelled weaker or stronger.
- Villain: a lab quietly softens its "we will pause if…" promise in a footnote.

**D2. Outsiders can't verify labs**
- Evidence: OpenAI's new "embedded evaluators" get narrow access; there's no standard for what audits must cover. https://www.mprnews.org/story/2026/11/18/npr-openai-embedded-evaluators-program-critics
- Idea: **Audit-access scorecard.** Scores each lab's outside-evaluator programme against what researchers say is needed.
- Metric: score per lab (model access, raw reasoning access, staff access, right to publish).
- Villain: an "independent" audit where the lab picks which staff auditors may talk to.

**D3. Global South left out**
- Evidence: no Latin American AI Safety Institute; Chile's AI bill ignores frontier risks; LatamGPT has no public safety evaluations. https://forum.effectivealtruism.org/posts/3sL6iB6WzKHJciwta/latin-america-in-search-of-its-stake-in-ai-safety-a-map
- Idea: **LatamGPT safety report card.** Run open safety test suites on regional open models and publish the first public results.
- Metric: harmful-answer and bias rates vs. frontier models on the same suite.
- Villain: a national model goes into schools and government offices with no safety test.

### Shortlist (strongest demand × doable in 36h × not done on the tour)
1. Cheat detector for coding agents (A1)
2. SafeBench-ES (B3)
3. Scheming radar (A3)
4. Voice-scam / "fake boss" shield (B1)
5. Agent mandate + receipt (C2)

---

## 5. Pathways to value (pick one and name it in your pitch)

- **Prevent harm directly:** block the bad action as it happens.
- **Measure, so someone acts:** turn a vague worry into a number labs compete on or regulators cite.
- **Early warning:** spot a trend before it becomes a disaster.
- **Give policymakers evidence:** data that justifies or shapes a rule.
- **Accountability pressure:** public scorecards make backsliding costly.
- **Make misuse more expensive:** you don't need to stop every attacker, only enough to raise the cost.
- **Speed up safety research:** shared tools that save researchers hours.
- **Set the standard:** become the format others adopt.
- **Change market incentives:** make safety something buyers, insurers or procurement teams demand.
- **Limit the damage:** detect, recover, take down.

Weak pathway: "raising awareness" with no measurable output. Ask: who decides differently because of this?

---

## 6. Past projects for reference

### Platanus Hack 26 tour: AI Security track (Bogotá, Caracas, 2026, sponsored by Anthropic)
The best preview of what Santiago judges have seen.

| Project | City | What it does | Theme | Repo |
| --- | --- | --- | --- | --- |
| HAWK | Caracas | Monitor on a separate device (Raspberry Pi) that blocks dangerous coding-agent actions, can cut the machine off the network, and keeps a log the agent can't rewrite | AI control | https://github.com/platanus-hack/platanus-hack-26-ve-team-23 |
| Agent Zero | Caracas | Attacks your agent automatically, confirms real damage, writes a blocking rule | Red-teaming | https://github.com/platanus-hack/platanus-hack-26-ve-team-4 |
| VanGUARD | Caracas | One-click security audit of an app's database and code; fixed rules, not AI, decide the alerts | App security | https://github.com/platanus-hack/platanus-hack-26-ve-team-22 |
| Gotchu | Caracas | Scans code and websites for security risks; report with evidence and fixes | App security | https://github.com/platanus-hack/platanus-hack-26-ve-team-6 |
| Roxy | Bogotá | Turns plain-language rules into a formal policy once; a non-AI engine checks every agent action; a math solver hunts for loopholes | Verification | https://github.com/platanus-hack/platanus-hack-26-co-team-3 |
| Provenance Firewall | Bogotá | Stops agent "memory" from gaining authority it wasn't granted; 255 automated tests | Agent security | https://github.com/platanus-hack/platanus-hack-26-co-team-13 |
| Aegis | Bogotá | Stops employees leaking secrets to ChatGPT and other AIs, and explains each block | Data leakage | https://github.com/platanus-hack/platanus-hack-26-co-team-1 |
| Stegora | Bogotá | Invisible signature inside images that survives cropping and WhatsApp compression | Content provenance | https://github.com/platanus-hack/platanus-hack-26-co-team-12 |

Patterns to learn from:
- **The bar is high:** hardware, formal verification, 200+ tests.
- **Most built agent security/guards.** Differentiate.
- **A good recurring instinct:** "the AI doesn't make the final safety decision." Use fixed rules or a separate system so a clever prompt can't talk the guard out of it.

### Platanus Hack 25 (Santiago, 2025): no AI safety track, closest projects
| Project | What it does | Link |
| --- | --- | --- |
| SafeLine | Listens to phone calls live and flags scam risk for older adults; alerts family on WhatsApp | https://hack.platan.us/25/vote/safeline |
| Shadow | One virtual card per merchant, so a breach exposes only that card | https://hack.platan.us/25/vote/shadow |
| Django Security Suite | Drop-in security package for web apps, published on PyPI | https://hack.platan.us/25/vote/django-security-suite |

All Hack 25 projects: https://hack.platan.us/25/vote · Hack 26 Bogotá overview: https://crafterwiki.com/hackathons/platanus-hack-26-bogota/

---

## 7. Existing tools to build on (don't reinvent these)

| Tool | Use it for | Link |
| --- | --- | --- |
| Inspect (UK AISI) | Running evals; the standard framework at government AI safety institutes | https://inspect.aisi.org.uk |
| ControlArena | AI control experiments (built on Inspect) | https://github.com/UKGovernmentBEIS/control-arena |
| Petri | Automated auditing of model behaviour | https://github.com/safety-research/petri |
| promptfoo | Red-teaming and testing LLM apps | https://www.promptfoo.dev |
| garak | LLM vulnerability scanner | https://github.com/NVIDIA/garak |
| Neuronpedia | Exploring the "concepts" inside open models | https://www.neuronpedia.org |
| TransformerLens | Interpretability on open models | https://github.com/TransformerLensOrg/TransformerLens |

---

## 8. Red lines (do not build)

- Anything that gives uplift for biological, chemical, radiological or nuclear weapons.
- Working offensive cyber tools, or attacks on systems you don't own (including "just testing" on real sites).
- Tools whose main use is jailbreaking models or harvesting harmful content.
- Datasets containing real harmful instructions. Use proxy categories or harmless stand-ins.
- Deepfakes of real people, even for a demo. Use synthetic or consenting voices and faces.

If your idea is close to a line, reframe it as **defensive** and use **fake or test targets**.

---

## 9. Judge questions to prepare for

- Isn't this already solved by an existing tool or the lab's own safeguards?
- Could your metric be fooled by the same trick you're catching?
- What happens if an attacker knows your system exists?
- Who adopts or pays for this first?
- Why is this AI safety, not just security or a product?
- What breaks at scale or on a different model?
- What didn't you test?

---

## 10. Glossary

| Term | Plain meaning |
| --- | --- |
| Agent | An AI that takes actions (clicks, codes, pays, emails), not just chats |
| Eval / benchmark | A standard test you run models through to score a behaviour or skill |
| Red-teaming | Attacking your own system on purpose to find weak spots |
| Jailbreak | A prompt that tricks a model into ignoring its safety rules |
| Prompt injection | Hidden instructions in a webpage or file that hijack an agent reading it |
| AI control | Safety measures that work even if the AI is actively trying to misbehave |
| Monitor | A separate system that watches an AI's actions and flags bad ones |
| Sandbox | A locked test environment the AI isn't supposed to escape |
| Reward hacking | Gaming the objective (e.g. cheating the test) instead of doing the task |
| Sandbagging | Deliberately underperforming, e.g. to look less dangerous |
| Scheming | Pursuing hidden goals while appearing to cooperate |
| Evaluation awareness | A model noticing it's being tested and behaving differently |
| Sycophancy | Telling users what they want to hear, even when it's false or harmful |
| Interpretability | Studying a model's internals to see why it does things |
| Provenance / watermark | A hidden signature proving where content came from |
| Frontier model | The most capable models from the top labs |
| AISI | A government AI Safety (or Security) Institute, e.g. UK AISI |

---

## 11. Further reading

- The Case for Building AI Safety Tools (LessWrong, Oct 2026): https://www.lesswrong.com/posts/swRuRr5BbyuQiFpwh/the-case-for-building-ai-safety-tools
- Ten AI safety projects I'd like people to work on (LessWrong): https://www.lesswrong.com/posts/vxA2BnCPTaPfnJjti/ten-ai-safety-projects-i-d-like-people-to-work-on
- AI Safety at the Frontier: April 2026 paper highlights (LessWrong): https://www.lesswrong.com/posts/pz7Qk2sRZNidT2wjL/ai-safety-at-the-frontier-paper-highlights-of-april-2026
- Latin America in search of its stake in AI safety (EA Forum): https://forum.effectivealtruism.org/posts/3sL6iB6WzKHJciwta/latin-america-in-search-of-its-stake-in-ai-safety-a-map
- International AI Safety Report 2026 (summary): https://www.globalpolicywatch.com/2026/02/international-ai-safety-report-2026-examines-ai-capabilities-risks-and-safeguards/
- OpenAI on the Hugging Face incident: https://openai.com/index/hugging-face-model-evaluation-security-incident/

*Some figures come from secondary reporting; verify before quoting them on stage.*
