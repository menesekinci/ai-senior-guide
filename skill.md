---
name: ai-senior-guide
description: Engineering knowledge base for AI-assisted software development
license: MIT
compatibility: opencode
---

# AI Knowledge Skill

> **Production-grade engineering standards for AI-assisted software development**

This skill provides access to a comprehensive engineering knowledge base designed to prevent "silent failures" in AI-generated code. It contains battle-tested architectural patterns, security guidelines, database concurrency best practices, and performance optimization strategies.

**Critical Problem Addressed:** 40-45% of AI-generated code contains silent failures that traditional testing cannot catch.

---

## 🧠 COGNITIVE PROTOCOL (The 5-Step Deep Thinking)

> **Execute BEFORE generating any code or solution**

Before implementing features, you MUST internally process these 5 strategic questions. This transforms you from a "code writer" to a "software architect."

### Step 1: Intent Analysis ("What & Why")
- **Question:** What exactly is the user asking for, and what is the business value?
- **Action:** Identify the core requirement vs. the underlying need
- **Example:** "User needs login" → "Business needs secure identity management"

### Step 2: Future-Proofing ("What's Next")
- **Question:** What features will logically follow this implementation?
- **Action:** Design extensible solutions, avoiding "dead-end" architectures
- **Example:** Login → 2FA → RBAC → Profile Management → Session Management

### Step 3: Standardization ("How to do it Right")
- **Question:** Which industry standards and Knowledge Base files apply here?
- **Action:** Map the request to relevant knowledge files
- **Check:** Anti-patterns in `Contextual_Architecture_Decision_Matrix`

### Step 4: Systemic Impact ("Interactions")
- **Question:** How does this interact with other systems (DB, Cache, Frontend, queues)?
- **Action:** Consider side effects like race conditions, thundering herd, cascading failures
- **Reference:** `Architectural_Resilience` for failure modes

### Step 5: Validation Strategy ("How to Verify")
- **Question:** How will we prove this works beyond happy-path testing?
- **Action:** Plan for observability, logging, edge cases, and property-based testing
- **Consider:** Security vulnerabilities, performance under load, error scenarios

---

## ⚠️ OVERENGINEERING PREVENTION (Right-Sizing Check)

> **CRITICAL WARNING:** Do NOT apply every pattern from the Knowledge Base indiscriminately. A simple Todo app does NOT need microservices, distributed caching, or complex security layers.

### Before Implementing, Ask: "How Much Is Actually Needed?"

**Reference:** `Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

### The "Complexity vs. Need" Assessment

For every feature or pattern you consider applying, evaluate:

| Aspect | Simple Project (MVP) | Production System |
|--------|---------------------|-------------------|
| **Authentication** | Basic JWT | JWT + HttpOnly + Refresh Rotation + 2FA |
| **Database** | SQLite/JSON file | PostgreSQL + Connection Pooling + Read Replicas |
| **Caching** | In-memory Map | Redis Cluster + CDN + Cache Invalidation Strategy |
| **Security** | Basic input validation | CSP + Rate Limiting + WAF + Security Headers |
| **Deployment** | Single container | Kubernetes + Auto-scaling + Circuit Breakers |

### Red Flags for Overengineering

❌ **STOP if you find yourself:**
- Adding Kubernetes for a prototype
- Implementing CQRS for a CRUD app
- Using microservices for < 1000 users
- Adding distributed caching for < 100 RPS
- Implementing event sourcing for simple state
- Creating abstractions "just in case"

### The "YAGNI" Principle (You Ain't Gonna Need It)

**Rule:** If the feature isn't needed RIGHT NOW, don't build it.

**Examples:**
- ❌ "I'll add Redis caching now for when we scale to 1M users"
- ✅ "Simple in-memory cache is enough for current 100 users"
- ❌ "I'll implement full RBAC with 10 permission levels"
- ✅ "Basic admin/user roles are sufficient for MVP"

### Context-Aware Decision Matrix

**Step 1: Assess Project Context**
- Current user count?
- Expected growth timeline?
- Criticality of downtime?
- Team size and expertise?
- Budget constraints?

**Step 2: Match Solution to Context**
```
Startup MVP (0-100 users)     → Monolith + SQLite
Growing Product (1K-10K)      → Monolith + PostgreSQL
Scale-up (10K-100K)          → Modular Monolith + Redis
Enterprise (100K+)           → Microservices + Full Stack
```

**Step 3: Document the Trade-off**
When choosing a simpler solution, document:
- Why simpler approach was chosen
- When to upgrade (triggers)
- Technical debt created
- Migration path for future

### Practical Examples

**Example 1: Todo App**
```
❌ OVER-ENGINEERED:
   - Kubernetes deployment
   - Microservices (AuthService, TodoService, UserService)
   - Redis caching
   - CQRS pattern
   - Event sourcing

