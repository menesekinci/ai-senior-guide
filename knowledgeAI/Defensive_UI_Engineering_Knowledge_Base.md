# Defensive UI Engineering

> **Knowledge Domain:** Resilient Interface Architecture, Error Handling, UX Patterns  
> **Purpose:** Build UIs that gracefully handle failures and edge cases  
> **Target:** LLM agents creating production-ready interfaces  
> **Version:** 1.0  

---

## Table of Contents

1. [Resilient UI Architecture](#1-resilient-ui-architecture)
2. [Error Handling Patterns](#2-error-handling-patterns)
3. [Loading and Skeleton States](#3-loading-and-skeleton-states)
4. [Optimistic UI with Rollback](#4-optimistic-ui-with-rollback)
5. [Accessibility in Error States](#5-accessibility-in-error-states)

---

## 1. Resilient UI Architecture

**Keywords:** `resilient-UI`, `defensive-programming`, `graceful-degradation`, `fault-tolerance`, `error-boundaries`

**Overview:** UIs must handle failures gracefully. Network errors, API failures, and unexpected data should not crash the application.

**Core Principles:**

| Principle | Implementation |
|-----------|----------------|
| **Fail Gracefully** | Show meaningful error messages, not crashes |
| **Recover Automatically** | Retry failed operations when appropriate |
| **Preserve User Input** | Don't lose user's work on failure |
| **Provide Escape Hatches** | Allow users to recover from error states |

---

### 1.1 Error Boundaries

**Keywords:** `error-boundaries`, `React-error-boundary`, `component-isolation`, `crash-prevention`

**Purpose:** Catch JavaScript errors in child components, prevent entire app crash.

**Implementation (React):**
```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false, error: null };

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    logErrorToService(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <FallbackUI error={this.state.error} />;
    }
    return this.props.children;
  }
}
```

**Best Practices:**
- Wrap major feature areas
- Provide recovery options
- Log errors for monitoring
- Don't swallow errors silently

---

## 2. Error Handling Patterns

**Keywords:** `error-handling`, `retry-logic`, `exponential-backoff`, `user-feedback`, `toast-notifications`

### 2.1 Network Error Handling

**Keywords:** `network-errors`, `offline-detection`, `connection-recovery`, `retry-strategies`

**Pattern - Retry with Exponential Backoff:**
```javascript
async function fetchWithRetry(url, options, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      return await fetch(url, options);
    } catch (error) {
      if (i === maxRetries - 1) throw error;
      await delay(Math.pow(2, i) * 1000); // 1s, 2s, 4s
    }
  }
}
```

### 2.2 User-Facing Error Messages

**Keywords:** `error-messages`, `user-friendly`, `technical-details`, `actionable-feedback`

**Error Message Guidelines:**

| Bad | Good |
|-----|------|
| "Error 500" | "Unable to save your changes. Please try again." |
| "Network error" | "Connection lost. Reconnecting..." |
| "null pointer exception" | "Something went wrong. We've notified our team." |

**Structure:**
1. What happened (user-friendly)
2. Why it matters (context)
3. What to do next (actionable)

---

## 3. Loading and Skeleton States

**Keywords:** `loading-states`, `skeleton-screens`, `progressive-loading`, `perceived-performance`, `content-placeholders`

### 3.1 Skeleton Screens

**Keywords:** `skeleton-ui`, `placeholder-content`, `loading-skeleton`, `layout-stability`

**Purpose:** Reduce perceived loading time, prevent layout shift.

**Implementation:**
```jsx
function SkeletonCard() {
  return (
    <div className="skeleton-card">
      <div className="skeleton-image" />
      <div className="skeleton-title" />
      <div className="skeleton-text" />
    </div>
  );
}
```

**Best Practices:**
- Match final layout dimensions
- Use subtle animation (shimmer)
- Don't use for very fast loads (<200ms)

### 3.2 Progressive Loading

**Keywords:** `progressive-loading`, `lazy-loading`, `code-splitting`, `image-optimization`

**Strategy:**
1. Load critical content first
2. Defer non-critical content
3. Show placeholders for deferred content

---

## 4. Optimistic UI with Rollback

**Keywords:** `optimistic-UI`, `rollback`, `async-operations`, `state-synchronization`, `conflict-resolution`

**Pattern:** Update UI immediately, sync with server in background.

### 4.1 Implementation Pattern

**Keywords:** `optimistic-updates`, `pending-state`, `reconciliation`, `error-recovery`

```javascript
function useOptimisticUpdate() {
  const [state, setState] = useState(initialState);
  const [pending, setPending] = useState(false);

  const updateOptimistically = async (updateFn, apiCall) => {
    const previousState = state;

    // Optimistic update
    setState(updateFn(state));
    setPending(true);

    try {
      await apiCall();
    } catch (error) {
      // Rollback on failure
      setState(previousState);
      showError(error);
    } finally {
      setPending(false);
    }
  };

  return { state, pending, updateOptimistically };
}
```

### 4.2 Conflict Resolution

**Keywords:** `conflict-resolution`, `last-write-wins`, `manual-merge`, `server-reconciliation`

**Strategies:**

| Strategy | Use Case |
|----------|----------|
| **Last Write Wins** | Simple state, low conflict probability |
| **Server Wins** | Critical data, server is source of truth |
| **Manual Merge** | Complex data, user decision needed |
| **Operational Transform** | Collaborative editing |

---

## 5. Accessibility in Error States

**Keywords:** `a11y`, `accessibility`, `error-announcement`, `screen-readers`, `ARIA-live`, `focus-management`

### 5.1 Announcing Errors

**Keywords:** `ARIA-live`, `polite-announcements`, `assertive-announcements`, `screen-reader`

**Implementation:**
```jsx
<div aria-live="polite" aria-atomic="true">
  {error && <span className="sr-only">Error: {error.message}</span>}
</div>
```

### 5.2 Focus Management

**Keywords:** `focus-trap`, `focus-restoration`, `modal-focus`, `keyboard-navigation`

**Requirements:**
- Move focus to error message
- Trap focus in modal dialogs
- Restore focus on close
- Visible focus indicators

---

## Category Tree Schema

```
1. Resilient UI Architecture
   1.1 Error Boundaries
   1.2 Graceful Degradation

2. Error Handling Patterns
   2.1 Network Error Handling
   2.2 User-Facing Messages
   2.3 Retry Logic

3. Loading States
   3.1 Skeleton Screens
   3.2 Progressive Loading

4. Optimistic UI
   4.1 Implementation Pattern
   4.2 Conflict Resolution

5. Accessibility
   5.1 Error Announcement
   5.2 Focus Management
```

---

## Error State Decision Tree

```
Error Occurred
├── Network Error?
│   ├── Yes → Retry with backoff → Still failing? → Show offline message
│   └── No → Continue
├── User Input Error?
│   ├── Yes → Highlight field → Show inline error → Preserve input
│   └── No → Continue
├── Server Error?
│   ├── Yes → Log error → Show generic message → Provide retry
│   └── No → Continue
└── Unknown Error?
    └── Log error → Show fallback UI → Allow refresh
```
