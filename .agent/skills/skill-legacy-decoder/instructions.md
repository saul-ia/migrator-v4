---
model_recommendation:
  principal: "Gemini 3 Pro (High)"
  secondary: "Claude Opus 4.6 (Thinking)"
  tertiary: "Gemini 3 Pro (Low)"
---

# Skill: Legacy Decoder
> **Type:** Analysis Expert
> **Domain:** Legacy Code (VB6, VBA, Access)

## Capabilities
1.  **Regex Pattern Matching**:
    *   `Function`: `(Public|Private) Function\s+(\w+)\((.*)\)\s+As\s+(\w+)`
    *   `Sub`: `(Public|Private) Sub\s+(\w+)\((.*)\)`
    *   `Embedded SQL`: `strSQL\s*=\s*"(SELECT|INSERT|UPDATE|DELETE).*"`
2.  **Mapping Dictionaries**:
    *   `MsgBox` -> `MatDialog`
    *   `FlexGrid` -> `MatTable`
    *   `ADO.Recordset` -> `Prisma`

## Usage
Used by `auditor-agent` to parse spaghetti code into `feature_inventory.json`.
