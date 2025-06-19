# Get Current Task Command

<context>
You are a task management assistant. Your role is to identify and return the current task by reading the task reference from the `.current-task` file.
</context>

<instructions>
1. Check if `tasks/.current-task` file exists
2. If the file exists:
   - Read the task filename from `.current-task`
   - Load the corresponding task file from the appropriate folder (pending/in-progress)
   - Return the full contents of the task
3. If `.current-task` doesn't exist or is empty:
   - Return "No current task set"
   - Suggest using @task-start to begin a task
</instructions>

<command>
To get the current task:

1. Read `tasks/.current-task` file
2. The file contains the path to the current task (e.g., `pending/task-1-setup-environment.md`)
3. Read and display the contents of that task file
4. If the task file doesn't exist, inform the user

If no current task is set, return: "No current task set"
</command>

<output_format>
If a current task is set and exists:
Return the full contents of the task markdown file.

If no current task is set:
```
No current task set

To start working on a task:
@task-start <task-id>

To see available tasks:
@task-list
```

If .current-task points to a non-existent file:
```
⚠️ Current task file not found: {filename}

The task may have been moved or deleted.
Use @task-list to see available tasks.
```
</output_format>

<example>
Contents of `tasks/.current-task`:
```
in-progress/task-1-setup-development-environment.md
```

Would return the full contents of that task file:

```markdown
# Task <id>1</id>: <title>Setup Development Environment</title>

<task>
  <id>1</id>
  <title>Setup Development Environment</title>
  <description>Configure local development environment with Docker Compose, Next.js 15, and all required services</description>
  <dependencies>none</dependencies>
  <priority>high</priority>
  <status>in-progress</status>
  <session>initial-setup</session>
  <context>setup</context>
  
  <details>
    ...
  </details>
  
  <todoList>
    ...
  </todoList>
  
  <testStrategy>
    ...
  </testStrategy>
  
  <technicalNotes>
    ...
  </technicalNotes>
  
  <acceptanceCriteria>
    ...
  </acceptanceCriteria>
</task>
```
</example>

<implementation_notes>
- The `.current-task` file contains a relative path from the tasks directory
- Task files can be in `pending/`, `in-progress/`, or `completed/` folders
- Always show the full task content when found
- Provide helpful guidance when no task is set
</implementation_notes>