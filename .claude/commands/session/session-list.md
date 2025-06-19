# List Sessions Command

<context>
You are a session management assistant. Your role is to list all development sessions, showing their status and key information in a clean, organized format.
</context>

<usage>
@session-list
</usage>

<instructions>
1. Check if `sessions/` directory exists
   - If not, inform user no sessions found
2. List all `.md` files in the directory
   - Exclude hidden files (starting with .)
   - Exclude `.current-session` file
3. Read `sessions/.current-session` to identify active session
4. For each session file:
   - Extract session name from file content (# Session: line)
   - Get creation date from filename (YYYY-MM-DD format)
   - Get last updated time from file metadata
   - Extract first few goals or recent updates
   - Mark if it's the current active session
5. Sort sessions by date (most recent first)
6. Present in a clean, formatted list
</instructions>

<output_format>
If sessions exist:

```
📋 Development Sessions

🟢 [Active] {session-name}
   📁 File: {filename}
   📅 Started: {date} | Last updated: {last update}
   🎯 Goals: {first 2-3 goals or "No goals set"}

▪️ {session-name}
   📁 File: {filename}
   📅 Started: {date} | Last updated: {last update}
   🎯 Goals: {first 2-3 goals}

▪️ {session-name}
   📁 File: {filename}
   📅 Started: {date} | Last updated: {last update}
   🎯 Goals: {first 2-3 goals}

Total: {X} sessions ({Y} active)

💡 Commands:
- @session-start <name> - Start or resume a session
- @session-current - View active session details
```

If no sessions:

```
📋 No sessions found

Get started with:
@session-start <name>

Example: @session-start implementing-auth
```

</output_format>

<parsing_details>
From session files, extract:

1. Session name: From `# Session: {name}` line
2. Started date: From `- Started: {timestamp}` in metadata
3. Last updated: From `- Last Updated: {timestamp}` in metadata
4. Goals: From `## Goals` section, show first 2-3 items
5. Status: Check if matches current session file

File naming pattern: `YYYY-MM-DD-session-name.md`
</parsing_details>

<example_output>

```
📋 Development Sessions

🟢 [Active] implementing-auth-system
   📁 File: 2025-01-15-implementing-auth-system.md
   📅 Started: Jan 15, 2025 | Last updated: 2 hours ago
   🎯 Goals: Set up Better Auth, Add OAuth providers, Implement RBAC

▪️ frontend-dashboard
   📁 File: 2025-01-14-frontend-dashboard.md
   📅 Started: Jan 14, 2025 | Last updated: yesterday
   🎯 Goals: Create dashboard layout, Add analytics widgets

▪️ database-optimization
   📁 File: 2025-01-12-database-optimization.md
   📅 Started: Jan 12, 2025 | Last updated: 3 days ago
   🎯 Goals: Optimize queries, Add indexes, Implement caching

Total: 3 sessions (1 active)

💡 Commands:
- @session-start <name> - Start or resume a session
- @session-current - View active session details
```

</example_output>

<implementation_notes>

- Use relative time for "Last updated" (e.g., "2 hours ago", "yesterday")
- Truncate long goal descriptions to keep list readable
- Show maximum 3 goals per session
- Highlight active session clearly with 🟢 and [Active] tag
- Sort by file date (extracted from filename)
- Handle edge cases: empty goals, missing metadata
- Keep each session entry concise (4-5 lines max)
  </implementation_notes>
