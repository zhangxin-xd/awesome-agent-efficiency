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
