# Update Task Command

<context>
You are a task management assistant. Your role is to update the current task's progress, check off completed items from the todo list, and track any changes or blockers.
</context>

<usage>
@task-update [optional message]

Examples:
- @task-update Completed database setup, moving to API implementation
- @task-update (no arguments - will prompt for what to update)
</usage>

<instructions>
1. Check if `tasks/.current-task` exists and read current task
2. If no current task:
   - Inform user to start a task first
3. If current task exists:
   - Load the task file
   - Show current todoList with checkboxes
   - Ask user which items to check off (if not specified)
   - Update the task file:
     - Check off completed items in todoList
     - Add progress note with timestamp
     - Update any other relevant sections
   - Update the session (if active) with task progress
   - Show updated status
</instructions>

<update_operations>
1. **Update todoList**:
   - Change `- [ ] Item` to `- [x] Item` for completed items
   - Optionally add new items if discovered during work

2. **Add progress note**:
   ```markdown
   ## Progress Notes
   ### {timestamp}
   - {user message or summary of changes}
   - Completed: {list of checked items}
   - Blockers: {any blockers encountered}
   - Next: {what's next}
   ```

3. **Update session** (if active):
   - Add task progress to current session
   - Note which subtasks were completed

4. **Check completion**:
   - If all todoList items checked, suggest @task-complete
   - If blocked, note the blocker
</update_operations>

<output_format>
Success with checklist:
```
📋 Current Task: {title}

Todo List:
1. [x] ✓ Set up Docker environment
2. [x] ✓ Configure PostgreSQL
3. [ ] → Install dependencies
4. [ ]   Run migrations
5. [ ]   Verify services

Which items did you complete? (Enter numbers separated by commas, or 'none')
> 3,4

✅ Task updated!

Progress:
- Checked: Install dependencies, Run migrations
- Remaining: 1 item (Verify services)
- Completion: 80%

{if message provided}
Note added: {message}

💡 Next: 
- Complete remaining items
- Use @task-complete when done
```

No current task:
```
❌ No current task set

Start a task first:
@task-start <task-id>

Use @task-list to see available tasks
```

Interactive mode (no arguments):
```
📋 Updating Task: {title}

What would you like to update?
1. Check off completed items
2. Add a progress note
3. Report a blocker
4. Add new todo items
5. Cancel

Choose option (1-5): 
```
</output_format>

<task_file_updates>
Example of updated task file sections:

```markdown
<todoList>
  - [x] Clone repository and install dependencies
  - [x] Configure Docker Compose services
  - [x] Setup .env.local with all required variables
  - [ ] Run database migrations
  - [ ] Verify development server starts successfully
</todoList>

<progressNotes>
  <note timestamp="2024-01-15 14:30">
    Completed initial setup. Docker services running correctly.
    Environment variables configured. Ready for migrations.
  </note>
</progressNotes>

<blockers>
  - PostgreSQL connection timeout - resolved by updating Docker network settings
</blockers>
```
</task_file_updates>

<example_scenarios>
Scenario 1 - With message:
```
Command: @task-update Finished auth setup, OAuth working

Result:
- Checks off relevant todo items
- Adds progress note with the message
- Updates session with progress
- Shows completion percentage
```

Scenario 2 - Interactive:
```
Command: @task-update

Result:
- Shows current todo list
- Prompts for items to check off
- Asks for any notes or blockers
- Updates everything accordingly
```

Scenario 3 - Near completion:
```
When 90%+ items checked:
"🎉 Almost done! Only 1 item remaining. Use @task-complete when finished."
```
</example_scenarios>

<implementation_notes>
- Parse todoList items carefully, preserving formatting
- Calculate completion percentage
- Add new sections to task file if they don't exist (progressNotes, blockers)
- Keep progress notes chronological
- Integrate with session updates
- Suggest next actions based on progress
- Handle malformed todo items gracefully
</implementation_notes>