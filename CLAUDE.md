# CLAUDE.md

Suiying (随影) - macOS Claude Code plugin for desktop notifications and code review.

## Structure

```
.claude-plugin/plugin.json    # Version in this file
agents/                       # pragmatic-code-review, design-review, security-review
commands/                     # Slash commands
skills/design-principles/     # Auto-activating knowledge
hooks/hooks.json             # UserPromptSubmit, Stop, Notification events
scripts/ccnotify.py          # Notification system + SQLite tracking
```

## CCNotify System

SQLite database tracks sessions: `prompt` table (id, session_id, created_at, prompt, cwd, seq, stoped_at, lastWaitUserAt)

Notification formats:
- Task done: `{project} - 完成了` / `{prompt_preview} ({duration})`
- Permission: `{project} - 需要权限` / `{message}`
- Action: `{project} - 需要操作` / `{message}`
- Inquiry: `{project} - 问询` / `{message}`

Click opens Windsurf: `/Users/apple/.codeium/windsurf/bin/windsurf "{cwd}"`

## Code Conventions

**Python:**
- SQLite triggers for auto-increment seq
- subprocess.run() with check=False for terminal-notifier
- Duration: "5s", "2m30s", "1h15m"

**Agents/Skills:**
- YAML frontmatter: name, description, tools, model (optional), color (optional)
- Use `<example>` with `<commentary>` for triggers

**Hooks:**
- Use `${CLAUDE_PLUGIN_ROOT}` for paths
- Event names exact: UserPromptSubmit, Stop, Notification

## Release Checklist

1. Update `.claude-plugin/plugin.json` version
2. Validate `hooks/hooks.json` structure
3. Test notification flow
4. Update README if features changed
