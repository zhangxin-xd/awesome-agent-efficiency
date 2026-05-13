# 维护手册：Awesome Agent Efficiency

适用仓库：[awesome-agent-efficiency](https://github.com/zhangxin-xd/awesome-agent-efficiency)

---

## 一、论文来源：从哪里发现新论文

| 渠道 | 链接 | 频率 |
|------|------|------|
| arXiv cs.AI daily | https://arxiv.org/list/cs.AI/recent | 每天 |
| arXiv cs.LG daily | https://arxiv.org/list/cs.LG/recent | 每天 |
| arXiv cs.DC daily（serving/系统）| https://arxiv.org/list/cs.DC/recent | 每周 |
| Hugging Face Papers | https://huggingface.co/papers | 每天 |
| Twitter/X 关键词 | 见下 | 每天 |
| Semantic Scholar Alerts | 设置关键词订阅邮件 | 自动 |
| 顶会 proceedings | ICLR / NeurIPS / ACL / SOSP / OSDI / MLSys | 每次开会 |

**推荐搜索关键词**：
`LLM agent efficiency`、`KV cache agent`、`token compression agent`、`agent serving`、`multi-agent cost`、`agent planning efficiency`、`prompt compression`、`speculative decoding agent`、`agent inference optimization`

---

## 二、收录标准

### 必须满足

- [ ] 研究对象是 **agentic 系统**（单 agent 或多 agent），不是孤立的单次 LLM 推理
- [ ] 有实质贡献：新方法、新系统、新基准、或重要实证发现
- [ ] 有实验/数据支撑

> **注**：serving 层论文（如 vLLM、SGLang）即使不专注 agent，也可收录——前提是对 agentic workload 有明确优化或实验。

### 加分项

- 发表在顶会：ICLR / NeurIPS / ACL / SOSP / OSDI / MLSys / EMNLP
- arXiv 引用数 > 50（发布超过 3 个月）
- 填补现有分类中某个效率维度的空白
- 有量化的 token / latency / cost 数字可填入表格
- 有开源实现

### 直接排除

- ❌ 纯 LLM 效率，无 agentic 场景（如单次问答的推理加速，无工具/记忆/多轮）
- ❌ 没有实验的立场文章
- ❌ 与已有条目高度重复（核心思路相同，只换了场景）
- ❌ 发布不足 2 周、引用为 0、且无明显社区关注

### 早期论文的社区关注信号

预印本不足 2 周且引用为 0 时，满足以下任意一条可提前收录：

| 信号 | 参考阈值 | 查看方式 |
|------|---------|---------|
| GitHub 代码仓库 stars | > 200 | 论文页找代码链接 |
| HuggingFace Papers 点赞 | > 50 | huggingface.co/papers |
| Twitter/X 转发+点赞 | > 500（原作者推文）| 搜 arXiv 号 |
| 知名研究者/工程师公开推荐 | 任意 | Twitter、Newsletter |
| 被主流框架引用 | 任意 | 如 vLLM、LangChain、AutoGen 博客提及 |

提前收录时在 CHANGELOG 中标注 `[early, high-attention]`，一个月后复查引用数和量化数据。

### 快速判断流程

```
读摘要 (30秒)
    │
    ├── 研究对象是 agent？ → No → 排除
    │   （或对 agentic workload 有明确优化？）
    │
    ├── 有新方法/系统/基准？ → No → 排除
    │
    ├── 顶会 OR 引用 > 50？
    │       ├── Yes → 直接收录
    │       └── No  → 发布不足 2 周？
    │                   ├── No → 填补空白？
    │                   │         ├── Yes → 收录，备注 "fills gap"
    │                   │         └── No  → 暂缓
    │                   └── Yes → 社区关注信号？
    │                               ├── Yes → 收录，备注 "[early, high-attention]"
    │                               └── No  → 暂缓 2 周后复查
    │
    └── 放入正确的效率维度分类
```

---

## 三、收录格式

```markdown
| [论文标题](arxiv或论文链接) | 会议/期刊 年份 | Token Δ | Accuracy Δ | Latency Δ | 贡献一句话；局限一句话 |
```

### 量化列填写规范

| 列名 | 含义 | 示例 |
|------|------|------|
| Token Δ | 与 baseline 相比每步 token 变化 | `−75%`、`+10×`、`—` |
| Accuracy Δ | 任务成功率变化 | `<−3%`、`+15%`、`≈0%` |
| Latency Δ | 延迟变化（↓快 ↑慢） | `↓3×`、`↑10×`、`—` |

> `—` 表示论文无数据，不要编造数字。

**数字来源优先级**：
1. 论文主实验表格
2. 摘要中提到的数字
3. 数量级估计（标注"approx."）
4. 无数据填 `—`

**评注写法规范**：
- 前半句：贡献（结果/改进）
- 后半句：局限（假设、适用条件、或缺少什么）
- 用分号隔开，控制在 20 词以内

**示例**：
```
Compresses verbose CoT into compact drafts; up to 80% token reduction with minimal accuracy loss
```

**放入哪个分类**：

| 内容 | 对应分类 |
|------|---------|
| 减少推理步骤、优化规划路径 | §1.1 Planning & Reasoning Efficiency |
| 压缩 prompt、管理长上下文 | §1.2 Token & Context Efficiency |
| 减少工具调用次数、提升工具选择准确率 | §1.3 Tool Use Efficiency |
| 减少多 agent 通信开销、优化协调 | §1.4 Multi-Agent Coordination |
| 加速 RAG 检索、压缩记忆 | §1.5 Memory & Retrieval Efficiency |
| GPU 显存、吞吐、KV cache、推测解码 | §1.6 Inference & Serving Efficiency |

---

## 四、每日 Log

在仓库根目录维护 `CHANGELOG.md`，每次更新追加：

```markdown
## 2026-05-14

### Added
- [CacheTTL](https://arxiv.org/abs/2511.02230) → §1.6 | Token Δ: — | Acc Δ: ≈0% | Lat Δ: ↓8× | KV cache TTL for multi-turn agent scheduling; agent-specific gap, highly cited early [early, high-attention]
  - 来源：arXiv daily
  - 收录理由：填补 §5.6 open problem，agent-specific serving

### Considered but Rejected
- [论文标题](链接) | 排除原因：单次 LLM 推理加速，无 agentic 场景

---
```

**格式要求**：
- Added：标题 + 链接 + 分类 + 三列数字 + 评注 + 来源 + 收录理由
- Rejected：标题 + 链接 + 一句排除原因
- 拒绝记录同样重要，防止重复评估

---

## 五、定期维护

### 每周
- [ ] 检查各渠道新论文，按流程筛选
- [ ] 更新 CHANGELOG.md
- [ ] 更新 README 顶部 `updated` badge 日期
- [ ] Push 到 GitHub

### 每月
- [ ] 复查上月 `[early, high-attention]` 条目，补充引用数和量化数字
- [ ] 检查已有条目论文是否发布新版本修正了实验结果
- [ ] 更新 §2 Stack Recommendations（如有新工具在某个场景超越原有选择）
- [ ] 检查 §5 Open Problems：是否有新论文填补了已列出的 gap，需从 §5 移入正文

### 每次顶会放榜后
- [ ] 下载 proceedings，搜索关键词批量筛选
- [ ] 重点关注系统类：SOSP / OSDI / MLSys（serving 层）
- [ ] 重点关注 ML 类：ICLR / NeurIPS / ACL（planning / compression 层）

---

## 六、Git 提交规范

```bash
# 新增论文
git commit -m "add: [PaperName] → §1.6 serving"

# 修正量化数字
git commit -m "fix: update Token Δ for LLMLingua based on v3 paper"

# 更新技术栈推荐
git commit -m "update: Stack A — replace X with Y for lower latency"

# 结构调整
git commit -m "refactor: split §1.3 into selection and parallelism"
```

---

## 七、快速参考卡

```
新论文 → 30秒读摘要 → 三问：
  1. Agent 场景（有工具/记忆/多轮/多 agent）？
  2. 有新方法/系统/基准？
  3. 顶会 / 高引 / 社区高关注 / 填空白？

全Yes → 填三列数字 → 写评注 → 加进去 → 记 CHANGELOG → push

格式：
  | [标题](链接) | 会议 年份 | Token Δ | Acc Δ | Lat Δ | 贡献; 局限 |

量化原则：有数填数，无数填 —，不编造
```
