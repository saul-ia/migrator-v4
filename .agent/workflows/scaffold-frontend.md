---
description: Phase 4. Generates Angular 21 Zoneless UI from OpenAPI Spec.
model_recommendation:
  principal: "Claude Sonnet 4.5"
  secondary: "Gemini 3 Pro (High)"
  tertiary: "Gemini 3 Flash"
---

1.  **Agent**: `frontend-stylist`
2.  **Input**: `src/openapi.json` + `feature_inventory.json`.
3.  **Process**:
    *   Generate Services matching API Contract.
    *   Generate Components using Signals & Control Flow.
    *   Apply Material Design & Responsive Layouts.
4.  **Output**:
    *   `src/app/pages/*` (Working UI).
