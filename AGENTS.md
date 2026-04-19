# Agent instructions

This repository contains the **`clojure-mcp`** skill - a structured set of Markdown files that teach an AI coding agent how to work with ClojureMCP, the MCP server for REPL-driven Clojure development with AI assistants.

**Any agent that understands this `AGENTS.md` convention should:**

1. Treat `clojure-mcp/SKILL.md` as the entry point - it contains a decision table pointing to the right reference file for the task.
2. Load reference files on demand based on that table:
   - `setup.md` - install, CLI assistant setup, Claude Desktop setup, API keys
   - `nrepl.md` - nREPL aliases, ports, auto-start, project-dir, multiple REPLs
   - `tools.md` - tool categories, `:cli-assist`, structural editing, bash behavior
   - `configuration.md` - `.clojure-mcp/config.edn`, allowed dirs, tool filters, tool model config
   - `customization.md` - custom tools, prompts, resources, custom MCP servers
   - `workflows.md` - project summaries, chat resume, REPL-driven development
   - `troubleshooting.md` - connection, path, nREPL, editing, and agent-tool issues
3. Clarify whether the user is configuring a CLI assistant or a desktop MCP client before recommending commands.
4. Prefer `:config-profile :cli-assist` for CLI coding assistants unless the user explicitly wants the full ClojureMCP toolchain.
5. Treat API-backed agent tools as opt-in because they can incur provider charges.

This file follows the [agents.md](https://agents.md/) convention and is honored by OpenAI Codex CLI, Cursor, Aider, Zed, Amp, Gemini CLI, Google Jules, Windsurf, Factory, RooCode, and many others.

For Claude Code, the richer native format is `.claude-plugin/` + `clojure-mcp/SKILL.md`.
