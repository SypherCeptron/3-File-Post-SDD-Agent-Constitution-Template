# How to Use the 3-File Agent Constitution System in Any AI Project

This repository provides a **3-file memory and governance template** (`AGENT.md`, `PARKED.md`, `UNFILTERED-AGENT.md`) for **Spec-Driven Development (SDD)**.

It solves a common problem in AI-assisted projects: **how to capture what the AI learned after implementing a spec without turning your project's `AGENT.md` into a bloated dumping ground of random, one-off fixes.**

---

## 1. What Are the 3 Files?

1. **[`constitution/AGENT.md`](./constitution/AGENT.md) — The Constitution (Hard Project Law)**
   - Read by the AI at the **start of every task**.
   - Contains the governance rules and 3 core shards (*Tech Stack & Commands*, *Source Tree & Boundaries*, *Non-Obvious Coding Standards*).
   - **Strict Gatekeeping:** Only accepts cross-cutting rules proven across **2+ specs** (`Seen >= 2`) or critical architectural boundaries. Capped at 150 lines.

2. **[`constitution/PARKED.md`](./constitution/PARKED.md) — The Incubator & Waiting Room**
   - Read by the AI **before planning a new spec** and **during post-spec triage**.
   - Holds reusable patterns that have only been seen **once** (`Seen: 1/2`) while waiting to see if they repeat in a future spec, plus deferred architectural rules and demoted/archived rules.

3. **[`constitution/UNFILTERED-AGENT.md`](./constitution/UNFILTERED-AGENT.md) — The Post-SDD Inbox**
   - Written by the AI **immediately after finishing a spec implementation**.
   - Captures raw *Spec vs. Reality Deviations*, *Debug Friction*, and *Discovered Codebase Quirks* before they are triaged.

---

## 2. Step-by-Step: Setting Up in Another AI Project

### Step 1: Copy the `constitution/` Folder (or the 3 Files) into Your Project
Copy the `constitution/` folder (containing `AGENT.md`, `PARKED.md`, and `UNFILTERED-AGENT.md`) into your target repository:

```bash
cp -r constitution/ /path/to/your-project/
```

### Step 2: Connect to Your AI Coding Tool
Depending on which AI coding assistant you use in that project, point it to `AGENT.md`:
- **Claude Code:** Rename or symlink `AGENT.md` to `CLAUDE.md` (or add `@AGENT.md` inside `CLAUDE.md`).
- **Cursor / Windsurf / Codex / Antigravity:** Rename or symlink `AGENT.md` to `AGENTS.md` (or reference `AGENT.md` in `.cursor/rules/`).
- **Cline / Roo Code:** Add `"Always read AGENT.md at the start of every task"` in Custom Instructions.

### Step 3: Fill In Shards 1 & 2 for Your Project
Open `AGENT.md` in your project and replace the bracketed `[e.g., ...]` placeholders in:
- **Shard 1 (Tech Stack, Tooling & Exact Commands):** Your package manager, exact build/typecheck commands, test commands, and banned libraries.
- **Shard 2 (Source Tree & Architectural Boundaries):** Your folder structure and which folders are forbidden from importing each other.

*(Leave Shard 3 empty at the start of a new project—it will grow organically as you complete specs.)*

---

## 3. Daily Workflow: How to Use It Across Specs

### Phase A: Before Writing a New Spec or Plan
Prompt your AI agent:
> *"Read `AGENT.md` and `PARKED.md` before drafting the spec/plan for `<feature-name>`."*

- `AGENT.md` ensures the spec respects your permanent architectural boundaries.
- `PARKED.md` reminds the AI of incubating patterns (`Seen: 1/2`) and checks whether any deferred rule (`PARK-XX`) should now be unparked for this milestone.

### Phase B: During Spec Implementation
- The AI reads **only `AGENT.md`** at the start of coding tasks.
- It is **forbidden** from editing `AGENT.md` while mid-flight on coding tasks.

### Phase C: Post-SDD Spec Implementation (The Learning Loop)
Right after your spec implementation passes tests, run this single prompt before closing the branch/PR:

> *"We just finished implementing `<spec-name>`. Follow the Post-SDD Update Protocol in `AGENT.md`: log raw learnings into `UNFILTERED-AGENT.md`, triage reusable patterns into `PARKED.md`, and promote any rule that has now reached `Seen >= 2` into `AGENT.md`."*

What the AI will automatically do:
1. **Dump Raw Learnings (`UNFILTERED-AGENT.md`):** Write down where the spec differed from codebase reality, what caused test/debug friction, and any hidden quirks found.
2. **Filter Out Noise:**
   - If a quirk only affects one file → it adds a code comment in that file and deletes it from the inbox.
   - If it was a random one-off typo/bug → it deletes it from the inbox.
3. **Incubate New Patterns (`PARKED.md`):**
   - If a lesson looks reusable across future specs but this is the **first time** it happened → it moves to `PARKED.md` with `Seen: 1/2`.
4. **Promote Proven Laws (`AGENT.md`):**
   - If a lesson matches an existing `1/2` candidate in `PARKED.md` (hitting `2/2`), the AI distills it into a 1–2 line `"DO X / NEVER Y"` rule in `AGENT.md` Shard 3 and logs the amendment.

---

## 4. Visual Summary of the Funnel

```text
After Spec Implementation
          │
          ▼
[ UNFILTERED-AGENT.md ]  (1. Dump raw Spec Deviations, Debug Friction, Quirks)
          │
          ├── Single-file quirk? ──────► Put comment in code file & discard
          ├── Random 1-off error? ─────► Discard
          │
          ▼
    [ PARKED.md ]        (2. First time seeing a reusable pattern? Park as Seen: 1/2)
          │
          ├── Seen a 2nd time in a later spec (Seen: 2/2)?
          ▼
    [ AGENT.md ]         (3. Promote to Shard 3 as permanent 1-line DO/NEVER rule)
```

---

## License
MIT — see [LICENSE](./LICENSE).
