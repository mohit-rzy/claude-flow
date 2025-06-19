# AI Development Workflow System

A comprehensive AI-powered development workflow system that combines session management, task tracking, and project generation capabilities for enhanced productivity with Claude.

## Overview

This system integrates best practices from multiple proven methodologies to create a unified development workflow. It includes:

- **Session Management**: Track and maintain context across development sessions
- **Task Management**: AI-driven task creation, tracking, and implementation
- **Project Generation**: Automated generation of PRDs, UX designs, technical architecture, and more
- **Development Standards**: Enforced coding conventions, testing practices, and documentation requirements

## Custom Slash Commands

### Session Management Commands

#### `/session-start <name>`

Start or resume a development session. Creates a new session file or resumes an existing one.

- **Example**: `/session-start implementing-auth`
- **Purpose**: Maintains context across Claude conversations

#### `/session-current`

Display the current active session status, including duration, recent updates, and goals.

- **Example**: `/session-current`
- **Purpose**: Quick status check of ongoing work

#### `/session-update [message]`

Add a comprehensive update to the current session, automatically capturing git changes and progress.

- **Example**: `/session-update Fixed authentication bug and added tests`
- **Purpose**: Track progress with automatic git status inclusion

#### `/session-list`

List all development sessions showing active/inactive status, dates, and goals.

- **Example**: `/session-list`
- **Purpose**: Overview of all sessions for easy switching

#### `/session-help`

Display all available session management commands with examples.

- **Example**: `/session-help`
- **Purpose**: Quick reference for session commands

### Task Management Commands

#### `/task-list`

View all available tasks organized by status (pending, in-progress, completed).

- **Example**: `/task-list`
- **Purpose**: See task backlog and progress

#### `/task-start <id>`

Begin AI implementation of a specific task.

- **Example**: `/task-start 001`
- **Purpose**: AI-driven task implementation

#### `/task-update`

Track progress on the current task.

- **Example**: `/task-update`
- **Purpose**: Update task status and notes

#### `/task-complete`

Mark current task as complete and get suggestions for next tasks.

- **Example**: `/task-complete`
- **Purpose**: Task closure and workflow continuity

#### `/task-help`

Display all available task management commands.

- **Example**: `/task-help`
- **Purpose**: Quick reference for task commands

### Project Generation Commands

#### `/generate-prd`

Generate a comprehensive Product Requirements Document for the project.

- **Example**: `/generate-prd`
- **Purpose**: Create detailed project specifications

#### `/generate-ux`

Generate UX/UI design documentation and component specifications.

- **Example**: `/generate-ux`
- **Purpose**: Design system and user experience planning

#### `/generate-theme`

Generate theme configuration and design tokens.

- **Example**: `/generate-theme`
- **Purpose**: Consistent visual design system

#### `/generate-tech-architecture`

Generate technical architecture documentation and system design.

- **Example**: `/generate-tech-architecture`
- **Purpose**: Technical planning and infrastructure design

#### `/generate-tasks`

Generate a comprehensive task list based on PRD and architecture.

- **Example**: `/generate-tasks`
- **Purpose**: Break down project into actionable tasks

### Other Commands

#### `/model <model-name>`

Switch between different Claude models (opus, sonnet, etc.).

- **Example**: `/model opus`
- **Purpose**: Use different models for different tasks

#### `/git-commit`

Create a git commit with AI-generated commit message following repository conventions.

- **Example**: `/git-commit`
- **Purpose**: Automated commit creation with proper formatting

## Command Workflow

### Typical Project Setup

1. `/generate-prd` → Define project requirements
2. `/generate-ux` → Design user experience
3. `/generate-theme` → Create design system
4. `/generate-tech-architecture` → Plan technical implementation
5. `/generate-tasks` → Break down into tasks

### Development Workflow

1. `/session-start feature-name` → Begin work session
2. `/task-list` → View available tasks
3. `/task-start 001` → Start implementing a task
4. `/session-update` → Track progress regularly
5. `/task-complete` → Finish task and get next suggestion

### Data Storage Structure

```
sessions/                 # Session tracking with .current-session pointer
tasks/                    # pending/, in-progress/, completed/ with .current-task
context/                  # Generated docs (prd.md, ux.md, theme.md, tech-architecture.md)
.claude/commands/         # All command definitions organized by type
  ├── session/           # Session management commands
  ├── task/              # Task management commands
  ├── generate/          # Project generation commands
  └── git-commit.md      # Git commit command
```

## Credits & Acknowledgments

This system is built upon the excellent work from these three projects:

### 1. [Claude Sessions](https://github.com/iannuttall/claude-sessions)

By Ian Nuttall - Provides the foundation for session management and context persistence across Claude conversations.

### 2. [Claude Task Master](https://github.com/eyaltoledano/claude-task-master)

By Eyal Toledano - Implements the task management system that enables AI-driven task creation, tracking, and completion workflows.

### 3. [AI Dev Project Setup Prompts](https://notes.switchdimension.com/AI-Dev-Project-Setup-Prompts-18fb5b07a94380758bd6e92baa5e8c98)

From Switch Dimension - Contributes the project generation commands and structured development workflow patterns.

## Features

- **Session Tracking**: Maintain continuity across development sessions with automatic git change capture
- **Task Management**: AI-powered task breakdown and implementation tracking
- **Project Scaffolding**: Generate complete project documentation (PRD, UX, tech architecture)
- **Code Quality**: Enforced standards for testing and documentation
- **Command System**: Comprehensive slash commands for workflow management

## Usage

The system is designed to be used with Claude through the CLAUDE.md file, which contains:

- Command system for sessions and tasks
- Workflow patterns and best practices
- Quality standards and guidelines

## License

This project combines work from multiple open-source projects. Please refer to the original repositories for their respective licenses:

- [Claude Sessions License](https://github.com/iannuttall/claude-sessions/blob/main/LICENSE)
- [Claude Task Master License](https://github.com/eyaltoledano/claude-task-master/blob/main/LICENSE)

## Contributing

Contributions are welcome! Please ensure you maintain compatibility with the core systems and follow the established patterns from the original projects.

## Acknowledgments

Special thanks to Ian Nuttall, Eyal Toledano, and the Switch Dimension team for creating and sharing these valuable tools that make AI-assisted development more efficient and organized.
