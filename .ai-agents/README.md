# AI Agent Framework

Multi-agent collaboration framework for software development.

## Directory Structure

```
.ai-agents/
├── config.yaml           # Unified configuration
├── config.schema.json    # JSON Schema for validation
├── SECURITY.md           # Security and governance
├── agents/               # Agent definitions
│   ├── _base.md          # Common agent behavior
│   ├── _templates/       # Agent scaffolding templates
│   ├── {agent}.yaml      # Declaration (roles, skills, commands)
│   └── {agent}.prompt.md # Behavior prompts
├── skills/               # Modular capabilities
│   └── {skill}.md        # Skill definitions
├── workflows/            # Workflow state machines
│   └── {workflow}.yaml   # Workflow definitions
├── knowledge/            # Domain knowledge
│   ├── core/             # Core principles (with manifest.yaml)
│   ├── patterns/         # Architecture patterns (with manifest.yaml)
│   ├── principle/        # Project coding standards
│   └── project/          # Project-specific knowledge
└── workspace/            # Project working area
    ├── context.yaml      # Dynamic memory with state history
    ├── requirements/     # Requirements documents
    └── changes/          # Change tracking (90-day retention)
```

## Configuration

All configuration is centralized in `config.yaml` (validated by `config.schema.json`):

- **system**: Behavior settings (language, interaction mode, debug mode)
- **output**: Output formatting rules
- **pattern**: Active architecture pattern (DDD, Clean Architecture, etc.)
- **agents**: Registered agents with their skills
- **skills**: Available skills with agent assignments
- **workflows**: Defined workflows
- **knowledge**: Knowledge loading order and lazy-load rules

## Agents

Each agent has two files plus a common base:

1. **`_base.md`**: Common activation steps and behavior rules
2. **`{agent}.yaml`**: Declarative definition
   - ID, name, responsibilities
   - Boundaries (what the agent does NOT do)
   - Skills it can use
   - Commands it responds to

3. **`{agent}.prompt.md`**: Behavior prompt
   - Persona and communication style
   - Activation steps (referencing _base.md)
   - Command implementations
   - Boundary enforcement with examples
   - Output formats

## Skills

Skills are modular capabilities loaded on-demand:
- `review-execution.md` - Execute review checklists
- `test-generation.md` - Generate test cases
- `project-initialization.md` - Initialize project and analyze structure

## Workflows

Workflows define phase transitions:

- **requirement-to-code**: Full development cycle
  - analyze → design → implement → review → test

- **code-review**: Code quality review
  - analyze → review → report

## Dynamic Memory

`workspace/context.yaml` stores:

- Project information
- Current workflow state with phase history
- Session lock for concurrent access control
- Requirements summary
- Architecture decisions
- Implementation progress

**Rules**:
- Confirm with user before saving
- Keep information concise
- Update incrementally
- Record phase transitions with timestamps
- See `SECURITY.md` for permissions and retention

## Usage

1. Start with `#init` to initialize project analysis
2. Use `#start` to begin a workflow
3. Follow prompts and confirm transitions
4. Use specific commands (`#analyze`, `#design`, etc.) to invoke agents
5. Check `#status` to see current progress
6. Use `#pattern {name}` to switch architecture patterns
7. Use `#recover` if workflow enters error state
8. Use `#debug on` for verbose troubleshooting

## Extending

### Add Custom Agent

1. Copy templates from `agents/_templates/`
2. Create `agents/{name}.yaml` with definition
3. Create `agents/{name}.prompt.md` with behavior
4. Register in `config.yaml` under `agents`
5. Create `.github/agents/{name}.md` for GitHub Copilot

See `agents/_templates/README.md` for detailed instructions.

### Add Custom Skill

1. Create `skills/{name}.md` with skill definition
2. Register in `config.yaml` under `skills.core` or `skills.custom`
3. Add platform adapter in `.github/skills/{name}/SKILL.md`

### Add Architecture Pattern

1. Create `knowledge/patterns/{pattern}/` directory
2. Add `manifest.yaml` with pattern metadata
3. Add pattern documentation (overview.md, review-checklist.md)
4. Register in `config.yaml` under `pattern.available`
