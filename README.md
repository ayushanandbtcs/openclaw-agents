# OpenClaw Multi-Agent System

Real agent definitions powering the automation workflow.

## Multi-Agent Architecture

```
                    ┌─────────────────────────────────┐
                    │         USER REQUEST            │
                    └─────────────┬───────────────────┘
                                  │
                                  ▼
                    ┌─────────────────────────────────┐
                    │      HS-MAESTRO                 │
                    │   Orchestrates entire workflow  │
                    │   Dispatches to agents          │
                    └─────────────┬───────────────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
        ┌─────────────────────┐   ┌─────────────────────┐
        │   PLANNER AGENT     │   │   MYCROFT AGENT     │
        │   Creates plan      │   │   Researches/       │
        │   Decomposes tasks  │   │   Investigates      │
        └──────────┬──────────┘   └─────────────────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │   CODER AGENT       │
        │   Implements code   │
        │   Writes tests      │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │   REVIEWER AGENT    │
        │   Checks quality    │
        │   Finds issues      │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │   CRITIC AGENT      │◄── "Prove it to me"
        │   Gatekeeper        │    "Show me evidence"
        │   Blocks until      │    "Why not alternative?"
        │   convinced         │
        └──────────┬──────────┘
                   │ (approved)
                   │
                   ▼
        ┌─────────────────────┐
        │   BACK TO MAESTRO   │
        │   Create PR         │
        └─────────────────────┘
```

## The Agents

### 1. HS-Maestro Agent (Orchestrator) ⭐ FIRST
**Purpose:** Coordinates the entire workflow - receives request and dispatches to other agents

**Responsibilities:**
- Receives user requests
- Decides which agents to invoke
- Manages workflow state
- Handles handoffs between agents
- Creates final output (PRs, etc.)

**Files:**
- [AGENTS.md](agents/hs-maestro/agent/AGENTS.md) - Guidelines and rules
- [SOUL.md](agents/hs-maestro/agent/SOUL.md) - Core identity and principles
- [IDENTITY.md](agents/hs-maestro/agent/IDENTITY.md) - Role definition
- [TOOLS.md](agents/hs-maestro/agent/TOOLS.md) - Tool capabilities
- [BOOTSTRAP.md](agents/hs-maestro/agent/BOOTSTRAP.md) - Initialization
- [HEARTBEAT.md](agents/hs-maestro/agent/HEARTBEAT.md) - Periodic tasks
- [USER.md](agents/hs-maestro/agent/USER.md) - User context

---

### 2. Planner Agent
**Purpose:** Breaks complex tasks into executable steps

**Workflow:**
1. Understand requirements
2. Decompose into atomic tasks
3. Map dependencies
4. Assign to appropriate agents
5. Validate feasibility

**See:** [agents/planner/SOUL.md](agents/planner/SOUL.md)

---

### 3. Mycroft Agent
**Purpose:** Researches, investigates, analyzes - runs in parallel with planning

**Responsibilities:**
- Codebase exploration
- Bug investigation
- Pattern recognition
- Solution comparison
- Documentation search

**See:** [agents/mycroft/SOUL.md](agents/mycroft/SOUL.md)

---

### 4. Coder Agent  
**Purpose:** Generates and modifies code

**Workflow:**
1. Analyze requirements from plan
2. Design solution
3. Implement incrementally
4. Write tests
5. Document APIs
6. Submit for review

**See:** [agents/coder/SOUL.md](agents/coder/SOUL.md)

---

### 5. Reviewer Agent
**Purpose:** Validates code quality and catches issues

**Checks:**
- Code quality (naming, structure, duplication)
- Security (secrets, injection, XSS)
- Architecture (SOLID, dependencies)
- Testing (coverage, edge cases)

**See:** [agents/reviewer/SOUL.md](agents/reviewer/SOUL.md)

---

### 6. Critic Agent
**Purpose:** Gatekeeper who blocks workflow until convinced work is correct

**Philosophy:** Trust but verify - other agents must prove correctness

**Process:**
1. Challenges all submissions
2. Demands evidence and proof
3. Questions assumptions
4. Requires edge case handling
5. Only approves when convinced

**Power:**
- Can reject any agent's work
- Sends back for revision
- Escalates to Maestro if disagreements

**See:** [agents/critic/SOUL.md](agents/critic/SOUL.md)

---

## Example Workflow

### PR Creation Flow

```
User: "Add JWT authentication"
    │
    ▼
┌─────────────────────────────────────┐
│ 0. MAESTRO receives request         │
│    - Decides which agents to invoke │
│    - Starts workflow                │
└─────────────────────────────────────┘
    │
    ├─────────────────────────────────┐
    │                                 │
    ▼                                 ▼
┌──────────────────────┐  ┌──────────────────────────┐
│ 1a. PLANNER          │  │ 1b. MYCROFT (parallel)   │
│    Creates plan:     │  │    Searches codebase:    │
│    - Auth schema     │  │    - Existing patterns   │
│    - Middleware      │  │    - Similar features    │
│    - Login endpoint  │  │    - Best practices      │
│    - Tests           │  │                          │
└──────────┬───────────┘  └────────────┬─────────────┘
           │                           │
           └───────────┬───────────────┘
                       │
                       ▼
┌─────────────────────────────────────┐
│ 2. CODER implements each task       │
│    - Generates code                 │
│    - Writes tests                   │
│    - Adds documentation             │
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│ 3. REVIEWER validates code          │
│    - Scans for security issues      │
│    - Checks code quality            │
│    - Verifies test coverage         │
│    Score: 8.5/10                    │
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│ 4. CRITIC challenges everything     │
│    Critic: "Prove this is secure"   │
│    Coder: "bcrypt + rate limiting"  │
│    Critic: "Show me the tests"      │
│    [Coder shows evidence]           │
│    Critic: "Approved with caution"  │
└─────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────┐
│ 5. BACK TO MAESTRO                  │
│    - Creates branch                 │
│    - Commits changes                │
│    - Opens Pull Request             │
│    - Assigns reviewers              │
└─────────────────────────────────────┘
    │
    ▼
GitHub: PR #456 created successfully!
```

---

## Directory Structure

```
agents/
├── coder/
│   └── SOUL.md          # Code generation principles
├── planner/
│   └── SOUL.md          # Task decomposition rules
├── reviewer/
│   └── SOUL.md          # Code review checklist
├── critic/
│   └── SOUL.md          # Gatekeeper that blocks until convinced
├── mycroft/
│   └── SOUL.md          # Investigation methodology
└── hs-maestro/
    └── agent/
        ├── AGENTS.md    # Guidelines
        ├── SOUL.md      # Core identity
        ├── IDENTITY.md  # Role definition
        ├── TOOLS.md     # Tools available
        ├── BOOTSTRAP.md # Startup logic
        ├── HEARTBEAT.md # Background tasks
        └── USER.md      # User preferences
```

---

## Security Notice

This repository contains **only** agent behavior definitions:
- ✅ Markdown documentation
- ✅ Agent personalities and workflows
- ✅ Checklists and guidelines

**Excluded for security:**
- ❌ JSON configs (contain API keys)
- ❌ Session logs (private)
- ❌ Model endpoints
- ❌ Authentication credentials

---

## How OpenClaw Uses These

1. **At startup**, OpenClaw loads these SOUL.md files to understand each agent's purpose
2. **During execution**, agents reference their guidelines to determine how to act
3. **HS-Maestro** coordinates handoffs between agents based on the workflow
4. **All agents** communicate through OpenCode sessions to interact with repositories

The agents work together to automate the entire development lifecycle from planning to deployment.
