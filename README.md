# AI Knowledge Skill

[![GitHub](https://img.shields.io/github/license/menesekinci/ai-knowledge-skill)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/menesekinci/ai-knowledge-skill)](https://github.com/menesekinci/ai-knowledge-skill/stargazers)

> **Production-grade engineering standards for AI-assisted software development**

A comprehensive skill designed for LLM agents to prevent "silent failures" in AI-generated code through battle-tested architectural patterns, security guidelines, and best practices.

---

## 🎯 What is This?

**AI Knowledge Skill** is a structured knowledge base that AI coding assistants can reference to generate production-ready code. It addresses the critical gap where **40-45% of AI-generated code contains silent failures** - issues that pass tests but fail in production.

### The Silent Failure Problem

| What Testing Catches ✅ | What Testing Misses ❌ |
|------------------------|------------------------|
| Syntax errors | Race conditions |
| Runtime exceptions | Subtle security holes |
| Failing assertions | Performance degradation |
| | Architectural anti-patterns |
| | Concurrency anomalies |

### 🧠 Cognitive + Memory Protocol

This skill implements a revolutionary two-phase approach:

**Phase 1: Cognitive Protocol (Pre-Execution)**
AI thinks deeply before coding using the 5-Step Deep Thinking process:
1. Intent Analysis (What & Why)
2. Future-Proofing (What's Next)  
3. Standardization (How to do it Right)
4. Systemic Impact (Interactions)
5. Validation Strategy (How to Verify)

**Phase 2: Memory Protocol (Post-Execution)**  
AI maintains persistent memory via `architecturehistory.md`:
- Architecture Decision Records (ADR)
- Component dependencies
- Design rationale with Knowledge Base references
- Known technical debt

**Result:** AI transforms from a "code writer" to a "software architect" with institutional memory.

### ⚠️ Overengineering Prevention

**Critical:** This skill also prevents the opposite problem - **overengineering**. AI agents must ask "How much is actually needed?" before applying patterns.

**Reference:** `Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Examples:**
- ❌ Todo app with Kubernetes + Microservices
- ✅ Todo app with Monolith + SQLite

**The YAGNI Principle:** If it's not needed RIGHT NOW, don't build it.

---

## 🗃️ Project Memory: architecturehistory.md

Each project using this skill should maintain an `architecturehistory.md` file in the project root. This serves as the AI's "memory" across sessions.

### Template

```markdown
## [YYYY-MM-DD HH:MM] Change: [Feature Name]
- **Goal:** [What was implemented]
- **Decision:** [Chosen architecture]
- **Rationale:** [Why, with KB references]
- **Dependencies:** [Related components]
- **Risks/Debt:** [Known limitations]
```

### Example Entry

```markdown
## [2026-02-01 14:30] Change: Authentication System
- **Goal:** Implement secure login with session management
- **Decision:** JWT with HttpOnly Cookies + Redis Rate Limiting
- **Rationale:** Client_Side_Security_Architecture.md warns against localStorage XSS risks
- **Dependencies:** UserDB, Redis, AuthService API
- **Risks/Debt:** Strict rate limiting may need adjustment for high-traffic scenarios
```

---

---

## 📖 Start Here: skill.md

**`skill.md` is the primary entry point and index for this knowledge base.**

This file serves as:
- **Master index** of all 8 knowledge base files
- **Keyword directory** for quick topic lookup
- **Cross-reference guide** for related concepts
- **Usage instructions** for AI agents

**AI Agents:** Always begin by reading `skill.md` to understand the knowledge base structure and locate relevant files based on keywords.

---

## 🗂️ Repository Structure

```
ai-knowledge-skill/
├── skill.md                                    # ⭐ START HERE - Master index + Protocols
├── knowledgeAI/                                # Knowledge base directory
│   ├── AI_Guardrail_Architecture_Knowledge_Base.md
│   ├── Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md
│   ├── Client_Side_Security_Architecture_Knowledge_Base.md
│   ├── Comprehensive_Architectural_Framework_Knowledge_Base.md
│   ├── Contextual_Architecture_Decision_Matrix_Knowledge_Base.md
│   ├── Defensive_UI_Engineering_Knowledge_Base.md
│   ├── End_to_End_Type_Safety_Knowledge_Base.md
│   └── Modern_Web_Performance_Engineering_Knowledge_Base.md
├── README.md                                   # This file
└── architecturehistory.md                      # 🧠 Project memory (per project)
```

**Note:** `architecturehistory.md` should be created in each project using this skill to maintain AI's persistent memory across sessions.

All knowledge files follow the naming convention: `{Descriptive_Name}_Knowledge_Base.md`

---

## 📚 Available Knowledge Files

### 1. AI Guardrail Architecture
**File:** `/knowledgeAI/AI_Guardrail_Architecture_Knowledge_Base.md`

**Comprehensive distributed systems and security architecture**

**Keywords:** `distributed-systems`, `consistency`, `consensus`, `resilience`, `fault-tolerance`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

- Distributed Systems Architecture (Consistency, Consensus)
- Event-Driven Architecture & Async Patterns
- Database Engineering & Evolution
- Site Reliability Engineering (SRE) & Observability
- Security & Compliance Architecture

---

### 2. Architectural Resilience in High-Integrity Systems
**File:** `/knowledgeAI/Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md`

**Advanced reliability patterns for production workloads**

**Keywords:** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`, `kubernetes-hardening`

- Observability Data Plane & Tracing
- Property-Based Testing & Chaos Engineering
- High-Scale Caching Strategies
- Asynchronous Event Reliability
- Infrastructure as Code Security

---

### 3. Client-Side Security Architecture
**File:** `/knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md`

**Modern web application security fundamentals**

**Keywords:** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`, `SRI`

- Modern Threat Landscape (Mutation XSS, Magecart)
- Strict Content Security Policy Implementation
- Secure Token Storage Patterns
- HTML Sanitization & XSS Prevention
- Supply Chain Risk Mitigation

---

### 4. Comprehensive Architectural Framework
**File:** `/knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md`

**Database concurrency, performance, and security fundamentals**

**Keywords:** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

- Database Concurrency & Transactional Integrity
- The N+1 Query Problem & ORM Performance
- Distributed Locking (Redlock, Fencing Tokens)
- Frontend State Management Security
- API Security & Access Control

---

### 5. Contextual Architecture Decision Matrix
**File:** `/knowledgeAI/Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Avoiding overengineering and right-sizing solutions**

**Keywords:** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `monolith`, `microservices`, `architecture-astronaut`

- The Overengineering Trap Recognition
- Right-Sizing Principles
- Cynefin Framework for Technology Selection
- Architecture Decision Records (ADR)
- Anti-Patterns to Avoid

---

### 6. Defensive UI Engineering
**File:** `/knowledgeAI/Defensive_UI_Engineering_Knowledge_Base.md`

**Resilient user interface patterns**

**Keywords:** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`, `focus-management`

- React Error Boundaries & Resilient Architecture
- Network Error Handling Patterns
- Loading States & Skeleton Screens
- Optimistic UI with Rollback Strategies
- Accessibility in Error States

---

### 7. End-to-End Type Safety
**File:** `/knowledgeAI/End_to_End_Type_Safety_Knowledge_Base.md`

**Type-safe full-stack JavaScript development**

**Keywords:** `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`, `Pact`, `RTK-Query`

- Type Safety Spectrum (Compile-time to Runtime)
- Schema Sharing Strategies (Monorepo, OpenAPI, tRPC)
- Runtime Validation with Zod
- Contract Testing with Pact
- Type-Safe API Clients

---

### 8. Modern Web Performance Engineering
**File:** `/knowledgeAI/Modern_Web_Performance_Engineering_Knowledge_Base.md`

**Core Web Vitals and optimization strategies**

**Keywords:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

- Core Web Vitals Optimization (LCP, FID, CLS, INP)
- Bundle Analysis & Tree-Shaking
- Loading Strategies (Prefetch, Preload)
- Rendering Patterns (SSR, SSG, CSR)
- Performance Budgets

---

## 🔍 Quick Reference: Keyword Mapping

| If You're Working On... | Read This File |
|------------------------|----------------|
| API design, REST, gRPC, GraphQL | AI Guardrail Architecture |
| Database, transactions, concurrency | Comprehensive Architectural Framework |
| CSP, XSS, secure storage, JWT | Client-Side Security Architecture |
| Monitoring, tracing, observability | Architectural Resilience |
| Performance, bundle, Core Web Vitals | Modern Web Performance Engineering |
| Type safety, validation, schema | End-to-End Type Safety |
| Error handling, loading states | Defensive UI Engineering |
| Architecture decisions, overengineering | Contextual Architecture Decision Matrix |

---

## 🚀 How to Use

### For AI Agents (LLM Context)

#### Step 1: Cognitive Protocol (Pre-Execution)
Before writing any code, execute the 5-Step Deep Thinking:

1. **Intent Analysis** - Understand what & why
2. **Future-Proofing** - Plan for extensibility  
3. **Standardization** - Map to Knowledge Base files
4. **Systemic Impact** - Consider interactions
5. **Validation Strategy** - Plan verification

#### Step 2: Implementation
1. **Start with `skill.md`** - Read the master index
2. **Navigate to `/knowledgeAI/`** - All knowledge files are here
3. **Identify keywords** from the user's task
4. **Use keyword mapping** in `skill.md` to locate relevant files
5. **Reference cross-cutting concerns** for related topics
6. **Apply patterns** to prevent silent failures

#### Step 3: Memory Protocol (Post-Execution)
1. **Update `architecturehistory.md`** - Log the decision
2. **Document rationale** - Reference Knowledge Base files used
3. **Map dependencies** - List interacting components
4. **Note risks** - Known limitations or future debt

### For Developers

1. **Browse `skill.md`** to understand available topics
2. **Check `/knowledgeAI/`** directory for all files
3. **Use keyword search** to find relevant sections
4. **Reference during code reviews** as a quality checklist
5. **Study patterns** to deepen architectural knowledge
6. **Maintain `architecturehistory.md`** for project context

---

## 🏗️ Cross-Cutting Concerns

Topics spanning multiple knowledge files:

| Concern | Primary File | Also See |
|---------|-------------|----------|
| **Security** | Client-Side Security | AI Guardrail, Comprehensive Framework |
| **Performance** | Modern Web Performance | Architectural Resilience |
| **Reliability** | Architectural Resilience | AI Guardrail, Defensive UI |
| **Type Safety** | End-to-End Type Safety | Comprehensive Framework |

---

## 💡 Design Principles

### Guardrail Philosophy

These knowledge files act as **guardrails** - not rigid rules, but guidance:

- **Context-aware:** Right-sizing over overengineering
- **Evidence-based:** Grounded in production failures
- **AI-optimized:** Structured for LLM context efficiency
- **Pragmatic:** Patterns, not mandates

### Target Audience

- **AI Coding Assistants:** Claude, GPT-4, Copilot, etc.
- **Senior Engineers:** Architecture review reference
- **Mid-level Developers:** Learning advanced patterns
- **Tech Leads:** Team standards and guidelines

---

## 🤝 Contributing

This knowledge base represents collective learnings from production systems:

- **New patterns** with real-world examples
- **Updated practices** as technologies evolve
- **Additional keywords** for better discoverability
- **Cross-references** between related topics

---

## 📄 License

MIT License - See repository for details.

---

## 🙏 Acknowledgments

Synthesized from:
- Production incident post-mortems
- Industry best practices (Google SRE, OWASP, W3C)
- Academic distributed systems research
- Real-world AI coding assistant failure modes

---

> **Remember:** The goal is not to prevent all failures, but to prevent the failures that matter in production.
