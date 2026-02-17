---
description: Phase 3. Generates Express 5 API with Swagger from Prisma Client.
model_recommendation:
  principal: "Gemini 3 Pro (High)"
  secondary: "Claude Sonnet 4.5"
  tertiary: "Gemini 3 Flash"
---

1.  **Agent**: `backend-architect`
2.  **Input**: `node_modules/@prisma/client` + `audit-report.json` (for SQL Intent).
3.  **Process**:
    *   Generate Express Controllers for each Entity.
    *   Translate Legacy SQL to Semantic Prisma Queries (NO Raw SQL if possible).
    *   Add Zod Validation & OpenApi Decorators.
4.  **Output**:
    *   `src/app.ts`
    *   `src/openapi.json` (Strict Contract).
