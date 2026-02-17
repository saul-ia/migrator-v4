---
description: Phase 2. Generates SQLite DB and Prisma Client from Audit Report or Connection String.
model_recommendation:
  principal: "Claude Sonnet 4.5 (Thinking)"
  secondary: "Gemini 3 Pro (High)"
  tertiary: "Claude Sonnet 4.5"
---

1.  **Agent**: `backend-architect`
2.  **Input**: `audit-report.json` OR `{{connection_string}}`.
3.  **Process**:
    *   Normalize Data Types (`Currency` -> `Decimal`).
    *   Generate `schema.prisma`.
    *   Run `npx prisma db push`.
    *   Run `npx prisma generate`.
4.  **Output**:
    *   `node_modules/@prisma/client` (Strictly Typed Client).
    *   `schema.prisma`.
