# Optimus

> **Product Availability Note**: The production-ready, distributed product currently available is **Optimus CLI** (`optimus`), an autonomous command-line AI coding assistant. The desktop application (**Optimus Desktop**) and the multi-tenant service mode (Fastify backend, web chat widget, admin backoffice) are currently **in active development** and will be released in future standalone distributions.

Optimus is an autonomous, high-performance command-line AI coding assistant built for developers. Operating directly within your terminal, Optimus inspects codebases, plans multi-step refactorings, applies precise transactional Myers diffs, executes shell commands and supervised background tasks, and collaborates with language models under strict user-controlled permission boundaries.

---

## Key Highlights

- **Native Multilingual Architecture**: Full internationalization across 6 languages (English, Francais, Espanol, Deutsch, 中文, 日本語) with instant dynamic switching via `/lang [locale]` or the interactive `/settings` panel.
- **Autonomous Multi-Agent Swarm**: Parallel sub-agent execution with bounded capacity, hermetic mailboxes, and isolated execution contexts.
- **Granular Permission Modes**: Cycle dynamically (`Shift+Tab`) across `manual`, `acceptEdits`, `plan`, `auto`, and `bypassPermissions` tiers.
- **Transactional Code Editing**: Myers diff algorithm with linear memory complexity $O(N+M)$ and atomic file operations (open-write-fsync-rename) preventing data corruption.
- **Ultra-Responsive TUI Engine**: Custom React terminal renderer (@o-agent/o-ui) with ANSI/VT pipeline, sub-50ms Escape key cancellation, and spatial focus navigation.
- **Supervised Background Tasks**: Launch, monitor, stream logs, and cleanly terminate long-running processes and sub-processes (`/tasks`).
- **Universal Provider Connectivity**: Seamless integration with Anthropic Claude, OpenAI, Google Gemini, Ollama, and custom OpenAI-compatible endpoints.
- **Zero-Intermediary Privacy**: Direct-to-provider API calls. No telemetry collection, no proxy servers, no external tracking. Fully compliant with [PRIVACY.md](https://github.com/brightbraincoder/optimus-releases/blob/main/PRIVACY.md).

---

## Interactive Slash Commands

| Command | Description |
|---|---|
| `/help` | Display comprehensive usage instructions, shortcuts, and command references |
| `/lang [locale]` | View active language or switch instantly across English, Francais, Espanol, Deutsch, 中文, 日本語 |
| `/settings` | Interactively inspect and modify global and project configuration parameters with live hot-reloading |
| `/sessions` | List, filter, and inspect local conversation histories and metadata |
| `/resume` | Resume an existing conversation session by identifier or index |
| `/new` | Reset context and start a clean session in the current directory |
| `/plan [goal]` | Generate an architectural implementation plan before executing code changes |
| `/think <level>` | Adjust model reasoning effort (`off`, `low`, `medium`, `high`, `max`) |
| `/model [alias]` | Switch active LLM provider and model architecture on the fly |
| `/compact` | Trigger manual context compaction and history summarization |
| `/tasks` | Manage supervised background tasks, inspect live logs, and terminate processes |
| `/purge` | Purge local session history, cached checkpoints, and workspace state |
| `/logs` | Open the interactive diagnostic session event ring buffer (`Ctrl+L`) |
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
- Language selection (English, Francais, Espanol, Deutsch, 中文, 日本語).
- Color palette selection (Dark, Light, Daltonized, High-Contrast ANSI-16).
- Security policy acknowledgement.
- Provider authentication (OAuth for Claude, or API keys for Anthropic, OpenAI, Gemini, Ollama).
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

1. **Global Configuration** (`~/.optimus/config.json`): System-wide defaults including active theme, language, default permission tier, model aliases, and provider endpoints.
2. **Project Configuration** (`<project>/.optimus/config.json`): Repository-specific settings, path allow/deny rules, test runner configurations, and project instructions.
3. **Environment Variables & CLI Flags**: Highest precedence per command invocation (e.g., `--lang=fr`, `OPTIMUS_MODEL`, `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `GEMINI_API_KEY`).

### Example Configuration (`config.json`)

```json
{
  "theme": "dark",
  "language": "en",
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

- **Internationalization Engine (@o-agent/i18n)**: Zero-latency O(1) translation lookup, Unicode UAX #11 visual width metrology, and CLDR pluralization rules.
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
