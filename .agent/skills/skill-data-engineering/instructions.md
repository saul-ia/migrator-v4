---
model_recommendation:
  principal: "Claude Sonnet 4.5 (Thinking)"
  secondary: "Gemini 3 Pro (High)"
  tertiary: "Claude Sonnet 4.5"
---

# Skill: Data Engineering
> **Type:** Backend Expert
> **Domain:** Database Schema & Migration

## Capabilities
1.  **Source Agnostic Strategy**:
    *   **ODBC/JDBC**: Connection String -> ETL Extraction.
    *   **Flat Files**: CSV/Excel -> `sqlite3 .import`.
    *   **SQL Dumps**: Parse `CREATE TABLE` DDL.
    *   **Legacy (.mdb)**: `mdb-export` (Only if strictly needed).
2.  **Schema Normalization**:
    *   `Currency` -> `Decimal`
    *   `Date` -> `DateTime`
    *   `Long` -> `Int`
    *   Enforce `cuid` for PKs if new, or `Int` if preserving legacy IDs.
3.  **Seeding**:
    *   Generates `prisma/seed.ts` from migrated data.

## Usage
Used by `backend-architect` to build `schema.prisma`.
