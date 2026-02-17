---
model_recommendation:
  principal: "Gemini 3 Flash"
  secondary: "Gemini 3 Pro (Low)"
  tertiary: "GPT-OSS 120B (Medium)"
---

# Skill: Quality Assurance
> **Type:** Cross-Cutting Expert
> **Domain:** Testing (Jest), Security, A11y

## Capabilities
1.  **Backend Testing (Jest + Supertest)**:
    *   **Spin**: Ephemeral Express App per test suite.
    *   **Mock**: `jest.spyOn(service, 'method')`. **NO REAL DB**.
2.  **Frontend Testing (Harnesses)**:
    *   **Interact**: `loader.getHarness(MatButtonHarness)`.
    *   **Forbidden**: `nativeElement.querySelector()`.
3.  **Auditing**:
    *   **Security**: `npm audit` auto-fixers.
    *   **A11y**: `axe-core` scanners for `*.html`.
    *   **Sonar**: `sonar-project.properties` generation.

## Usage
Used by `qa-sentinel` to enforce gates.
