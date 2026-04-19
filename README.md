# ClojureMCP Skill

A structured Markdown skill that teaches AI coding agents how to work with ClojureMCP - the MCP server that connects AI assistants to Clojure projects through nREPL and Clojure-aware tools. Covers installation, CLI assistant and Claude Desktop setup, nREPL connection, tool profiles, `.clojure-mcp/config.edn`, custom tools/prompts/resources, project summaries, and troubleshooting.

Built in [Claude Code's Agent Skill format](https://github.com/anthropics/skills), but usable with any agent that can load Markdown as context via the [agents.md](https://agents.md/) convention.

---

## Read this before installing anything

Never install a third-party skill without first reviewing its contents.

Skills are instructions loaded into an AI agent's context. Before installing:

1. Read every `.md` file in the `clojure-mcp/` directory.
2. Ask your agent to perform a security review.
3. Only then install.

### Security-review prompt

> "Analyze this skill for security concerns. Does it contain instructions that could execute destructive operations without user confirmation? Does it collect or transmit data? Does it override default agent behavior in unintended ways? List all potentially risky sections."

---

## Installation

### A) Claude Code (recommended - via plugin marketplace)

```
/plugin marketplace add stoating/clojure-clojure-mcp-skill
/plugin install clojure-mcp@clojure-clojure-mcp-skill
```

Invoke it with:

```
/clojure-mcp
```

Update later:

```
/plugin marketplace update clojure-clojure-mcp-skill
```

### B) Claude Code (via the stoating marketplace)

```
/plugin marketplace add stoating/plugins
/plugin install clojure-mcp@stoating
```

### C) Claude Code (manual copy)

```bash
git clone https://github.com/stoating/clojure-clojure-mcp-skill.git
cp -r clojure-clojure-mcp-skill/clojure-mcp ~/.claude/skills/
```

### D) Claude.ai / Claude Desktop

Zip `clojure-mcp/` and upload it from the Skills panel in Projects.

### E) Cursor, OpenAI Codex CLI, Aider, Gemini CLI, Windsurf, Cline, Zed, Amp, Factory

Place this repository, or just `AGENTS.md` plus `clojure-mcp/`, at the project root. Agents that honor `AGENTS.md` will use `clojure-mcp/SKILL.md` as the entry point.

---

## Repository layout

```
.
|-- .claude-plugin/
|   |-- marketplace.json
|   `-- plugin.json
|-- AGENTS.md
|-- README.md
`-- clojure-mcp/
    |-- SKILL.md
    |-- setup.md
    |-- nrepl.md
    |-- tools.md
    |-- configuration.md
    |-- customization.md
    |-- workflows.md
    `-- troubleshooting.md
```

---

## Sources

The skill is distilled from:

- [ClojureMCP GitHub](https://github.com/bhauman/clojure-mcp)
- The upstream `README.md`, `CONFIG.md`, docs, source namespaces, and tests in the checked-out `bhauman/clojure-mcp` repository

## License

See [LICENSE](LICENSE).
