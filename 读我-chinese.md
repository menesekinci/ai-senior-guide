# AI 高级指南

[![GitHub](https://img.shields.io/github/license/menesekinci/ai-senior-guide)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/menesekinci/ai-senior-guide)](https://github.com/menesekinci/ai-senior-guide/stargazers)

> **AI 辅助软件开发的工程级标准**

一个全面的指南，旨在通过经过实战检验的架构模式、安全指南和最佳实践来防止 AI 生成代码中的"静默故障"。

---

## 🎯 这是什么？

**AI 高级指南**是一个结构化知识库，AI 编程助手可以参考它来生成可用于生产环境的代码。它解决了关键的差距，即 **40-45% 的 AI 生成代码包含静默故障** - 这些问题通过了测试，但在生产环境中失败。

### 静默故障问题

| 测试能捕获的内容 ✅ | 测试遗漏的内容 ❌ |
|---------------------|-------------------|
| 语法错误 | 竞态条件 |
| 运行时异常 | 细微的安全漏洞 |
| 失败的断言 | 性能下降 |
| | 架构反模式 |
| | 并发异常 |

### 🧠 认知 + 记忆协议

本指南实现了一种革命性的两阶段方法：

**阶段 1：认知协议（执行前）**
AI 在编码前使用 5 步深度思考过程进行深入思考。

**阶段 2：记忆协议（执行后）**
AI 通过 `architecturehistory.md` 维护持久记忆。

**结果：** AI 从"代码编写者"转变为具有机构记忆的"软件架构师"。

### ⚠️ 过度工程预防

**关键：** 本指南还防止了相反的问题 - **过度工程**。AI 代理在应用模式之前必须问自己"实际需要多少？"

---

## 🗃️ 项目记忆：architecturehistory.md

使用本指南的每个项目都应在项目根目录中维护一个 `architecturehistory.md` 文件。这充当 AI 在会话之间的"记忆"。

### 模板

```markdown
## [YYYY-MM-DD HH:MM] 变更：[功能名称]
- **目标：** [实现了什么]
- **决策：** [选择的架构]
- **理由：** [为什么，附带 KB 参考]
- **依赖项：** [相关组件]
- **风险/债务：** [已知限制]
```

---

## 📖 从这里开始：skill.md

**`skill.md` 是此知识库的主要入口点和索引。**

此文件用作：
- 所有 8 个知识库文件的**主索引**
- 用于快速主题查找的**关键字目录**
- 相关概念的**交叉引用指南**
- AI 代理的**使用说明**

---

## 🗂️ 仓库结构

```
ai-senior-guide/
├── skill.md                                    # ⭐ 从这里开始 - 主索引
├── knowledgeAI/                                # 知识库目录
│   ├── AI_Guardrail_Architecture_Knowledge_Base.md
│   ├── Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md
│   ├── Client_Side_Security_Architecture_Knowledge_Base.md
│   ├── Comprehensive_Architectural_Framework_Knowledge_Base.md
│   ├── Contextual_Architecture_Decision_Matrix_Knowledge_Base.md
│   ├── Defensive_UI_Engineering_Knowledge_Base.md
│   ├── End_to_End_Type_Safety_Knowledge_Base.md
│   └── Modern_Web_Performance_Engineering_Knowledge_Base.md
├── README.md                                   # 此文件
└── architecturehistory.md                      # 🧠 项目记忆
```

---

## 📚 可用知识文件

### 1. AI Guardrail 架构
**文件：** `/knowledgeAI/AI_Guardrail_Architecture_Knowledge_Base.md`

**全面的分布式系统和安全架构**

**关键字：** `distributed-systems`, `consistency`, `consensus`, `resilience`, `fault-tolerance`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

---

### 2. 高完整性系统中的架构弹性
**文件：** `/knowledgeAI/Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md`

**生产工作负载的高级可靠性模式**

**关键字：** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`, `kubernetes-hardening`

---

### 3. 客户端安全架构
**文件：** `/knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md`

**现代 Web 应用安全基础**

**关键字：** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`, `SRI`

---

### 4. 综合架构框架
**文件：** `/knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md`

**数据库并发、性能和安全基础**

**关键字：** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

---

### 5. 情境架构决策矩阵
**文件：** `/knowledgeAI/Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**避免过度工程和正确调整解决方案规模**

**关键字：** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `monolith`, `microservices`, `architecture-astronaut`

---

### 6. 防御性 UI 工程
**文件：** `/knowledgeAI/Defensive_UI_Engineering_Knowledge_Base.md`

**弹性用户界面模式**

**关键字：** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`, `focus-management`

---

### 7. 端到端类型安全
**文件：** `/knowledgeAI/End_to_End_Type_Safety_Knowledge_Base.md`

**类型安全的全栈 JavaScript 开发**

**关键字：** `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`, `Pact`, `RTK-Query`

---

### 8. 现代 Web 性能工程
**文件：** `/knowledgeAI/Modern_Web_Performance_Engineering_Knowledge_Base.md`

**Core Web Vitals 和优化策略**

**关键字：** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

---

## 🔍 快速参考：关键字映射

| 您正在处理的主题 | 阅读此文件 |
|------------------|------------|
| API 设计、REST、gRPC、GraphQL | AI Guardrail 架构 |
| 数据库、事务、并发 | 综合架构框架 |
| CSP、XSS、安全存储、JWT | 客户端安全架构 |
| 监控、追踪、可观测性 | 架构弹性 |
| 性能、打包、Core Web Vitals | 现代 Web 性能工程 |
| 类型安全、验证、模式 | 端到端类型安全 |
| 错误处理、加载状态 | 防御性 UI 工程 |
| 架构决策、过度工程 | 情境架构决策矩阵 |

---

## 🚀 如何使用

### 对于 AI 代理（LLM 上下文）

#### 阶段 1：认知协议（执行前）
在编写任何代码之前，执行 5 步深度思考。

#### 阶段 2：实施
1. **从 `skill.md` 开始** - 阅读主索引
2. **导航到 `/knowledgeAI/`** - 所有知识文件都在这里
3. **从用户任务中识别关键字**
4. **使用关键字映射** 定位相关文件

#### 阶段 3：记忆协议（执行后）
1. **更新 `architecturehistory.md`** - 记录决策
2. **记录理由** - 引用使用的知识库文件

### 对于开发者

1. **浏览 `skill.md`** 了解可用主题
2. **检查 `/knowledgeAI/` 目录** 查看所有文件
3. **使用关键字搜索** 查找相关部分
4. **在代码审查期间参考** 作为质量检查清单

---

## 📄 许可证

MIT 许可证 - 详情请参见仓库。

---

> **记住：** 目标不是防止所有故障，而是防止在生产环境中重要的故障。
