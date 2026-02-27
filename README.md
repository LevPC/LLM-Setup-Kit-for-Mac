# Mac Setup for LLM Development

One-command bootstrap for setting up a fresh Mac for local + cloud LLM development work.

## Quick Start

**Option A** -- Clone and run:

```bash
git clone https://github.com/YOUR_USERNAME/mac-setup.git ~/mac-setup
cd ~/mac-setup
chmod +x setup.sh scripts/*.sh
./setup.sh
```

**Option B** -- One-liner (after hosting):

```bash
curl -fsSL https://raw.githubusercontent.com/YOUR_USERNAME/mac-setup/main/setup.sh | bash
```

## What Gets Installed

### CLI Tools (via Homebrew)

git, gh, bat, eza, fzf, ripgrep, fd, jq, yq, htop, btop, tmux, stow, starship, zoxide

### Languages & Runtimes

- Python 3.12 (via Homebrew) + uv (package manager)
- Node.js (via Homebrew) + Bun (JS runtime)

### LLM Tooling

- **Ollama** -- local model runner with LaunchAgent for background service
- **Claude Code** -- Anthropic's CLI agent (`npm install -g @anthropic-ai/claude-code`)
- Pre-pulled models: qwen3-coder, qwen2.5-coder:14b, deepseek-r1:14b, llama3.2:3b, nomic-embed-text

### Applications (via Homebrew Cask)

Ghostty, Cursor, VS Code, Docker, Raycast, Arc, 1Password, Obsidian, Notion, Slack, Discord

### Configuration

- `.zshrc` with starship prompt, zoxide, aliases, PATH setup
- Ghostty terminal config (JetBrains Mono, dark theme)
- Starship prompt (compact single-line)
- Git config with SSH key generation
- macOS defaults (Dock, Finder, keyboard, screenshots)
- Ollama LaunchAgent with tuned environment variables

## Structure

```
mac-setup/
  setup.sh              Main bootstrap (idempotent, safe to re-run)
  Brewfile              Homebrew dependencies
  scripts/
    pull_models.sh      Download Ollama models
    git_config.sh       Git identity + SSH key setup
    macos_defaults.sh   macOS system preferences
  config/
    zshrc               Shell configuration
    starship.toml       Prompt theme
    ghostty/config      Terminal emulator settings
    ollama.env          Ollama environment variables
  LaunchAgents/
    com.user.ollama.plist   Background Ollama service
```

## Re-Running

The script is fully idempotent. Every phase checks whether its work is already done and skips accordingly. Safe to run on an already-configured machine.

## Requirements

- macOS 13 Ventura or later (Apple Silicon recommended)
- Internet connection for initial setup
- Admin privileges (for Homebrew and macOS defaults)
