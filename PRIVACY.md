# Privacy Policy for Optimus

**Last Updated:** September 2026  
**Publisher:** BrightBrainCoder  
**Repository:** https://github.com/brightbraincoder/optimus-releases

---

## Overview

Optimus is an autonomous, terminal-based AI coding assistant developed by BrightBrainCoder. Optimus is engineered with a **local-first architecture**. All core execution, file management, workspace analysis, session management, and shell execution occur directly on your local workstation.

BrightBrainCoder does not operate intermediate proxy servers or telemetry databases that ingest, store, inspect, or monetize your code, prompts, credentials, or session history.

---

## 1. Data Transmission and Model Providers

### Direct Client-to-Provider Communication
When you interact with Optimus, workspace context (such as file snippets, diffs, directory structures, terminal command output, and user prompts) is packaged into context requests and transmitted **directly from your local machine to the Large Language Model (LLM) API provider** configured in your environment or settings.

Supported LLM providers include, but are not limited to:
- Anthropic (Claude API)
- OpenAI (GPT models)
- Google (Gemini API)
- Ollama / Local LLM inference engines
- Custom OpenAI-compatible endpoints

### Third-Party Provider Policies
Because communications flow directly between your machine and your chosen provider, data processing and retention are governed by the respective terms of service and privacy policies of that provider:
- **Anthropic:** https://www.anthropic.com/privacy
- **OpenAI:** https://openai.com/policies/privacy-policy
- **Google Gemini:** https://policies.google.com/privacy

BrightBrainCoder has no visibility into or control over the data processed by third-party model providers.

---

## 2. API Keys and Credentials

- **Local Storage:** API keys, access tokens, OAuth credentials, and custom endpoint configurations are stored strictly on your local machine (e.g., in your user directory `~/.optimus/` or OS keychain when configured).
- **Zero Ingestion:** Optimus never transmits your API keys or credentials to BrightBrainCoder or any third party other than the intended model provider for HTTP authentication.
- **Environment Isolation:** Optimus reads environment variables (such as `ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `GEMINI_API_KEY`) in-memory and does not leak or write them to shared logs.

---

## 3. Local Data Storage, Retention, and Deletion

All persistent artifacts generated during your use of Optimus remain under your complete control on your local filesystem:
- **Conversation Transcripts & Checkpoints:** Stored in `~/.optimus/` and workspace `.o-agent/` directories for undo history, session resumption, and audit logs.
- **SQLite Database:** Local vector indexes, code graph metadata, and token usage ledgers are stored in local SQLite databases.
- **Data Deletion:**
  - You can remove session history and cached checkpoints at any time from within the CLI using the `/purge` command.
  - You can completely erase all local data by deleting the `~/.optimus` directory and any `.o-agent` workspace directories.

---

## 4. Sensitive Data and PII Protection

Optimus includes an integrated redaction subsystem (`redaction-pii` plugin) that helps prevent unintentional leakage of sensitive data:
- Masks common patterns such as email addresses, IP addresses, credit card numbers, private keys, and secret access tokens prior to context serialization.
- Users can customize and extend pattern filters in their local configuration.

---

## 5. Telemetry and Analytics

- **No Remote Telemetry:** Optimus CLI does not collect, transmit, or sell tracking analytics, usage telemetry, or profiling data.
- **Local Diagnostics Only:** Any debug logs generated during troubleshooting are written strictly to local temporary files and are only shared if you voluntarily attach them to a GitHub issue.

---

## 6. Security and Vulnerability Reporting

If you discover a potential security or privacy issue in Optimus, please report it via our GitHub issues repository:
- **Issue Tracker:** https://github.com/brightbraincoder/optimus-releases/issues
- **Contact:** BrightBrainCoder Security Team

---

## 7. Changes to This Policy

We may update this Privacy Policy periodically to reflect enhancements in the software or changes in applicable regulations. Any updates will be published in the public `brightbraincoder/optimus-releases` repository.
