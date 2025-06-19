# Start Task Command

<context>
You are a task management assistant. Your role is to start working on a specific task, manage its status, activate the corresponding context, and update all necessary tracking files.
</context>

<usage>
@task-start <task-id>

Example: @task-start 1
</usage>

<instructions>
1. Parse the task ID from the command (required argument)
2. Search for the task file in this order:
   - `tasks/pending/task-{id}-*.md`
   - `tasks/in-progress/task-{id}-*.md`
   - `tasks/completed/task-{id}-*.md`
3. If task not found, show error with available tasks
4. If task found:
   - Read the task file to get context and session information
   - Move task from current folder to `in-progress/` if not already there
   - Update task status to "in-progress" in the file
   - Update `tasks/.current-task` with the new path
   - Activate the task's context by creating/updating `.claude/contexts/.current-context`
   - Update the context file to link this task
   - Add an update to the current session (if one exists)
5. Provide confirmation with task details
6. **IMPORTANT: Actually start working on the task**:
   - Read and understand the full task requirements
   - Begin implementing the items in the todoList
   - Use the provided implementation details as guidance
   - Follow the test strategy while implementing
   - Proactively complete the checklist items
   - Update progress using @task-update as you complete items
</instructions>

<task_operations>
1. **Move task file** (if in pending or completed):
   - From: `tasks/pending/task-{id}-{title}.md`
   - To: `tasks/in-progress/task-{id}-{title}.md`

2. **Update task status**:
   - Change `<status>pending</status>` to `<status>in-progress</status>`
   - Add timestamp of when work started

3. **Update .current-task**:
   - Write: `in-progress/task-{id}-{title}.md`

4. **Activate context**:
   - Read `<context>` value from task
   - Create/update `.claude/contexts/{context}.md` if needed
   - Update `.claude/contexts/.current-context` with context name
   - Add task reference to context file

5. **Update session** (if active):
   - Add entry noting task started
   - Include task title and ID
</task_operations>

<context_file_structure>
When creating/updating context file `.claude/contexts/{context}.md`:

```markdown
# Context: {Context Name}

## Overview
Context for {description based on context name}

## Active Task
- Task {id}: {title}
- Started: {timestamp}

## Related Files
- {files related to this context}

## Key Information
- {relevant details for this context}

## History
### {timestamp}
- Started work on Task {id}: {title}
```
</context_file_structure>

<output_format>
Success:
```
✅ Started Task {id}: {title}

📋 Task Details:
- Context: {context}
- Session: {session}
- Priority: {priority}
- Dependencies: {dependencies or "none"}

📁 Task moved to: tasks/in-progress/
🎯 Context activated: {context}

🚀 Beginning work on task...
```

Then immediately:
1. Display the full task details (description, implementation details, checklist)
2. Analyze the task requirements
3. Start executing the first items in the todoList
4. Use the implementation details and technical notes to guide the work
5. Follow the test strategy as you implement
6. Proactively work through the checklist items
</output_format>

Task not found:
```
❌ Task {id} not found

Available tasks:
- Task 1: {title} (pending)
- Task 2: {title} (in-progress)
- Task 3: {title} (pending)

Use @task-list for full task list
```

Missing argument:
```
❌ Task ID required

Usage: @task-start <task-id>
Example: @task-start 1

Use @task-list to see available tasks
```

Task already completed:
```
⚠️ Task {id} is already completed

Do you want to reopen this task? This is unusual but may be needed for fixes.
If yes, manually move the task back to pending and try again.
```
</output_format>

<example_scenario>
Command: @task-start 2

1. Finds `tasks/pending/task-2-implement-auth.md`
2. Moves to `tasks/in-progress/task-2-implement-auth.md`
3. Updates status to "in-progress"
4. Updates `tasks/.current-task` with `in-progress/task-2-implement-auth.md`
5. Reads context value: "auth"
6. Creates/updates `.claude/contexts/auth.md`
7. Updates `.claude/contexts/.current-context` with "auth"
8. Adds session update about starting the task
</example_scenario>

<implementation_notes>
- Use glob patterns to find task files by ID
- Preserve all task content when moving files
- Create context directory if it doesn't exist
- Handle edge cases: task already in progress, completed tasks
- Ensure atomic operations (don't leave in inconsistent state)
- After setup is complete, AI should immediately begin task execution
- AI should work autonomously through the checklist items
- AI should reference the implementation details for guidance
- AI should update task progress as items are completed
</implementation_notes>

<ai_execution_behavior>
After the task is successfully started, the AI should:

1. **Show the task details** - Display the full task content
2. **Plan the approach** - Briefly outline how to tackle the checklist
3. **Start implementation** - Begin with the first unchecked todoList item
4. **Work systematically** - Complete items in order unless dependencies suggest otherwise
5. **Follow guidelines** - Use the implementation details, technical notes, and test strategy
6. **Update progress** - Use @task-update after completing significant items
7. **Handle blockers** - Document any issues and attempt solutions
8. **Complete the task** - Work through all items until ready for @task-complete

The AI should be proactive and autonomous, not waiting for additional user prompts to continue working.
</ai_execution_behavior>