✅ RIGHT-SIZED:
   - Single monolithic app
   - SQLite database
   - In-memory session storage
   - Simple REST API
```

**Example 2: E-commerce MVP**
```
❌ OVER-ENGINEERED:
   - Event-driven architecture
   - Distributed transaction saga pattern
   - Multi-region deployment
   - ML-powered recommendation engine

✅ RIGHT-SIZED:
   - Monolithic architecture
   - PostgreSQL database
   - Basic caching
   - Simple collaborative filtering
```

### Decision Checklist

Before adding ANY architectural pattern, verify:

- [ ] **Is this needed NOW?** (Not "might need in future")
- [ ] **Does complexity match project stage?** (MVP vs. Production)
- [ ] **Is team capable of maintaining this?** (Learning curve vs. benefit)
- [ ] **Is the cost justified?** (Time, money, complexity)
- [ ] **Can we start simple and evolve?** (Evolution vs. Big Bang)

### When in Doubt, Start Simple

**Golden Rule:** You can always add complexity later. You cannot easily remove it.

**Prefer:**
- Working simple code over perfect complex code
- Concrete requirements over imagined future needs
- Team understanding over architectural purity
- Ship fast over build perfect

---

## 🤖 SUBAGENT KNOWLEDGE RETRIEVAL PROTOCOL

> **CRITICAL: DO NOT load full KB files into context. Use subagents instead.**

### The Context Window Problem

Knowledge Base files are LARGE (thousands of tokens each). Loading them directly into your context will:
- ❌ **Bloat context window** - Leaves less room for actual coding
- ❌ **Increase token costs** - Expensive and inefficient
- ❌ **Slow down responses** - More tokens = slower processing
- ❌ **Cause truncation** - Important details may be lost

### Solution: Knowledge Retrieval Subagent

**Instead of reading KB files directly, spawn a subagent to do it for you.**

#### When to Use Subagents

**ALWAYS use subagent when:**
- Reading any file from `knowledgeAI/` directory
- Need specific section from large KB file
- Context window is already >50% full
- Multiple KB files need to be referenced

**NEVER read directly when:**
- File is >1000 tokens
- Multiple files needed
- Context is constrained

#### Subagent Task Template

```
@general
Task: Read and summarize relevant sections from Knowledge Base

Files to check:
- knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md
- knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md

Keywords from user request: "JWT", "token storage", "frontend"

Instructions:
1. Search for relevant sections matching keywords
2. Extract ONLY the specific patterns/anti-patterns
3. Return concise summary (max 500 tokens):
   - Key patterns to apply
   - Critical anti-patterns to avoid
   - Code examples if relevant
   - Specific file sections for reference

DO NOT return full file content. Only relevant extracts.
```

#### Example Workflow

**❌ WRONG (Context Bloat):**
```
User: "How should I store JWT tokens?"
AI: [Reads entire Client_Side_Security_Architecture_Knowledge_Base.md - 5000 tokens]
    [Context now 70% full]
    [Less room for actual solution]
```

**✅ RIGHT (Subagent Pattern):**
```
User: "How should I store JWT tokens?"
AI: [Spawns subagent with specific task]
    Subagent: [Reads KB, extracts JWT section only - 300 tokens]
    Subagent returns: "Use HttpOnly cookies. Avoid localStorage due to XSS."
    AI: [Uses 300 token summary to generate solution]
    [Context stays clean, efficient, fast]
