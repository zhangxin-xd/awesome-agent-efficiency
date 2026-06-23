# ⚡ Awesome Agentic Efficiency

> A curated list of papers, benchmarks, tools, and resources on the efficiency of agentic AI systems — organized by **efficiency dimension**, with quantified cost-performance tradeoffs and practical engineering guidance.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![Last Updated](https://img.shields.io/badge/updated-May%202026-blue)
![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)
![Scope](https://img.shields.io/badge/scope-agentic%20efficiency-orange)

---

## Why This List?

Most existing lists on agent efficiency are **paper dumps** — long, flat, and hard to navigate. This list is different:

- 📌 **Organized by efficiency bottleneck** — so you know *where* your cost comes from
- 📊 **Quantified tradeoffs** — token savings, accuracy delta, and latency change for each technique
- 🔧 **Engineer-first** — includes practical stack recommendations for common deployment scenarios
- 💬 **Commentary on every entry** — what it contributes and what it misses
- 🔭 **Open problems section** — explicit gaps for researchers to target

**Scope**: Efficiency of agentic AI systems (single and multi-agent). We cover planning efficiency, token/context compression, tool use optimization, multi-agent coordination, memory/retrieval, and inference serving. We do *not* cover general LLM training efficiency or hardware-level optimization.

---

## Contents

- [Where Is Your Bottleneck?](#where-is-your-bottleneck)
- [0. Surveys & Position Papers](#0-surveys--position-papers)
- [1. Efficiency by Dimension](#1-efficiency-by-dimension)
  - [1.1 Planning & Reasoning Efficiency](#11-planning--reasoning-efficiency)
  - [1.2 Token & Context Efficiency](#12-token--context-efficiency)
  - [1.3 Tool Use Efficiency](#13-tool-use-efficiency)
  - [1.4 Multi-Agent Coordination](#14-multi-agent-coordination)
  - [1.5 Memory & Retrieval Efficiency](#15-memory--retrieval-efficiency)
  - [1.6 Inference & Serving Efficiency](#16-inference--serving-efficiency)
- [2. Practical Stack Recommendations](#2-practical-stack-recommendations)
- [3. Benchmarks & Evaluation](#3-benchmarks--evaluation)
- [4. Tools & Frameworks](#4-tools--frameworks)
- [5. Open Problems](#5-open-problems)
- [Contributing](#contributing)

---

## Where Is Your Bottleneck?

Use this decision tree before diving into the paper sections.

```
Your agent is too slow or too expensive?
│
├── Per-step token count too high?
│   └── → §1.2 Token & Context Efficiency
│
├── Too many steps / poor planning?
│   └── → §1.1 Planning & Reasoning Efficiency
│
├── Too many or redundant tool calls?
│   └── → §1.3 Tool Use Efficiency
│
├── Multi-agent communication overhead?
│   └── → §1.4 Multi-Agent Coordination
│
├── Memory/RAG retrieval slow or noisy?
│   └── → §1.5 Memory & Retrieval Efficiency
│
└── GPU memory / throughput bottleneck?
    └── → §1.6 Inference & Serving Efficiency
```

> **Reading guide for tradeoff columns**
> - **Token Δ**: reduction (−) or increase (+) in tokens per step vs. baseline
> - **Accuracy Δ**: task success rate change vs. baseline
> - **Latency Δ**: wall-clock time change per step; ↓ = faster, ↑ = slower

---

## 0. Surveys & Position Papers

| Paper | Venue | Commentary |
|-------|-------|------------|
| [Efficient Large Language Models: A Survey](https://arxiv.org/abs/2312.03863) | TMLR 2024 | Broad survey of LLM efficiency; covers data, architecture, and inference but treats agents superficially |
| [A Survey on LLM-based Autonomous Agents](https://arxiv.org/abs/2308.11432) | arXiv 2023 | Canonical agent architecture overview; efficiency not the focus but useful as baseline |
| [The Landscape of Emerging AI Agent Architectures](https://arxiv.org/abs/2404.11584) | arXiv 2024 | Practitioner-oriented taxonomy; highlights where latency and cost accumulate in real deployments |
| [AgentBench: Evaluating LLMs as Agents](https://arxiv.org/abs/2308.03688) | ICLR 2024 | Establishes task completion vs. cost tradeoff baseline across 8 environments |
| [Toward Efficient Agents: Memory, Tool Learning, and Planning](https://arxiv.org/abs/2601.14192) | arXiv 2026 | Surveys agent efficiency across memory, tool learning, and planning using effectiveness-cost Pareto frontiers; survey without a new optimization method |

---

## 1. Efficiency by Dimension

### 1.1 Planning & Reasoning Efficiency

Reducing the number of steps, tokens, and retries needed for an agent to complete a task.

| Paper | Venue | Token Δ | Accuracy Δ | Latency Δ | Commentary |
|-------|-------|---------|------------|-----------|------------|
| [ReAct](https://arxiv.org/abs/2210.03629) | ICLR 2023 | baseline | baseline | baseline | Foundational interleaved think-act loop; verbose reasoning traces are its main inefficiency |
| [Tree of Thoughts](https://arxiv.org/abs/2305.10601) | NeurIPS 2023 | +10× | +15% | ↑10× | Explores multiple paths; major accuracy gain but prohibitive cost for most deployments |
| [LATS](https://arxiv.org/abs/2310.04406) | ICML 2024 | +20× | +20% | ↑20× | State-of-the-art on many benchmarks; only viable with aggressive beam pruning |
| [Chain of Draft](https://arxiv.org/abs/2502.18600) | arXiv 2025 | −75% | <−3% | ↓3× | Compresses verbose CoT into compact drafts; best efficiency gain with minimal accuracy loss |
| [Reflexion](https://arxiv.org/abs/2303.11366) | NeurIPS 2023 | +1 step | +10% | ↑1 step | Self-correction via verbal reflection; reduces failure retries over episodes but adds a reflection step |
| [AgentQ](https://arxiv.org/abs/2408.07199) | arXiv 2024 | varies | +25% | ↑offline | MCTS + self-critique for web agents; requires offline training, inference cost amortized over runs |
| [Chain-of-Abstraction](https://arxiv.org/abs/2401.17464) | arXiv 2024 | −30% | ≈0% | ↓1.5× | Decouples reasoning from tool calls; reduces unnecessary API calls with little accuracy cost |
| [Cognitive Duality](https://arxiv.org/abs/2508.05081) | arXiv 2025 | −75% tokens | 43.96% WebArena success | — | Switches between fast reactive and slow deliberative web-agent modes; web-navigation specific and not yet venue-accepted |
| [Divide, Optimize, Merge](https://arxiv.org/abs/2505.03973) | arXiv 2025 | −56.3% prompt tokens | +1.6–8.6% | offline optimization | Scales agent optimization by divide-and-merge; requires offline optimization data |
| [DEPO](https://arxiv.org/abs/2511.15392) | arXiv 2025 | -60.9% tokens; -26.9% steps | up to +29.3% | - | Optimizes step-level and trajectory-level agent efficiency via preference optimization; training-based and mainly validated on WebShop/BabyAI |
| [More with Less](https://arxiv.org/abs/2510.16786) | arXiv 2025 | cost -24-68%; extra -12-24% with dynamic turns | comparable / better solve rates | fewer turns | Controls coding-agent turn budgets with simple deployment strategies; empirical study rather than a new framework |
| [Task-Decoupled Planning](https://arxiv.org/abs/2601.07577) | arXiv 2026 | up to −82.4% output tokens | HotpotQA 85.88% / 82.14% acc | — | Decouples long-horizon planning into scoped sub-tasks; sub-task granularity is still hand-tuned. |
| [Think Fast and Slow](https://arxiv.org/abs/2602.12662) | arXiv 2026 | -62% tokens | 82.3% success rate | — | Routes each agent step to an appropriate cognitive depth; requires two-stage cognition-aware training |
| [EGSS](https://arxiv.org/abs/2602.05242) | arXiv 2026 | >-28% inference tokens | +5-10% | — | Allocates test-time compute using entropy-guided search; mainly validated on SWE-Bench-Verified |
| [Agentic Test-Time Scaling for WebAgents](https://arxiv.org/abs/2602.12276) | arXiv 2026 | up to 2.3x fewer tokens | up to +9.1% vs. ReAct | dynamic compute allocation | Scales compute only at uncertain web-agent steps; evidence is web-navigation specific |
| [ELHPlan](https://arxiv.org/abs/2509.24230) | arXiv 2026 | uses 30-40% of SOTA tokens | comparable success | lower planning time | Plans with intention-bound action chains for multi-agent collaboration; evaluated on embodied multi-agent benchmarks |
| [SAGE](https://arxiv.org/abs/2512.17102) | arXiv 2026 | -59% tokens | +8.9% scenario goal completion | -26% interaction steps | Learns reusable skills through sequential rollouts; depends on RL training and skill-library infrastructure |
| [EET](https://arxiv.org/abs/2601.05777) | ACL Findings 2026 | input -30%, output -25% | resolution loss <=0.2% | total cost -19-55%; API calls -21% | Terminates unproductive SE-agent iterations using prior experience; focused on SWE-bench-style issue resolution |

---

### 1.2 Token & Context Efficiency

Compressing prompts, managing long contexts, and reducing per-step token consumption.

| Paper | Venue | Token Δ | Accuracy Δ | Latency Δ | Commentary |
|-------|-------|---------|------------|-----------|------------|
| [LLMLingua](https://arxiv.org/abs/2310.05736) | EMNLP 2023 | −80% | <−5% | ↓4× | Token-level prompt compression via small proxy model; drop-in for most agent pipelines |
| [LongLLMLingua](https://arxiv.org/abs/2310.06839) | ACL 2024 | −70% | +2% vs LLMLingua | ↓3× | Question-aware compression; better preserves relevant info for long-context retrieval |
| [MemGPT](https://arxiv.org/abs/2310.08560) | SOSP 2024 | −60% (ctx) | ≈0% | ↓2× | OS-style memory paging; effective for long-running agents; adds architectural complexity |
| [Lost in the Middle](https://arxiv.org/abs/2307.03172) | TACL 2024 | — | — | — | Reveals positional bias in long contexts; motivates reranking/compression before agent input |
| [RECOMP](https://arxiv.org/abs/2310.04408) | ICLR 2024 | −65% | +3% vs naive RAG | ↓2× | Abstractive + extractive compressors for RAG; directly applicable to agent memory retrieval |
| [Selective Context](https://arxiv.org/abs/2310.06201) | arXiv 2023 | −50% | <−2% | ↓2× | Self-information-based pruning of redundant context; lightweight, no proxy model needed |
| [SCOUT](https://arxiv.org/abs/2605.04496) | ICML 2026 | up to −8× | ≈SOTA proprietary | — | Actively forages query-sufficient evidence; strongest for sparse-evidence LTU |
| [DataLab](https://arxiv.org/abs/2412.02205) | ICDE 2025 | −61.65% token cost | up to +58.58% | — | Manages BI notebook context via cell dependencies; domain-specific platform |
| [ACON](https://arxiv.org/abs/2510.00615) | arXiv 2025 | peak tokens −26–54% | >95% accuracy preserved after distillation | — | Optimizes long-horizon agent context compression across observations and histories; preprint without venue signal |
| [FocusAgent](https://arxiv.org/abs/2510.03204) | arXiv 2025 | observation size −50%+ | ≈strong baselines on WebArena / WorkArena | — | Trims noisy web-agent context and reduces prompt-injection exposure; mainly validated on web agents |
| [Efficient On-Device Agents](https://arxiv.org/abs/2511.03728) | arXiv 2025 | >6× smaller initial context; 10–25× slower context growth | matches or exceeds baseline | — | Compresses memory and tool schemas for on-device agents; device-side setting limits generality |
| [Prune4Web](https://arxiv.org/abs/2511.21398) | arXiv 2025 | 25-50x fewer candidate DOM elements | 46.8% -> 88.28% grounding accuracy | - | Replaces raw DOM reading with programmatic pruning for web agents; web-DOM specific and depends on generated pruning programs |
| [UIFormer](https://arxiv.org/abs/2512.13438) | arXiv 2025 | −48.7–55.8% UI tokens | Maintained / improved GUI-agent success | 5.7 ms avg overhead; prod −26.1% latency | Synthesizes compact UI transformations for GUI agents; strongest for UI-navigation workloads. |
| [An Information Theoretic Perspective on Agentic System Design](https://arxiv.org/abs/2512.21720) | arXiv 2025 | 4.6× more concise summaries; 74% API-cost cut | 99% frontier-LM accuracy recovered | — | Frames agent efficiency as information bottleneck design; more principle/analysis than drop-in system. |
| [FoldAct](https://arxiv.org/abs/2512.22733) | arXiv 2025 | 0.25–0.65 context ratio | HotpotQA 38.5 F1 / 29.5 EM; PopQA 32.9 F1 / 29.0 EM | 5.19× training speedup | Folds long trajectories during RL training; still training-time focused and consistency loss is costly. |
| [CCPO](https://arxiv.org/abs/2601.11631) | arXiv 2026 | up to −55.01% visual tokens | AITW 75.12 overall; AC 73.25 SR | up to 3.8× training speedup | Compresses GUI-agent visual contexts with curriculum policy optimization; domain-specific to coordinate/GUI agents. |
| [AgentOCR](https://arxiv.org/abs/2601.04786) | arXiv 2026 | >-50% tokens | >95% text-agent performance preserved | 20x rendering speedup | Compresses agent history into visual representations; adds rendering and visual-cache machinery |
| [AgentDiet](https://arxiv.org/abs/2509.23586) | arXiv 2026 | -39.9% to -59.7% input tokens | maintained | -21.1% to -35.9% total cost | Removes useless, redundant, and expired trajectory content at inference time; validated mainly on coding agents |
| [SkillReducer](https://arxiv.org/abs/2603.29919) | arXiv 2026 | −48% descriptions / −39% bodies | +2.8% functional quality | — | Compresses LLM-agent skills for token efficiency; needs validation beyond skill repositories |
| [LightThinker++](https://arxiv.org/abs/2604.03679) | arXiv 2026 | peak −70% | +14.8% | ↓26% | Combines reasoning compression with memory management; strongest evidence is on long-horizon tasks |
| [Active Context Curation](https://arxiv.org/abs/2604.11462) | arXiv 2026 | −8.8% WebArena / up to 8× on DeepSearch | WebArena 36.4→41.2 / DeepSearch 53.9→57.1 | — | RL policy actively curates agent context; requires environment-specific training |
| [GenericAgent](https://arxiv.org/abs/2604.17091) | arXiv 2026 | fewer tokens and interactions | outperforms leading agent systems | — | Maximizes context information density for long-horizon agents; abstract lacks exact token-reduction percentage |

---

### 1.3 Tool Use Efficiency

Reducing unnecessary tool calls, improving tool selection, and enabling parallel execution.

| Paper | Venue | Call Δ | Accuracy Δ | Latency Δ | Commentary |
|-------|-------|--------|------------|-----------|------------|
| [Gorilla](https://arxiv.org/abs/2305.15334) | NeurIPS 2024 | −40% hallucinated | +18% | ↓1.5× | Retrieval-augmented API selection; substantially reduces hallucinated tool calls |
| [ToolLLM](https://arxiv.org/abs/2307.16789) | ICLR 2024 | varies | +20% | ↓vs random | DFSDT search finds tool paths faster than ReAct; training required |
| [AnyTool](https://arxiv.org/abs/2402.04253) | arXiv 2024 | −50% search | +12% | ↓2× | Hierarchical dispatcher prunes irrelevant APIs; strong at scale with 16K+ tools |
| [Parallel Function Calling](https://platform.openai.com/docs/guides/function-calling) | OpenAI 2024 | — | ≈0% | ↓N× (N=parallel calls) | Native parallelism for independent tool calls; largest latency win when dependency graph allows |
| [ToolkenGPT](https://arxiv.org/abs/2305.11554) | NeurIPS 2023 | — | +8% | ↓1.3× | Encodes tools as token embeddings; zero-overhead selection but less flexible for dynamic tools |
| [API-Bank](https://arxiv.org/abs/2304.08244) | EMNLP 2023 | — | — | — | Benchmark rather than method; first systematic tool-use efficiency evaluation |
| [TSCG](https://arxiv.org/abs/2605.04107) | arXiv 2026 | −52–57% schema tokens | +84.4pp on Phi-4 14B | — | Compiles JSON tool schemas into compact text; gains vary by model/schema sensitivity |
| [RepoAudit](https://arxiv.org/abs/2501.18160) | ICML 2025 | on-demand repo scan | 78.43% precision | 0.44h / $2.54 per project | Uses memory-guided code exploration and validation; focused on code-auditing agents |
| [MCP-Zero](https://arxiv.org/abs/2506.01056) | arXiv 2025 | −98% tool-context tokens | high accuracy maintained | — | Actively discovers tools instead of injecting all schemas; evaluated mainly on MCP/APIBank-style tool pools |
| [Smurfs](https://arxiv.org/abs/2405.05955) | NAACL 2025 Long | −60.9% tokens vs DFSDT | SOTA on StableToolBench / HotpotQA | training-free | Makes DFSDT tool planning context-efficient with MAS modules; still inherits tree-search setup complexity |
| [BridgeScope](https://arxiv.org/abs/2508.04031) | arXiv 2025 | up to −80% token usage | — | bypasses inter-tool transfer | Modularizes database tools and proxy data transfer for DB agents; strongest evidence is database-specific |
| [LLM-Explorer](https://arxiv.org/abs/2505.10593) | MobiCom 2025 | LLM-less action generation | highest app coverage | 148× lower cost | Uses LLMs mainly for compact exploration knowledge; focused on mobile app exploration |
| [RepoMaster](https://arxiv.org/abs/2505.21577) | arXiv 2025 | repo exploration pruning | +110% valid submissions / 40.7→62.9% pass rate | −95% tokens | Explores GitHub repositories via dependency and call graphs for code agents; software-engineering specific |
| [ToolGen](https://arxiv.org/abs/2410.03439) | ICLR 2025 | no separate tool retrieval | superior on retrieval + agent tasks | — | Generates tool calls as tool tokens; requires tool-token training |
| [Z-Space](https://arxiv.org/abs/2511.19483) | arXiv 2025 | -96.26% tool-inference tokens | 92% tool invocation accuracy | - | Filters enterprise MCP tools through multi-agent orchestration; production evidence but limited open reproducibility |
| [ToolRM](https://arxiv.org/abs/2510.26167) | arXiv 2025 | RM-guided tool selection | up to +17.94% weighted tool-call accuracy; +4.64/+5.62 pp RL gains | >66% fewer output tokens on ACEBench | Fine-grained reward models for tool reasoning; needs curated tool-use preference data. |
| [HyFunc](https://arxiv.org/abs/2602.13665) | arXiv 2026 | hybrid-model function selection | 80.1% | 0.828 s inference | Accelerates function calls using model cascading and dynamic templates; specialized inference implementation required |
| [OpaqueToolsBench](https://arxiv.org/abs/2602.15197) | arXiv 2026 | interaction-driven tool documentation | outperforms existing methods | 3.5-7.5x fewer total tokens | Learns opaque tool behavior from execution feedback; strongest when tool documentation is incomplete |
| [Agents Learn Their Runtime](https://arxiv.org/abs/2603.01209) | arXiv 2026 | interpreter-state alignment | quality unchanged | avoids up to 3.5x redundant tokens | Shows runtime persistence should match tool-agent training traces; evidence comes from controlled synthetic tasks |
| [AutoTool](https://arxiv.org/abs/2603.13348) | arXiv 2026 | automatic tool reasoning scaling | +9.8% | ~-81% computational overhead | Uses entropy-constrained RL to adapt tool-use reasoning length; requires RL training |
| [Semantic Tool Discovery](https://arxiv.org/abs/2603.20313) | arXiv 2026 | -99.6% tool tokens | 97.1% hit rate at K=3 | sub-100ms retrieval | Retrieves only relevant MCP tools instead of exposing full catalogs; benchmark is 121 tools across 5 MCP servers |
| [WorkflowGen](https://arxiv.org/abs/2604.19756) | arXiv 2026 | trajectory-based workflow reuse | +20% success on medium-similarity queries | >-40% tokens | Rewrites reusable workflow trajectories instead of planning from scratch; evidence is qualitative/comparative |
| [Computer Environments](https://arxiv.org/abs/2601.16206) | arXiv 2026 | up to −8× tokens | up to +15.5% | — | Uses executable computer environments to elicit agentic behavior; depends on sandbox/tool availability |
| [Dynamic analysis enhances issue resolution](https://arxiv.org/abs/2603.22048) | arXiv 2026 | −25% input tokens | 79.4% SWE-bench Verified | cost −10% | Adds dynamic analysis to SWE agents; focused on software issue resolution |
| [WebMAC](https://arxiv.org/abs/2604.13559) | arXiv 2026 | multi-agent web testing | +30–60% execution success | −47.6% tokens / +29% efficiency | Coordinates agents for web scenario testing; domain-specific to web systems |
| [Agentic Compilation](https://arxiv.org/abs/2604.09718) | arXiv 2026 | one-shot workflow compilation | 80-94% zero-shot compilation success | <$0.10 per workflow; $0.002-$0.092 per compilation | Compiles repeated web-agent workflows into deterministic execution; best for repetitive browser automation |

---

### 1.4 Multi-Agent Coordination

Reducing communication overhead, redundant work, and orchestration cost in multi-agent systems.

| Paper | Venue | Agent Δ | Accuracy Δ | Cost Δ | Commentary |
|-------|-------|---------|------------|--------|------------|
| [AutoGen](https://arxiv.org/abs/2308.08155) | ICLR 2024 | baseline | baseline | baseline | De facto standard framework; conversation overhead grows linearly with agent count |
| [MetaGPT](https://arxiv.org/abs/2308.00352) | ICLR 2024 | fixed roles | +15% | −50% msg tokens | Role-based SOP halves communication tokens vs. free-form agents |
| [DyLAN](https://arxiv.org/abs/2310.02170) | ICML 2024 | dynamic prune | +8% | −35% | Dynamically prunes agent connections by relevance; best balance of cost and accuracy |
| [AgentPrune](https://arxiv.org/abs/2402.05840) | arXiv 2024 | −60% agents | <−3% | −60% | Single-agent planner eliminates redundant sub-agents; strong for structured tasks |
| [EvoAgent](https://arxiv.org/abs/2406.14228) | arXiv 2024 | adaptive | +10% | varies | Evolves team size to match task complexity; avoids over-provisioning but needs offline evolution |
| [Scaling Test-Time Compute](https://arxiv.org/abs/2408.03314) | arXiv 2024 | — | +20% | ≈same | Per-task adaptive compute budget more efficient than fixed-depth search |
| [AgentPrune](https://arxiv.org/abs/2410.02506) | ICLR 2025 | one-shot graph pruning | ≈SOTA / +3.5–10.8% robust | −28.1–72.8% tokens | Prunes redundant multi-agent messages; requires topology optimization before deployment |
| [G-Designer](https://openreview.net/forum?id=LpE54NUnmO) | ICML 2025 | task-adaptive topology | MMLU 84.50%, HumanEval 89.90% | −95.33% tokens | Designs per-task MAS communication graphs with GNNs; requires topology training/setup |
| [Optima](https://aclanthology.org/2025.findings-acl.601/) | ACL Findings 2025 | trained MAS communication | up to 2.8× | uses <10% tokens | Trains agents for concise collaboration; requires task-specific optimization |
| [GroupDebate](https://arxiv.org/abs/2409.14051) | AAMAS 2026 | grouped debate | +25% | −51.7% tokens | Groups debate agents and exchanges summaries; still costlier than single-agent CoT |
| [S$^2$-MAD](https://aclanthology.org/2025.naacl-long.475/) | NAACL 2025 Long | sparse debate participation | drop <2.0% | up to −94.5% tokens | Sparsifies multi-agent debate to skip low-value exchanges; strongest for debate-style reasoning tasks |
| [Beyond Frameworks](https://aclanthology.org/2025.acl-long.1037/) | ACL 2025 Long | centralized governance + instructor-led participation/context | maintained / better | up to −93.0% tokens | Identifies low-level MAS collaboration strategies that improve token-accuracy tradeoff; design guidance rather than a standalone framework |
| [CodeAgents](https://arxiv.org/abs/2507.03254) | arXiv 2025 | codified MAS reasoning | +3–36pp | input −55–87%, output −41–70% tokens | Converts multi-agent reasoning into structured pseudocode; prompting framework depends on task-specific codification |
| [Adaptive Graph Pruning](https://arxiv.org/abs/2506.02951) | ECAI 2025 | hard+soft graph pruning | +2.58–9.84% | −90%+ tokens | Dynamically prunes agent count and communication topology; requires pruning-network training |
| [RCR-Router](https://arxiv.org/abs/2508.04903) | arXiv 2025 | role-aware context routing | maintained / improved answer quality | up to −30% tokens | Routes task-relevant memory subsets per agent role and stage; arXiv-only with limited reproducibility signal |
| [Maestro](https://arxiv.org/abs/2509.04642) | Technical Report 2025 | joint graph+config optimization | +12% vs MIPROv2 / +4.9% vs GEPA | fewer rollouts than GEPA | Optimizes agent graph structure and node configuration under budgets; technical report with weaker publication signal |
| [AgentInit](https://arxiv.org/abs/2509.19236) | EMNLP 2025 Findings | diversity+expertise initialization | up to +1.2 / +1.6 over baselines | significantly lower token use | Initializes MAS teams for efficient collaboration; abstract lacks exact token-reduction number |
| [AgentDropout](https://arxiv.org/abs/2503.18891) | arXiv 2025 | dynamic agent/edge dropout | +1.14 avg task score | −21.6% prompt / −18.4% completion tokens | Drops redundant agents across rounds; overlaps with pruning-based MAS methods |
| [OpenCity](https://arxiv.org/abs/2410.21286) | arXiv 2024 | 10k-agent scheduling + prompt distillation | — | 600× speed / −70% requests / −50% tokens | Scales massive LLM-agent simulation; strongest evidence is urban-simulation specific |
| [Agent-GSPO](https://arxiv.org/abs/2510.22477) | arXiv 2025 | communication-aware GSPO | SOTA on seven reasoning benchmarks | fraction of baseline tokens | Trains agents to communicate concisely with token-aware rewards; abstract lacks exact token-reduction percentage |
| [iMAD](https://arxiv.org/abs/2511.11306) | arXiv 2025 | selective debate triggering | up to +13.5% | up to -92% tokens | Triggers multi-agent debate only when useful; limited to debate-style agent workflows |
| [When Single-Agent with Skills Replace Multi-Agent Systems and When They Fail](https://arxiv.org/abs/2601.04748) | arXiv 2026 | MAS→SAS; API calls 3–4→1 | avg +0.7% accuracy | −53.7% tokens; −49.5% latency | Shows when skill-equipped single agents can replace MAS; preliminary and not all MAS patterns are compilable. |
| [Training-Free Agentic AI](https://arxiv.org/abs/2603.13256) | arXiv 2026 | belief-guided delegation; -17% agent calls | maintained / robust under degradation | -28% tokens; -19% time-to-success | Routes recursive delegation using probabilistic control without training; evaluated mainly on split-knowledge tasks |
| [HyperAgent](https://arxiv.org/abs/2510.10611) | arXiv 2025 | adaptive hypergraph topology | 95.07% on GSM8K | -25.33% tokens | Models group-level multi-agent communication with hypergraphs; requires topology-learning setup |
| [RUMAD](https://arxiv.org/abs/2602.23864) | arXiv 2026 | dynamic debate topology | improves over single LLM and MAD baselines | >-80% token cost | Controls multi-agent debate communication with RL; strongest evidence is debate-style reasoning |
| [Stop Wasting Your Tokens](https://arxiv.org/abs/2510.26585) | arXiv 2026 | runtime supervision | success maintained | -29.68% tokens on GAIA | Adds lightweight adaptive supervision for MAS at runtime; intervention quality depends on filter reliability |
| [LDP](https://arxiv.org/abs/2603.08852) | arXiv 2026 | identity-aware delegation protocol | aggregate quality not improved in small pool | ~12x lower latency on easy tasks; -37% tokens | Adds model identity and payload negotiation to agent protocols; early evidence from small local delegate pools |
| [SafeSieve](https://arxiv.org/abs/2508.11733) | arXiv 2026 | progressive communication pruning | 94.01% avg accuracy | -12.4% to -27.8% tokens; -13.3% deployment cost | Prunes multi-agent communication using semantics and feedback; gains are smaller than heavier topology-training methods |
| [Agent Q-Mix](https://arxiv.org/abs/2604.00344) | arXiv 2026 | RL action selection | HLE 20.8 vs 19.2 | token-efficient policy | Selects actions for LLM multi-agent systems with QMIX; exact token savings are not fully reported |
| [Dynamic Attentional Context Scoping](https://arxiv.org/abs/2604.07911) | arXiv 2026 | isolated per-agent focus sessions | steering 90–98.4% | up to 3.53× context efficiency | Scopes context per agent to reduce interference; evaluated mainly on steering/orchestration tasks |
| [TopoDIM](https://arxiv.org/abs/2601.10120) | arXiv 2026 | one-shot topology generation | +1.50% | −46.41% tokens | Generates diverse MAS interaction topologies in one shot; gains are modest outside token savings |
| [Latent-Space Agent Communication](https://arxiv.org/abs/2511.09149) | arXiv 2025 | latent communication | — | up to 24× faster inference | Lets agents communicate in latent space; interpretability and debugging are harder |
| [Cost-Effective Communication](https://arxiv.org/abs/2511.13193) | arXiv 2026 | auction-gated speaking | MMLU 84.32%, HumanEval 91.21% pass@1 | 6.25M tokens on GSM8K | Treats MAS communication as scarce bandwidth; exact savings vs each baseline need table-level verification |
| [Recursive Multi-Agent Systems](https://arxiv.org/abs/2604.25917) | arXiv 2026 | recursive latent MAS | +8.3% avg accuracy | -34.6% to -75.6% tokens; 1.2x-2.4x speedup | Scales collaboration through latent recursive computation; requires specialized recursive training |
| [Agent Capsules](https://arxiv.org/abs/2605.00410) | arXiv 2026 | quality-gated compound execution | +0.020/+0.017 quality; +0.052 vs MIPROv2 | -19% to -68% tokens | Merges multi-agent pipeline stages under quality gates; evaluated on selected business pipelines |





---

### 1.5 Memory & Retrieval Efficiency

Efficiently storing, indexing, and retrieving agent memories and external knowledge.

| Paper | Venue | Retrieval Δ | Accuracy Δ | Index Cost | Commentary |
|-------|-------|-------------|------------|------------|------------|
| [RAPTOR](https://arxiv.org/abs/2401.18059) | ICLR 2024 | multi-granularity | +12% | High | Tree-indexed retrieval; upfront indexing cost pays off for repeated queries |
| [Self-RAG](https://arxiv.org/abs/2310.11511) | ICLR 2024 | on-demand | +15% | Low | Skips retrieval when unnecessary; requires fine-tuned model |
| [Adaptive-RAG](https://arxiv.org/abs/2403.14403) | NAACL 2024 | complexity-routed | +8% | Low | Classifier routes simple queries to single-step; reduces overhead for easy questions |
| [GraphRAG](https://arxiv.org/abs/2404.16130) | arXiv 2024 | graph-structured | +20% global | Very high | Best for global/relational queries; indexing cost prohibitive for small corpora |
| [HyDE](https://arxiv.org/abs/2212.10496) | ACL 2023 | +1 LLM call | +10% | None | Hypothetical doc embeddings improve precision; adds one generation per query |
| [A-MEM](https://arxiv.org/abs/2502.12110) | arXiv 2025 | dynamic linking | +12% long-horizon | Low | Dynamic note-taking + linking outperforms static stores on long-horizon tasks |
| [GeAR](https://aclanthology.org/2025.findings-acl.624/) | ACL Findings 2025 | >10% gain on MuSiQue | SOTA multi-hop QA | offline graph expansion | Uses graph expansion and agentic retrieval; depends on triple extraction quality |
| [StepSearch](https://aclanthology.org/2025.emnlp-main.1106/) | EMNLP 2025 | approx. −3.8–25.8% queries vs Search-R1-it; Rec. 83.11–84.52% | +11.2pp / +4.2pp over 3B / 7B search-RL baselines | 19k search trajectories + retriever index | Step-wise PPO rewards information gain and penalizes redundant search; requires RL training and retrieval setup |
| [R-Search](https://arxiv.org/abs/2506.08352) | arXiv 2025 | single-LLM multi-source DAG search | outperforms SOTA search agents | ReFT training; −70% context tokens / −50% latency | Unifies planning, search, and synthesis in one inference process; requires specialized RL fine-tuning |
| [Mem0](https://arxiv.org/abs/2504.19413) | arXiv 2025 | persistent memory retrieval | +26% LLM-as-judge vs OpenAI | −91% p95 latency / >90% token cost | Extracts salient long-term memories with lower latency/cost; graph memory adds system complexity |
| [TeaRAG](https://arxiv.org/abs/2511.05385) | arXiv 2025 | graph triplet retrieval + IP-DPO | +4% / +2% EM | -61% / -59% output tokens | Compresses retrieval content and reasoning steps for agentic RAG; requires graph retrieval and DPO setup |
| [ParallelMuse](https://arxiv.org/abs/2510.24698) | arXiv 2025 | partial rollout reuse + compressed aggregation | up to +62% | -10-30% exploratory tokens | Reuses and compresses deep information-seeking trajectories; mainly useful for long-horizon search agents |
| [Semantic Caching and Intent-Driven Context Optimization for LLM-Powered Enterprise Analytics](https://arxiv.org/abs/2601.11687) | arXiv 2026 | 67.3% cache utilization | 94.3% semantic accuracy; cached answers 98.7% | −51.7% prompt tokens; 8.2 s avg latency | Combines semantic cache and context filtering in production analytics; evidence is domain-specific. |
| [ACE: To Retrieve or To Think? Teaching LLMs Adaptive Context-Efficient Reasoning](https://arxiv.org/abs/2601.08747) | arXiv 2026 | retrieve-or-think controller | HotpotQA 62.8%; 2WikiQA 47.9%; MultiHop-RAG 57.9% | −42% tokens vs IterDRAG on MultiHop-RAG | Dynamically avoids redundant retrieval in multi-hop QA; still costlier than single-step RAG. |
| [SimpleMem](https://arxiv.org/abs/2601.02553) | arXiv 2026 | semantic compression + intent-aware retrieval | +26.4% F1 on LoCoMo | up to 30x fewer inference tokens | Compresses and synthesizes lifelong agent memory; adds a multi-stage memory pipeline |
| [A-RAG](https://arxiv.org/abs/2602.03442) | arXiv 2026 | adaptive hierarchical retrieval | outperforms existing RAG approaches | comparable or fewer retrieved tokens | Exposes retrieval interfaces directly to the agent; abstract lacks an exact token-reduction percentage |
| [M$^2$](https://arxiv.org/abs/2603.00503) | arXiv 2026 | dual memory for web agents | up to +19.6% success | -58.7% tokens | Combines trajectory summarization with insight retrieval for long-horizon web agents; web-navigation focused |
| [Tiny-Critic RAG](https://arxiv.org/abs/2603.00846) | arXiv 2026 | SLM fallback gate | ≈GPT-4o-mini routing accuracy | order-of-magnitude latency reduction | Uses a LoRA small model for reflective RAG routing; focused on binary fallback decisions |
| [Mem-T](https://arxiv.org/abs/2601.23014) | arXiv 2026 | memory-operation tree credit assignment | up to +14.92% | -24.45% inference tokens | Trains long-horizon memory agents with dense rewards; requires RL and hierarchical memory database |
| [Test-Time Strategies for Agentic RAG](https://arxiv.org/abs/2603.12396) | arXiv 2026 | contextualization + retrieval de-duplication | +5.6% EM | -10.5% turns | Improves Search-R1-style agentic RAG at test time; evaluated on QA datasets |
| [D-MEM](https://arxiv.org/abs/2603.14597) | arXiv 2026 | reward-prediction memory routing | outperforms baselines | >-80% tokens; removes $O(N^2)$ write bottleneck | Routes memory updates through fast/slow paths; adds critic router and memory-evolution pipeline |
| [Memori](https://arxiv.org/abs/2603.19935) | arXiv 2026 | structured persistent memory | 81.95% on LoCoMo | 1,294 tokens/query; -67% vs competitors | Converts dialogue into triples and summaries for agent memory; system-layer memory design rather than model method |
| [OThink-SRR1](https://arxiv.org/abs/2604.19766) | arXiv 2026 | fewer retrieval/refinement steps | improves 4 multi-hop QA benchmarks | RL search setup | Reinforces search-refine-reason loops for efficient agentic retrieval; needs RL pipeline |
| [MemMachine](https://arxiv.org/abs/2604.04853) | arXiv 2026 | ≈80% fewer input tokens | LoCoMo 0.9169 / LongMemEvalS 93% | memory system | Preserves personalized agent memory with much lower context cost; adds dedicated memory infrastructure |
| [StructMem](https://arxiv.org/abs/2604.21748) | ACL 2026 Main | structured hierarchical memory | better LoCoMo temporal/multi-hop performance | lower tokens, API calls, and runtime | Adds event bindings and semantic consolidation for long-term memory; exact reduction numbers need PDF table check |




---

### 1.6 Inference & Serving Efficiency

Reducing per-token latency and increasing throughput for deployed agent workloads.

| Paper / Tool | Venue | Throughput Δ | Latency Δ | Memory Δ | Commentary |
|-------|-------|-------------|-----------|----------|------------|
| [FlashAttention-2](https://arxiv.org/abs/2307.08691) | ICLR 2024 | +2× | ↓2× | ≈same | IO-aware attention; foundational for all serving stacks, apply first |
| [PagedAttention / vLLM](https://arxiv.org/abs/2309.06180) | SOSP 2023 | +24× | ↓3× | −40% waste | KV cache paging eliminates memory waste; now the default in most deployments |
| [Speculative Decoding](https://arxiv.org/abs/2211.17192) | ICML 2023 | — | ↓2–3× | +small model | Draft-then-verify decoding; biggest win on generation-heavy agent steps |
| [SGLang / RadixAttention](https://arxiv.org/abs/2312.07104) | NeurIPS 2024 | +5× | ↓4× | −shared prefix | KV cache reuse across requests; especially effective for shared system prompts |
| [Prompt Cache](https://arxiv.org/abs/2311.04934) | MLSys 2024 | — | ↓2× prefix | — | Reuses KV cache for fixed prompt prefixes; direct win for agents with long system prompts |
| [MInference](https://arxiv.org/abs/2407.02490) | NeurIPS 2024 | — | ↓10× prefill | — | Sparse attention for long-context prefill; critical when agent history exceeds 100K tokens |
| [LongSpec](https://arxiv.org/abs/2502.17421) | ACL 2025 Main | up to +3.26× decoding speed | ↓2.25× on AIME24 | constant-size draft KV cache | Accelerates long-context speculative decoding for agentic long-context workloads; requires specialized draft model and inference implementation |
| [SuffixDecoding](https://arxiv.org/abs/2411.04975) | NeurIPS 2025 Spotlight | — | — | up to 5.3× speedup | Caches repeated suffixes for agentic inference workloads; serving-layer method rather than orchestration method |
| [GUI-KV](https://arxiv.org/abs/2510.00536) | arXiv 2025 | — | +4.1% step accuracy | −38.9% decoding FLOPs | Compresses GUI-agent KV cache with spatio-temporal awareness; strongest for screenshot-heavy GUI agents |
| [REFRAG](https://arxiv.org/abs/2509.01092) | arXiv 2025 | — | no loss in perplexity / accuracy | 30.85× TTFT speedup | Removes unnecessary RAG-context decoding computation for multi-turn and agentic RAG; agentic use is one target scenario among several |
| [XGrammar](https://arxiv.org/abs/2411.15100) | MLSys 2025 | up to +100× CFG execution | near-zero overhead structured generation | token-mask cache | Speeds constrained decoding for function calls; only helps structured-output workloads |
| [KVCOMM](https://arxiv.org/abs/2510.12872) | arXiv 2025 | >70% KV reuse | no quality degradation | up to 7.8x speedup; TTFT ~430 ms -> ~55 ms | Reuses cross-agent KV caches for overlapping contexts; benefits depend on shared context across agents |
| [Scaling Graph-CoT / GLM](https://arxiv.org/abs/2511.01633) | arXiv 2025 | up to 15.1x throughput | up to +38% | -90.3% latency; -95.7% token cost | Co-designs multi-agent Graph-CoT with serving optimizations; strongest evidence is graph-reasoning specific |
| [Agent.xpu](https://arxiv.org/abs/2506.24045) | arXiv 2025 | +1.2–4.9× proactive throughput | — | −91–97% reactive latency; −26.8% energy | Runtime scheduler for heterogeneous on-device agents; hardware/system-level rather than agent-policy-level. |
| [AgentInfer](https://arxiv.org/abs/2512.18337) | arXiv 2025 | 1.8-2.5x end-to-end speedup | preserved | >50% fewer ineffective tokens | Co-designs agent architecture, scheduling, decoding, and memory compression; deployment requires multiple integrated modules |
| [Optimizing FaaS Platforms for MCP-enabled Agentic Workflows](https://arxiv.org/abs/2601.14735) | arXiv 2026 | FaaS agent orchestration | up to 13x faster | -88% input tokens; -66% cost | Optimizes MCP agent workflows using caching, persistence, and function fusion; strongly tied to AWS serverless infrastructure |
| [ICaRus](https://arxiv.org/abs/2603.13281) | arXiv 2026 | shared cross-model KV cache | comparable to task-specific fine-tuning | 11.1x lower P95 latency; 3.8x throughput | Shares identical KV caches across specialized models; requires compatible fine-tuning setup |
| [RelayCaching](https://arxiv.org/abs/2603.13289) | arXiv 2026 | >80% decoding KV reuse | negligible degradation | up to 4.7x TTFT speedup | Reuses previous agents' decoding KV caches during later prefill; assumes reusable shared content |
| [IndexCache](https://arxiv.org/abs/2603.12201) | arXiv 2026 | removes 75% indexer computations | negligible quality degradation | 1.82x prefill; 1.48x decode | Reuses sparse-attention indices across layers for long-context agentic workflows; tied to DSA-style serving stacks |
| [AgentStop](https://arxiv.org/abs/2605.15206) | ACM CAIS 2026 | early termination supervisor | utility drop <5% | energy -15% to -20% | Stops low-success local-agent trajectories to save energy; tuned for consumer-device local agents |
| [Not All Prefills Are Equal](https://arxiv.org/abs/2603.13358) | ICML 2026 | PPD routing for multi-turn serving | competitive TPOT | Turn 2+ TTFT -68%; cached KV reuse | Routes append-prefill locally on decode nodes; serving-layer method with SLO-dependent routing |



---

## 2. Practical Stack Recommendations

Curated technique combinations for common deployment scenarios.

### Stack A — Low-Latency Interactive Agent
*Goal: minimize wall-clock time per user interaction*

| Layer | Choice | Why |
|-------|--------|-----|
| Serving | SGLang + FlashAttention-2 | Prefix KV reuse + IO-efficient attention |
| Tool calls | Parallel Function Calling | Eliminate sequential tool round-trips |
| Planning | Chain of Draft | 75% fewer tokens, faster generation |
| Retrieval | Adaptive-RAG | Skip retrieval when not needed |

Expected outcome: **3–5× latency reduction** vs. naive ReAct + standard serving.

---

### Stack B — Low-Cost Batch Agent
*Goal: minimize dollar cost per task at scale*

| Layer | Choice | Why |
|-------|--------|-----|
| Serving | vLLM (PagedAttention) | Maximize GPU utilization |
| Context | LLMLingua | 80% prompt token reduction |
| Planning | Chain of Draft | Shorter outputs = fewer output tokens |
| Retrieval | Self-RAG | Skip retrieval when unnecessary |
| Coordination | AgentPrune | Eliminate redundant agents |

Expected outcome: **60–80% cost reduction** vs. vanilla multi-agent setup.

---

### Stack C — Long-Horizon Autonomous Agent
*Goal: handle multi-hour tasks without context overflow or memory degradation*

| Layer | Choice | Why |
|-------|--------|-----|
| Memory | MemGPT / Letta | OS-style paging prevents context overflow |
| Retrieval | RAPTOR + HyDE | Multi-granularity + improved recall |
| Serving | Prompt Cache + MInference | Handle accumulated agent history efficiently |
| Coordination | DyLAN | Prune inter-agent connections as task evolves |

Expected outcome: **stable performance** on tasks exceeding 100 steps or 500K tokens.

---

## 3. Benchmarks & Evaluation

| Benchmark | Venue | Measures | Gap |
|-----------|-------|----------|-----|
| [AgentBench](https://arxiv.org/abs/2308.03688) | ICLR 2024 | Task completion across 8 environments | No cost/token breakdown; success-only metric |
| [τ-bench](https://arxiv.org/abs/2406.12045) | arXiv 2024 | Reliability under repeated runs (pass^k) | Narrow retail/airline domains |
| [WebArena](https://arxiv.org/abs/2307.13854) | ICLR 2024 | Web navigation success | No efficiency metric |
| [OSWorld](https://arxiv.org/abs/2404.07972) | NeurIPS 2024 | Desktop GUI task completion | Evaluation slow due to VM overhead |
| [SWE-bench](https://arxiv.org/abs/2310.06770) | ICLR 2024 | Software engineering task resolution | Cost per resolved issue not standardized |
| [GAIA](https://arxiv.org/abs/2311.12983) | ICLR 2024 | General assistant task success | Does not track token usage or step count |
| [SWE-Effi](https://arxiv.org/abs/2509.09853) | arXiv 2025 | Software-agent effectiveness under token/time constraints | Focuses on resource-aware reranking, not new agent method |
| [FDABench](https://arxiv.org/abs/2509.02473) | arXiv 2025 | Data-agent benchmark over 2,007 heterogeneous analytical tasks | Benchmark construction includes latency/token cost but does not optimize agents directly |
| [LoCoBench-Agent](https://arxiv.org/abs/2511.13998) | arXiv 2025 | Long-context software-agent benchmark with 9 comprehension and efficiency metrics over 10K-1M tokens | Benchmark only; does not directly optimize agents |
| [MCP vs RAG vs NLWeb vs HTML](https://arxiv.org/abs/2511.23281) | Technical Report 2025 | Compares web-agent interfaces on F1, token usage, runtime, and completion rate | Simulated e-shop testbed; technical report status |
| [IDRBench](https://arxiv.org/abs/2601.06676) | arXiv 2026 | Interactive deep research quality plus turns/tokens cost | Benchmark only; user simulator and 100-pair base dataset. |
| [SWEnergy](https://arxiv.org/abs/2512.09543) | arXiv 2025 | Energy, duration, token usage, and memory over SLM issue-resolution agents | Empirical study; near-zero solve rates limit success-cost conclusions. |
| [AgentAssay](https://arxiv.org/abs/2603.02601) | arXiv 2026 | Token-efficient regression testing for nondeterministic agent workflows with 7,605 trials | Testing framework rather than an agent optimization method |
| [SkillCraft](https://arxiv.org/abs/2603.00718) | arXiv 2026 | Benchmark for tool-skill formation and reuse; skill saving cuts tokens by up to 80% | Measures reusable tool composition, not a standalone efficiency method |
| [On the Impact of AGENTS.md Files](https://arxiv.org/abs/2601.20404) | arXiv 2026 | Measures runtime and output-token impact across 10 repos / 124 PRs | Observational study; not a reusable method |
| [Single-Agent LLMs Outperform Multi-Agent Systems Under Equal Thinking Token Budgets](https://arxiv.org/abs/2604.02460) | arXiv 2026 | Compares single-agent vs multi-agent reasoning under equal token budgets | Focused on multi-hop reasoning; benchmark-style evidence rather than a framework |
| [How Do AI Agents Spend Your Money?](https://arxiv.org/abs/2604.22750) | arXiv 2026 | Token consumption patterns for coding agents on SWE-bench Verified | Empirical study; does not propose a new optimization method |
| [SWE Context Bench](https://arxiv.org/abs/2602.08316) | arXiv 2026 | Context reuse in coding agents across 1,100 base tasks and 376 related tasks | Benchmark; gains depend on accurate summarized/retrieved prior context |


> **Critical gap**: No widely-adopted benchmark jointly reports task success rate, total token cost, step count, and wall-clock latency on the same tasks. See §5.

---

## 4. Tools & Frameworks

| Tool | What it optimizes | Key feature |
|------|------------------|-------------|
| [vLLM](https://github.com/vllm-project/vllm) | Serving throughput | PagedAttention + continuous batching |
| [SGLang](https://github.com/sgl-project/sglang) | Multi-turn latency | RadixAttention for prefix KV reuse |
| [LLMLingua](https://github.com/microsoft/LLMLingua) | Prompt token count | Up to 20× compression with proxy model |
| [AutoGen](https://github.com/microsoft/autogen) | Multi-agent orchestration | Built-in cost tracking utilities |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Agent step control | Explicit graph over LLM call points |
| [MemGPT / Letta](https://github.com/letta-ai/letta) | Long-horizon context | OS-style memory paging |
| [LiteLLM](https://github.com/BerriAI/litellm) | Cost visibility | Unified cost tracking across 400+ models |
| [AgentOps](https://github.com/AgentOps-AI/agentops) | Observability | Token cost + latency + step trace per run |
| [EffGen](https://github.com/ctrl-gaurav/effGen) | Local small-model agents | Open-source framework with 70-80% context compression, complexity routing, tool calling, and unified memory |
| [SkVM](https://arxiv.org/abs/2604.03088) | Cross-harness skill execution | Up to −40% token consumption, 3.2× speedup, and large latency reductions |


---

## 5. Open Problems

These gaps represent active research opportunities not addressed by existing work.

**5.1 No unified efficiency benchmark**
Every existing benchmark measures task success only. No standard reports (success rate, token cost, step count, latency) jointly on the same tasks, making cross-paper comparison impossible.

**5.2 Planning efficiency vs. accuracy Pareto frontier**
It is unclear where the optimal tradeoff between reasoning depth (Tree of Thoughts, LATS) and cost (ReAct, Chain of Draft) lies as a function of task type and difficulty.

**5.3 Multi-agent communication cost modeling**
There is no principled model for predicting when adding an agent helps vs. hurts efficiency. Empirical results are task- and framework-specific.

**5.4 Compression + accuracy interaction under tool use**
Prompt compression techniques (LLMLingua, Selective Context) are evaluated on QA tasks. Their interaction with tool call accuracy — especially for structured output formats — is understudied.

**5.5 Long-horizon efficiency degradation**
How agent performance and cost evolve over very long task horizons (100+ steps) is rarely reported. Most benchmarks cap at 10–20 steps.

**5.6 Serving efficiency for agentic workloads specifically**
Most serving benchmarks assume independent requests. Agentic workloads have long sequential dependencies, dynamic context growth, and bursty tool call patterns — none of which are captured by standard throughput/latency benchmarks.

---

## Contributing

Contributions welcome! Please follow these guidelines:

1. **Format**: Add to the relevant table with all columns filled
2. **Tradeoff numbers**: Use reported paper results where available; estimate order-of-magnitude if not
3. **Commentary**: State what the paper contributes AND what it misses or assumes
4. **Placement**: Add to the most specific applicable dimension
5. **Quality bar**: Top-venue papers (ICLR/NeurIPS/ACL/SOSP/OSDI/MLSys) preferred; arXiv accepted if widely cited or fills a clear gap

Open a PR or issue to suggest additions or correct tradeoff numbers.

---

## Maintainers

<!-- Add your name/GitHub handle here -->

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
