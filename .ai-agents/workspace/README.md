# Workspace Directory

This directory contains project-specific working files:

- `context.yaml` - Dynamic memory for project context
- `requirements/` - Requirements documents and analysis
- `changes/` - Change request tracking

## Context Management

The `context.yaml` file is the central memory store for the AI agents. It maintains:

- Project information (language, framework, architecture)
- Current workflow state and phase
- Requirements summary
- Architecture decisions
- Implementation progress
- Review notes

## Rules

1. **Confirm Before Save**: Always confirm with user before updating `context.yaml`
2. **Keep It Concise**: Only store essential information
3. **Update Incrementally**: Update relevant sections only, don't overwrite unrelated data
4. **Timestamp Changes**: Record when significant updates are made (ISO 8601 format)
5. **Record Phase History**: Log all phase transitions for audit and recovery
6. **Check Lock**: Verify no active lock before making changes

## Workflow State Management

### Phase Lifecycle

Phases transition through these states:
- `in-progress` - Phase is currently being executed
- `completed` - Phase finished successfully
- `failed` - Phase encountered errors
- `skipped` - Phase was intentionally skipped

### Recovery

If workflow enters an error state, use `#recover` command to:
1. Diagnose the issue from phase_history
2. Reset to last known good state
3. Resume from a specific phase
