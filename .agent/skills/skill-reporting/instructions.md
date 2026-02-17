---
model_recommendation:
  principal: "Gemini 3 Pro (Low)"
  secondary: "Gemini 3 Flash"
  tertiary: "GPT-OSS 120B (Medium)"
---

# Skill: Reporting
> **Type:** Cross-Cutting Expert
> **Domain:** Metrics, Dashboards, Visualization

## Capabilities
1.  **Dashboard Generation**:
    *   **Input**: JSON reports (audit, tests, coverage), source code stats.
    *   **Output**: `MIGRATION_DASHBOARD.html` (Standalone, interactive).
    *   **Tools**: Python (`pandas`, `jinja2` if available, or pure string manipulation for zero-dependency).
2.  **Trend Analysis**:
    *   Comparing current metrics vs historical data (if available).
3.  **Visualizations**:
    *   Charts for test coverage, migration progress, and code quality.

## Usage
Used by `fixer-agent` or manually invoked to generate the project status dashboard.
