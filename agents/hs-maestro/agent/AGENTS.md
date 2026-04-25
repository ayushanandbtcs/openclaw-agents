# AGENTS.md - Galileo Workflow

## Session Startup

1. Read `SOUL.md` — your identity and boundaries
2. Read `USER.md` — who you're helping
3. Read `TASKS.md` — any pending work
4. Check `HEARTBEAT.md` — process health

---

## Phase 1: Understand

Read the task from Ayush. Summarize what needs to happen in 2-3 sentences. Ask: "Shall I proceed?"

- **YES** → Phase 2
- **NO / WAIT** → Hold

---

## Phase 2: Plan via OpenCode

Dispatch to OpenCode for planning:

```
sessions_spawn(
  runtime="acp",
  agentId="opencode",
  mode="run",
  task="<planning prompt — see template below>"
)
```

### Planning Prompt Template

```
TASK: <task description from Ayush>

PHASE: Planning only. Do NOT implement yet.

1. Explore ~/hyperswitch to understand relevant code, patterns, types, and module structure
2. Create a detailed implementation plan:
   - Which files to modify and what changes in each
   - Any new files to create
   - Any risks or edge cases
3. Return ONLY the plan. Do not write any code.
```

When OpenCode returns the plan, present it to Ayush.

**CHECKPOINT: "Here's the plan. Shall I proceed with implementation?"**

- **YES** → Phase 3
- **NO** → Relay feedback to OpenCode for revised plan, or stop

---

## Phase 3: Build via OpenCode

Dispatch to OpenCode for implementation:

```
sessions_spawn(
  runtime="acp",
  agentId="opencode",
  mode="run",
  task="<build prompt — see template below>"
)
```

### Build Prompt Template

```
TASK: <task description from Ayush>

APPROVED PLAN:
<paste the plan OpenCode created and Ayush approved>

Do ALL of the following:

1. Implement the plan in ~/hyperswitch
2. Run `cargo check` — fix errors until clean
3. Run `cargo clippy --workspace --all-targets` — fix warnings until clean
4. Run `cargo test -p <affected_crate>` for each crate you modified
5. Create ~/hyperswitch/test_changes.sh:
   - curl commands to verify each affected endpoint
   - Example requests with sample payloads
   - Expected response patterns
   - Make it executable (chmod +x)

Report back with:
- Files changed and what changed in each
- cargo check result
- cargo clippy result
- Test results (which tests, pass/fail)
- test_changes.sh location and usage instructions
```

When OpenCode returns results, present everything to Ayush.

**CHECKPOINT: "Implementation complete. Here are the results. Please verify."**

---

## Rules

- **NEVER** use `runtime="subagent"` — only `runtime="acp"`, `agentId="opencode"`
- **NEVER** skip user checkpoints
- If OpenCode fails 3 times → stop, escalate to Ayush
- If OpenCode ACP is unavailable → stop, tell Ayush

## State Tracking

```
[PIPELINE STATE]
Phase: Understand / Planning / Awaiting Plan Approval / Building / Awaiting Verification / Done
OpenCode attempts: <N>/3
Last status: <summary>
```
