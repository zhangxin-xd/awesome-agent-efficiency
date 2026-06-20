# Changelog

All additions and rejections are logged here. Most recent entries appear first.

---

## 2026-05-13

### Added
- [Chain of Draft](https://arxiv.org/abs/2502.18600) → §1.1 Planning | Token Δ: −75% | Acc Δ: <−3% | Lat Δ: ↓3× | Compresses verbose CoT into compact drafts; minimal accuracy loss
  - 来源：初始建库
  - 收录理由：效率提升最显著的 planning 论文之一，数字扎实

- [LLMLingua](https://arxiv.org/abs/2310.05736) → §1.2 Token & Context | Token Δ: −80% | Acc Δ: <−5% | Lat Δ: ↓4× | Token-level prompt compression via proxy model; drop-in for most pipelines
  - 来源：初始建库
  - 收录理由：token 压缩方向最被广泛引用的论文，EMNLP 2023

- [MemGPT](https://arxiv.org/abs/2310.08560) → §1.2 Token & Context | Token Δ: −60% (ctx) | Acc Δ: ≈0% | Lat Δ: ↓2× | OS-style memory paging for long-running agents; adds architectural complexity
  - 来源：初始建库
  - 收录理由：长任务 agent 上下文管理的代表性工作，SOSP 2024

- [Gorilla](https://arxiv.org/abs/2305.15334) → §1.3 Tool Use | Call Δ: −40% hallucinated | Acc Δ: +18% | Lat Δ: ↓1.5× | Retrieval-augmented API selection; substantially reduces hallucinated tool calls
  - 来源：初始建库
  - 收录理由：工具调用准确率提升最有影响力的论文

- [Parallel Function Calling](https://platform.openai.com/docs/guides/function-calling) → §1.3 Tool Use | Call Δ: — | Acc Δ: ≈0% | Lat Δ: ↓N× | Native parallelism for independent tool calls; largest win when dependency graph allows
  - 来源：初始建库
  - 收录理由：工程上最直接有效的延迟优化手段，常被忽视

- [DyLAN](https://arxiv.org/abs/2310.02170) → §1.4 Multi-Agent Coordination | Agent Δ: dynamic prune | Acc Δ: +8% | Cost Δ: −35% | Dynamically prunes agent connections by relevance; best cost-accuracy balance
  - 来源：初始建库
  - 收录理由：多 agent 协调效率最佳权衡论文，ICML 2024

- [PagedAttention / vLLM](https://arxiv.org/abs/2309.06180) → §1.6 Serving | Throughput Δ: +24× | Lat Δ: ↓3× | Mem Δ: −40% waste | KV cache paging eliminates memory waste; now the default in most deployments
  - 来源：初始建库
  - 收录理由：serving 层最重要的基础工作，SOSP 2023

- [SGLang / RadixAttention](https://arxiv.org/abs/2312.07104) → §1.6 Serving | Throughput Δ: +5× | Lat Δ: ↓4× | Mem Δ: −shared prefix | KV cache reuse across requests; especially effective for shared system prompts
  - 来源：初始建库
  - 收录理由：对 agent 固定 system prompt 场景有直接优化，NeurIPS 2024

- [CacheTTL / Continuum](https://arxiv.org/abs/2511.02230) → §1.6 Serving | Token Δ: — | Acc Δ: ≈0% | Lat Δ: ↓8× | KV cache TTL for multi-turn agent scheduling; fills §5.6 open problem
  - 来源：arXiv daily
  - 收录理由：唯一专门针对 multi-turn agentic workload 的 serving 优化 [early, high-attention]

---
## 2026-05-19

### Added
- [AgentPrune](https://arxiv.org/abs/2410.02506) → §1.4 Multi-Agent Coordination | Agent Δ: one-shot graph pruning | Acc Δ: ≈SOTA / +3.5–10.8% robust | Cost Δ: −28.1–72.8% tokens | Prunes redundant multi-agent messages; requires topology optimization before deployment
  - 来源：arXiv / OpenReview
  - 收录理由：ICLR 2025，直接优化 multi-agent communication cost，有开源实现和强量化结果

- [G-Designer](https://openreview.net/forum?id=LpE54NUnmO) → §1.4 Multi-Agent Coordination | Agent Δ: task-adaptive topology | Acc Δ: MMLU 84.50%, HumanEval 89.90% | Cost Δ: −95.33% tokens | Designs per-task MAS communication graphs with GNNs; requires topology training/setup
  - 来源：arXiv / OpenReview
  - 收录理由：ICML 2025 spotlight，直接优化 multi-agent communication topology

- [Optima](https://aclanthology.org/2025.findings-acl.601/) → §1.4 Multi-Agent Coordination | Agent Δ: trained MAS communication | Acc Δ: up to 2.8× | Cost Δ: uses <10% tokens | Trains agents for concise collaboration; requires task-specific optimization
  - 来源：ACL Anthology / arXiv
  - 收录理由：ACL Findings 2025，直接优化 multi-agent communication efficiency

- [GroupDebate](https://arxiv.org/abs/2409.14051) → §1.4 Multi-Agent Coordination | Agent Δ: grouped debate | Acc Δ: +25% | Cost Δ: −51.7% tokens | Groups debate agents and exchanges summaries; still costlier than single-agent CoT
  - 来源：arXiv daily
  - 收录理由：AAMAS 2026，直接优化 multi-agent debate 的 token-cost/accuracy tradeoff

- [GeAR](https://aclanthology.org/2025.findings-acl.624/) → §1.5 Memory & Retrieval | Retrieval Δ: >10% on MuSiQue | Acc Δ: SOTA multi-hop QA | Index Cost: offline graph expansion | Uses graph expansion and agentic retrieval; depends on triple extraction quality
  - 来源：ACL Anthology / arXiv
  - 收录理由：ACL Findings 2025，优化 agentic multi-hop RAG 的 retrieval efficiency

- [SCOUT](https://arxiv.org/abs/2605.04496) → §1.2 Token & Context | Token Δ: up to −8× | Acc Δ: ≈SOTA proprietary | Lat Δ: — | Actively forages query-sufficient evidence; strongest for sparse-evidence LTU
  - 来源：arXiv daily
  - 收录理由：ICML 2026，明确优化 long-text agent 的 token-cost tradeoff

- [TSCG](https://arxiv.org/abs/2605.04107) → §1.3 Tool Use | Token Δ: −52–57% schema tokens | Acc Δ: +84.4pp on Phi-4 14B | Lat Δ: — | Compiles JSON tool schemas into compact text; gains vary by model/schema sensitivity
  - 来源：arXiv daily / GitHub
  - 收录理由：填补 tool-schema overhead gap，有开源实现和大规模 tool-call 实验

- [RepoAudit](https://arxiv.org/abs/2501.18160) → §1.3 Tool Use | Call Δ: on-demand repo scan | Acc Δ: 78.43% precision | Cost Δ: $2.54/project | Uses memory-guided code exploration and validation; focused on code-auditing agents
  - 来源：arXiv / ICML
  - 收录理由：ICML 2025，面向 repository-level code auditing 的 autonomous LLM-agent

- [DataLab](https://arxiv.org/abs/2412.02205) → §1.2 Token & Context | Token Δ: −61.65% token cost | Acc Δ: up to +58.58% | Lat Δ: — | Manages BI notebook context via cell dependencies; domain-specific platform
  - 来源：arXiv daily / ICDE 2025
  - 收录理由：面向 BI agent workflow 的上下文管理优化，有量化 token-cost 实验



## 2026-05-25


### Added
- [S$^2$-MAD](https://aclanthology.org/2025.naacl-long.475/) → §1.4 Multi-Agent Coordination | Agent Δ: selective debate participation | Acc Δ: <−2.0% | Cost Δ: up to −94.5% tokens | Filters redundant viewpoints and skips low-value debate turns in multi-agent debate
  - 来源：ACL Anthology / NAACL 2025
  - 收录理由：NAACL 2025 Long，直接优化 multi-agent debate 的 token cost，量化收益强

- [Beyond Frameworks](https://aclanthology.org/2025.acl-long.1037/) → §1.4 Multi-Agent Coordination | Agent Δ: governance / participation ablation | Acc Δ: maintained / better | Cost Δ: up to −93.0% tokens | Identifies centralized governance and instructor-curated context as efficient MAS protocols
  - 来源：ACL Anthology / ACL 2025
  - 收录理由：ACL 2025 Long，系统分析 multi-agent collaboration strategy 对准确率和 token cost 的影响

- [StepSearch](https://aclanthology.org/2025.emnlp-main.1106/) → §1.5 Memory & Retrieval | Retrieval Δ: −3.8–25.8% queries vs Search-R1-it | Acc Δ: +11.2pp / +4.2pp over 3B / 7B baselines | Index Cost: 19k search trajectories + retriever index | Step-wise PPO rewards information gain and penalizes redundant search
  - 来源：ACL Anthology / EMNLP 2025 / GitHub
  - 收录理由：EMNLP 2025，优化 search agent 的 multi-hop retrieval efficiency，有开源实现和明确量化结果

- [LongSpec](https://arxiv.org/abs/2502.17421) → §1.6 Serving | Throughput Δ: up to +3.26× decoding speed | Lat Δ: ↓2.25× on AIME24 / avg. ↓2.34× on QwQ math | Mem Δ: constant-size draft KV cache | Lossless speculative decoding for long-context agents and long reasoning
  - 来源：arXiv / GitHub
  - 收录理由：ACL 2025 Main，直接优化 long-context agent 和 long reasoning 的 decoding latency



## 2026-05-30

### Added
- [Cognitive Duality](https://arxiv.org/abs/2508.05081) → §1.1 Planning | Token Δ: −75% | Acc Δ: 43.96% WebArena success | Lat Δ: — | Switches between fast reactive and slow deliberative web-agent modes; web-navigation specific
  - 来源：arXiv
  - 收录理由：直接优化 web agent 的 reasoning budget 和 token cost，有明确 WebArena 结果

- [MCP-Zero](https://arxiv.org/abs/2506.01056) → §1.3 Tool Use | Token Δ: −98% tool-context tokens | Acc Δ: high accuracy maintained | Lat Δ: — | Actively discovers tools instead of injecting all schemas; evaluated mainly on MCP/APIBank-style tool pools
  - 来源：arXiv
  - 收录理由：直接解决 tool schema/context 爆炸问题，适合补充 tool-use efficiency

- [Smurfs](https://arxiv.org/abs/2405.05955) → §1.3 Tool Use | Token Δ: −60.9% vs DFSDT | Acc Δ: SOTA on StableToolBench / HotpotQA | Lat Δ: training-free | Makes DFSDT tool planning context-efficient with MAS modules; still inherits tree-search setup complexity
  - 来源：arXiv / NAACL 2025
  - 收录理由：NAACL 2025 Long，面向 tool planning 的 context-efficient multi-agent method

- [BridgeScope](https://arxiv.org/abs/2508.04031) → §1.3 Tool Use | Token Δ: up to −80% | Acc Δ: — | Lat Δ: bypasses inter-tool transfer | Modularizes database tools and proxy data transfer for DB agents; database-specific evidence
  - 来源：arXiv
  - 收录理由：优化 LLM agent 与数据库工具交互时的 token 传输瓶颈

- [LLM-Explorer](https://arxiv.org/abs/2505.10593) → §1.3 Tool Use | Call Δ: LLM-less action generation | Acc Δ: highest app coverage | Lat Δ: 148× lower cost | Uses LLMs mainly for compact exploration knowledge; focused on mobile app exploration
  - 来源：arXiv / MobiCom 2025
  - 收录理由：MobiCom 2025，显著降低移动 app exploration agent 的 LLM 调用成本

- [CodeAgents](https://arxiv.org/abs/2507.03254) → §1.4 Multi-Agent Coordination | Agent Δ: codified MAS reasoning | Acc Δ: +3–36pp | Cost Δ: input −55–87%, output −41–70% tokens | Converts multi-agent reasoning into structured pseudocode; depends on task-specific codification
  - 来源：arXiv
  - 收录理由：同时提升多 agent planning accuracy 和 token efficiency，量化结果清晰

- [Adaptive Graph Pruning](https://arxiv.org/abs/2506.02951) → §1.4 Multi-Agent Coordination | Agent Δ: hard+soft graph pruning | Acc Δ: +2.58–9.84% | Cost Δ: −90%+ tokens | Dynamically prunes agent count and communication topology; requires pruning-network training
  - 来源：arXiv / ECAI 2025
  - 收录理由：直接优化 multi-agent communication topology，token 降幅很强

- [R-Search](https://arxiv.org/abs/2506.08352) → §1.5 Memory & Retrieval | Retrieval Δ: single-LLM multi-source DAG search | Acc Δ: outperforms SOTA search agents | Index Cost: ReFT training; −70% context tokens / −50% latency | Unifies planning, search, and synthesis in one inference process; requires specialized RL fine-tuning
  - 来源：arXiv / GitHub
  - 收录理由：减少多 agent search framework 的上下文 token 和执行延迟，适合补充 agentic search efficiency


## 2026-06-02

### Added
- [ACON](https://arxiv.org/abs/2510.00615) → §1.2 Token & Context | Token Δ: peak tokens −26–54% | Acc Δ: >95% preserved after distillation | Lat Δ: — | Optimizes long-horizon agent context compression across observations and histories; preprint without venue signal
  - 来源：arXiv / GitHub
  - 收录理由：直接面向 long-horizon LLM agents 的 context compression，有明确 token/memory 指标和开源实现

- [FocusAgent](https://arxiv.org/abs/2510.03204) → §1.2 Token & Context | Token Δ: observation size −50%+ | Acc Δ: ≈strong baselines on WebArena / WorkArena | Lat Δ: — | Trims noisy web-agent context and reduces prompt-injection exposure; mainly validated on web agents
  - 来源：arXiv
  - 收录理由：直接优化 web agent 的大上下文输入，并兼顾效率和安全性

- [Efficient On-Device Agents](https://arxiv.org/abs/2511.03728) → §1.2 Token & Context | Token Δ: >6× smaller initial context; 10–25× slower context growth | Acc Δ: matches or exceeds baseline | Lat Δ: — | Compresses memory and tool schemas for on-device agents; device-side setting limits generality
  - 来源：arXiv
  - 收录理由：补充 on-device agent 的 context management 和 tool schema 压缩方向

- [RepoMaster](https://arxiv.org/abs/2505.21577) → §1.3 Tool Use | Call Δ: repo exploration pruning | Acc Δ: +110% valid submissions / 40.7→62.9% pass rate | Lat Δ: −95% tokens | Explores GitHub repositories via dependency and call graphs for code agents; software-engineering specific
  - 来源：arXiv / GitHub
  - 收录理由：代码 agent 复用 GitHub repo 时显著降低上下文 token，并提升任务通过率

- [RCR-Router](https://arxiv.org/abs/2508.04903) → §1.4 Multi-Agent Coordination | Agent Δ: role-aware context routing | Acc Δ: maintained / improved answer quality | Cost Δ: up to −30% tokens | Routes task-relevant memory subsets per agent role and stage; arXiv-only with limited reproducibility signal
  - 来源：arXiv
  - 收录理由：直接优化 multi-agent collaboration 中的 memory exposure 和 token cost

- [Maestro](https://arxiv.org/abs/2509.04642) → §1.4 Multi-Agent Coordination | Agent Δ: joint graph+config optimization | Acc Δ: +12% vs MIPROv2 / +4.9% vs GEPA | Cost Δ: fewer rollouts than GEPA | Optimizes agent graph structure and node configuration under budgets; technical report with weaker publication signal
  - 来源：arXiv
  - 收录理由：把 agent graph 结构和 node config 一起纳入预算约束下优化，覆盖现有 prompt-only optimizer 的空白

- [AgentInit](https://arxiv.org/abs/2509.19236) → §1.4 Multi-Agent Coordination | Agent Δ: diversity+expertise initialization | Acc Δ: up to +1.2 / +1.6 over baselines | Cost Δ: significantly lower token use | Initializes MAS teams for efficient collaboration; abstract lacks exact token-reduction number
  - 来源：arXiv / EMNLP 2025 Findings / GitHub
  - 收录理由：EMNLP 2025 Findings，直接优化 multi-agent team initialization 的效率和效果

- [SuffixDecoding](https://arxiv.org/abs/2411.04975) → §1.6 Serving | Throughput Δ: up to 5.3× speedup | Lat Δ: up to 5.3× speedup | Mem Δ: suffix-tree cache | Caches repeated suffixes for agentic inference workloads; serving-layer method rather than orchestration method
  - 来源：arXiv / NeurIPS 2025 Spotlight / GitHub
  - 收录理由：NeurIPS 2025 Spotlight，明确针对 agentic repetitive inference workloads，有强速度指标和开源实现

- [GUI-KV](https://arxiv.org/abs/2510.00536) → §1.6 Serving | Throughput Δ: −38.9% decoding FLOPs | Lat Δ: — | Mem Δ: GUI-specific KV compression | Compresses GUI-agent KV cache with spatio-temporal awareness; strongest for screenshot-heavy GUI agents
  - 来源：arXiv
  - 收录理由：直接面向 GUI agents 的 KV cache 压缩，兼顾效率和 step accuracy

- [REFRAG](https://arxiv.org/abs/2509.01092) → §1.6 Serving | Throughput Δ: — | Lat Δ: 30.85× TTFT speedup | Mem Δ: long-context RAG decoding compression | Removes unnecessary RAG-context decoding computation for multi-turn and agentic RAG; agentic use is one target scenario among several
  - 来源：arXiv
  - 收录理由：优化 RAG / multi-turn / agentic long-context decoding latency，速度指标强

- [SWE-Effi](https://arxiv.org/abs/2509.09853) → §3 Benchmarks & Evaluation | Metric Δ: resource-aware effectiveness score | Acc Δ: re-ranks SWE agents by accuracy/resource tradeoff | Cost/Lat Δ: token and time constrained evaluation | Evaluates software agents under token/time budgets; benchmark rather than new efficiency method
  - 来源：arXiv
  - 收录理由：补充 software agent 的 cost-aware evaluation，避免只看 SWE-bench accuracy

- [FDABench](https://arxiv.org/abs/2509.02473) → §3 Benchmarks & Evaluation | Metric Δ: 2,007 heterogeneous analytical tasks | Acc Δ: evaluates data-agent quality | Cost/Lat Δ: tracks latency/token cost | Benchmarks data agents over heterogeneous analytical queries; does not optimize agents directly
  - 来源：arXiv
  - 收录理由：补充 data agent benchmark，并显式关注 latency 和 token cost

- [ToolGen](https://arxiv.org/abs/2410.03439) → §1.3 Tool Use | Call Δ: no separate tool retrieval | Acc Δ: superior on retrieval + agent tasks | Lat Δ: — | Generates tool calls as tool tokens; requires tool-token training
  - 来源：arXiv / ICLR 2025
  - 收录理由：直接优化大规模 tool retrieval/calling，把工具选择从额外检索步骤变成生成过程

- [Divide, Optimize, Merge](https://arxiv.org/abs/2505.03973) → §1.1 Planning | Token Δ: −56.3% prompt tokens | Acc Δ: +1.6–8.6% | Lat Δ: offline optimization | Scales agent optimization by divide-and-merge; requires offline optimization data
  - 来源：arXiv
  - 收录理由：面向 agent optimization at scale，明确减少 prompt token 并提升 ALFWorld / LogisticsQA / GAIA 表现

- [AgentDropout](https://arxiv.org/abs/2503.18891) → §1.4 Multi-Agent Coordination | Agent Δ: dynamic agent/edge dropout | Acc Δ: +1.14 avg task score | Cost Δ: −21.6% prompt / −18.4% completion tokens | Drops redundant agents across rounds; overlaps with pruning-based MAS methods
  - 来源：arXiv / GitHub
  - 收录理由：直接优化 multi-agent communication redundancy，有 token 与 task-performance 双重收益

- [OpenCity](https://arxiv.org/abs/2410.21286) → §1.4 Multi-Agent Coordination | Agent Δ: 10k-agent scheduling + prompt distillation | Acc Δ: — | Cost Δ: 600× speed / −70% requests / −50% tokens | Scales massive LLM-agent simulation; strongest evidence is urban-simulation specific
  - 来源：arXiv
  - 收录理由：填补 massive LLM-agent simulation 的系统级效率条目，有请求数、token 和仿真速度量化结果

- [Mem0](https://arxiv.org/abs/2504.19413) → §1.5 Memory & Retrieval | Retrieval Δ: persistent memory retrieval | Acc Δ: +26% LLM-as-judge vs OpenAI | Cost/Lat Δ: −91% p95 latency / >90% token cost | Extracts salient long-term memories with lower latency/cost; graph memory adds system complexity
  - 来源：arXiv
  - 收录理由：面向 production AI agents 的长期记忆系统，直接报告 latency 与 token-cost 收益

- [XGrammar](https://arxiv.org/abs/2411.15100) → §1.6 Serving | Throughput Δ: up to +100× CFG execution | Lat Δ: near-zero overhead structured generation | Mem Δ: token-mask cache | Speeds constrained decoding for function calls; only helps structured-output workloads
  - 来源：arXiv / MLSys 2025
  - 收录理由：优化 agent structured output / function calling 的 constrained decoding overhead，系统实现价值高


## 2026-06-08

### Added
- [DEPO](https://arxiv.org/abs/2511.15392) -> §1.1 Planning | Token Δ: -60.9% tokens; -26.9% steps | Acc Δ: up to +29.3% | Lat Δ: - | Optimizes step-level and trajectory-level agent efficiency; training-based and mainly validated on WebShop/BabyAI
  - 来源：arXiv / project page
  - 收录理由：直接定义并优化 agent token-per-step 和 trajectory-step efficiency，量化结果清楚

- [More with Less](https://arxiv.org/abs/2510.16786) -> §1.1 Planning | Token Δ: cost -24-68%; dynamic turns add -12-24% | Acc Δ: comparable / better solve rates | Lat Δ: fewer turns | Controls coding-agent turn budgets; empirical study rather than a new framework
  - 来源：arXiv
  - 收录理由：填补 coding agent turn-control 成本管理方向，策略简单且工程可用

- [Prune4Web](https://arxiv.org/abs/2511.21398) -> §1.2 Token & Context | Token Δ: 25-50x fewer candidate DOM elements | Acc Δ: 46.8% -> 88.28% grounding accuracy | Lat Δ: - | Programmatically prunes web-agent DOM context; web-DOM specific
  - 来源：arXiv
  - 收录理由：直接解决 web agent DOM token/context 爆炸问题，准确率和压缩收益都明确

- [Z-Space](https://arxiv.org/abs/2511.19483) -> §1.3 Tool Use | Call Δ: -96.26% tool-inference tokens | Acc Δ: 92% tool invocation accuracy | Lat Δ: - | Filters enterprise MCP tools through multi-agent orchestration; production evidence but limited open reproducibility
  - 来源：arXiv
  - 收录理由：面向大规模 MCP/tool selection 的 token 开销优化，有生产级量化结果

- [Agent-GSPO](https://arxiv.org/abs/2510.22477) -> §1.4 Multi-Agent Coordination | Agent Δ: communication-aware GSPO | Acc Δ: SOTA on seven reasoning benchmarks | Cost Δ: fraction of baseline tokens | Trains concise multi-agent communication; abstract lacks exact token-reduction percentage
  - 来源：arXiv
  - 收录理由：直接优化 MAS communication token economy，方向与 §1.4 高度匹配

- [iMAD](https://arxiv.org/abs/2511.11306) -> §1.4 Multi-Agent Coordination | Agent Δ: selective debate triggering | Acc Δ: up to +13.5% | Cost Δ: up to -92% tokens | Triggers MAD only when beneficial; limited to debate-style workflows
  - 来源：arXiv
  - 收录理由：直接降低 multi-agent debate 的无效触发成本，同时提升准确率

- [TeaRAG](https://arxiv.org/abs/2511.05385) -> §1.5 Memory & Retrieval | Retrieval Δ: graph triplet retrieval + IP-DPO | Acc Δ: +4% / +2% EM | Cost/Lat Δ: -61% / -59% output tokens | Compresses retrieval content and reasoning steps; requires graph retrieval and DPO setup
  - 来源：arXiv / GitHub
  - 收录理由：面向 agentic RAG 的 token-efficient retrieval 和 reasoning，指标清楚且有代码

- [ParallelMuse](https://arxiv.org/abs/2510.24698) -> §1.5 Memory & Retrieval | Retrieval Δ: partial rollout reuse + compressed aggregation | Acc Δ: up to +62% | Cost/Lat Δ: -10-30% exploratory tokens | Reuses deep search trajectories; mainly useful for long-horizon information-seeking agents
  - 来源：arXiv
  - 收录理由：补充 deep information-seeking agent 的 parallel rollout reuse 和压缩聚合方向

- [KVCOMM](https://arxiv.org/abs/2510.12872) -> §1.6 Serving | Throughput Δ: >70% KV reuse | Lat Δ: up to 7.8x speedup; TTFT ~430 ms -> ~55 ms | Mem Δ: online anchor pool | Reuses cross-agent KV caches; benefits depend on overlapping agent contexts
  - 来源：arXiv
  - 收录理由：专门面向 multi-agent repeated-prefill overhead，属于 agentic serving 的强相关系统论文

- [Scaling Graph-CoT / GLM](https://arxiv.org/abs/2511.01633) -> §1.6 Serving | Throughput Δ: up to 15.1x | Lat Δ: -90.3% | Mem Δ: graph-specific KV cache | Co-designs multi-agent Graph-CoT with serving; strongest evidence is graph reasoning
  - 来源：arXiv
  - 收录理由：同时报告 token、latency、throughput 和 accuracy 收益，适合补 agentic serving

- [LoCoBench-Agent](https://arxiv.org/abs/2511.13998) -> §3 Benchmarks & Evaluation | Metric Δ: 9 efficiency/comprehension metrics over 10K-1M tokens | Acc Δ: evaluates long-context software agents | Cost/Lat Δ: tracks tool and conversation efficiency | Benchmark only; no new optimization method
  - 来源：arXiv
  - 收录理由：补充 long-context software agent 的效率评测基准

- [MCP vs RAG vs NLWeb vs HTML](https://arxiv.org/abs/2511.23281) -> §3 Benchmarks & Evaluation | Metric Δ: web-agent interface comparison | Acc Δ: F1 0.67 HTML -> 0.75-0.77 alternatives | Cost/Lat Δ: 241k -> 47k-140k tokens; 291s -> 50-62s | Simulated e-shop testbed; technical report status
  - 来源：arXiv
  - 收录理由：直接比较 web agent 接口选择对 effectiveness、token 和 runtime 的影响

## 2026-06-14

### Added

- [UIFormer](https://arxiv.org/abs/2512.13438) → §1.2 Token & Context Efficiency | Token Δ: −48.7–55.8% UI tokens | Acc Δ: maintained / improved | Lat Δ: 5.7 ms overhead; prod −26.1% latency | Compact UI representation for GUI agents; UI-navigation-specific.
  - 来源：arXiv / PDF
  - 收录理由：直接优化 GUI agent 的上下文 token，是 agent efficiency 主题的强相关论文。

- [Task-Decoupled Planning](https://arxiv.org/abs/2601.07577) → §1.1 Planning & Reasoning Efficiency | Token Δ: up to −82.4% output tokens | Acc Δ: HotpotQA up to 85.88% | Lat Δ: — | Separates planning into smaller scoped sub-tasks; sub-task granularity remains a limitation.
  - 来源：arXiv / PDF
  - 收录理由：用任务解耦减少长程 agent 规划的输出 token，和 planning efficiency 强相关。

- [Agent.xpu](https://arxiv.org/abs/2506.24045) → §1.6 Inference & Serving Efficiency | Throughput Δ: +1.2–4.9× | Lat Δ: −91–97% reactive latency | Cost Δ: −26.8% energy | Heterogeneous on-device scheduling for agent workloads; hardware-specific.
  - 来源：arXiv / PDF
  - 收录理由：覆盖端侧 agent 的吞吐、延迟和能耗效率，适合放入 serving/system efficiency。

- [ToolRM](https://arxiv.org/abs/2510.26167) → §1.3 Tool Use Efficiency | Call Δ: RM-guided tool selection | Acc Δ: up to +17.94% weighted accuracy | Token Δ: >66% fewer output tokens on ACEBench | Reward models for tool reasoning; requires curated preference data.
  - 来源：arXiv / PDF
  - 收录理由：直接提升 tool-use agent 的调用判断与 token 效率。

- [Semantic Caching and Intent-Driven Context Optimization](https://arxiv.org/abs/2601.11687) → §1.5 Memory & Retrieval Efficiency | Retrieval Δ: 67.3% cache utilization | Acc Δ: 94.3% semantic accuracy | Token Δ: −51.7% prompt tokens | Production enterprise analytics cache/context optimizer; domain-specific.
  - 来源：arXiv / PDF
  - 收录理由：同时优化 semantic cache、context filtering、latency 和 cost，和 retrieval/context efficiency 高相关。

- [An Information Theoretic Perspective on Agentic System Design](https://arxiv.org/abs/2512.21720) → §1.2 Token & Context Efficiency | Token Δ: 4.6× more concise summaries | Acc Δ: 99% frontier-LM accuracy recovered | Cost Δ: 74% API-cost cut | Information-bottleneck view of agent compression; more conceptual than plug-in framework.
  - 来源：arXiv / PDF
  - 收录理由：提供 agent 上下文压缩的理论视角和成本实验证据。

- [FoldAct](https://arxiv.org/abs/2512.22733) → §1.2 Token & Context Efficiency | Token Δ: 0.25–0.65 context ratio | Acc Δ: HotpotQA 38.5 F1 / 29.5 EM | Lat Δ: 5.19× training speedup | Context folding for long-horizon search-agent RL; training-time method.
  - 来源：arXiv / PDF
  - 收录理由：面向长轨迹 agent 训练的上下文压缩方法，效率指标明确。

- [CCPO](https://arxiv.org/abs/2601.11631) → §1.2 Token & Context Efficiency | Token Δ: up to −55.01% visual tokens | Acc Δ: AITW 75.12 overall | Lat Δ: up to 3.8× training speedup | Curriculum compression for GUI agents; coordinate/GUI-specific.
  - 来源：arXiv / PDF
  - 收录理由：直接减少 GUI agent 多轮视觉上下文，且报告 token、FLOPs、训练速度收益。

- [ACE](https://arxiv.org/abs/2601.08747) → §1.5 Memory & Retrieval Efficiency | Retrieval Δ: adaptive retrieve-or-think | Acc Δ: HotpotQA 62.8%; MultiHop-RAG 57.9% | Token Δ: −42% vs IterDRAG on MultiHop-RAG | Adaptive context-efficient reasoning; higher token cost than one-shot RAG.
  - 来源：arXiv / PDF
  - 收录理由：把“是否检索”作为 agent 决策来优化上下文成本，适合 retrieval efficiency。

- [When Single-Agent with Skills Replace Multi-Agent Systems and When They Fail](https://arxiv.org/abs/2601.04748) → §1.4 Multi-Agent Coordination | Agent Δ: API calls 3–4→1 | Acc Δ: avg +0.7% | Cost Δ: −53.7% tokens; −49.5% latency | Skill-equipped single agents can replace some MAS; preliminary scope.
  - 来源：arXiv / PDF
  - 收录理由：直接比较 MAS 和 skill-based single agent 的成本、token、latency trade-off。

- [IDRBench](https://arxiv.org/abs/2601.06676) → §3 Benchmarks & Evaluation | Measures: report quality, turns, interaction tokens | Gap: benchmark only | Cost Δ: measured, not optimized | Interactive deep research benchmark with cost-aware metrics.
  - 来源：arXiv / PDF
  - 收录理由：提供 deep-research agent 的交互成本和质量评估框架。

- [SWEnergy](https://arxiv.org/abs/2512.09543) → §3 Benchmarks & Evaluation | Measures: energy, duration, tokens, memory | Gap: near-zero solve rates | Cost Δ: AutoCodeRover Gemma uses 9.4× more energy than OpenHands Gemma | Energy-focused evaluation of SLM software-engineering agents.
  - 来源：arXiv / PDF
  - 收录理由：补上 agent efficiency repo 里较少覆盖的能耗评估维度。

## 2026-06-20-14:00

### Added
- [Toward Efficient Agents: Memory, Tool Learning, and Planning](https://arxiv.org/abs/2601.14192) → §0 Surveys | Metric Δ: agent efficiency taxonomy | Acc Δ: — | Cost/Lat Δ: covers tokens, steps, and latency | Surveys memory, tool-learning, and planning efficiency; does not introduce a new optimization method
  - 来源：arXiv
  - 收录理由：主题与 repo 高度一致，并以效果与成本的 Pareto 权衡统一整理 agent efficiency 研究

- [Think Fast and Slow](https://arxiv.org/abs/2602.12662) → §1.1 Planning | Token Δ: -62% | Acc Δ: 82.3% success rate | Lat Δ: — | Routes each step to an appropriate cognitive depth; requires two-stage training
  - 来源：arXiv
  - 收录理由：直接优化长程 agent 每一步的推理深度，同时显著减少 token 并提高任务成功率

- [EGSS](https://arxiv.org/abs/2602.05242) → §1.1 Planning | Token Δ: >-28% inference tokens | Acc Δ: +5-10% | Lat Δ: — | Allocates test-time compute using entropy-guided search; mainly validated on SWE-Bench-Verified
  - 来源：arXiv
  - 收录理由：在软件工程 agent 中同时提升准确率并降低测试时扩展的 token 开销

- [Agentic Test-Time Scaling for WebAgents](https://arxiv.org/abs/2602.12276) → §1.1 Planning | Token Δ: up to 2.3x fewer tokens | Acc Δ: up to +9.1% vs. ReAct | Lat Δ: dynamic compute allocation | Scales compute only at uncertain steps; web-navigation specific
  - 来源：arXiv
  - 收录理由：利用不确定性按步骤分配推理预算，避免 uniform scaling 的无效计算

- [HyFunc](https://arxiv.org/abs/2602.13665) → §1.3 Tool Use | Call Δ: hybrid-model function selection | Acc Δ: 80.1% | Lat Δ: 0.828 s inference | Accelerates function calls using model cascading and dynamic templates; specialized implementation required
  - 来源：arXiv / GitHub
  - 收录理由：直接消除 function calling 中的工具描述、模型生成和固定语法冗余

- [OpaqueToolsBench](https://arxiv.org/abs/2602.15197) → §1.3 Tool Use | Call Δ: interaction-driven tool documentation | Acc Δ: outperforms existing methods | Cost/Lat Δ: 3.5-7.5x fewer total tokens | Learns opaque tool behavior from execution feedback; strongest with incomplete documentation
  - 来源：arXiv
  - 收录理由：优化 agent 探索和学习未知工具行为时产生的高额 token 成本

- [Training-Free Agentic AI](https://arxiv.org/abs/2603.13256) → §1.4 Multi-Agent Coordination | Agent Δ: belief-guided delegation; -17% calls | Acc Δ: maintained / robust | Cost Δ: -28% tokens; -19% time-to-success | Improves recursive delegation without training; evaluated mainly on split-knowledge tasks
  - 来源：arXiv
  - 收录理由：用轻量概率控制减少 multi-agent 路由中的无效调用、token 和执行时间

- [HyperAgent](https://arxiv.org/abs/2510.10611) → §1.4 Multi-Agent Coordination | Agent Δ: adaptive hypergraph topology | Acc Δ: 95.07% on GSM8K | Cost Δ: -25.33% tokens | Models group-level communication using hypergraphs; requires topology-learning setup
  - 来源：arXiv
  - 收录理由：相比现有 pairwise graph 方法，补充了多 agent 群组通信拓扑优化方向

- [SimpleMem](https://arxiv.org/abs/2601.02553) → §1.5 Memory & Retrieval | Retrieval Δ: semantic compression + intent-aware retrieval | Acc Δ: +26.4% F1 on LoCoMo | Cost/Lat Δ: up to 30x fewer inference tokens | Compresses lifelong agent memory; adds a multi-stage memory pipeline
  - 来源：arXiv / GitHub
  - 收录理由：同时提升长期记忆准确率、检索效率并大幅减少推理 token

- [A-RAG](https://arxiv.org/abs/2602.03442) → §1.5 Memory & Retrieval | Retrieval Δ: adaptive hierarchical retrieval | Acc Δ: outperforms existing RAG approaches | Cost/Lat Δ: comparable or fewer retrieved tokens | Lets agents control retrieval interfaces; abstract lacks an exact token-reduction percentage
  - 来源：arXiv / GitHub
  - 收录理由：将检索决策交给 agent，并在更少或相当检索 token 下提高效果

- [AgentInfer](https://arxiv.org/abs/2512.18337) → §1.6 Serving | Throughput Δ: 1.8-2.5x speedup | Acc Δ: preserved | Mem Δ: >50% fewer ineffective tokens | Co-designs agent architecture and serving; deployment requires multiple integrated modules
  - 来源：arXiv
  - 收录理由：面向完整 agent 任务而非单次模型调用，联合优化调度、解码和上下文压缩

- [Optimizing FaaS Platforms for MCP-enabled Agentic Workflows](https://arxiv.org/abs/2601.14735) → §1.6 Serving | Throughput Δ: FaaS orchestration | Lat Δ: up to 13x faster | Mem Δ: -88% input tokens; -66% cost | Optimizes MCP workflows through serverless execution; strongly tied to AWS infrastructure
  - 来源：arXiv
  - 收录理由：提供 agentic MCP 工作流在延迟、token 和成本上的完整系统级优化结果

- [EffGen](https://arxiv.org/abs/2602.00887) → §4 Tools & Frameworks | Metric Δ: local SLM agent framework | Acc Δ: outperforms LangChain, AutoGen, and Smolagents | Cost/Lat Δ: 70-80% context compression | Combines routing, tool calling, and memory for local agents; individual contributions are less isolated
  - 来源：arXiv / GitHub
  - 收录理由：提供可直接使用的开源小模型 agent 框架，并报告明确的上下文压缩和执行效率收益

## 2026-06-20-15:00

### Added
- [ELHPlan](https://arxiv.org/abs/2509.24230) → §1.1 Planning | Token Δ: uses 30-40% of SOTA tokens | Acc Δ: comparable success | Lat Δ: lower planning time | Plans with intention-bound action chains for multi-agent collaboration; evaluated on embodied multi-agent benchmarks
  - 来源：arXiv
  - 收录理由：直接优化 long-horizon multi-agent planning 的 token 与规划成本，指标清楚

- [SAGE](https://arxiv.org/abs/2512.17102) → §1.1 Planning | Token Δ: -59% | Acc Δ: +8.9% scenario goal completion | Lat Δ: -26% interaction steps | Learns reusable skills through sequential rollouts; depends on RL training and skill-library infrastructure
  - 来源：arXiv
  - 收录理由：通过 skill library 降低 agent 交互步骤和 token，同时提升任务完成率

- [AgentOCR](https://arxiv.org/abs/2601.04786) → §1.2 Token & Context | Token Δ: >-50% | Acc Δ: >95% text-agent performance preserved | Lat Δ: 20x rendering speedup | Compresses agent history into visual representations; adds rendering and visual-cache machinery
  - 来源：arXiv
  - 收录理由：直接压缩多轮 agent history，是 token/context efficiency 的强相关方向

- [AgentDiet](https://arxiv.org/abs/2509.23586) → §1.2 Token & Context | Token Δ: -39.9% to -59.7% input tokens | Acc Δ: maintained | Cost/Lat Δ: -21.1% to -35.9% total cost | Removes useless and expired trajectory content at inference time; mainly validated on coding agents
  - 来源：arXiv
  - 收录理由：无需训练即可减少 agent trajectory token，且不损失任务表现

- [Agents Learn Their Runtime](https://arxiv.org/abs/2603.01209) → §1.3 Tool Use | Call Δ: interpreter-state alignment | Acc Δ: quality unchanged | Cost/Lat Δ: avoids up to 3.5x redundant tokens | Shows runtime persistence should match tool-agent traces; controlled synthetic-task evidence
  - 来源：arXiv
  - 收录理由：揭示 CodeAct/tool agent 的 runtime 语义会显著影响 token 成本和稳定性

- [AutoTool](https://arxiv.org/abs/2603.13348) → §1.3 Tool Use | Call Δ: automatic tool reasoning scaling | Acc Δ: +9.8% | Cost/Lat Δ: ~-81% computational overhead | Uses entropy-constrained RL to adapt tool-use reasoning length; requires RL training
  - 来源：arXiv
  - 收录理由：直接解决 tool-use agent 在简单问题中过度思考导致的 token 浪费

- [Semantic Tool Discovery](https://arxiv.org/abs/2603.20313) → §1.3 Tool Use | Call Δ: -99.6% tool tokens | Acc Δ: 97.1% hit rate at K=3 | Lat Δ: sub-100ms retrieval | Retrieves relevant MCP tools instead of exposing full catalogs; benchmark has 121 tools
  - 来源：arXiv
  - 收录理由：针对 MCP tool selection 的上下文爆炸问题，token 降幅极强

- [WorkflowGen](https://arxiv.org/abs/2604.19756) → §1.3 Tool Use | Call Δ: trajectory-based workflow reuse | Acc Δ: +20% success on medium-similarity queries | Cost/Lat Δ: >-40% tokens | Rewrites reusable workflow trajectories instead of planning from scratch; evidence is qualitative/comparative
  - 来源：arXiv
  - 收录理由：通过复用历史 workflow experience 减少工具型 agent 的重复规划成本

- [RUMAD](https://arxiv.org/abs/2602.23864) → §1.4 Multi-Agent Coordination | Agent Δ: dynamic debate topology | Acc Δ: improves over single LLM and MAD baselines | Cost Δ: >-80% token cost | Controls MAD communication with RL; strongest for debate-style reasoning
  - 来源：arXiv
  - 收录理由：直接优化 multi-agent debate 的通信拓扑和 token 成本，同时提升准确率

- [Stop Wasting Your Tokens](https://arxiv.org/abs/2510.26585) → §1.4 Multi-Agent Coordination | Agent Δ: runtime supervision | Acc Δ: success maintained | Cost Δ: -29.68% tokens on GAIA | Adds lightweight adaptive supervision for MAS at runtime; depends on filter reliability
  - 来源：arXiv
  - 收录理由：无需改 base agent 架构即可减少 runtime multi-agent 系统 token 浪费

- [LDP](https://arxiv.org/abs/2603.08852) → §1.4 Multi-Agent Coordination | Agent Δ: identity-aware delegation protocol | Acc Δ: aggregate quality not improved in small pool | Cost Δ: ~12x lower latency on easy tasks; -37% tokens | Adds model identity and payload negotiation to agent protocols; early local evidence
  - 来源：arXiv
  - 收录理由：从协议层减少 multi-agent delegation 的延迟和 payload token

- [SafeSieve](https://arxiv.org/abs/2508.11733) → §1.4 Multi-Agent Coordination | Agent Δ: progressive communication pruning | Acc Δ: 94.01% avg accuracy | Cost Δ: -12.4% to -27.8% tokens; -13.3% deployment cost | Prunes MAS communication using semantics and feedback; gains are moderate but practical
  - 来源：arXiv / GitHub
  - 收录理由：GPU-free progressive pruning 方法，直接面向 multi-agent communication efficiency

- [M$^2$](https://arxiv.org/abs/2603.00503) → §1.5 Memory & Retrieval | Retrieval Δ: dual memory for web agents | Acc Δ: up to +19.6% success | Cost/Lat Δ: -58.7% tokens | Combines trajectory summarization with insight retrieval; web-navigation focused
  - 来源：arXiv
  - 收录理由：同时提升长程 web agent 成功率并明显降低 token 使用

- [Tiny-Critic RAG](https://arxiv.org/abs/2603.00846) → §1.5 Memory & Retrieval | Retrieval Δ: SLM fallback gate | Acc Δ: ≈GPT-4o-mini routing accuracy | Cost/Lat Δ: order-of-magnitude latency reduction | Uses a LoRA SLM for reflective RAG routing; focused on binary fallback decisions
  - 来源：arXiv
  - 收录理由：用小模型替代大模型 evaluator，降低 agentic RAG routing 成本

- [Mem-T](https://arxiv.org/abs/2601.23014) → §1.5 Memory & Retrieval | Retrieval Δ: memory-operation tree credit assignment | Acc Δ: up to +14.92% | Cost/Lat Δ: -24.45% inference tokens | Trains long-horizon memory agents with dense rewards; requires RL and hierarchical memory DB
  - 来源：arXiv
  - 收录理由：直接优化 memory agent 的构建、更新和检索策略，并报告 token 收益

- [Test-Time Strategies for Agentic RAG](https://arxiv.org/abs/2603.12396) → §1.5 Memory & Retrieval | Retrieval Δ: contextualization + de-duplication | Acc Δ: +5.6% EM | Cost/Lat Δ: -10.5% turns | Improves Search-R1-style agentic RAG at test time; evaluated on QA datasets
  - 来源：arXiv
  - 收录理由：减少 agentic RAG 的重复检索 turn，同时提高答案准确率

- [D-MEM](https://arxiv.org/abs/2603.14597) → §1.5 Memory & Retrieval | Retrieval Δ: reward-prediction memory routing | Acc Δ: outperforms baselines | Cost/Lat Δ: >-80% tokens; removes $O(N^2)$ write bottleneck | Routes memory updates through fast/slow paths; adds critic router
  - 来源：arXiv
  - 收录理由：直接解决 lifelong agent memory 的 token 成本和写入延迟瓶颈

- [Memori](https://arxiv.org/abs/2603.19935) → §1.5 Memory & Retrieval | Retrieval Δ: structured persistent memory | Acc Δ: 81.95% on LoCoMo | Cost/Lat Δ: 1,294 tokens/query; -67% vs competitors | Converts dialogue into triples and summaries; system-layer memory design
  - 来源：arXiv
  - 收录理由：持久化 memory layer 有清楚的 token/cost 数字，适合补充 memory efficiency

- [ICaRus](https://arxiv.org/abs/2603.13281) → §1.6 Serving | Throughput Δ: 3.8x | Lat Δ: 11.1x lower P95 latency | Mem Δ: shared cross-model KV cache | Shares identical KV caches across specialized models; requires compatible fine-tuning setup
  - 来源：arXiv
  - 收录理由：面向 multi-model / multi-agent workflow 的 KV cache 共享，latency 和 throughput 指标强

- [RelayCaching](https://arxiv.org/abs/2603.13289) → §1.6 Serving | Throughput Δ: >80% KV reuse | Lat Δ: up to 4.7x TTFT speedup | Mem Δ: decoding KV reuse | Reuses previous agents' decoding KV caches during later prefill; assumes shared content
  - 来源：arXiv
  - 收录理由：专门减少多 agent 协作中的重复 prefill 计算和 TTFT

- [IndexCache](https://arxiv.org/abs/2603.12201) → §1.6 Serving | Throughput Δ: removes 75% indexer computations | Lat Δ: 1.82x prefill; 1.48x decode | Mem Δ: cross-layer sparse-index reuse | Reuses sparse-attention indices across layers; tied to DSA-style serving stacks
  - 来源：arXiv
  - 收录理由：针对 long-context agentic workflow 的 attention serving bottleneck，有明确加速数字

- [AgentAssay](https://arxiv.org/abs/2603.02601) → §3 Benchmarks & Evaluation | Metric Δ: token-efficient regression testing | Acc Δ: 86% detection power where binary testing has 0% | Cost/Lat Δ: 78-100% cost reduction | Tests nondeterministic agent workflows; testing framework rather than optimizer
  - 来源：arXiv
  - 收录理由：补充 agent workflow 回归测试与成本受控评估方向

- [SkillCraft](https://arxiv.org/abs/2603.00718) → §3 Benchmarks & Evaluation | Metric Δ: tool-skill formation and reuse benchmark | Acc Δ: success correlates with tool composition | Cost/Lat Δ: up to -80% tokens from skill saving and reuse | Evaluates reusable tool compositions; not a standalone efficiency method
  - 来源：arXiv
  - 收录理由：补充 tool-use agent 是否能形成并复用技能的效率评测

