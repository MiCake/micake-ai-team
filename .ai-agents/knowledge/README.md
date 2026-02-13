# Knowledge Base

Reference documentation for AI agents across all technology stacks and patterns.

## Structure

| Directory | Description | Manifest |
|-----------|-------------|----------|
| `core/` | Universal software principles (always loaded) | `core/manifest.yaml` |
| `patterns/` | Architecture pattern packs | `patterns/{pattern}/manifest.yaml` |
| `principle/` | Project coding standards (auto-generated) | `principle/manifest.yaml` |
| `project/` | Project-specific knowledge | `project/manifest.yaml` |

## Knowledge Loading

Knowledge is loaded based on the order defined in `config.yaml`:

```yaml
knowledge:
  loading_order:
    - core/*           # Priority 1: Always load
    - patterns/{active}/* # Priority 2: Active pattern
    - principle/*      # Priority 3: Coding standards
    - project/*        # Priority 4: Project-specific
```

Each directory contains a `manifest.yaml` that defines:
- Knowledge pack metadata (id, name, version)
- Loading behavior (priority, auto_load)
- File listing and descriptions

## Knowledge Layers

### Core Knowledge
Universal software engineering principles and practices that apply regardless of technology stack or architecture pattern.

**Files:**
- `software-principles.md` - SOLID, DRY, KISS, YAGNI

### Pattern Knowledge
Architecture-specific patterns, terminology, and best practices. Loaded based on `config.yaml` active pattern.

**Available Patterns:**
- `ddd/` - Domain-Driven Design patterns (see `patterns/ddd/manifest.yaml`)
- `clean-architecture/` - Clean Architecture principles (see `patterns/clean-architecture/manifest.yaml`)

### Development Principles
Coding standards, conventions, and best practices for code quality and maintainability.

**Usage:**
Add files like `coding-standards.md` and `review-checklist.md` to provide guidelines for code analysis and review execution skills.

### Project Knowledge
Custom knowledge specific to your project.

**Usage:**
Add your project-specific documentation to `knowledge/project/`:
- Project-specific patterns
- Business domain glossary

## Usage by Agents

Agents automatically load knowledge based on:
1. **Always**: Core knowledge (`core/`)
2. **Based on Config**: Active pattern knowledge (`patterns/{active}/`)
3. **As Needed**: Development principles (`principle/`)
4. **Project-Specific**: Custom project knowledge (`project/`)

## File Format

All knowledge files should:
- Use Markdown format
- Include clear headings
- Provide code examples where applicable
- Be optimized for AI agent consumption
