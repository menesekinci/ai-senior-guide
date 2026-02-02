# Modern Web Performance Engineering

> **Knowledge Domain:** Web Performance, Bundle Optimization, Core Web Vitals  
> **Purpose:** Optimize web application performance and user experience  
> **Target:** LLM agents creating performance-conscious applications  
> **Version:** 1.0  

---

## Table of Contents

1. [Core Web Vitals](#1-core-web-vitals)
2. [Bundle Analysis and Optimization](#2-bundle-analysis-and-optimization)
3. [Tree-Shaking Strategies](#3-tree-shaking-strategies)
4. [Loading Strategies](#4-loading-strategies)
5. [Rendering Patterns](#5-rendering-patterns)

---

## 1. Core Web Vitals

**Keywords:** `Core-Web-Vitals`, `LCP`, `FID`, `CLS`, `INP`, `page-experience`, `Google-ranking`

**Overview:** Google's page experience metrics that impact search ranking and user experience.

### 1.1 The Three Core Metrics

**Keywords:** `LCP`, `FID`, `CLS`, `performance-metrics`, `user-centric`

| Metric | Description | Target | Measures |
|--------|-------------|--------|----------|
| **LCP** | Largest Contentful Paint | < 2.5s | Loading performance |
| **FID** | First Input Delay | < 100ms | Interactivity |
| **CLS** | Cumulative Layout Shift | < 0.1 | Visual stability |

### 1.2 Interaction to Next Paint (INP)

**Keywords:** `INP`, `Interaction-to-Next-Paint`, `FID-replacement`, `responsiveness`

**Status:** Replacing FID in 2024

**Measures:** Responsiveness to all interactions during page lifecycle.

**Target:** < 200ms (good), < 500ms (needs improvement)

### 1.3 Measuring Core Web Vitals

**Keywords:** `PageSpeed-Insights`, `Lighthouse`, `Chrome-UX-Report`, `Web-Vitals-JS`

| Tool | Use Case |
|------|----------|
| **PageSpeed Insights** | Field + lab data, SEO impact |
| **Lighthouse** | Local development testing |
| **Chrome UX Report** | Real user monitoring (RUM) |
| **Web Vitals JS** | In-application measurement |

---

## 2. Bundle Analysis and Optimization

**Keywords:** `bundle-analysis`, `webpack-bundle-analyzer`, `rollup-plugin-visualizer`, `bundle-size`, `code-splitting`

### 2.1 Analyzing Bundle Size

**Keywords:** `bundle-analyzer`, `size-visualization`, `dependency-analysis`, `duplicates`

**Tools:**

| Tool | Framework | Output |
|------|-----------|--------|
| webpack-bundle-analyzer | Webpack | Interactive treemap |
| rollup-plugin-visualizer | Rollup | Sunburst/treemap |
| @next/bundle-analyzer | Next.js | Treemap |
| source-map-explorer | Any | Interactive analysis |

### 2.2 Bundle Size Targets

**Keywords:** `bundle-budgets`, `size-targets`, `performance-budget`

| Resource | Target | Critical Point |
|----------|--------|----------------|
| Initial JS | < 200KB gzipped | > 500KB |
| Initial CSS | < 50KB gzipped | > 100KB |
| Images | < 100KB each | > 500KB |
| Total Page | < 1MB | > 3MB |

### 2.3 Common Bundle Bloat Sources

**Keywords:** `bundle-bloat`, `large-dependencies`, `moment-js`, `lodash`, `polyfills`

**Offenders:**
- Moment.js (use date-fns or dayjs)
- Full lodash (use lodash-es or specific imports)
- Unused polyfills
- Large icon libraries (tree-shake or use subset)
- Duplicate dependencies

---

## 3. Tree-Shaking Strategies

**Keywords:** `tree-shaking`, `dead-code-elimination`, `ES-modules`, `side-effects`, `pure-modules`

### 3.1 How Tree-Shaking Works

**Keywords:** `static-analysis`, `ESM`, `import/export`, `unused-exports`, `webpack`, `rollup`

**Requirements:**
- ES Modules (import/export)
- Static imports (no dynamic requires)
- Side-effect free code

### 3.2 Library-Side Configuration

**Keywords:** `package.json`, `sideEffects`, `module`, `main`, `exports`

```json
{
  "name": "my-library",
  "main": "dist/index.cjs",
  "module": "dist/index.mjs",
  "exports": {
    ".": {
      "import": "./dist/index.mjs",
      "require": "./dist/index.cjs"
    }
  },
  "sideEffects": false
}
```

### 3.3 Consumer-Side Optimization

**Keywords:** `named-imports`, `specific-imports`, `barrel-files`, `deep-imports`

**Good:**
```javascript
import { map } from 'lodash-es';
import { format } from 'date-fns';
```

**Bad:**
```javascript
import _ from 'lodash'; // Imports everything
import moment from 'moment'; // Large bundle
```

---

## 4. Loading Strategies

**Keywords:** `lazy-loading`, `code-splitting`, `dynamic-imports`, `prefetching`, `preloading`

### 4.1 Code Splitting

**Keywords:** `route-based-splitting`, `component-splitting`, `React-lazy`, `Suspense`

**Route-Based Splitting:**
```jsx
import { lazy, Suspense } from 'react';

const Dashboard = lazy(() => import('./Dashboard'));
const Settings = lazy(() => import('./Settings'));

function App() {
  return (
    <Suspense fallback={<Loading />}>
      <Routes>
        <Route path="/dashboard" element={<Dashboard />} />
        <Route path="/settings" element={<Settings />} />
      </Routes>
    </Suspense>
  );
}
```

### 4.2 Resource Hints

**Keywords:** `prefetch`, `preload`, `preconnect`, `dns-prefetch`, `resource-hints`

| Hint | Use Case | Example |
|------|----------|---------|
| `preload` | Critical resources needed soon | Fonts, hero images |
| `prefetch` | Resources for next navigation | Next page bundle |
| `preconnect` | Establish early connection | CDN, API domain |
| `dns-prefetch` | DNS lookup early | Third-party domains |

```html
<link rel="preload" href="/fonts/main.woff2" as="font" type="font/woff2" crossorigin>
<link rel="prefetch" href="/next-page.js">
<link rel="preconnect" href="https://api.example.com">
```

---

## 5. Rendering Patterns

**Keywords:** `SSR`, `SSG`, `CSR`, `ISR`, `hydration`, `streaming`, `partial-hydration`

### 5.1 Rendering Pattern Comparison

**Keywords:** `server-side-rendering`, `static-generation`, `client-side-rendering`, `incremental-static-regeneration`

| Pattern | Build | Request | Best For |
|---------|-------|---------|----------|
| **SSG** | Pre-render | CDN cache | Content that rarely changes |
| **SSR** | Build-time | Server render | Dynamic data, SEO critical |
| **CSR** | Minimal | Client render | Highly interactive apps |
| **ISR** | Pre-render + update | Stale-while-revalidate | Large sites with updates |

### 5.2 Hydration Strategies

**Keywords:** `hydration`, `progressive-hydration`, `islands-architecture`, `partial-hydration`, `server-components`

**Traditional Hydration:**
- Server renders HTML
- Client downloads JS
- React "hydrates" - attaches event listeners
- Page becomes interactive

**Progressive Hydration:**
- Hydrate critical components first
- Defer non-critical hydration
- Reduce Time to Interactive (TTI)

**Islands Architecture (Astro):**
- Server-render everything by default
- Only hydrate interactive "islands"
- Zero JavaScript for static content

---

## Category Tree Schema

```
1. Core Web Vitals
   1.1 LCP, FID, CLS
   1.2 INP (FID Replacement)
   1.3 Measurement Tools

2. Bundle Optimization
   2.1 Bundle Analysis
   2.2 Size Targets
   2.3 Common Bloat Sources

3. Tree-Shaking
   3.1 How It Works
   3.2 Library Configuration
   3.3 Consumer Optimization

4. Loading Strategies
   4.1 Code Splitting
   4.2 Resource Hints

5. Rendering Patterns
   5.1 SSR vs SSG vs CSR
   5.2 Hydration Strategies
```

---

## Performance Checklist

| Area | Action | Tool |
|------|--------|------|
| Bundle | Analyze size | webpack-bundle-analyzer |
| Images | Optimize, use WebP | squoosh, sharp |
| Fonts | Subset, preload | fonttools |
| CSS | Purge unused | PurgeCSS |
| JS | Tree-shake, code-split | Rollup, Webpack |
| Network | Enable compression, HTTP/2 | Server config |
| Caching | Set proper headers | Cache-Control |
| CDN | Use edge caching | Cloudflare, Vercel |

---

## Core Web Vitals Targets

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP | ≤ 2.5s | ≤ 4.0s | > 4.0s |
| FID/INP | ≤ 100ms | ≤ 200ms | > 200ms |
| CLS | ≤ 0.1 | ≤ 0.25 | > 0.25 |
