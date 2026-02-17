---
description: Phase 6. Runs Security Audit, A11y Checks and Sonar Analysis.
model_recommendation:
  principal: "Gemini 3 Pro (Low)"
  secondary: "Gemini 3 Flash"
  tertiary: "GPT-OSS 120B (Medium)"
---

1.  **Agent**: `qa-sentinel`
2.  **Process**:
    *   Run `npm audit fix` (Auto-patch vulnerabilities).
    *   Run `npx axe-cli ./src/**/*.html` (A11y Check).
    *   Generate `sonar-project.properties`.
3.  **Gate**:
    *   Fail if Critical Vulnerabilities found.
