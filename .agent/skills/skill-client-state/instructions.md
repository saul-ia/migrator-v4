---
model_recommendation:
  principal: "Claude Sonnet 4.5 (Thinking)"
  secondary: "Claude Opus 4.6 (Thinking)"
  tertiary: "Claude Sonnet 4.5"
---

# Skill: Client State
> **Type:** Frontend Logic Expert (No UI)
> **Domain:** Signals, State, Business Logic

## Capabilities
1.  **Zoneless Logic**:
    *   **Signals**: `signal()`, `computed()`, `effect()`.
    *   **Inputs/Outputs**: `input()`, `output()`.
    *   **NO**: `BehaviorSubject` (unless strictly needed for RxJS interop).
2.  **Service Layers**:
    *   `HttpClient` wrappers strictly typed to `openapi.json` interfaces.
    *   Global Error Handling via Interceptors.
3.  **Routing**:
    *   Functional Guards (`canActivateFn`).
    *   Resolvers using Signals.

## Usage
Used by `frontend-stylist` (and `fixer-agent`) to implement the "Brain" of components.
