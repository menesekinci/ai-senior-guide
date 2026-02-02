# AI Guida Senior

[![GitHub](https://img.shields.io/github/license/menesekinci/ai-senior-guide)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/menesekinci/ai-senior-guide)](https://github.com/menesekinci/ai-senior-guide/stargazers)

> **Standard di ingegneria di livello produzione per lo sviluppo software assistito da AI**

Una guida completa progettata per prevenire "fallimenti silenziosi" nel codice generato da AI attraverso pattern architetturali collaudati, linee guida sulla sicurezza e best practice.

---

## 🎯 Cos'è Questo?

**AI Guida Senior** è una base di conoscenza strutturata che gli assistenti di codifica AI possono consultare per generare codice pronto per la produzione. Affronta il divario critico dove il **40-45% del codice generato da AI contiene fallimenti silenziosi** - problemi che superano i test ma falliscono in produzione.

### Il Problema dei Fallimenti Silenziosi

| Cosa i Test Catturano ✅ | Cosa i Test Mancano ❌ |
|-------------------------|------------------------|
| Errori di sintassi | Race condition |
| Eccezioni runtime | Vulnerabilità di sicurezza sottili |
| Asserzioni fallite | Degradamento delle prestazioni |
| | Anti-pattern architetturali |
| | Anomalie di concorrenza |

### 🧠 Protocollo Cognitivo + Memoria

Questa guida implementa un approccio rivoluzionario in due fasi:

**Fase 1: Protocollo Cognitivo (Pre-Esecuzione)**
L'AI pensa profondamente prima di codificare utilizzando il processo di Pensiero Profondo in 5 Fasi.

**Fase 2: Protocollo Memoria (Post-Esecuzione)**
L'AI mantiene memoria persistente tramite `architecturehistory.md`.

**Risultato:** L'AI si trasforma da "scrittore di codice" a "architetto software" con memoria istituzionale.

### ⚠️ Prevenzione del Sovra-ingegnerizzazione

**Critico:** Questa guida previene anche il problema opposto - **il sovra-ingegnerizzazione**. Gli agenti AI devono chiedere "Quanto è realmente necessario?" prima di applicare i pattern.

---

## 🗃️ Memoria del Progetto: architecturehistory.md

Ogni progetto che utilizza questa guida dovrebbe mantenere un file `architecturehistory.md` nella root del progetto. Questo serve come "memoria" dell'AI tra le sessioni.

### Template

```markdown
## [AAAA-MM-GG HH:MM] Modifica: [Nome Funzionalità]
- **Obiettivo:** [Cosa è stato implementato]
- **Decisione:** [Architettura scelta]
- **Razionale:** [Perché, con riferimenti KB]
- **Dipendenze:** [Componenti correlati]
- **Rischi/Debito:** [Limitazioni note]
```

---

## 📖 Inizia Qui: skill.md

**`skill.md` è il punto di ingresso principale e l'indice di questa base di conoscenza.**

Questo file serve come:
- **Indice principale** di tutti i 8 file della base di conoscenza
- **Directory delle parole chiave** per la ricerca rapida degli argomenti
- **Guida di riferimento incrociato** per concetti correlati
- **Istruzioni d'uso** per gli agenti AI

---

## 🗂️ Struttura del Repository

```
ai-senior-guide/
├── skill.md                                    # ⭐ INIZIA QUI - Indice principale
├── knowledgeAI/                                # Directory base di conoscenza
│   ├── AI_Guardrail_Architecture_Knowledge_Base.md
│   ├── Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md
│   ├── Client_Side_Security_Architecture_Knowledge_Base.md
│   ├── Comprehensive_Architectural_Framework_Knowledge_Base.md
│   ├── Contextual_Architecture_Decision_Matrix_Knowledge_Base.md
│   ├── Defensive_UI_Engineering_Knowledge_Base.md
│   ├── End_to_End_Type_Safety_Knowledge_Base.md
│   └── Modern_Web_Performance_Engineering_Knowledge_Base.md
├── README.md                                   # Questo file
└── architecturehistory.md                      # 🧠 Memoria progetto
```

---

## 📚 File di Conoscenza Disponibili

### 1. Architettura AI Guardrail
**File:** `/knowledgeAI/AI_Guardrail_Architecture_Knowledge_Base.md`

**Sistemi distribuiti completi e architettura di sicurezza**

**Parole chiave:** `distributed-systems`, `consistency`, `consensus`, `resilience`, `fault-tolerance`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

---

### 2. Resilienza Architetturale in Sistemi ad Alta Integrità
**File:** `/knowledgeAI/Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md`

**Pattern avanzati di affidabilità per carichi di lavoro di produzione**

**Parole chiave:** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`, `kubernetes-hardening`

---

### 3. Architettura di Sicurezza Lato Client
**File:** `/knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md`

**Fondamenti di sicurezza delle applicazioni web moderne**

**Parole chiave:** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`, `SRI`

---

### 4. Framework Architetturale Completo
**File:** `/knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md`

**Concorrenza del database, prestazioni e fondamenti di sicurezza**

**Parole chiave:** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

---

### 5. Matrice di Decisione Architetturale Contestuale
**File:** `/knowledgeAI/Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Evitare il sovra-ingegnerizzazione e dimensionare correttamente le soluzioni**

**Parole chiave:** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `monolith`, `microservices`, `architecture-astronaut`

---

### 6. Ingegneria UI Difensiva
**File:** `/knowledgeAI/Defensive_UI_Engineering_Knowledge_Base.md`

**Pattern di interfaccia utente resilienti**

**Parole chiave:** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`, `focus-management`

---

### 7. Type Safety End-to-End
**File:** `/knowledgeAI/End_to_End_Type_Safety_Knowledge_Base.md`

**Sviluppo JavaScript full-stack type-safe**

**Parole chiave:** `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`, `Pact`, `RTK-Query`

---

### 8. Ingegneria delle Prestazioni Web Moderne
**File:** `/knowledgeAI/Modern_Web_Performance_Engineering_Knowledge_Base.md`

**Core Web Vitals e strategie di ottimizzazione**

**Parole chiave:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

---

## 🔍 Riferimento Rapido: Mappatura Parole Chiave

| Argomento | Leggi Questo File |
|-----------|-------------------|
| Progettazione API, REST, gRPC, GraphQL | Architettura AI Guardrail |
| Database, transazioni, concorrenza | Framework Architetturale Completo |
| CSP, XSS, archiviazione sicura, JWT | Architettura di Sicurezza Lato Client |
| Monitoraggio, tracciamento, osservabilità | Resilienza Architetturale |
| Prestazioni, bundle, Core Web Vitals | Ingegneria delle Prestazioni Web |
| Type safety, validazione, schema | Type Safety End-to-End |
| Gestione errori, stati di caricamento | Ingegneria UI Difensiva |
| Decisioni architetturali, sovra-ingegnerizzazione | Matrice di Decisione Contestuale |

---

## 🚀 Come Usare

### Per Agenti AI (Contesto LLM)

#### Fase 1: Protocollo Cognitivo (Pre-Esecuzione)
Prima di scrivere qualsiasi codice, esegui il Pensiero Profondo in 5 Fasi.

#### Fase 2: Implementazione
1. **Inizia con `skill.md`** - Leggi l'indice principale
2. **Naviga in `/knowledgeAI/`** - Tutti i file di conoscenza sono qui
3. **Identifica parole chiave** dal compito dell'utente
4. **Usa la mappatura parole chiave** per localizzare i file pertinenti

#### Fase 3: Protocollo Memoria (Post-Esecuzione)
1. **Aggiorna `architecturehistory.md`** - Registra la decisione
2. **Documenta il razionale** - Riferisci i file della Knowledge Base utilizzati

### Per Sviluppatori

1. **Sfoglia `skill.md`** per comprendere gli argomenti disponibili
2. **Controlla la directory `/knowledgeAI/`** per tutti i file
3. **Usa la ricerca per parole chiave** per trovare sezioni pertinenti
4. **Fai riferimento durante le revisioni del codice** come checklist di qualità

---

## 📄 Licenza

Licenza MIT - Vedi il repository per i dettagli.

---

> **Ricorda:** L'obiettivo non è prevenire tutti i fallimenti, ma prevenire i fallimenti che contano in produzione.
