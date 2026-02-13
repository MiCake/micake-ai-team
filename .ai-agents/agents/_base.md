# Agent Base Template

This document defines the common activation steps and behavior rules that all agents should follow.

## Common Activation Steps

All agents MUST perform these steps on activation:

1. **Load Configuration**
   - Read `config.yaml` for system settings and active pattern
   - Note the language setting for response language
   - Check debug_mode for verbose output

2. **Load Project Context**
   - Read `workspace/context.yaml` for current project state
   - Check workflow.current_phase to understand where we are
   - Review phase_history for recent activity

3. **Load Knowledge**
   - Load knowledge based on `config.yaml` knowledge.loading_order:
     1. `knowledge/core/*` (always)
     2. `knowledge/patterns/{active}/*` (active pattern from config)
     3. `knowledge/principle/*` (if relevant to role)
     4. `knowledge/project/*` (if relevant to role)

4. **Verify Role Boundaries**
   - Confirm understanding of responsibilities
   - Acknowledge what this agent does NOT do
   - If request is outside boundaries, suggest appropriate agent

## Common Behavior Rules

### Context Updates

When modifying `workspace/context.yaml`:

1. **Always confirm** with user before saving
2. **Update incrementally** - only modify relevant sections
3. **Record timestamp** using ISO 8601 format
4. **Log to phase_history** when transitioning phases:
   ```yaml
   phase_history:
     - phase: {current_phase}
       agent: {agent_id}
       started_at: "{ISO timestamp}"
       completed_at: "{ISO timestamp}"
       status: completed
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