```

#### Subagent Output Format

Subagent should return:
```markdown
## Relevant Patterns
- [Pattern name]: [One-line description]
- [Pattern name]: [One-line description]

## Anti-Patterns to Avoid
- [Anti-pattern]: [Why it's bad]

## Quick Reference
- File: [KB filename]
- Section: [Specific section/heading]
- Key Takeaway: [One-line actionable advice]
```

#### Token Budget Rules

- **Subagent task description:** Max 200 tokens
- **Subagent return summary:** Max 500 tokens
- **Your context after subagent:** Should be <60% full
- **Multiple KB files:** Spawn multiple subagents in parallel, not sequentially

### Context Management Checklist

Before reading ANY file:
- [ ] Check current context usage
- [ ] If >50% full → Use subagent
- [ ] If file >1000 tokens → Use subagent
- [ ] If multiple files needed → Use subagent
- [ ] Keep summaries, not full text

### Benefits of Subagent Pattern

✅ **Efficient context usage** - Only relevant info in main context
✅ **Faster responses** - Less token processing
✅ **Cost effective** - Minimal token waste
✅ **Parallel processing** - Multiple subagents can work simultaneously
✅ **Clean architecture** - Separation of concerns

---

## 💾 MEMORY PROTOCOL (Architecture Decision Records)

> **Execute AFTER implementing any significant feature**

After implementing features, you MUST maintain persistent memory of architectural decisions. **CRITICAL: Keep entries CONCISE to avoid token bloat.**

### ⚠️ TOKEN OPTIMIZATION RULE

**Memory entries must be SHORT and SCANNABLE:**
- **Max 2-3 lines per field**
- **Use bullet points, not paragraphs**
- **Reference KB files by name only** (don't copy content)
- **Focus on DECISION + RATIONALE only**

**❌ BAD (Too verbose):**
```markdown
## [2026-02-01] Auth System
- **Goal:** User wanted login system with high security and good performance...
- **Decision:** Implemented JWT with HttpOnly cookies following OWASP guidelines...
- **Rationale:** According to Client_Side_Security_Architecture.md section 3.2...
```

**✅ GOOD (Token-efficient):**
```markdown
## Auth: JWT + HttpOnly Cookies
Why: XSS protection (ref: Client_Side_Security)
Deps: UserDB, Redis
Risk: Rate limit strict
```

### Ultra-Compact Template

Create `architecturehistory.md` in project root:

```markdown
## [Feature]: [Decision]
Why: [One-line rationale] (ref: KB_File)
Deps: [Component list]
Risk: [One-line debt/risk]
```

### What to Log (Keep it SHORT)
1. **Feature:Decision** - Brief identifier
2. **Why** - One-line rationale + KB reference
3. **Deps** - Component names only
4. **Risk** - Known limitation (optional)

### Token Budget per Entry
- **Maximum 100 tokens per entry**
- **Maximum 50 entries per file**
- **If file grows large → Archive old entries to `architecturehistory.archive.md`**

### Why Minimal Memory Matters
- **Fast context loading** - Less token burn on file read
- **Quick scanning** - Find relevant decisions instantly
- **Cross-session persistence** - Survives context resets
- **Human-readable** - Developers can understand at a glance

---

## 📚 Knowledge Base Structure

This skill references 8 comprehensive knowledge base files located in the `knowledgeAI/` directory:

### 1. AI Guardrail Architecture
**Scope:** Distributed systems, security architecture, microservices  
**Keywords:** `distributed-systems`, `consistency`, `consensus`, `resilience`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

**Key Topics:**
- Core Distributed Systems Architecture (Consistency, Consensus, Resilience)
- Event-Driven Architecture & Async Patterns
- Database Engineering & Evolution
- Site Reliability Engineering (SRE) & Observability
- Security & Compliance Architecture
- Infrastructure as Code (IaC) & FinOps

---

### 2. Architectural Resilience in High-Integrity Systems
**Scope:** Reliability patterns, observability, chaos engineering  
**Keywords:** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`

**Key Topics:**
- Observability Data Plane (Tracing, Metrics Hierarchy, Structured Logging)
- Property-Based Testing & Chaos Engineering
- High-Scale Data Access and Caching
- Asynchronous Architecture and Event Reliability
- Traffic Control and Rate Limiting
- Infrastructure as Code Security

---

### 3. Client-Side Security Architecture
**Scope:** Web security, XSS prevention, token storage  
**Keywords:** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`

**Key Topics:**
- Modern Client-Side Threat Landscape (Mutation XSS, Magecart)
- Content Security Policy (Strict CSP, Nonce-Based Architecture)
- Secure Storage Patterns for Authentication Tokens
- HTML Sanitization and XSS Prevention
- Supply Chain Risk Mitigation

---

### 4. Comprehensive Architectural Framework
**Scope:** Database concurrency, ORM performance, security anomalies  
**Keywords:** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

**Key Topics:**
- Database Concurrency and Transactional Integrity
- The N+1 Query Problem and ORM Performance
- Distributed Locking and Coordination (Redlock, Fencing Tokens)
- Frontend State Management and Security
- API Security and Access Control

---

### 5. Contextual Architecture Decision Matrix
**Scope:** Overengineering prevention, technology selection  
**Keywords:** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `microservices`, `monolith`

**Key Topics:**
- The Overengineering Trap Recognition
- Right-Sizing Principles
- Decision Framework (Cynefin Framework, Decision Checklist)
- Technology Selection Matrix
- Architecture Decision Records (ADR)
- Anti-Patterns to Avoid

---

### 6. Defensive UI Engineering
**Scope:** Resilient UI patterns, error handling  
**Keywords:** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`

**Key Topics:**
- Resilient UI Architecture (Error Boundaries)
- Error Handling Patterns (Network Errors, User-Facing Messages)
- Loading and Skeleton States
- Optimistic UI with Rollback
- Accessibility in Error States

---

### 7. End-to-End Type Safety
**Scope:** TypeScript, schema validation, runtime validation  
**Keywords:** `type-safety`, `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`

**Key Topics:**
- Type Safety Spectrum (Compile-time to Runtime)
- Schema Sharing Strategies (Monorepo, OpenAPI, tRPC)
- Runtime Validation (Zod Patterns, Type Guards)
- Contract Testing (Pact Implementation)
- Type-Safe API Clients

---

### 8. Modern Web Performance Engineering
**Scope:** Core Web Vitals, bundle optimization, rendering patterns  
**Keywords:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

**Key Topics:**
- Core Web Vitals Optimization (LCP, FID, CLS, INP)
- Bundle Analysis and Optimization
- Tree-Shaking Strategies
- Loading Strategies (Code Splitting, Resource Hints)
- Rendering Patterns (SSR, SSG, CSR, Hydration)

---

## 🔍 Quick Reference: Keyword Mapping

Use this table to quickly identify which knowledge base to reference:

| Topic Area | Knowledge Base File | Key Keywords |
|------------|-------------------|--------------|
| API Design, REST, gRPC, GraphQL | AI Guardrail Architecture | `REST`, `gRPC`, `GraphQL`, `idempotency` |
| Database Transactions, Concurrency | Comprehensive Architectural Framework | `ACID`, `isolation-levels`, `N-plus-1` |
| Web Security, XSS, CSP, JWT | Client-Side Security Architecture | `XSS`, `CSP`, `JWT-storage`, `BFF-pattern` |
| Monitoring, Tracing, Observability | Architectural Resilience | `OpenTelemetry`, `distributed-tracing`, `SRE` |
| Performance, Bundling, Core Web Vitals | Modern Web Performance Engineering | `LCP`, `CLS`, `tree-shaking`, `SSR` |
| TypeScript, Validation, Schema | End-to-End Type Safety | `Zod`, `tRPC`, `runtime-validation` |
| Error Handling, UI Resilience | Defensive UI Engineering | `error-boundaries`, `optimistic-UI` |
| Architecture Decisions | Contextual Architecture Decision Matrix | `ADR`, `overengineering`, `Cynefin` |

---

## 🏗️ Cross-Cutting Concerns

Many topics span multiple knowledge bases. Reference them together for comprehensive coverage:

| Concern | Primary Knowledge Base | Secondary Knowledge Bases |
|---------|----------------------|--------------------------|
| **Security** | Client-Side Security Architecture | AI Guardrail Architecture, Comprehensive Framework |
| **Performance** | Modern Web Performance Engineering | Architectural Resilience |
| **Reliability** | Architectural Resilience | AI Guardrail Architecture, Defensive UI Engineering |
| **Type Safety** | End-to-End Type Safety | Comprehensive Architectural Framework |

---

## 💡 How to Use This Skill

### When Implementing Features:

1. **Identify keywords** from the user's request or task description
2. **Match keywords** to the appropriate knowledge base using the Quick Reference table
3. **Reference the relevant sections** to understand best practices and anti-patterns
4. **Apply the guidelines** to ensure production-grade code quality
5. **Check cross-cutting concerns** for related patterns

### When Reviewing Code:

1. Scan code for potential issues matching knowledge base topics
2. Reference relevant sections for validation
3. Identify anti-patterns and suggest improvements
4. Ensure security, performance, and reliability standards

---

## 🎯 Core Principles

### The Silent Failure Problem

AI-generated code often contains issues that **pass tests but fail in production**:

- ✅ **What Testing Catches:** Syntax errors, runtime exceptions, failing assertions
- ❌ **What Testing Misses:** 
  - Race conditions and concurrency anomalies
  - Subtle security vulnerabilities (XSS variants, BOLA attacks)
  - Performance degradation (N+1 queries, thundering herd)
  - Architectural anti-patterns
  - Resilience failure modes

### Guardrail Philosophy

This knowledge base acts as **guardrails**, not rigid rules:

- **Context-aware:** Right-sizing over overengineering
- **Evidence-based:** Grounded in real production failures
- **AI-optimized:** Structured for efficient LLM context usage
- **Pragmatic:** Provides patterns, not mandates

---

## 📁 File Naming Convention

All knowledge base files follow the pattern:
```
{Descriptive_Name}_Knowledge_Base.md
```

This enables:
- Easy identification of topics
- Programmatic access
- Consistent organization

---

## 🔗 Integration with Opencode

This skill automatically activates when the user mentions relevant keywords in their requests. The knowledge base provides:

- **Proactive guidance** during code generation
- **Quality validation** during code review
- **Best practice enforcement** for production readiness
- **Cross-reference suggestions** for comprehensive solutions

---

## 📖 Example Usage

### Example 1: Database Concurrency
```
User: "Add a transaction to transfer funds between accounts"

Skill Action:
1. Detect keywords: "transaction", "database"
2. Reference: Comprehensive Architectural Framework
3. Apply: Isolation levels, deadlock prevention, ACID compliance
4. Cross-check: AI Guardrail Architecture for distributed patterns
```

### Example 2: API Security
```
User: "Store JWT tokens in the frontend"

Skill Action:
1. Detect keywords: "JWT", "token", "frontend"
2. Reference: Client-Side Security Architecture
3. Apply: Secure storage patterns, HttpOnly cookies, BFF pattern
4. Warn: localStorage risks, in-memory storage alternatives
```

### Example 3: Type Safety
```
User: "Validate API response data"

Skill Action:
1. Detect keywords: "validate", "API", "TypeScript"
2. Reference: End-to-End Type Safety
3. Apply: Zod runtime validation, type guards
4. Suggest: Schema sharing between frontend and backend
```

---

## 🎓 Target Audience

- **AI Coding Assistants:** Claude, GPT-4, Copilot, etc.
- **Senior Engineers:** Architecture review reference
- **Mid-level Developers:** Learning advanced patterns
- **Tech Leads:** Team standards and guidelines

---

## 🙏 Sources

This knowledge base synthesizes:
- Production incident post-mortems
- Industry best practices (Google SRE, OWASP, W3C)
- Academic distributed systems research
- Real-world AI coding assistant failure modes

---

> **Remember:** The goal is not to prevent all failures, but to prevent the failures that matter in production.
