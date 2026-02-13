# My-Virtual-TechTeam

A virtual IT team made up of AI agents. Help unleash your potential by leveraging the power of AI.

## Overview

This is an AI Agent Framework built on prompt engineering principles. It defines multiple AI agent roles that work together to assist in software development workflows, similar to BMAD Method or Open Spec approaches.

## Quick Start

1. Open this project in VS Code with GitHub Copilot or Claude Code
2. Start a chat and type `#start` to begin a new development workflow
3. Follow the guided prompts to move through the development phases

## Commands

| Command | Description |
|---------|-------------|
| `#start` | Start a new development workflow |
| `#status` | Check current workflow status |
| `#init` | Initialize and analyze project structure |
| `#pattern {name}` | Switch architecture pattern (ddd, clean-architecture) |
| `#recover` | Recover from error state |
| `#analyze` | Analyze requirements |
| `#design` | Create architecture design |
| `#implement` | Implement code |
| `#review` | Review code |
| `#test` | Generate tests |

## Architecture

```
.ai-agents/           # Core framework (platform-agnostic)
├── config.yaml       # Unified configuration
├── agents/           # Agent definitions (.yaml + .prompt.md)
├── skills/           # Modular skills
├── workflows/        # Workflow definitions
├── knowledge/        # Domain knowledge
└── workspace/        # Project context and memory

.github/              # GitHub Copilot adapter
├── copilot-instructions.md
├── agents/           # Agent activation files
└── skills/           # Skill references
```

## Agents

| Agent | Role |
|-------|------|
| **Conductor** | Workflow coordinator and task dispatcher |
| **Analyst** | Requirements analysis and concept extraction |
| **Architect** | System architecture and technical design |
| **Developer** | Code implementation |
| **Reviewer** | Code quality review |
| **Tester** | Test design and execution |

## Features

- **Role Separation**: Each agent has clear responsibilities and boundaries
- **Platform Agnostic**: Works with GitHub Copilot (Claude Code adapter planned)
- **Dynamic Memory**: Context persists across sessions via `workspace/context.yaml`
- **Semi-automatic Workflow**: Guided progression with user confirmation
- **Modular Skills**: Load capabilities on-demand to optimize context usage
- **Language Agnostic**: Supports any programming language

## License

MIT
