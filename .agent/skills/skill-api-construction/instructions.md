---
model_recommendation:
  principal: "Gemini 3 Flash"
  secondary: "Gemini 3 Pro (Low)"
  tertiary: "GPT-OSS 120B (Medium)"
---

# Skill: API Construction
> **Type:** Backend Expert
> **Domain:** Express 5 & Prisma Logic

## Capabilities
1.  **Semantic SQL Re-Engineering**:
    *   **Analyze Intent**: "Get Top 5 Debtors"
    *   **Rebuild**: `prisma.debtors.findMany({ take: 5, orderBy: { debt: 'desc' } })`
    *   **Fallback**: Typed `$queryRaw` (Only if unavoidable). **NO TODOs**.
2.  **Boilerplate Generation**:
    *   `Controller`: Async handler, Zod validation, Service call.
    *   `Service`: Business logic, Prisma calls, Error throwing.
    *   `Route`: Express Router, JWT Middleware, Swagger Docs.

## Usage
Used by `backend-architect` to generate the Node.js API.
