---
description: The Master Workflow. Full Technical Stack (Ang21/Node24) with Configurable Flags, Strict Testing, SonarQube, QA & 100% Parity Check.
model_recommendation:
  principal: "Claude Sonnet 4.5 (Thinking)"
  secondary: "Gemini 3 Pro (High)"
  tertiary: "Claude Sonnet 4.5"
---

# 🎼 Workflow: Orchestrate Migration

## 🚨 Phase 0: Pre-flight & Configuration

### 0.1 Control Panel (Flags)
> **Instruction:** Set these variables to `true` or `false` to control the workflow scope.
> *Default value is `true` for all if not specified.*

* `{{RUN_TESTS}}`: **true** (Executes Jest/Supertest loops with >80% coverage).
* `{{RUN_SONAR}}`: **true** (Generates `sonar-project.properties` & `lcov.info`).
* `{{RUN_QA_AUDIT}}`: **true** (Executes Security `npm audit` & A11y checks).
* `{{GENERATE_DOCS}}`: **true** (Generates README & Migration Report).
* `{{AUTO_START}}`: **true** (Installs dependencies and launches the app at the end).

### 0.2 Setup & Naming (MANDATORY)
1.  **Input Variable:** `{{legacy_path_variable}}` (Must be provided).
2.  **Versioning Strategy (Dynamic Naming):**
    * **Rule:** **NEVER** use generic names like "biblioteca".
    * **Format:** `[APP_NAME]_[TIMESTAMP]` (e.g., `inventory_20260217_1030`).
    * **Action:** Create output directory and set as `{{OUTPUT_DIR}}`.
3.  **Context:** STRICTLY FOLLOW rules defined in `.agent/rules/RULES.md`.

---

## Phase 1: 🔍 Deep Audit & Feature Inventory
> **Status:** MANDATORY.
> **Objective:** Map every button, modal, and flow to ensure 100% migration.

1.  **Trigger:** Workflow `/audit-legacy`
    * **Input:** `{{legacy_path_variable}}`
3.  **Output Artifacts:**
    *   `audit-report.json` (Schema & Entities).
    *   `feature_inventory.json` (UI/UX Flows).
    *   **Status:** 🟢 Ready for Phase 2.
2.  **🛑 GATEKEEPER:** Pause if "CRITICAL_UNKNOWN" logic is detected.

---

## Phase 2: 🗄️ Data Foundation (SQLite & Prisma)
> **Status:** MANDATORY.
> **Dependency:** Consumes `audit-report.json`.

1.  **Trigger:** Workflow `/migrate-db`
    *   **Input:** `audit-report.json` (Entities).
    *   **Action 1:** Generate `schema.prisma`.
    *   **Action 2:** Generate Migration Script (Legacy -> SQLite).
    *   **Action 3:** Run `npx prisma generate` (Creates Type-Safe Client).
    *   **Output Artifact:** `node_modules/@prisma/client` (Source of Truth for Backend).
    *   **Constraint:** **NO DATA LOSS**. 100% record transfer required.

---

## Phase 3: 🏗️ Backend Core (Node 24 + Express 5)
> **Status:** MANDATORY.
> **Dependency:** Consumes `Prisma Client` (Type Safety).

1.  **Trigger:** Workflow `/scaffold-backend`
2.  **Setup Server:** Express v5+ (Native Async/Await).
3.  **Input:** `node_modules/@prisma/client` (Ensures Backend types match DB exactly).
3.  **Architecture:** Strict Layering (`Routes` -> `Controllers` -> `Services`).
4.  **🔄 Loop (Per Entity in `audit-report.json`):**
    *   **Action:** Generate RESTful CRUD using Prisma Types.
    *   **Validation:** Zod Schemas derived from Prisma models.
5.  **Output Artifact:** `src/openapi.json` (Auto-generated Swagger Spec).
    *   *Critial:* This JSON defines the contract for the Frontend.
6.  **Core Features:**
    *   **Auth:** JWT security implementation.
    *   **Reporting:** **PDFMake** Service.
    *   **Error Handling:** Global Handler.
5.  **Cleanup:** Remove all legacy dead code/orphan functions.

---

## Phase 4: 🎨 Frontend Construction (Modern Angular 21)
> **Status:** MANDATORY.
> **Dependency:** Consumes `openapi.json` (API Contract) & `feature_inventory.json` (UI Layout).

1.  **Trigger:** Workflow `/scaffold-frontend`
2.  **Core Setup:**
    *   **Tech:** Angular v21 (Standalone Components).
    *   **Input 1:** `src/openapi.json` -> Run `openapi-generator` -> Generate **Strictly Typed Services**.
    *   **Input 2:** `feature_inventory.json` -> Scaffolds Pages/Components.
