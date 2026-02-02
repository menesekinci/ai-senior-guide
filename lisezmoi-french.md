# AI Guide Senior

[![GitHub](https://img.shields.io/github/license/menesekinci/ai-senior-guide)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/menesekinci/ai-senior-guide)](https://github.com/menesekinci/ai-senior-guide/stargazers)

> **Standards d'ingénierie de niveau production pour le développement logiciel assisté par IA**

Un guide complet conçu pour prévenir les "échecs silencieux" dans le code généré par l'IA grâce à des patterns architecturaux éprouvés, des directives de sécurité et des meilleures pratiques.

---

## 🎯 Qu'est-ce Que C'est?

**AI Guide Senior** est une base de connaissances structurée que les assistants de codage IA peuvent consulter pour générer du code prêt pour la production. Il aborde le fossé critique où **40-45% du code généré par l'IA contient des échecs silencieux** - des problèmes qui passent les tests mais échouent en production.

### Le Problème des Échecs Silencieux

| Ce Que les Tests Capturent ✅ | Ce Que les Tests Manquent ❌ |
|------------------------------|------------------------------|
| Erreurs de syntaxe | Conditions de course |
| Exceptions d'exécution | Failles de sécurité subtiles |
| Assertions échouées | Dégradation des performances |
| | Anti-patterns architecturaux |
| | Anomalies de concurrence |

### 🧠 Protocole Cognitif + Mémoire

Ce guide met en œuvre une approche révolutionnaire en deux phases:

**Phase 1: Protocole Cognitif (Pré-Exécution)**
L'IA réfléchit en profondeur avant de coder en utilisant le processus de Réflexion Profonde en 5 Étapes.

**Phase 2: Protocole Mémoire (Post-Exécution)**
L'IA maintient une mémoire persistante via `architecturehistory.md`.

**Résultat:** L'IA se transforme d'"écrivain de code" en "architecte logiciel" avec une mémoire institutionnelle.

### ⚠️ Prévention de la Sur-ingénierie

**Critique:** Ce guide prévient également le problème opposé - **la sur-ingénierie**. Les agents IA doivent se demander "Combien est réellement nécessaire?" avant d'appliquer des patterns.

---

## 🗃️ Mémoire du Projet: architecturehistory.md

Chaque projet utilisant ce guide devrait maintenir un fichier `architecturehistory.md` à la racine du projet. Cela sert de "mémoire" de l'IA entre les sessions.

### Template

```markdown
## [AAAA-MM-JJ HH:MM] Changement: [Nom de la Fonctionnalité]
- **Objectif:** [Ce qui a été implémenté]
- **Décision:** [Architecture choisie]
- **Justification:** [Pourquoi, avec références KB]
- **Dépendances:** [Composants liés]
- **Risques/Dette:** [Limitations connues]
```

---

## 📖 Commencez Ici: skill.md

**`skill.md` est le point d'entrée principal et l'index de cette base de connaissances.**

Ce fichier sert de:
- **Index principal** des 8 fichiers de la base de connaissances
- **Répertoire de mots-clés** pour la recherche rapide de sujets
- **Guide de référence croisée** pour les concepts connexes
- **Instructions d'utilisation** pour les agents IA

---

## 🗂️ Structure du Dépôt

```
ai-senior-guide/
├── skill.md                                    # ⭐ COMMENCEZ ICI - Index principal
├── knowledgeAI/                                # Répertoire base de connaissances
│   ├── AI_Guardrail_Architecture_Knowledge_Base.md
│   ├── Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md
│   ├── Client_Side_Security_Architecture_Knowledge_Base.md
│   ├── Comprehensive_Architectural_Framework_Knowledge_Base.md
│   ├── Contextual_Architecture_Decision_Matrix_Knowledge_Base.md
│   ├── Defensive_UI_Engineering_Knowledge_Base.md
│   ├── End_to_End_Type_Safety_Knowledge_Base.md
│   └── Modern_Web_Performance_Engineering_Knowledge_Base.md
├── README.md                                   # Ce fichier
└── architecturehistory.md                      # 🧠 Mémoire du projet
```

---

## 📚 Fichiers de Connaissance Disponibles

### 1. Architecture AI Guardrail
**Fichier:** `/knowledgeAI/AI_Guardrail_Architecture_Knowledge_Base.md`

**Systèmes distribués complets et architecture de sécurité**

**Mots-clés:** `distributed-systems`, `consistency`, `consensus`, `resilience`, `fault-tolerance`, `microservices`, `CAP-theorem`, `circuit-breaker`, `event-driven`, `SRE`, `observability`, `zero-trust`

---

### 2. Résilience Architecturale dans les Systèmes à Haute Intégrité
**Fichier:** `/knowledgeAI/Architectural_Resilience_High_Integrity_Systems_Knowledge_Base.md`

**Patterns avancés de fiabilité pour les charges de travail de production**

**Mots-clés:** `observability`, `distributed-tracing`, `OpenTelemetry`, `chaos-engineering`, `rate-limiting`, `transactional-outbox`, `CDC`, `cache-stampede`, `kubernetes-hardening`

---

### 3. Architecture de Sécurité Côté Client
**Fichier:** `/knowledgeAI/Client_Side_Security_Architecture_Knowledge_Base.md`

**Fondamentaux de sécurité des applications web modernes**

**Mots-clés:** `XSS`, `CSP`, `DOM-based-XSS`, `supply-chain-risk`, `JWT-storage`, `HttpOnly-cookies`, `BFF-pattern`, `DOMPurify`, `SRI`

---

### 4. Cadre Architectural Complet
**Fichier:** `/knowledgeAI/Comprehensive_Architectural_Framework_Knowledge_Base.md`

**Concurrence de base de données, performances et fondamentaux de sécurité**

**Mots-clés:** `ACID`, `isolation-levels`, `dirty-read`, `phantom-read`, `N-plus-1`, `ORM`, `optimistic-locking`, `Redlock`, `BOLA`, `IDOR`

---

### 5. Matrice de Décision Architecturale Contextuelle
**Fichier:** `/knowledgeAI/Contextual_Architecture_Decision_Matrix_Knowledge_Base.md`

**Éviter la sur-ingénierie et dimensionner correctement les solutions**

**Mots-clés:** `overengineering`, `premature-optimization`, `YAGNI`, `Cynefin`, `ADR`, `right-sizing`, `monolith`, `microservices`, `architecture-astronaut`

---

### 6. Ingénierie UI Défensive
**Fichier:** `/knowledgeAI/Defensive_UI_Engineering_Knowledge_Base.md`

**Patterns d'interface utilisateur résilients**

**Mots-clés:** `error-boundaries`, `graceful-degradation`, `retry-logic`, `skeleton-screens`, `optimistic-UI`, `a11y`, `ARIA-live`, `focus-management`

---

### 7. Type Safety de Bout en Bout
**Fichier:** `/knowledgeAI/End_to_End_Type_Safety_Knowledge_Base.md`

**Développement JavaScript full-stack type-safe**

**Mots-clés:** `TypeScript`, `schema-sharing`, `OpenAPI`, `tRPC`, `Zod`, `runtime-validation`, `contract-testing`, `Pact`, `RTK-Query`

---

### 8. Ingénierie des Performances Web Modernes
**Fichier:** `/knowledgeAI/Modern_Web_Performance_Engineering_Knowledge_Base.md`

**Core Web Vitals et stratégies d'optimisation**

**Mots-clés:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `bundle-analysis`, `tree-shaking`, `code-splitting`, `SSR`, `SSG`, `hydration`

---

## 🔍 Référence Rapide: Mappage des Mots-Clés

| Sujet | Lisez Ce Fichier |
|-------|------------------|
| Conception API, REST, gRPC, GraphQL | Architecture AI Guardrail |
| Base de données, transactions, concurrence | Cadre Architectural Complet |
| CSP, XSS, stockage sécurisé, JWT | Architecture de Sécurité Côté Client |
| Monitoring, traçage, observabilité | Résilience Architecturale |
| Performances, bundle, Core Web Vitals | Ingénierie des Performances Web |
| Type safety, validation, schéma | Type Safety de Bout en Bout |
| Gestion des erreurs, états de chargement | Ingénierie UI Défensive |
| Décisions architecturales, sur-ingénierie | Matrice de Décision Contextuelle |

---

## 🚀 Comment Utiliser

### Pour les Agents IA (Contexte LLM)

#### Phase 1: Protocole Cognitif (Pré-Exécution)
Avant d'écrire du code, exécutez la Réflexion Profonde en 5 Étapes.

#### Phase 2: Implémentation
1. **Commencez avec `skill.md`** - Lisez l'index principal
2. **Naviguez vers `/knowledgeAI/`** - Tous les fichiers de connaissance sont ici
3. **Identifiez les mots-clés** de la tâche de l'utilisateur
4. **Utilisez le mappage des mots-clés** pour localiser les fichiers pertinents

#### Phase 3: Protocole Mémoire (Post-Exécution)
1. **Mettez à jour `architecturehistory.md`** - Enregistrez la décision
2. **Documentez la justification** - Référencez les fichiers de la Knowledge Base utilisés

### Pour les Développeurs

1. **Parcourez `skill.md`** pour comprendre les sujets disponibles
2. **Vérifiez le répertoire `/knowledgeAI/`** pour tous les fichiers
3. **Utilisez la recherche par mots-clés** pour trouver les sections pertinentes
4. **Référencez lors des revues de code** comme checklist de qualité

---

## 📄 Licence

Licence MIT - Voir le dépôt pour les détails.

---

> **N'oubliez pas:** L'objectif n'est pas de prévenir tous les échecs, mais de prévenir les échecs qui comptent en production.
