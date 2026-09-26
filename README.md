<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/wordmark-dark.svg">
    <img src="assets/wordmark-light.svg" alt="Optimus" width="360">
  </picture>
</p>

<p align="center">
  <strong>Autonomous, ultra-fast terminal AI coding assistant designed for professional engineers.</strong>
</p>

<p align="center">
  <a href="#overview">Overview</a> ·
  <a href="#key-features">Key Features</a> ·
  <a href="#slash-commands">Slash Commands</a> ·
  <a href="#installation">Installation</a> ·
  <a href="#quick-start">Quick Start</a> ·
  <a href="#configuration">Configuration</a> ·
  <a href="#architecture">Architecture</a> ·
  <a href="#privacy-security--license">Privacy & License</a>
</p>

---

## Overview

**Optimus** is an autonomous, high-performance terminal AI coding assistant built for professional software developers. It reads codebases, drafts Myers diffs, executes verified file edits, runs tests and shell commands, and orchestrates complex multi-agent workflows directly inside your terminal.

Built on a **100% Local-First Architecture**, Optimus executes everything locally on your workstation. Your source code, file contents, workspace indexes, and session histories remain strictly on your machine. API calls are transmitted directly from your workstation to your configured model provider without intermediary proxies or telemetry servers.

For full details on data handling and confidentiality, see our [Privacy Policy (PRIVACY.md)](https://github.com/brightbraincoder/optimus-releases/blob/main/PRIVACY.md).

---

## Key Features

### Multi-Agent Swarm Engine
- **Parallel Subagent Orchestration**: Launch, supervise, and coordinate autonomous subagents concurrently for complex refactoring, parallel testing, and deep workspace exploration.
- **Dynamic Capacity Control**: Automatic workload distribution and capacity throttling prevent rate-limit exhaustion and context saturation across agent trees.

### Granular Permission Modes
Control agent autonomy with five granular security tiers, switchable on the fly (`Shift+Tab`):
- `manual`: Prompt for explicit confirmation before every tool call, file modification, and shell execution.
- `acceptEdits`: Automatically apply workspace file modifications while requiring confirmation for shell execution and sensitive operations.
- `plan`: Purely read-only exploration and architecture analysis; outputs an executable plan file before any write reaches disk.
- `auto`: Autonomous execution with automated heuristic evaluation of risky operations.
- `bypassPermissions`: Autonomous execution governed strictly by an immutable system denylist.

### Transactional Editing & Myers Diff Engine
- **Atomic Operations**: File writes and multi-file patches are applied atomically with automated rollback mechanisms to prevent workspace corruption.
- **Myers Diff O((N+M)D)**: High-performance differential generation ensures minimal, precise line-by-line modifications with live terminal visual previews.
- **Stale Content Protection**: Edits are automatically rejected if target files were modified externally since the last read.

### High-Performance Terminal Interface (`@o-agent/o-ui`)
- **Instant Escape Interruption**: Sub-50ms keystroke reactivity instantly halts running agent loops, tool executions, or streaming completions.
- **Virtualized Rendering**: Handles massive transcripts and hundreds of sequential tool calls with zero UI lag.
- **Rich Terminal Markdown**: Syntax-highlighted code blocks, tables, ANSI-16 / TrueColor themes, and full mouse support (scrolling, clicking, selection).

### Supervised Background Tasks (`/tasks`)
- **Process Isolation**: Long-running builds, servers, and test suites run in managed background processes.
- **Orphan Tree Detection**: Active process tree tracking prevents dangling zombie processes upon session termination.
- **Interactive Inspection**: Real-time log streaming, status queries, input forwarding, and task termination.

### Universal Multi-Provider Connectivity
Connect seamlessly to any frontier or self-hosted LLM:
- **Anthropic**: Claude 3.5 Sonnet, Claude 3.7 Sonnet (with hybrid reasoning), Claude 3 Opus, Claude 3.5 Haiku (API keys and OAuth).
- **OpenAI**: GPT-4o, GPT-4o-mini, o1, o3-mini.
- **Google**: Gemini 2.0 Flash, Gemini 2.0 Pro, Gemini 1.5 Pro.
- **Local & Self-Hosted**: Ollama, vLLM, LM Studio, LocalAI, and any OpenAI- or Anthropic-compatible HTTP endpoint.

---

## Slash Commands

| Command | Description |
|---|---|
| `/help` | Display command catalog, keyboard shortcuts, and active configuration summary |
| `/sessions` | List all saved conversation sessions across projects with metadata |
| `/resume` | Resume a previous session with full context, transcript, and tool history |
| `/new` | Initialize a fresh conversation session in the current workspace |
| `/think` | Configure model reasoning effort (`off`, `low`, `medium`, `high`, `max`) |
| `/plan` | Enter read-only planning mode to design changes before execution |
| `/model` | Switch the active LLM provider or model architecture on the fly |
| `/compact` | Trigger manual context compaction and history summarization |
| `/tasks` | Manage supervised background tasks, inspect logs, and terminate processes |
| `/purge` | Purge local session history, cached checkpoints, and workspace state |
| `/logs` | Open the interactive diagnostic session log (`Ctrl+L`) |
| `/settings` | Interactively inspect and modify global and project configuration parameters |
| `/quit` | Safely terminate active processes and exit Optimus |

---

## Installation

Optimus is distributed as standalone, zero-dependency compiled binaries for Windows, macOS, and Linux on both `x64` and `arm64` architectures.

| Platform / Manager | Installation Command |
|---|---|
| **Homebrew** (macOS / Linux) | `brew install brightbraincoder/optimus/optimus-cli` |
| **Scoop** (Windows) | `scoop bucket add optimus https://github.com/brightbraincoder/optimus-releases`<br>`scoop install optimus/optimus-cli` |
| **Winget** (Windows) | `winget install BrightBrainCoder.OptimusCli`<br>*(Submission PR: [microsoft/winget-pkgs#426342](https://github.com/microsoft/winget-pkgs/pull/426342))* |
| **AUR** (Arch Linux) | `yay -S optimus-cli-bin` *(or your preferred AUR helper)* |
| **Direct Binary Download** | Download standalone binaries from [GitHub Releases](https://github.com/brightbraincoder/optimus-releases/releases) |

### Binary Integrity Verification
Every release includes a cryptographic `checksums.txt` file containing SHA-256 hashes. Verify your download:

```sh
# macOS / Linux
sha256sum -c checksums.txt

# Windows (PowerShell)
Get-FileHash -Algorithm SHA256 optimus.exe
```

---

## Quick Start

### 1. Launch Optimus
Navigate to your project root and start the CLI:

```sh
cd /path/to/your/project
optimus
```

### 2. Onboarding Setup
On the first launch, the interactive onboarding wizard will guide you through:
- Color palette selection (Dark, Light, Daltonized, High-Contrast ANSI-16).
- Security policy acknowledgment.
- Provider authentication (OAuth for Claude, or API key for Anthropic, OpenAI, Gemini, Ollama).
- Default model selection.

### 3. Prompting & Iteration
Provide instructions in natural language:

```
> Analyze src/auth/jwt.ts, add refresh token rotation, and write comprehensive unit tests.
```

Optimus inspects dependencies, plans edits, generates Myers diffs, runs tests, and requests confirmation according to your active permission mode.

### Useful Daily Shortcuts
- `Shift+Tab`: Cycle permission mode (`manual` -> `acceptEdits` -> `plan` -> `auto` -> `bypassPermissions`).
- `Escape`: Instantly halt active generation or tool execution (< 50ms).
- `Ctrl+L`: Toggle live event and tool call diagnostic logs.
- `@filename`: Inject file or directory contents directly into prompt context.

---

## Configuration

Optimus uses a hierarchical configuration cascade:

1. **Global Configuration** (`~/.optimus/config.json`): System-wide defaults including active theme, default permission tier, model aliases, and provider endpoints.
2. **Project Configuration** (`<project>/.optimus/config.json`): Repository-specific settings, path allow/deny rules, test runner configurations, and project instructions.
3. **Environment Variables & CLI Flags**: Highest precedence per command invocation (e.g., `OPTIMUS_MODEL`, `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `GEMINI_API_KEY`).

### Example Configuration (`config.json`)

```json
{
  "theme": "dark",
  "permissionMode": "acceptEdits",
  "provider": "anthropic",
  "model": "claude-3-7-sonnet",
  "reasoningEffort": "medium",
  "autoCompactThreshold": 0.85,
  "telemetry": false
}
```

You can modify settings directly via the `/settings` slash command inside the CLI without manually editing JSON files.

---

## Architecture

Optimus is structured around an extensible, modular agentic core:

- **Pluggable Loop Plugins**: Lifecycle hooks before and after every reasoning cycle for PII redaction, prompt-injection defense, automated compaction, and audit logging.
- **Provider Abstraction Layer**: Unified protocol for streaming tokens, thinking blocks, tool calls, and prompt caching breakpoints across diverse LLM backends.
- **Skill Engine**: On-demand procedural knowledge bundles loaded dynamically based on task context without bloating baseline system prompts.
- **Sandboxed Tool Runtime**: Isolated execution environment for file manipulation, semantic AST search, process supervision, and shell command evaluation.

---

## Privacy, Security & License

### Privacy & Data Ownership
- **Zero Intermediary Servers**: Optimus communicates directly with your chosen LLM provider API. BrightBrainCoder does not host telemetry relays, proxy proxies, or ingestion backends.
- **No Remote Telemetry**: Usage metrics, prompts, source code, and credentials are never collected or transmitted.
- **Comprehensive Policy**: Review the full [PRIVACY.md](https://github.com/brightbraincoder/optimus-releases/blob/main/PRIVACY.md) document for complete details.

### Security
- **Denylist Safeguards**: Protected system files (`.git`, `.env`, shell configurations) and destructive commands are blocked across all permission modes.
- **Local Credential Storage**: Authentication tokens and API keys are stored exclusively on your local workstation.

### License
Optimus is proprietary software. Copyright BrightBrainCoder. All rights reserved. Redistribution of compiled binaries is authorized solely through the official package managers and release channels listed in this repository. Source code is proprietary and not licensed for unauthorized modification, decompilation, or redistribution.

---

<p align="center"><sub>Built by <strong>BrightBrainCoder</strong></sub></p>
