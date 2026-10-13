# Optimus

Optimus is an AI coding assistant for your terminal. It helps you read code, edit files, run commands, and work on software projects using your preferred AI model.

Optimus CLI is available today. A desktop app is planned for a future release.

## Features

- Works in your terminal: chat with AI directly from your command line.
- Multiple languages: English, French, Spanish, German, Chinese, and Japanese.
- Smart file editing: reviews your project, plans changes, and edits files safely.
- Multiple AI providers: works with Claude, OpenAI, Google Gemini, Ollama, and compatible services.
- Permission control: choose how much autonomy the assistant has (ask before editing, auto-apply, or plan only).
- Background tasks: run and monitor long commands while continuing to chat.
- Private: connects directly to your AI provider with no tracking, telemetry, or middleman servers.

## Installation

Optimus is available as a standalone app for Windows, macOS, and Linux.

| System | Command |
| --- | --- |
| Homebrew (macOS / Linux) | `brew install brightbraincoder/optimus/optimus-cli` |
| Scoop (Windows) | `scoop bucket add optimus https://github.com/brightbraincoder/optimus-releases`<br>`scoop install optimus/optimus-cli` |
| WinGet (Windows) | `winget install BrightBrainCoder.OptimusCli` |
| Arch Linux (AUR) | `yay -S optimus-cli-bin` |
| Standalone binary | Download directly from [GitHub Releases](https://github.com/brightbraincoder/optimus-releases/releases) |

### Check your download

You can verify your download with the SHA-256 hash in `checksums.txt`:

```sh
# macOS / Linux
sha256sum -c checksums.txt

# Windows (PowerShell)
Get-FileHash -Algorithm SHA256 optimus.exe
```

## Getting Started

### 1. Start Optimus

Open your terminal in any project folder and run:

```sh
optimus
```

### 2. First-time setup

The first time you run Optimus, a quick guide helps you choose:
- Display language
- Color theme
- AI provider and API key
- Default model

### 3. Ask for changes

Ask for what you want in simple words:

```
> Check src/auth.ts, add refresh tokens, and run the tests.
```

Optimus inspects your code, shows proposed changes, runs tests, and asks for confirmation when required by your permission settings.

### Useful shortcuts

- Shift+Tab: Change permission mode (manual, ask to edit, plan only, or auto).
- Escape: Stop the current task or response.
- Ctrl+L: View activity logs.
- @filename: Add a file directly to your prompt.

## Commands

Type these commands in the chat for quick actions:

| Command | Description |
| --- | --- |
| /help | Show available commands and help |
| /lang [code] | Change the display language |
| /settings | Open settings menu |
| /new | Start a fresh conversation |
| /resume | Reopen a previous conversation |
| /sessions | List saved conversations |
| /plan [task] | Create a plan before making changes |
| /think [level] | Set reasoning level (off, low, medium, high, max) |
| /model [name] | Switch AI provider or model |
| /tasks | View or stop running background tasks |
| /logs | Show recent activity logs |
| /quit | Exit Optimus |

## Configuration

Settings are saved in:
- Global settings: `~/.optimus/config.json`
- Project settings: `.optimus/config.json`

You can change most settings with the `/settings` command inside Optimus, without editing files manually.

Example configuration:

```json
{
  "theme": "dark",
  "language": "en",
  "permissionMode": "acceptEdits",
  "provider": "anthropic",
  "model": "claude-3-7-sonnet"
}
```

## Privacy and Security

- Direct connections: Optimus talks directly to your selected AI provider. No intermediate servers or telemetry.
- Safe defaults: Protected files (like `.git` and `.env`) are blocked from accidental edits.
- Local keys: Your API keys stay on your machine.
- For full details, see [PRIVACY.md](https://github.com/brightbraincoder/optimus-releases/blob/main/PRIVACY.md).

## License

Optimus is proprietary software. Copyright BrightBrainCoder. All rights reserved.

---

Built by BrightBrainCoder.
