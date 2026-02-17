---
description: Phase 5. Generates and Runs Tests (Jest). Triggers Fixer if failures occur.
model_recommendation:
  principal: "Gemini 3 Flash"
  secondary: "Gemini 3 Pro (Low)"
  tertiary: "GPT-OSS 120B (Medium)"
---

1.  **Agent**: `qa-sentinel`
2.  **Input**: `src/` (Full Source Code).
3.  **Process**:
    *   Generate `*.spec.ts` (Backend) & `*.component.spec.ts` (Frontend).
    *   Run `npm test -- --coverage`.
4.  **Loop (Self-Healing)**:
    *   IF `Fail` OR `Coverage < 80%`:
        *   Trigger `fixer-agent` on failing files.
        *   Retry Test.
        *   Max Retries: 3.
