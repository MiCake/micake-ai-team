# Agent Base Template

This document defines the common activation steps and behavior rules that all agents should follow.

## Common Activation Steps

All agents MUST perform these steps on activation:

### Step 1: [AUTO] Load Registry
- System automatically loads `registry.yaml`
- Provides quick access to all resources
- No LLM action needed

### Step 2: [AUTO] Load Context Contract
- System reads current agent's `context_contract` from `{agent}.yaml`
- Identifies required and conditional sources
- Validates required sources exist

### Step 3: [AUTO] Execute Context Loader
- Load all `required` sources based on context_contract
- Generate summaries for resources exceeding 2000 tokens
- Update `workspace/state/knowledge-cache.yaml`
- Report missing resources to LLM

### Step 4: [LLM] Verify Context
- Confirm critical context is loaded
- Request additional context if needed via `conditional` sources
- Check `workspace/state/session.yaml` for current workflow state

### Step 5: [LLM] Acknowledge Boundaries
- Confirm understanding of role from `{agent}.yaml`
- Acknowledge what this agent does NOT do
- If request is outside boundaries, suggest appropriate agent
- Ready to process user request

## Context Contract

Each agent defines its context requirements in `{agent}.yaml`:

```yaml
context_contract:
  required:
    - source: knowledge/core/
      reason: "Core principles"
      
  conditional:
    - source: knowledge/patterns/{active}/
      condition: "When architecture patterns needed"
      
  outputs:
    - target: workspace/context/{file}.yaml
      format: yaml
```

## Knowledge Loading Levels

| Level | Description                   | When to Use         |
| ----- | ----------------------------- | ------------------- |
| 1     | Manifest only                 | Get overview        |
| 2     | Targeted (via semantic_index) | Specific tasks      |
| 3     | Full loading                  | Full knowledge need |

## Common Behavior Rules

### Context Updates

When modifying workspace files:

1. **Always confirm** with user before saving
2. **Update incrementally** - only modify relevant sections
3. **Record timestamp** using ISO 8601 format
4. **Use correct tier**:
   - `state/` - Current session data (hot)
   - `context/` - Project context (warm)
   - `artifacts/` - Work products per change

**State Updates** (`workspace/state/`):
```yaml
# session.yaml
session:
  last_agent: "{agent_id}"
workflow:
  current_phase: "{phase}"
```

**Context Updates** (`workspace/context/`):
```yaml
# architecture.yaml - append decision
decisions:
  - topic: "{topic}"
    choice: "{choice}"
    date: "{ISO date}"
    reason: "{reason}"
```

### Output Rules

Follow output rules from `config.yaml`:

- `output.no_emojis`: Do not use emojis if true
- `output.use_mermaid`: Use Mermaid for diagrams if true
- `output.data_format`: Use yaml or json for structured data
- `output.use_xml_tags`: Use `<thought>` and `<output>` tags if true
- `output.max_description`: Keep descriptions under this limit

### Next Step Guidance

At the end of every response, suggest the next logical action:

```markdown
---
**Suggested Next Steps**: 
- [Relevant next action 1]
- [Relevant next action 2]
```

## Directory Discovery Protocol 

When exploring an unknown directory within the framework, follow this protocol:

### Step 1: Check Registry (Preferred)
```
READ registry.yaml → quick_index
IF resource found in quick_index:
    RETURN resource_path (fastest path)
```

### Step 2: Check Directory Index
```
IF _index.yaml exists in target directory:
    PARSE _index for structure and contents
    RETURN indexed resources
```

### Step 3: Check Manifest
```
IF manifest.yaml exists in directory:
    PARSE manifest for structure and loading rules
    RETURN manifest-defined resources
```

### Step 4: Fallback Discovery
```
LIST directory contents
INFER structure from naming conventions:
- {name}.yaml + {name}.prompt.md in agents/ = Agent definition
- {name}.md in skills/ = Skill definition (check frontmatter)
- {name}.yaml in workflows/ = Workflow definition
```

### Discovery Quick Reference

| Directory            | Primary Method                       | Index File    |
| -------------------- | ------------------------------------ | ------------- |
| Root                 | registry.yaml                        | registry.yaml |
| `agents/`            | _index.yaml                          | _index.yaml   |
| `skills/`            | _index.yaml                          | _index.yaml   |
| `workflows/`         | _index.yaml                          | _index.yaml   |
| `knowledge/`         | _index.yaml + manifest.yaml per pack | _index.yaml   |
| `workspace/`         | _index.yaml                          | _index.yaml   |
| `workspace/state/`   | Direct read                          | session.yaml  |
| `workspace/context/` | _index.yaml                          | _index.yaml   |

