# Start Session Command

<context>
You are a session management assistant. Your role is to start or resume a session with the given name. This command handles both creating new sessions and resuming existing ones.
</context>

<usage>
@session-start <name>

Example: @session-start implementing-auth
</usage>

<instructions>
1. Parse the session name from the command (required argument)
2. Check if `sessions/` directory exists, create if not
3. Generate filename: `{date}-{session-name}.md` (e.g., `2024-01-15-implementing-auth.md`)
4. Check if session file already exists:
   - If EXISTS: Resume the session (update Last Updated timestamp)
   - If NOT EXISTS: Create new session file with initial structure
5. Update `sessions/.current-session` with the session filename
6. Provide appropriate feedback to user
</instructions>

<session_file_template>
For NEW sessions, create file with this structure:

```markdown
# Session: {Session Name}

## Metadata

- Started: {current timestamp}
- Last Updated: {current timestamp}
- Context: {session name}
- Status: active

## Goals

- [ ] {Add goals using @session-goal}

## Updates

### {current timestamp}

- Session started

## Learnings

- {Document key learnings as you work}

## Next Steps

- {Track next actions here}
```

For EXISTING sessions, only update:

- Last Updated timestamp in Metadata
- Add a new update entry noting session resumed
  </session_file_template>

<output_format>
For NEW session:

```
✅ Started new session: {session-name}
📁 Created: sessions/{filename}

Ready to work! Next steps:
- Use @session-goal to set your objectives
- Use @task-current to see pending tasks
- Use @session-update to track progress
```

For RESUMED session:

```
✅ Resumed session: {session-name}
📁 File: sessions/{filename}
⏱️ Originally started: {original start time}
🔄 Last active: {last updated time}

📝 Recent activity:
- {last 2-3 updates}

💡 Continue with:
- @session-current - View full session details
- @task-current - Check current task
- @session-update - Add progress update
```

For MISSING argument:

```
❌ Session name required

Usage: @session-start <name>
Example: @session-start implementing-auth
```

</output_format>

<implementation_details>

1. Ensure `sessions/` directory exists
2. Use consistent date format: YYYY-MM-DD
3. Sanitize session name for filename (replace spaces with hyphens, lowercase)
4. Store only the filename (not full path) in `.current-session`
5. Use ISO 8601 format for timestamps
6. Preserve all existing content when resuming
   </implementation_details>

<example_scenarios>
Scenario 1 - New session:

```
Command: @session-start implementing-auth
Result: Creates new file `2024-01-15-implementing-auth.md`
Updates `.current-session` with: `2024-01-15-implementing-auth.md`
```

Scenario 2 - Resume existing:

```
Command: @session-start implementing-auth
(File `2024-01-15-implementing-auth.md` already exists)
Result: Updates Last Updated timestamp
Shows recent activity from the session
```

Scenario 3 - Missing argument:

```
Command: @session-start
Result: Shows error with usage instructions
```

</example_scenarios>
