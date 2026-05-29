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
