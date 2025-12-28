# Suiying (随影)

My personal Claude Code plugin - a self-hosted collection of preferred configs, workflows, and development practices.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Features

### 🔔 Desktop Notifications (CCNotify Integration)
Get macOS notifications when Claude Code needs your input or completes tasks:
- Task completion notifications with duration tracking
- Permission/approval prompts
- Clickable notifications that jump back to Windsurf IDE

### 🔍 Code Review Tools
- `/suiying:code-review` - Comprehensive code review
- `/suiying:design-review` - Architecture and design review
- `/suiying:security-review` - Security-focused review

### 🤖 Specialized Agents
- **pragmatic-code-review** - Practical code review focusing on maintainability
- **design-review** - Architecture and design analysis

### 📚 Skills
- **design-principles** - Software design best practices and patterns

## Installation

### Prerequisites
- macOS only (for notifications)
- `terminal-notifier` (for desktop notifications)
  ```bash
  brew install terminal-notifier
  ```

### Option 1: Install via Marketplace (Recommended)

The easiest way to install:

```bash
# Add the marketplace
/plugin marketplace add nmhjklnm/suiying-marketplace

# Install the plugin
/plugin install suiying@suiying-marketplace
```

That's it! The plugin will be automatically installed and ready to use.

### Option 2: Local Development (Symlink)

For local development and testing:

```bash
# Clone the repository
git clone https://github.com/nmhjklnm/suiying-marketplace.git

# Create symlink to Claude plugins directory
ln -s "$(pwd)/suiying-marketplace" ~/.claude/plugins/suiying

# Reload plugin in Claude Code after making changes
```

## Structure

```
suiying-plugin/
├── .claude-plugin/
│   ├── plugin.json          # Plugin metadata
│   └── marketplace.json     # Marketplace config
├── commands/                # Custom slash commands
├── skills/                  # Auto-activating knowledge
├── agents/                  # Specialized subagents
├── hooks/                   # Event-driven automation
│   └── hooks.json           # Desktop notification hooks
└── scripts/                 # Helper utilities
    └── ccnotify.py          # Notification script
```

## Usage

After installation, all commands, skills, and agents become available automatically.

### Available Commands

```bash
# Code review commands
/suiying:code-review [file-or-directory]
/suiying:design-review [file-or-directory]
/suiying:security-review [file-or-directory]
```

### Desktop Notifications

Desktop notifications work automatically through hooks:
- Get notified when Claude needs your input
- Track task completion times
- Click notifications to jump back to Windsurf IDE

### Testing Notifications

To test if notifications are working:

```bash
# Start Claude Code
claude

# Run a quick test
after 1 second, echo 'hello'
```

You should see a macOS notification appear!

## Credits

- **CCNotify Integration**: Based on [CCNotify](https://github.com/dazuiba/CCNotify) by dazuiba

## Contributing

This is a personal plugin, but feel free to fork and adapt for your own needs!

## License

MIT - see [LICENSE](LICENSE) file for details
