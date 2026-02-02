# End-to-End Type Safety in Full-Stack JavaScript

> **Knowledge Domain:** Type Safety, Schema Validation, Contract Testing  
> **Purpose:** Ensure type safety across full-stack JavaScript applications  
> **Target:** LLM agents building type-safe applications  
> **Version:** 1.0  

---

## Table of Contents

1. [The Type Safety Spectrum](#1-the-type-safety-spectrum)
2. [Schema Sharing Strategies](#2-schema-sharing-strategies)
3. [Runtime Validation](#3-runtime-validation)
4. [Contract Testing](#4-contract-testing)
5. [Type-Safe API Clients](#5-type-safe-api-clients)

---

## 1. The Type Safety Spectrum

**Keywords:** `type-safety`, `compile-time`, `runtime`, `TypeScript`, `static-typing`, `dynamic-typing`

**Overview:** Type safety exists on spectrum from purely dynamic to fully static with runtime guarantees.

### 1.1 Levels of Type Safety

**Keywords:** `type-safety-levels`, `type-guards`, `assertions`, `validation`

| Level | Description | Tools |
|-------|-------------|-------|
| **None** | Pure JavaScript, no type checking | - |
| **Compile-time** | TypeScript for development | TypeScript |
| **Build-time** | Type checking in CI/CD | tsc, type-check scripts |
| **Runtime** | Validation at execution | Zod, Joi, Yup |
| **Contract** | API contract enforcement | Pact, OpenAPI |

### 1.2 The TypeScript Boundary Problem

**Keywords:** `boundary-problem`, `IO-boundary`, `external-data`, `type-assertions`, `unsafe-casts`

**Problem:** TypeScript types disappear at runtime. External data (API responses, user input) enters system untyped.

**Anti-pattern:**
```typescript
// UNSAFE: Type assertion without validation
const user = response.data as User;
```

**Solution:** Runtime validation at boundaries.

---

## 2. Schema Sharing Strategies

**Keywords:** `schema-sharing`, `monorepo`, `shared-types`, `code-generation`, `OpenAPI`

### 2.1 Monorepo Approach

**Keywords:** `monorepo`, `shared-package`, `internal-types`, `turborepo`, `nx`

**Structure:**
```
packages/
├── types/          # Shared TypeScript types
├── schemas/        # Shared validation schemas
├── api/            # Backend API
└── web/            # Frontend app
```

**Benefits:**
- Single source of truth
- Instant propagation of changes
- No code generation needed

### 2.2 Code Generation from OpenAPI

**Keywords:** `OpenAPI`, `code-generation`, `swagger`, `openapi-generator`, `contract-first`

**Workflow:**
1. Define API contract in OpenAPI/Swagger
2. Generate TypeScript types from spec
3. Generate API client from spec
4. Server implements contract

**Tools:**
- OpenAPI Generator
- Orval
- Swagger Codegen

### 2.3 tRPC for Full-Stack Type Safety

**Keywords:** `tRPC`, `end-to-end-types`, `procedure-calls`, `type-inference`, `zero-schema`

**Benefits:**
- Automatic type inference
- No code generation
- Type-safe API calls
- IDE autocomplete

```typescript
// Server
const appRouter = router({
  user: router({
    get: procedure
      .input(z.object({ id: z.string() }))
      .query(({ input }) => {
        return db.user.findById(input.id);
      }),
  }),
});

// Client - fully typed
const user = await trpc.user.get.query({ id: '123' });
```

---

## 3. Runtime Validation

**Keywords:** `runtime-validation`, `schema-validation`, `Zod`, `Joi`, `Yup`, `io-ts`, `type-guards`

### 3.1 Validation Libraries Comparison

**Keywords:** `validation-libraries`, `schema-definition`, `type-inference`, `bundle-size`

| Library | Type Inference | Bundle Size | Best For |
|---------|---------------|-------------|----------|
| **Zod** | Excellent | ~12kb | Most projects |
| **Joi** | Good (with @types) | ~100kb | Node.js backend |
| **Yup** | Good | ~25kb | Form validation |
| **io-ts** | Excellent | ~20kb | FP enthusiasts |
| **Valibot** | Good | ~1kb | Bundle-constrained |

### 3.2 Zod Patterns

**Keywords:** `Zod`, `schema-definition`, `type-inference`, `refinement`, `transform`

**Basic Schema:**
```typescript
import { z } from 'zod';

const UserSchema = z.object({
  id: z.string().uuid(),
  email: z.string().email(),
  age: z.number().min(0).max(150).optional(),
  role: z.enum(['admin', 'user', 'guest']),
});

type User = z.infer<typeof UserSchema>;
```

**Validation at Boundary:**
```typescript
// API route
app.post('/users', (req, res) => {
  const result = UserSchema.safeParse(req.body);

  if (!result.success) {
    return res.status(400).json({ errors: result.error.issues });
  }

  const user = result.data; // Fully typed
  // ...
});
```

### 3.3 Type Guards

**Keywords:** `type-guards`, `user-defined-type-guards`, `narrowing`, `predicate-functions`

```typescript
// Custom type guard
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

// Usage
if (isString(unknownValue)) {
  unknownValue.toUpperCase(); // TypeScript knows it's a string
}
```

---

## 4. Contract Testing

**Keywords:** `contract-testing`, `consumer-driven-contracts`, `Pact`, `API-contract`, `integration-testing`

### 4.1 Consumer-Driven Contracts

**Keywords:** `CDC`, `consumer`, `provider`, `contract-verification`, `Pact`

**Concept:** Consumers define expectations, providers verify they meet them.

**Benefits:**
- Detect breaking changes early
- Enable independent deployment
- Reduce integration test burden

### 4.2 Pact Implementation

**Keywords:** `Pact`, `pact-broker`, `contract-verification`, `mock-provider`

**Consumer Test:**
```typescript
// Consumer defines expected interaction
const pact = new Pact({
  consumer: 'WebApp',
  provider: 'UserAPI',
});

await pact.addInteraction({
  state: 'user exists',
  uponReceiving: 'get user by id',
  withRequest: {
    method: 'GET',
    path: '/users/123',
  },
  willRespondWith: {
    status: 200,
    body: like({
      id: '123',
      email: 'user@example.com',
    }),
  },
});
```

**Provider Verification:**
```typescript
// Provider verifies against contract
const verifier = new Verifier({
  provider: 'UserAPI',
  pactBrokerUrl: 'https://pact.example.com',
  publishVerificationResult: true,
});

await verifier.verify();
```

---

## 5. Type-Safe API Clients

**Keywords:** `type-safe-client`, `fetch-wrapper`, `axios-types`, `generated-client`, `RTK-Query`

### 5.1 Typed Fetch Wrapper

**Keywords:** `fetch-wrapper`, `generic-types`, `response-typing`, `error-typing`

```typescript
async function api<T>(
  url: string,
  options?: RequestInit
): Promise<T> {
  const response = await fetch(url, options);

  if (!response.ok) {
    throw new ApiError(response.status, await response.text());
  }

  return response.json() as Promise<T>;
}

// Usage
const user = await api<User>('/api/users/123');
```

### 5.2 RTK Query

**Keywords:** `RTK-Query`, `Redux-Toolkit`, `cache-management`, `automatic-refetching`, `type-generation`

```typescript
const api = createApi({
  baseQuery: fetchBaseQuery({ baseUrl: '/api' }),
  endpoints: (builder) => ({
    getUser: builder.query<User, string>({
      query: (id) => `users/${id}`,
    }),
    updateUser: builder.mutation<User, Partial<User>>({
      query: (body) => ({
        url: `users/${body.id}`,
        method: 'PUT',
        body,
      }),
    }),
  }),
});
```

---

## Category Tree Schema

```
1. Type Safety Foundation
   1.1 Type Safety Spectrum
   1.2 TypeScript Boundary Problem

2. Schema Sharing
   2.1 Monorepo Approach
   2.2 OpenAPI Code Generation
   2.3 tRPC

3. Runtime Validation
   3.1 Validation Libraries
   3.2 Zod Patterns
   3.3 Type Guards

4. Contract Testing
   4.1 Consumer-Driven Contracts
   4.2 Pact Implementation

5. Type-Safe Clients
   5.1 Typed Fetch
   5.2 RTK Query
```

---

## Type Safety Checklist

| Boundary | Validation Method | Tool |
|----------|-------------------|------|
| API Request Body | Schema validation | Zod |
| API Response | Schema validation | Zod |
| URL Parameters | Schema validation | Zod |
| Query Parameters | Schema validation | Zod |
| Form Input | Schema + UI validation | Zod + React Hook Form |
| External APIs | Contract testing | Pact |
| Database | ORM types | Prisma/TypeORM |
