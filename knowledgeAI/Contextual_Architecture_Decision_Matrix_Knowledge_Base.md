# Contextual Architecture Decision Matrix

> **Knowledge Domain:** Right-Sizing, Overengineering Prevention, Pragmatic Architecture  
> **Purpose:** Prevent overengineering in AI-assisted development  
> **Target:** LLM agents making architecture decisions  
> **Version:** 1.0  

---

## Table of Contents

1. [The Overengineering Trap](#1-the-overengineering-trap)
2. [Right-Sizing Principles](#2-right-sizing-principles)
3. [Decision Framework](#3-decision-framework)
4. [Technology Selection Matrix](#4-technology-selection-matrix)
5. [Anti-Patterns to Avoid](#5-anti-patterns-to-avoid)

---

## 1. The Overengineering Trap

**Keywords:** `overengineering`, `premature-optimization`, `YAGNI`, `complexity`, `AI-generated-code`, `future-proofing`

**Overview:** AI models, trained on enterprise-grade codebases, tend to generate complex solutions for simple problems. This creates "overengineering by default."

**Common AI Overengineering Patterns:**
- Microservices for simple CRUD apps
- Kubernetes for single-container deployments
- GraphQL for simple REST APIs
- Event sourcing for basic state management
- Distributed systems for single-node requirements

**Cost of Overengineering:**
- Increased development time
- Higher maintenance burden
- Steeper learning curve
- Slower iteration cycles
- Technical debt accumulation

---

## 2. Right-Sizing Principles

**Keywords:** `right-sizing`, `pragmatic-architecture`, `evolutionary-design`, `start-simple`, `scale-when-needed`

**Core Principles:**

| Principle | Description |
|-----------|-------------|
| **Start Simple** | Begin with the simplest solution that works |
| **Evolve When Needed** | Add complexity only when justified by requirements |
| **Measure First** | Identify actual bottlenecks before optimizing |
| **YAGNI** | You Aren't Gonna Need It - don't build for hypothetical futures |
| **Optimize for Change** | Design for easy modification, not premature flexibility |

---

## 3. Decision Framework

**Keywords:** `decision-framework`, `contextual-decisions`, `requirement-analysis`, `constraint-evaluation`

### 3.1 The Cynefin Framework for Architecture

**Keywords:** `Cynefin`, `complex-domain`, `complicated-domain`, `clear-domain`, `chaotic-domain`

| Domain | Characteristics | Approach |
|--------|-----------------|----------|
| **Clear** | Cause-effect obvious | Best practices, SOPs |
| **Complicated** | Cause-effect analyzable | Expert analysis, good practices |
| **Complex** | Cause-effect only retrospective | Probe-sense-respond, emergent solutions |
| **Chaotic** | No cause-effect relationship | Act-sense-respond, stabilize first |

### 3.2 Decision Checklist

**Keywords:** `decision-checklist`, `architecture-decision-records`, `ADR`

Before adding complexity, answer:

1. What specific problem does this solve?
2. What is the simplest solution that addresses this problem?
3. What are the trade-offs of simpler alternatives?
4. Is the added complexity justified by the benefit?
5. Can we easily reverse this decision later?
6. What is the cost of being wrong?

---

## 4. Technology Selection Matrix

**Keywords:** `technology-selection`, `fit-for-purpose`, `appropriateness`, `context-aware`

### 4.1 Database Selection

**Keywords:** `database-selection`, `SQL`, `NoSQL`, `PostgreSQL`, `MongoDB`, `SQLite`

| Scenario | Recommended | Avoid |
|----------|-------------|-------|
| Simple CRUD, single user | SQLite | PostgreSQL cluster |
| Relational data, ACID needed | PostgreSQL | Custom distributed DB |
| Document store, flexible schema | MongoDB | Over-normalized SQL |
| High-write, time-series | InfluxDB/TimescaleDB | Generic SQL |
| Cache layer | Redis | Database-as-cache |

### 4.2 Architecture Patterns

**Keywords:** `monolith`, `microservices`, `modular-monolith`, `serverless`

| Team Size | Traffic | Recommended Pattern |
|-----------|---------|---------------------|
| 1-3 devs | Low | Monolith |
| 3-10 devs | Medium | Modular Monolith |
| 10+ devs | High | Microservices |
| Variable/spiky | Any | Serverless functions |

### 4.3 Frontend Framework Selection

**Keywords:** `React`, `Vue`, `Svelte`, `jQuery`, `vanilla-JS`, `framework-selection`

| Complexity | Team Expertise | Recommended |
|------------|----------------|-------------|
| Simple static site | Any | Vanilla JS + HTML |
| Interactive SPA | React experience | React |
| Performance critical | Any | Svelte/Vanilla |
| Rapid prototyping | Vue experience | Vue |
| Legacy maintenance | jQuery | jQuery (don't rewrite) |

---

## 5. Anti-Patterns to Avoid

**Keywords:** `anti-patterns`, `architecture-astronaut`, `gold-plating`, `bike-shedding`

### 5.1 Architecture Astronaut

**Keywords:** `architecture-astronaut`, `abstract-factories`, `enterprise-patterns`, `indirection`

**Symptoms:**
- Multiple layers of abstraction for simple operations
- Abstract factories for object creation
- Interface explosion
- "Enterprise" patterns everywhere

**Solution:**
- Direct code over indirection
- Concrete implementations first
- Abstract only when multiple implementations exist

### 5.2 Gold Plating

**Keywords:** `gold-plating`, `unnecessary-features`, `scope-creep`, `perfectionism`

**Symptoms:**
- Features nobody asked for
- Polish before functionality
- Configurability for every option

**Solution:**
- Ship minimum viable product
- Add features based on user feedback
- Make opinionated choices

### 5.3 Premature Optimization

**Keywords:** `premature-optimization`, `Knuth`, `profile-first`, `micro-optimizations`

**Famous Quote:** "Premature optimization is the root of all evil" - Donald Knuth

**Symptoms:**
- Optimizing without profiling
- Micro-optimizations in non-critical paths
- Complex caching for rarely-accessed data

**Solution:**
- Make it work, then make it fast
- Profile before optimizing
- Focus on algorithmic complexity first

---

## Category Tree Schema

```
1. Overengineering Awareness
   1.1 AI-Generated Complexity
   1.2 Cost of Overengineering

2. Right-Sizing Principles
   2.1 Start Simple
   2.2 Evolve When Needed
   2.3 YAGNI

3. Decision Framework
   3.1 Cynefin Framework
   3.2 Decision Checklist

4. Technology Selection
   4.1 Database Selection
   4.2 Architecture Patterns
   4.3 Frontend Frameworks

5. Anti-Patterns
   5.1 Architecture Astronaut
   5.2 Gold Plating
   5.3 Premature Optimization
```

---

## Quick Decision Guide

| Question | If Yes | If No |
|----------|--------|-------|
| Do you have >10 developers? | Consider microservices | Start with monolith |
| Is traffic >10k RPM? | Add caching/CDN | Optimize later |
| Do you need real-time? | WebSockets/SSE | Polling is fine |
| Is data relational? | PostgreSQL | Consider alternatives |
| Is this MVP? | Ship fast, refactor later | Build for maintainability |
