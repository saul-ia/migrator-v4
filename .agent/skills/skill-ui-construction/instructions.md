---
model_recommendation:
  principal: "Gemini 3 Flash"
  secondary: "Claude Sonnet 4.5"
  tertiary: "Gemini 3 Pro (Low)"
---

# Skill: UI Construction
> **Type:** Frontend Visual Expert (No Logic)
> **Domain:** HTML, CSS, Material, Layouts

## Capabilities
1.  **Modern Syntax**:
    *   **Control Flow**: `@if`, `@for`, `@switch`, `@defer`.
    *   **Reference**: `viewChild()` instead of `@ViewChild`.
2.  **Material Design**:
    *   **Components**: `MatDialog` (Modals), `MatTable` (Grids), `MatSidenav`.
    *   **Icons**: `Lucide Angular` (Priority) > `Material Icons`.
3.  **Strict Forms**:
    *   **Reactive**: `FormControl<string>`, `FormGroup<{...}>`.
    *   **Validation**: Sync/Async validators.

## Usage
Used by `frontend-stylist` (and `fixer-agent`) to implement the "Face" of components.
