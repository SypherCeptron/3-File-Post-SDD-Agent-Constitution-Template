# Parked & Incubating Rules (`PARKED.md`)
> **Role:** Middle tier between raw spec takeaways (`UNFILTERED-AGENT.md`) and hard project law (`AGENT.md`).
> **When to Read:** Before drafting a new SDD `spec.md`/`plan.md`, and during Post-SDD Triage.

---

## 1. Incubating Candidate Rules (Waiting for 2nd Validation)
*Patterns discovered during a single spec that look reusable, but need confirmation in at least one more spec (`Seen >= 2`) before promotion to `AGENT.md`.*

| ID | Candidate Rule (Imperative Draft) | Reason / Context | Seen Count | Specs Observed |
| :--- | :--- | :--- | :---: | :--- |
| `CAND-01` | `[e.g., Always wrap webhook handlers in idempotency middleware before parsing body]` | `[e.g., Stripe retries caused duplicate state transitions during local testing]` | `1/2` | `spec-01-billing` |
| `CAND-02` | `[e.g., Prefer cursor-based pagination over offset for all public list endpoints]` | `[e.g., Offset query degraded on joined tables]` | `1/2` | `spec-02-feed` |

---

## 2. Deferred Architectural Decisions (Parked for Future Phase)
*Valid rules or constraints intentionally paused until a specific milestone, scale threshold, or refactor.*

| ID | Parked Rule / Decision | Trigger to Unpark | Parked On | Source Spec |
| :--- | :--- | :--- | :--- | :--- |
| `PARK-01` | `[e.g., Enforce strict multi-tenant row-level security (RLS) on all tables]` | `[e.g., When B2B org/team workspaces spec starts]` | `2026-10-24` | `spec-01-auth` |

---

## 3. Demoted / Deprecated Rules (Archive)
*Rules removed from `AGENT.md` because tooling now enforces them automatically or the architecture changed.*

- `[e.g., Demoted 2026-10-24: "Never use console.log in src/" -> Now enforced automatically by ESLint no-console rule.]`
