# Update Session Command

<context>
You are a session management assistant. Your role is to add comprehensive updates to the current development session, tracking progress, changes, and learnings.
</context>

<usage>
@session-update [optional message]

Examples:

- @session-update Implemented user authentication with OAuth
- @session-update (no arguments - will auto-summarize recent activities)
  </usage>

<instructions>
1. Check if `sessions/.current-session` exists
2. If no active session:
   - Inform user to start one with @session-start
3. If session exists:
   - Read current session filename
   - Gather comprehensive update information:
     - Git status (files changed, branch, last commit)
     - Todo list progress
     - User's message or auto-generated summary
   - Append update to session file in specified format
   - Confirm update was added
</instructions>

<update_format>

```markdown
### Update - {timestamp in YYYY-MM-DD HH:MM AM/PM format}

**Summary**: {user provided message or auto-generated summary}

**Git Changes**:

- Modified: {list of modified files from git status --porcelain}
- Added: {list of added files}
- Deleted: {list of deleted files}
- Current branch: {branch name} (commit: {last commit hash})

**Todo Progress**: {X completed}, {Y in progress}, {Z pending}

- ✓ Completed: {task title}
- ⚡ In Progress: {task title}
- ○ Started: {newly started tasks}

**Details**: {extended description, issues, solutions, learnings}
```

</update_format>

<gathering_information>
For Git status:

- Use `git status --porcelain` to get file changes
- Use `git branch --show-current` for current branch
- Use `git log -1 --format="%h"` for last commit hash

For Todo progress:

- Count tasks in `tasks/completed/`, `tasks/in-progress/`, `tasks/pending/`
- List any tasks that changed status since last update
- Note newly completed or started tasks

For auto-summary (when no arguments provided):

- Analyze recent file changes
- Identify patterns (e.g., "Working on authentication" if auth files changed)
- Include any error fixes or refactoring
  </gathering_information>

<output_format>
Success:

```
✅ Session updated: {session-name}

📝 Update Summary:
{show the Summary line from the update}

📊 Progress:
- Git: {X files changed} on {branch}
- Tasks: {X completed}, {Y in progress}, {Z pending}

💾 Update saved to: sessions/{filename}
```

No active session:

```
❌ No active session found

Start a session first:
@session-start <name>

Example: @session-start implementing-auth
```

</output_format>

<example_updates>
Example 1 - With user message:

```markdown
### Update - 2025-01-15 02:30 PM

**Summary**: Implemented user authentication with OAuth

**Git Changes**:

- Modified: app/middleware.ts, lib/auth.ts, .env.example
- Added: app/login/page.tsx, app/api/auth/[...auth]/route.ts
- Current branch: feature/auth (commit: abc123f)

**Todo Progress**: 3 completed, 1 in progress, 2 pending

- ✓ Completed: Set up Better Auth configuration
- ✓ Completed: Create login page UI
- ✓ Completed: Add OAuth providers (Google, GitHub)
- ⚡ In Progress: Implement RBAC

**Details**: Implemented OAuth authentication using Better Auth. Added Google and GitHub providers. Login page now functional with proper error handling. Next: implement role-based access control.
```

Example 2 - Auto-generated summary:

```markdown
### Update - 2025-01-15 04:45 PM

**Summary**: Fixed authentication middleware and updated UI components

**Git Changes**:

- Modified: middleware.ts, app/components/Header.tsx
- Added: app/components/UserMenu.tsx
- Current branch: feature/auth (commit: def456g)

**Todo Progress**: 4 completed, 0 in progress, 1 pending

- ✓ Completed: Implement RBAC

**Details**: Auto-generated summary: Fixed issue with middleware not properly checking authentication status. Added user menu component to header. All authentication tasks now complete.
```

</example_updates>

<implementation_notes>

- Always use consistent timestamp format
- Group git changes by status (Modified, Added, Deleted)
- Show task progress changes clearly
- Keep summaries concise but informative
- Include any errors/issues and their solutions
- Auto-summary should analyze actual changes made
  </implementation_notes>
