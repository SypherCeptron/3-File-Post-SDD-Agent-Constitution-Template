# Unfiltered Post-SDD Inbox (`UNFILTERED-AGENT.md`)
> **Role:** High-volatility scratchpad (BMAD `Dev Agent Record`).
> **Rule:** Immediately after implementing any SDD spec, dump raw learnings here **before** closing the task. Do **NOT** edit `AGENT.md` directly from raw implementation thoughts.

---

## Active Post-Spec Dump Template
*(Copy/fill this block at the end of each spec implementation, then triage items into Code Comments, `PARKED.md`, or Discard.)*

### Spec: `[e.g., spec-03-notifications]` — Date: `[YYYY-MM-DD]`

#### 1. Spec vs. Reality Deviations
*Where did the written `spec.md` or `plan.md` make an assumption that turned out to be false in the actual codebase?*
- `[e.g., Spec assumed User table had a timezone column; had to read from UserPreferences relation instead.]`

#### 2. Debug Friction & Repeated Tooling/Test Failures
*What caused wasted turns, failed test runs, or human corrections during this implementation?*
- `[e.g., Integration test failed 3 times because Redis mock wasn't cleared between vitest runs.]`

#### 3. Discovered Codebase Quirks & Patterns
*Undocumented conventions or traps discovered while reading/modifying existing code.*
- `[e.g., Queue worker silently drops jobs if payload contains raw Date objects instead of ISO strings.]`

#### 4. Triage Action Taken (Check off to clear inbox)
- [ ] **Single-file quirk?** Added inline comment directly in the code file & deleted from inbox.
- [ ] **Reusable pattern (1st time seen)?** Moved to `PARKED.md` (`[Seen: 1/2]`).
- [ ] **Matched existing item in `PARKED.md` (`Seen: 2/2`)?** Promoted to `AGENT.md` Shard 3.
- [ ] **One-off noise?** Deleted from this file.
