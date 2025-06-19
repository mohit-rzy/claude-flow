# Session Help Command

<context>
You are a help assistant. Your role is to display all available session management commands by reading the command files from the @sessions-commands/ directory and presenting them in an organized, helpful format.
</context>

<usage>
@session-help
</usage>

<instructions>
1. List all `.md` files in the `@sessions-commands/` directory
2. For each command file:
   - Extract the command name from the filename
   - Read the file to get the command description and usage
   - Extract key information from the <context> and <usage> sections
3. Present all commands in a clean, organized format
4. Include examples and common workflows
</instructions>

<output_format>

```
📁 Session Management Commands

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📍 AVAILABLE COMMANDS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

@session-start <name>
  ▫️ Start or resume a development session
  ▫️ Creates new session or resumes existing one
  ▫️ Example: @session-start implementing-auth
  ▫️ File: @sessions-commands/session-start.md

@session-current
  ▫️ Show current session status and details
  ▫️ Displays: duration, recent updates, goals, tasks
  ▫️ Example: @session-current
  ▫️ File: @sessions-commands/session-current.md

@session-update [message]
  ▫️ Add comprehensive update to current session
  ▫️ Tracks: git changes, todo progress, work done
  ▫️ Example: @session-update Fixed authentication bug
  ▫️ File: @sessions-commands/session-update.md

@session-list
  ▫️ List all development sessions
  ▫️ Shows: active/inactive, dates, goals
  ▫️ Example: @session-list
  ▫️ File: @sessions-commands/session-list.md

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔄 TYPICAL WORKFLOW
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Start a session:
   @session-start feature-development

2. Check session status:
   @session-current

3. As you work, update progress:
   @session-update Implemented user model
   @session-update Fixed validation errors

4. Switch between sessions:
   @session-list
   @session-start different-feature

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📂 SESSION FILE STRUCTURE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Sessions are stored in: sessions/
Current session tracked in: sessions/.current-session

Each session file contains:
• Metadata (start time, last update)
• Goals and objectives
• Progress updates with timestamps
• Learnings and notes
• Next steps

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 TIPS & BEST PRACTICES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

• Use descriptive session names (e.g., "auth-implementation")
• Update regularly to maintain context
• One session per feature or major task
• Sessions persist across Claude conversations
• Updates include git status automatically

For detailed help on any command, read the command file directly.
```

</output_format>

<dynamic_loading>
Note: In a real implementation, this command would:

1. Dynamically read the @sessions-commands/ directory
2. Parse each .md file to extract descriptions
3. Build the help content based on available commands
4. Always show the most up-to-date command list
   </dynamic_loading>

<implementation_notes>

- List commands in logical order (start → current → update → list)
- Include file locations for reference
- Show practical workflow example
- Explain where session data is stored
- Add helpful tips for effective usage
- Keep format consistent with task-help
  </implementation_notes>
