---
trigger: always_on
---

# Rules (Zoneless & UX Enhanced)

> [!IMPORTANT]
> Estas reglas son de cumplimiento MANDATORIO para todos los agentes y desarrolladores. 
> La excelencia técnica sin una interfaz usable es un fallo en la migración.

---

## 📋 1. Naming & Translation Conventions

### 1.1 Files & Components
| Origen (VB6) | Destino (Angular) | Regla |
| :--- | :--- | :--- |
| `Frm[Name]` | `[name-kebab].component.ts` | Remove prefix `Frm`, convert to kebab-case |
| `Mod[Name]` | `[name-kebab].service.ts` | Remove prefix `Mod`, suffix `.service` |
| `Cls[Name]` | `[name-kebab].model.ts` | Remove prefix `Cls`, suffix `.model` |
| `MDI[Name]` | `[name-kebab]-layout.component.ts` | treat MDI forms as Layouts |

### 1.2 Variables & Functions
| Origen (VB6) | Destino (TypeScript) | Regla |
| :--- | :--- | :--- |
| `str[Name]` | `name: string` | Remove Hungarian `str`, CamelCase result |
| `int[Name]`, `lng[Name]` | `name: number` | Remove Hungarian `int/lng`, CamelCase result |
| `cur[Name]`, `dbl[Name]` | `name: number` | Remove Hungarian `cur/dbl`, CamelCase result |
| `dt[Name]`, `date[Name]`| `name: Date` | Remove Hungarian `dt/date`, CamelCase result |
| `bol[Name]`, `bln[Name]`| `name: boolean` | Remove Hungarian `bol/bln`, CamelCase result |
| `Public Function [Name]` | `[name]()` in Service | Move logic to Service, CamelCase name |
| `Private Sub [Name]` | `private [name]()` | Logic stays in Component (if UI related) |

---

## 🏗️ 2. Architecture (ZONELESS Angular 21)

### 2.1 Frontend Rules
* **Zoneless Change Detection**: Prohibido el uso de `zone.js`. Se debe configurar mediante `provideExperimentalZonelessChangeDetection()`.
* **Signals for ALL State**: Prohibido usar variables de clase planas para el estado. Uso obligatorio de `signal()`, `computed()` e `input()`.
* **OnPush Strategy**: Todos los componentes deben tener `changeDetection: ChangeDetectionStrategy.OnPush`.
* **Standalone Components**: Prohibido el uso de `NgModules`.
* **Reactive Forms**: Uso obligatorio de `FormControl/FormGroup`. Prohibido Template-driven forms.


### 2.1.1 Mandatory Libraries (Frontend)
* **Notifications**: Use `@ngneat/hot-toast` (Prohibido `MatSnackBar` default).
* **Reporting**: Use `pdfmake` for client-side generation or buffer handling.
* **Modals**: Use `MatDialog` exclusively.

### 2.2 Backend (Node 24 + Express 5 + Prisma)
* **Node 24**: Uso obligatorio de LTS v24.x.
* **Express 5**: Use native `async/await`. Prohibido usar `try/catch` manual en cada controlador (Usar Global Error Handler).
* **Thin Controllers**: Los controladores solo gestionan entrada/salida. La lógica reside en `Services`.
* **API Documentation**: Obligatorio uso de decoradores `Swagger/OpenAPI` en todos los endpoints.
* **Pino Logging**: Prohibido el uso de `console.log`. Usar el logger institucional.
* **Prisma ORM**: Prohibido SQL crudo (`db.query`). Usar métodos del ORM.

---

## 🎨 3. UX/UI & Feedback

### 3.1 Responsiveness
* **Mobile First**: Todos los formularios y tablas deben ser funcionales en una resolución mínima de **375px**.
* **Layout**: Uso de Flexbox/Grid. Prohibidos los anchos fijos en contenedores principales.

### 3.2 Visual Feedback
* **Loading States**: Operaciones que excedan los 300ms **deben** mostrar un `MatProgressSpinner` o `Skeleton`.
* **Non-Blocking UI**: Las llamadas a la API no deben bloquear la interacción del usuario a menos que sea estrictamente necesario (modales).
* **Material Theme**: Uso estricto de la paleta de colores y tipografía definida en el `Angular Material Theme`.

### 3.3 Icons & Components
* **Icons**: Prioridad a `Lucide Icons`. `Material Icons` solo como alternativa secundaria.
* **Modals**: Usar `MatDialog` para flujos de edición rápidos. Evitar navegaciones innecesarias para cambios de un solo campo.

---

## 🔒 4. Security & Data Integrity

### 4.1 Security Rules
* **No Hardcoded Credentials**: Uso estricto de variables de entorno.
* **Validation**: Validación doble (Frontend para UX, Backend para seguridad).
* **Sanitization**: Prohibido `innerHTML` con datos del usuario. Usar binding de propiedades de Angular.

### 4.2 Data Types
| Legacy | SQLite | TypeScript | Prisma |
| :--- | :--- | :--- | :--- |
| `Long` | `INTEGER` | `number` | `Int` |
| `Currency` | `REAL` | `number` | `Decimal` |
| `Date` | `TEXT (ISO)` | `Date` | `DateTime` |
| `Boolean` | `INTEGER (0/1)`| `boolean` | `Boolean` |

---

## 🧪 5. Testing Standards (Strict)

### 5.1 Backend Testing
* **Tool**: Jest + `supertest`.
* **Coverage**: 100% Endpoint coverage mandated.
* **Pattern**: Integration tests must spin up a real ephemeral Express app.

### 5.2 Frontend Testing (Component)
* **Tool**: Jest + `Angular Component Harnesses`.
* **Forbidden**: `fixture.nativeElement.querySelector`. Interaction MUST happen via Harnesses.
* **Mocking**: Signal overrides must be used for input setups.

---

## 🩺 6. Self-Healing & Refactoring Axioms (Agent Guidelines)

### 6.1 Fixer Agent Rules
* **Composition > Inheritance**: Never create base classes to share logic; use Composition or Services.
* **Strict Typing**: If an object type is unknown, use `unknown` and cast via Zod/Guard, never `any`.
* **Signals**:
    * Prefer `output()` over `@Output() + EventEmitter`.
    * Prefer `viewChild()` over `@ViewChild`.
    * Prefer `input()` over `@Input()`.

---

## 🚦 7. Inter-Phase Gate Conditions (CI/CD)

Ningún desarrollo pasará a la siguiente fase sin cumplir estos criterios:

### Gate 1: Análisis → Backend
* Inventory, Schema y Metrics generados correctamente.
* Reportes JSON de auditoría disponibles en `audit-report.json`.

### Gate 2: Backend → Frontend
* 0 errores de compilación en `tsc --noEmit`.
* Auditoría de seguridad sin hallazgos críticos.

### Gate 3: Frontend → Testing
* **Linter**: `ng lint` con 0 errores.
* **A11y**: Auditoría de accesibilidad básica aprobada.
* **Coverage**: Mínimo **80% de cobertura global** (Jest).

### Gate 4: Deploy Final
* **Parity Check**: Confirmación de paridad de campos al 100% mediante `parity_checker.py`.
* **Build**: Compilación de producción exitosa.

---

## 🚫 Prohibited Patterns Summary
* ❌ `import 'zone.js'`
* ❌ `any` en TypeScript
* ❌ `ngOnInit` para carga de datos (Usar constructor + logic/effects)
* ❌ `setTimeout` para sincronización de estados
* ❌ `On Error Resume Next` (Usar `try/catch` centralizado)