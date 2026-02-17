---
description: Phase 1. Decodes legacy assets (VB6, SQL, Data) and generates Audit Report & Inventory.
model_recommendation:
  principal: "Gemini 3 Pro (High)"
  secondary: "Claude Opus 4.6 (Thinking)"
  tertiary: "GPT-OSS 120B (Medium)"
---

1.  **Agent**: `auditor-agent`
2.  **Input**: `{{legacy_path_variable}}` (Path to Code or Data Source Configuration).
3.  **Process**:
    *   Scan directory recursively.
    *   Identify Code (`.frm`, `.bas`, `.cls`) and **Data Sources** (Connection Strings, DDL, DB Files).
    *   Extract SQL strings using `skill-legacy-decoder`.
    *   Map UI controls to User Stories.
4.  **Output**:
    *   `audit-report.json`
    *   `feature_inventory.json`