2.  **Loop (Per View/Form):**
    *   **Constraint 1 (Zoneless):** `provideExperimentalZonelessChangeDetection()`.
    *   **Constraint 2 (Signals):** `input()`, `output()`, `viewChild()`.
    *   **Constraint 3 (Forms):** Typed Reactive Forms matching OpenAPI models.
    *   **Constraint 4 (UX/UI):** Lucide Icons, SCSS, Premium Design.
    *   **Constraint 5 (Accessibility):** ARIA labels, Keyboard navigation.

---

## Phase 5: 🧪 Strict Testing & Metrics
> **CONDITION:** Execute ONLY if `{{RUN_TESTS}}` is **true**.
> **Dependency:** Scans generated Codebase.

1.  **Trigger:** Workflow `/auto-test`
2.  **Strategy:** Unit & Integration Testing (No E2E/Playwright).
3.  **Configuration:** Jest configured to output `coverage/lcov.info` (for Sonar).
3.  **Backend Tests:**
    *   **Input:** Scans `src/controllers/*.ts`.
    *   **Action:** Generates tests matching 1:1 with Controller methods.
    *   **Tool:** Jest + **Supertest**.
4.  **Frontend Tests:**
    *   **Input:** Scans `src/app/pages/*.component.ts`.
    *   **Action:** Generates Harness-based tests for user interactions.
    *   **Tool:** Jest + **Angular Component Harnesses**.
5.  **⚡ TEST & HEAL LOOP (Max 3 Iterations):**
    *   **Action:** Run tests with coverage.
    *   **Condition:** If Fail OR Coverage < 80%:
        *   **Fixer Agent** patches code -> Retry.

---

## Phase 6: 🛡️ QA, Security & SonarQube
> **CONDITION:** Execute ONLY if `{{RUN_QA_AUDIT}}` is **true**.

1.  **Trigger:** Workflow `/run-qa`
2.  **Security Audit:**
    * Run `npm audit` (auto-fix). Verify JWT/Auth security.
3.  **A11y Final Audit:**
    * Run automated accessibility scanner (e.g., `axe`) on templates.
    * **Constraint:** 0 Critical Violations.
4.  **SonarQube Integration:**
    * **Condition:** Execute ONLY if `{{RUN_SONAR}}` is **true**.
    * **Action:** Generate `sonar-project.properties`.
    * **Config:** Point `sonar.typescript.lcov.reportPaths` to `coverage/lcov.info`.
    * **Key:** Set `sonar.projectKey` to `{{APP_NAME}}`.

---

## Phase 7: 📚 Documentation & Handover
> **CONDITION:** Execute ONLY if `{{GENERATE_DOCS}}` is **true**.

1.  **Trigger:** Workflow `/generate-docs`.
2.  **Inputs:** `audit-report.json`, `feature_inventory.json`, `coverage-summary.json`, `qa-report.json`.
3.  **Action: HTML Dashboard Generation (`MIGRATION_DASHBOARD.html`)**
    * **Tech:** Single-file HTML5 with embedded CSS (Modern, Clean Design).
    * **Content Blueprint (MANDATORY SECTIONS):**
        * **Header:** App Name, Timestamp, Migration Version (Ang21/Node24).
        * **Executive Summary:** Total Files Migrated, Database Tables Transferred.
        * **Feature Parity Matrix:** A Table comparing `Legacy Feature` vs `New Component` (Status: ✅ Migrated). Data source: `feature_inventory.json`.
        * **Quality Gates:** Visual Badges for Test Coverage %, A11y Pass/Fail, SonarQube Ready.
        * **Architecture Overview:** Brief description of the Zoneless/Signals architecture.
        * **Known Issues:** List of items marked "NEEDS_MANUAL_REVIEW" (if any).
4.  **Action:** Generate `README.md` (Setup Instructions).
5.  **Final Deliverable:** Fully contained `{{APP_NAME}}_{{TIMESTAMP}}` folder.

---

## Phase 8: 🚀 Installation, Build & Launch
> **CONDITION:** Execute ONLY if `{{AUTO_START}}` is **true**.

1.  **Dependency Installation:**
    * **Action:** Execute `npm install` in the root (ensuring recursive installation for both the Angular client and the Node.js v24 server).
2.  **Production Build:**
    * **Action:** Execute `npm run build` (Build Angular to `dist/` folder).
    * **Config:** Ensure Node.js server is configured to serve static files from `dist/` on the root route `/`.
3.  **Launch Sequence:**
    * **Action:** Execute `npm start`.
    * **Validation:** Verify that the server is listening on the assigned port and that the SQLite connection is active.
4.  **Auto-Open Interface:**
    * **Action:** If the environment supports it, **automatically open** the default web browser with two tabs:
        1.  **Main App:** `http://localhost:[PORT]`
        2.  **Swagger Documentation:** `http://localhost:[PORT]/api-docs`
    * **Output:**
        * "🚀 Application successfully launched!"
        * "🌐 Web URL: http://localhost:[PORT]"
        * "📖 Swagger API Docs: http://localhost:[PORT]/api-docs"