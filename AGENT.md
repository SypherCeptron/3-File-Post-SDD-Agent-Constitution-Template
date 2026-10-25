# Project Constitution (`AGENT.md`)
> **Version:** `0.1` | **Max Cap:** `150 lines` | **Scope:** Global Project Law

I am an expert software engineer whose memory resets completely between sessions. Because I rely entirely on repository memory to prevent architectural drift, I **MUST** read `AGENT.md` at the start of **EVERY** task—this is not optional.

To prevent this Constitution from rotting with random one-off fixes, this project uses a **3-File Post-SDD Memory Funnel**.

---

## 1. The 3-File Memory Architecture

| File | Volatility | When to Read | When to Write |
| :--- | :--- | :--- | :--- |
| **`AGENT.md`** *(The Constitution)* | **Low** *(Hard Law)* | **Start of EVERY task** (Planning, Coding, Review). | **ONLY** via Promotion from `PARKED.md` (or explicit human directive). Never dump raw spec notes here. |
| **`PARKED.md`** *(The Incubator)* | **Medium** *(Staging)* | Before writing a new Spec/Plan, and during Post-SDD Triage. | When a reusable pattern is seen **once** (`[Seen: 1]`), or when an architectural rule is deferred to a future milestone. |
| **`UNFILTERED-AGENT.md`** *(Post-SDD Inbox)* | **High** *(Scratchpad)* | During Post-SDD Triage / Retrospectives. | **Immediately after implementing a Spec** (Dev Agent Record: deviations, debug friction, codebase quirks). |

---

## 2. Constitutional Governance (What Enters `AGENT.md`)

### A. The 4 Admission Gates (ALL must be true to enter `AGENT.md`)
1. **Cross-Cutting:** Applies across multiple modules/specs, not just the feature or file just built.
2. **Non-Obvious to Default LLM Training (BMAD Rule):** Document ONLY what an AI would guess wrong by default. Do not document standard framework behavior or things obvious from `package.json`/types.
3. **Not Enforced by Tooling:** If a linter, formatter, or compiler check already catches it, put the rule in the linter config—not here.
4. **Imperative & Compact:** Must be written as a 1–2 line `"DO X / NEVER Y (Reason)"` rule—never a narrative war story.

### B. Explicitly Banned from `AGENT.md`
- ❌ One-off bug fix stories or debugging logs *(keep in `UNFILTERED-AGENT.md` or git commit messages)*.
- ❌ Single-file quirks *(put a code comment directly in that file instead)*.
- ❌ Feature progress, task checklists, or current sprint status *(belongs in your SDD `spec.md` / `tasks.md`)*.
- ❌ Unproven patterns seen in only a single spec *(belongs in `PARKED.md` until validated a second time)*.

### C. The Post-SDD Update Protocol (End of Every Spec Implementation)
1. **Step 1 — Log Raw Reality (`UNFILTERED-AGENT.md`):** Record `Spec Deviations`, `Debug Friction`, and `Discovered Quirks` from the spec just completed.
2. **Step 2 — Triage & Cross-Check (`PARKED.md`):**
   - Discard one-off noise or move single-file quirks into code comments.
   - Check if any new learning matches an existing candidate in `PARKED.md`.
   - If it's a **new** reusable pattern, move it to `PARKED.md` with `[Seen: 1 | Spec: <spec-id>]`.
3. **Step 3 — Promote or Prune (`AGENT.md`):**
   - If a candidate in `PARKED.md` hits **`Seen >= 2`** across specs (or is a critical architectural boundary), distil it into a 1-line imperative rule in Section 3 below.
   - **Cap Enforcement:** If `AGENT.md` exceeds **150 lines**, you MUST merge redundant rules or demote a stale rule back to `PARKED.md` before adding a new one.

---

## 3. Constitutional Shards (Project Law)

### Shard 1: Tech Stack, Tooling & Exact Commands
*Only list pinned constraints, non-standard commands, and banned dependencies.*
- **Runtime & Package Manager:** `[e.g., Node 22+ / pnpm only — NEVER run npm or yarn]`
- **Build / Typecheck:** `[e.g., pnpm check — run before marking any task complete]`
- **Test Execution:** `[e.g., pnpm test:unit <path> — NEVER run full integration suite without flag]`
- **Banned Packages / APIs:** `[e.g., Do not introduce axios or moment; use native fetch and date-fns]`

### Shard 2: Source Tree & Architectural Boundaries
*Where code lives and strict import/dependency direction rules.*
- **Directory Ownership:**
  - `[e.g., src/domain/ -> Pure business logic; ZERO framework or DB imports allowed]`
  - `[e.g., src/infra/  -> External adapters, DB repositories, third-party SDKs]`
- **Boundary Invariants:**
  - `[e.g., UI components must NEVER import Prisma models or repository classes directly]`

### Shard 3: Non-Obvious Coding Standards & Anti-Patterns
*Proven rules promoted from `PARKED.md` (`[Promoted from: <spec-ids>]`).*
- **Error Handling:** `[e.g., Return typed Result<T, E> from domain services; NEVER throw raw Error across module boundaries. (Promoted: spec-01, spec-03)]`
- **Database / State:** `[e.g., Always pass explicit transaction context (tx) to multi-write repository methods. (Promoted: spec-02, spec-04)]`
- **Testing Traps:** `[e.g., Use vitest-mock-extended for repository mocks; NEVER hand-roll partial object literals. (Promoted: spec-01, spec-02)]`

---

## 4. Constitutional Amendment Log
| Version | Date | Spec Trigger | Amendment Summary |
| :--- | :--- | :--- | :--- |
| `0.1` | `2026-10-25` | `init` | Initialized 3-file Post-SDD Constitution template. |
