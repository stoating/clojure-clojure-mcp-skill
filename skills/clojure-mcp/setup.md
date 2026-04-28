# Setup

## Install

Prerequisites:

- Clojure CLI
- JDK 17 or later
- `ripgrep` is strongly recommended for faster search tools

Install globally with Clojure tools:

```bash
clojure -Ttools install-latest :lib io.github.bhauman/clojure-mcp :as mcp
```

This makes `clojure -Tmcp start` available.

## CLI Assistants

For Claude Code, Codex, and Gemini CLI, start with the `:cli-assist` profile. It keeps the assistant's native editing/shell workflow and adds ClojureMCP where it matters most.

```bash
claude mcp add clojure-mcp -- clojure -Tmcp start :config-profile :cli-assist
codex mcp add clojure-mcp -- clojure -Tmcp start :config-profile :cli-assist
gemini mcp add clojure-mcp clojure -Tmcp start :config-profile :cli-assist
```

Check the server manually from a project directory:

```bash
clojure -Tmcp start :config-profile :cli-assist
```

Expected startup output is JSON-RPC notifications for tools/resources/prompts list changes.

## Claude Desktop

Desktop clients launch MCP servers outside your project directory. Usually:

1. Start nREPL in the project.
2. Configure Claude Desktop to launch `clojure -Tmcp start` with `:not-cwd true` and the nREPL port.
3. Restart Claude Desktop.
4. Verify the `+` menu shows ClojureMCP tools/resources/prompts.

Example macOS Claude Desktop config:

```json
{
  "mcpServers": {
    "clojure-mcp": {
      "command": "/bin/zsh",
      "args": [
        "-c",
        "clojure -Tmcp start :not-cwd true :port 7888"
      ]
    }
  }
}
```

Use an explicit shell path that loads the same environment you use in terminals.

## API Keys

API keys are not required for basic ClojureMCP use. They are only needed for agent tools such as `dispatch_agent`, `architect`, and `code_critique`.

Relevant environment variables:

```bash
ANTHROPIC_API_KEY=...
OPENAI_API_KEY=...
GEMINI_API_KEY=...
```

If using Claude Desktop, ensure these variables are visible to the shell command that launches the MCP server.
