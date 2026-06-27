# plugai

> AI-powered CLI tool that analyzes your project and recommends the best open-source libraries from GitHub.

![Go](https://img.shields.io/badge/Go-1.21+-00ADD8?style=flat&logo=go)
![License](https://img.shields.io/badge/License-MIT-green)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue)

---

## What is plugai?

**plugai** scans your project, detects your tech stack, and uses AI to recommend open-source libraries you might be missing — with real GitHub star counts and ready-to-copy install commands.

No generic suggestions. Only libraries relevant to **your** project.

---

## How it works

```
Your project folder
       ↓
[Stack Detection]     → reads package.json, go.mod, requirements.txt, etc.
       ↓
[AI Analysis]         → sends context to AI (Claude, GPT-4, GitHub Copilot, Ollama...)
       ↓
[GitHub Search API]   → fetches real star counts for each recommendation
       ↓
[Interactive TUI]     → pick what to install, copy the command
```

---

## Features

- **Auto stack detection** - Go, Node.js, Python, Rust, Java, PHP, Ruby
- **Any AI provider** - works with Claude, OpenAI, GitHub Copilot (via copilot-api), Groq, Ollama
- **Real GitHub data** - star counts fetched live from GitHub Search API
- **Interactive TUI** - navigate with arrow keys, select plugins to install
- **ASCII-safe UI** - works in Windows CMD and Linux terminal
- **JSON output** - pipe results into other tools with `--json`
- **Analyze GitHub repos** - pass `--repo` to analyze any public repo without cloning

---

## Installation

### From source

```bash
git clone https://github.com/aisultan/plugai
cd plugai
go build -o plugai .
```

### Requirements

- Go 1.21+
- An AI provider (see below)

---

## Usage

```bash
# Analyze current directory
plugai --ai-url http://localhost:4141 --ai-key dummy --ai-model gpt-4.1

# Analyze a GitHub repo
plugai --repo https://github.com/user/project --ai-key sk-ant-xxx

# JSON output
plugai --json > analysis.json
```

### Flags

| Flag        | Description                        | Default                        |
|-------------|------------------------------------|--------------------------------|
| `--ai-url`  | AI provider base URL               | `https://api.anthropic.com`    |
| `--ai-key`  | API key                            | env: `PLUGAI_AI_KEY`           |
| `--ai-model`| Model name                         | `claude-sonnet-4-6`            |
| `--repo`    | GitHub repo URL to analyze         | current directory              |
| `--json`    | Output raw JSON                    | false                          |
| `--copilot` | Use local copilot-api on port 4141 | false                          |

---

## AI Providers

plugai works with any OpenAI-compatible API endpoint:

```bash
# GitHub Copilot (free with Copilot subscription)
# First run: npx copilot-api@latest start
plugai --copilot

# Claude (Anthropic)
plugai --ai-url https://api.anthropic.com --ai-key sk-ant-xxx --ai-model claude-sonnet-4-6

# OpenAI
plugai --ai-url https://api.openai.com --ai-key sk-xxx --ai-model gpt-4o

# Groq (free tier available)
plugai --ai-url https://api.groq.com/openai --ai-key gsk_xxx --ai-model llama3-70b-8192

# Ollama (fully local, free)
plugai --ai-url http://localhost:11434 --ai-key none --ai-model llama3
```

---

## Example Output

```
plugai v1.0 - AI Plugin Recommender
=====================================

[*] Project Analysis
This is a Go CLI project using cobra and bubbletea. Missing: structured
logging, config management, and test utilities.

[+] Recommended Plugins

+------------------------+--------+----------------------------------+----------+
| Plugin                 | Stars  | Install                          | Priority |
+------------------------+--------+----------------------------------+----------+
| sirupsen/logrus        | 25,736 | go get github.com/sirupsen/...   | Critical |
| spf13/viper            | 30,337 | go get github.com/spf13/viper    | Useful   |
| stretchr/testify       | 26,043 | go get github.com/stretchr/...   | Useful   |
| golangci/golangci-lint | 19,109 | go install github.com/...        | Optional |
+------------------------+--------+----------------------------------+----------+

Select plugins to install (space to toggle, enter to confirm):
> [ ] sirupsen/logrus
  [ ] spf13/viper
  [ ] stretchr/testify
```

---

## Supported Languages

| Language | File detected         |
|----------|-----------------------|
| Go       | `go.mod`              |
| Node.js  | `package.json`        |
| Python   | `requirements.txt`, `pyproject.toml` |
| Rust     | `Cargo.toml`          |
| Java     | `pom.xml`, `build.gradle` |
| PHP      | `composer.json`       |
| Ruby     | `Gemfile`             |

---

## Tech Stack

- [Go 1.21+](https://golang.org)
- [Cobra](https://github.com/spf13/cobra) — CLI framework
- [Bubbletea](https://github.com/charmbracelet/bubbletea) — TUI framework
- [Lipgloss](https://github.com/charmbracelet/lipgloss) — terminal styling
- [GitHub Search API](https://docs.github.com/en/rest/search) — star counts
- Any OpenAI-compatible AI API

---

## License

MIT
