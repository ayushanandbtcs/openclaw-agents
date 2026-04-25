# OpenClaw Agent Configurations

Real agent definition files from OpenClaw automation system.

## What's Included

This repository contains the markdown documentation and configuration files that define how each agent behaves. **No API keys or sensitive data included.**

### Agents

#### 1. hs-maestro (Orchestrator)
The main coordinator agent that manages workflow execution.
- `AGENTS.md` - Agent guidelines and red lines
- `SOUL.md` - Core personality and principles  
- `IDENTITY.md` - Role definition
- `TOOLS.md` - Available tools and capabilities
- `BOOTSTRAP.md` - Initialization instructions
- `HEARTBEAT.md` - Periodic task definitions
- `USER.md` - User preferences and context

#### 2. coder
Specialized for code generation and modification.

#### 3. planner  
Decomposes complex tasks into executable steps.

#### 4. reviewer
Performs code quality analysis and review.

#### 5. mycroft
Intelligence and analysis agent.

## Agent Structure

Each agent contains:
```
agent/
├── AGENTS.md      # Guidelines and rules
├── SOUL.md        # Core identity and principles
├── IDENTITY.md    # Role definition
├── TOOLS.md       # Tool definitions
├── BOOTSTRAP.md   # Startup instructions
├── HEARTBEAT.md   # Background tasks
└── USER.md        # User context
```

## Security Note

- ❌ API keys (stored separately in auth-profiles.json)
- ❌ Session logs (private to deployment)
- ❌ Model configurations (contain endpoints)
- ✅ Only documentation and behavior definitions

These files define **what** agents do, not **how** they authenticate.

## Usage

These configurations power OpenClaw's multi-agent automation system, allowing specialized agents to:

1. **Plan** - Break down complex tasks
2. **Code** - Generate and modify code  
3. **Review** - Analyze quality
4. **Orchestrate** - Coordinate workflow

See individual agent directories for their specific capabilities and behaviors.
