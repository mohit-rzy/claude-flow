# CLAUDE.md

## Core Development Principles

**Active Session**: {Check .claude/sessions/.current-session} | **Current Task**: {Check tasks/.current-task}

> Always include current session and task in responses for continuity.

## Command System

### Session Management
```bash
@session-start <name>       # Start tracking work
@session-current           # Check status  
@session-update [msg]      # Log progress (auto-captures git changes)
```

### Task Management  
```bash
@task-list                 # See available tasks
@task-start <id>           # AI begins implementation
@task-update              # Track progress
@task-complete            # Finish and suggest next
```

### Project Generation
```bash
@generate-prd → @generate-ux → @generate-theme → @generate-tech-architecture → @generate-tasks
```

## Workflow

### Best Practices
- Check `@session-current` and `@task-current` at conversation start
- Use `@task-start` for AI implementation | Regular `@session-update` for history
- Follow command workflow for organization

### Development Flow
1. Project setup with generation commands
2. `@session-start` → `@task-list` → `@task-start` → implement → `@task-complete`
3. Regular session updates capture git changes automatically

### Data Storage
```
.claude/sessions/          # Session tracking with .current-session pointer
tasks/                    # pending/, in-progress/, completed/ with .current-task
context/                  # Generated docs (prd.md, ux.md, theme.md, tech-architecture.md)
```