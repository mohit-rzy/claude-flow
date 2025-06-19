# Task Help Command

<context>
You are a help assistant. Your role is to display all available task and session management commands with clear descriptions and usage examples.
</context>

<usage>
@task-help
</usage>

<instructions>
Display a comprehensive list of all available commands organized by category:
1. Session Management Commands
2. Task Management Commands
3. Project Setup Commands
4. Getting Started Guide

Format each command with its purpose, usage syntax, and a brief example.
</instructions>

<output_format>
```
📚 Task & Session Management Help

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📁 SESSION MANAGEMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

@session-start <name>
  ▫️ Start or resume a development session
  ▫️ Example: @session-start implementing-auth

@session-current
  ▫️ View current session details and recent updates
  ▫️ Shows: status, duration, goals, recent activity

@session-update [message]
  ▫️ Add progress update to current session
  ▫️ Example: @session-update Fixed auth middleware bug

@session-list
  ▫️ List all development sessions
  ▫️ Shows: active/inactive sessions, dates, goals

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📋 TASK MANAGEMENT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

@task-start <id>
  ▫️ Start working on a specific task
  ▫️ Example: @task-start 1
  ▫️ Note: AI will begin implementing the task immediately

@task-current
  ▫️ View the current active task details
  ▫️ Shows: full task specification and progress

@task-update [message]
  ▫️ Update current task progress and check off items
  ▫️ Example: @task-update Completed database setup

@task-list [filter]
  ▫️ List all tasks or filter by status
  ▫️ Filters: pending, in-progress, completed
  ▫️ Example: @task-list pending

@task-complete
  ▫️ Mark current task as completed
  ▫️ Moves task to completed folder

@task-help
  ▫️ Show this help message

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🚀 PROJECT SETUP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

@generate-prd
  ▫️ Generate Product Requirements Document
  ▫️ Creates: context/prd.md

@generate-ux
  ▫️ Generate User Interface Design Document
  ▫️ Creates: context/ux.md

@generate-theme
  ▫️ Generate Theme & Implementation Guide
  ▫️ Creates: context/theme.md

@generate-tech-architecture
  ▫️ Generate Technical Architecture Document
  ▫️ Creates: context/tech-architecture.md

@generate-tasks
  ▫️ Generate task list from all context documents
  ▫️ Creates: tasks/pending/*.md files

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎯 GETTING STARTED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Project Setup (run in order):
   @generate-prd → @generate-ux → @generate-theme → 
   @generate-tech-architecture → @generate-tasks

2. Start Development:
   @session-start my-project
   @task-list
   @task-start 1

3. Track Progress:
   @task-current - Check current task
   @task-update - Update progress
   @session-update - Log session progress

4. View Status:
   @session-current - Current session info
   @task-list - All tasks overview

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 TIPS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• Sessions track your overall work context
• Tasks are specific implementation units
• The AI works autonomously after @task-start
• Use @task-update frequently to track progress
• Dependencies are checked automatically
• All data is stored in .claude/ and tasks/ folders

Need more help? Check the individual command files for detailed documentation.
```
</output_format>

<implementation_notes>
- Group commands logically by function
- Show command syntax clearly with parameters
- Include practical examples
- Highlight the workflow sequence
- Add tips for effective usage
- Keep descriptions concise but informative
- Use visual separators for easy scanning
</implementation_notes>