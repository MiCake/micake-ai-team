# Changes Directory Rules

Rules for maintaining the changes directory.

## Rule 1: One Folder Per Change

**What**: Each change request gets its own folder.

**Why**: Isolation prevents confusion and enables clean tracking.

**How**: Create folder with standard naming convention.

## Rule 2: Standard Naming

**What**: Use `{YYYYMMDD}-{seq}-{description}` format.

**Why**: Chronological ordering and easy identification.

**How**: 
- Date: When change was initiated
- Sequence: Auto-increment daily (001, 002, ...)
- Description: 2-4 word kebab-case summary

## Rule 3: Required Artifacts

**What**: Every completed change must have at minimum:
- `request.md` - What was requested
- `summary.md` - What was delivered

**Why**: Minimum documentation for auditability.

**How**: Conductor creates these automatically.

## Rule 4: Immutable After Completion

**What**: Don't modify artifacts after change is marked complete.

**Why**: Preserves historical accuracy.

**How**: If follow-up needed, create new change request.

## Rule 5: Archive Old Changes

**What**: Move old changes to `_archive/YYYY/` after 90 days.

**Why**: Keeps active directory manageable.

**How**: 
1. Identify changes older than 90 days (based on folder date prefix)
2. Create `_archive/YYYY/` directory if not exists
3. Move the change folder to archive
4. Update `CHANGELOG.md` with archive note

**Archive Structure**:
```
changes/
├── _archive/
│   └── 2025/
│       └── 20251015-001-initial-setup/
├── 20260213-001-add-auth/  # Recent, stays in active
└── CHANGELOG.md
```

**Preservation**: Always keep `summary.md` accessible for reference.

---

## Artifact Templates

### request.md

```markdown
# Change Request: {title}

**ID**: {change-id}
**Date**: {date}
**Requested By**: {user}

## Description
{what needs to change}

## Reason
{why this change is needed}

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2

## Priority
{high/medium/low}

## Notes
{additional context}
```

### summary.md

```markdown
# Change Summary: {title}

**ID**: {change-id}
**Completed**: {date}
**Duration**: {time}

## What Changed
{summary of modifications}

## Files Modified
- `path/to/file1` - {what changed}
- `path/to/file2` - {what changed}

## Tests Added/Modified
- {test description}

## Documentation Updated
- {doc changes}

## Notes
{any follow-up needed}
```
