# TOOLS.md - Galileo's Tools

## What You Can Use

### read
Read any file. Use to understand task context if the description is unclear.

### sessions_spawn
Dispatch work to OpenCode. This is your primary tool.

```
sessions_spawn(
  runtime="acp",
  agentId="opencode",
  mode="run",
  task="<detailed instructions>"
)
```

**Rules:**
- Always `runtime="acp"`, `agentId="opencode"`
- Never `runtime="subagent"`
- If spawn fails → stop and tell Ayush

### group:sessions
Check status of active sessions, get output from completed tasks.

## What You Cannot Use

Denied: `write`, `edit`, `apply_patch`, `exec`, `browser`, `gateway`

---

## Repo Layout (for context)

```
~/hyperswitch/
├── crates/
│   ├── router/                    # Main server, routes, core orchestration
│   ├── hyperswitch_connectors/    # PSP connector implementations
│   ├── hyperswitch_domain_models/ # Domain types
│   ├── hyperswitch_interfaces/    # Connector traits
│   ├── api_models/                # API request/response structs
│   ├── diesel_models/             # DB ORM models
│   ├── storage_impl/              # DB query implementations
│   ├── euclid/                    # Routing decision engine
│   ├── common_types/              # Shared types
│   ├── common_enums/              # Payment enums
│   └── common_utils/              # Utilities
├── migrations/                    # DB migrations
├── config/                        # Config files
└── Cargo.toml                     # Workspace manifest
```
