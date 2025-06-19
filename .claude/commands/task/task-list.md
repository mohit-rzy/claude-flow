# List Tasks Command

<context>
You are a task management assistant. Your role is to list all tasks across different statuses (pending, in-progress, completed) in a clear, organized format with helpful information about each task.
</context>

<usage>
@task-list [filter]

Examples:
- @task-list - Show all tasks
- @task-list pending - Show only pending tasks
- @task-list in-progress - Show only in-progress tasks
- @task-list completed - Show only completed tasks
</usage>

<instructions>
1. Check the `tasks/` directory for subdirectories: pending, in-progress, completed
2. Parse optional filter argument (pending, in-progress, completed, or all)
3. For each relevant directory:
   - List all `.md` files
   - Extract task information from each file:
     - ID, title, description
     - Context, priority, dependencies
     - For in-progress: completion percentage from todoList
     - For completed: completion date
4. Check `.current-task` to identify the active task
5. Sort tasks:
   - Within each status: by priority (high → medium → low), then by ID
   - Overall order: in-progress → pending → completed
6. Present in a clean, scannable format
</instructions>

<task_parsing>
From each task file, extract:
- `<id>` - Task ID number
- `<title>` - Task title
- `<description>` - Brief description
- `<priority>` - high/medium/low
- `<context>` - Associated context
- `<dependencies>` - Other task IDs or "none"
- `<todoList>` - Count checked vs total items for progress

For completion percentage:
- Count `- [x]` as completed
- Count `- [ ]` as pending
- Calculate: (completed / total) * 100
</task_parsing>

<output_format>
Full list (no filter):
```
📋 Task List

🔄 IN PROGRESS (2 tasks)
━━━━━━━━━━━━━━━━━━━━━━
🎯 [CURRENT] Task 2: Implement User Authentication
   📁 Context: auth | Priority: high | Progress: 60% (3/5 items)
   🔗 Dependencies: Task 1
   
▫️ Task 5: Create Dashboard UI
   📁 Context: frontend | Priority: medium | Progress: 20% (1/5 items)
   🔗 Dependencies: Task 2, Task 3

📌 PENDING (3 tasks)
━━━━━━━━━━━━━━━━━━━━
▫️ Task 3: Set up Database Models
   📁 Context: database | Priority: high
   🔗 Dependencies: Task 1
   
▫️ Task 4: Implement API Endpoints
   📁 Context: api | Priority: medium
   🔗 Dependencies: Task 3
   
▫️ Task 6: Add Email Notifications
   📁 Context: notifications | Priority: low
   🔗 Dependencies: Task 2

✅ COMPLETED (1 task)
━━━━━━━━━━━━━━━━━━━━━
▫️ Task 1: Setup Development Environment
   📁 Context: setup | Completed: Jan 15, 2025
   
━━━━━━━━━━━━━━━━━━━━━
📊 Summary: 6 tasks total
- 2 in progress (33%)
- 3 pending (50%)
- 1 completed (17%)

💡 Commands:
- @task-start <id> - Start working on a task
- @task-current - View current task details
- @task-update - Update current task progress
```

Filtered list (e.g., pending only):
```
📋 Task List - PENDING

📌 PENDING (3 tasks)
━━━━━━━━━━━━━━━━━━━━━
▫️ Task 3: Set up Database Models
   📁 Context: database | Priority: high
   🔗 Dependencies: Task 1
   
▫️ Task 4: Implement API Endpoints
   📁 Context: api | Priority: medium
   🔗 Dependencies: Task 3
   
▫️ Task 6: Add Email Notifications
   📁 Context: notifications | Priority: low
   🔗 Dependencies: Task 2

💡 Ready to start:
- Task 3 (dependencies met) ✓

Use @task-start <id> to begin working on a task
```

No tasks found:
```
📋 No tasks found

Create tasks using @generate-tasks after setting up:
1. @generate-prd - Define product requirements
2. @generate-ux - Design user interface
3. @generate-theme - Set up theme
4. @generate-tech-architecture - Plan architecture
5. @generate-tasks - Generate task list
```
</output_format>

<special_indicators>
- 🎯 [CURRENT] - Marks the active task from .current-task
- ✓ - Shows when dependencies are met for pending tasks
- Progress percentage - Only shown for in-progress tasks
- Completion date - Only shown for completed tasks
</special_indicators>

<dependency_checking>
For pending tasks, check if dependencies are met:
- Read dependency task IDs
- Check if those tasks exist in completed/ or are marked as completed
- If all dependencies met, add ✓ indicator
- In summary, suggest which tasks are ready to start
</dependency_checking>

<example_scenarios>
Scenario 1 - Mixed statuses:
Shows tasks grouped by status, with current task highlighted

Scenario 2 - Filter by status:
`@task-list pending` shows only pending tasks with dependency status

Scenario 3 - Empty directory:
Shows helpful message about creating tasks

Scenario 4 - All completed:
Shows completion message and suggests reviewing or creating new tasks
</example_scenarios>

<implementation_notes>
- Use consistent task ID format for easy scanning
- Show most relevant info based on status
- Calculate real progress from todoList items
- Highlight actionable items (ready to start)
- Keep formatting clean and hierarchical
- Use visual separators for clarity
- Always show helpful next actions
</implementation_notes>