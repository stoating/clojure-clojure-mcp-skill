# Troubleshooting

## Server Starts But Client Shows No Tools

Check:

- MCP client was restarted after config changes.
- Command path and args are correct.
- `clojure -Tmcp start ...` works in a terminal.
- Desktop app has access to the same `PATH`, Java, Clojure CLI, and env vars.
- JSON-RPC startup output includes list-changed notifications.

## Wrong Project Directory

Desktop clients often launch outside the project. Use one of:

```bash
clojure -Tmcp start :not-cwd true :port 7888
clojure -Tmcp start :project-dir '"/path/to/project"'
```

`:not-cwd true` requires an nREPL connection and discovers the project directory through that connection.

## nREPL Connection Fails

Verify:

- nREPL is running.
- Port matches `:port`.
- Host matches `:host`.
- Firewall/container/sandbox permits the connection.
- The nREPL was started from the intended project directory.

Use:

```bash
clojure -M:nrepl
lein repl :headless :port 7888
```

## Auto-Start nREPL Does Not Work

`:start-nrepl-cmd` runs in the MCP process working directory. For CLI assistants this is usually the project directory. For Claude Desktop it is not.

For Claude Desktop, add `:project-dir`:

```bash
clojure -Tmcp start \
  :project-dir '"/path/to/project"' \
  :start-nrepl-cmd '["clojure" "-M:nrepl"]'
```

## Bash Tool Behaves Oddly

Check `:bash-over-nrepl`.

- `true`: bash runs over nREPL in an isolated session.
- `false`: bash runs locally in the MCP server process.

Use local mode when the nREPL target is not a normal JVM Clojure process, such as Babashka, Scittle, or some CLJS workflows.

## File Edit Blocked

Check `:write-file-guard`.

- `:partial-read`: collapsed or full reads allow editing.
- `:full-read`: only full reads allow editing.
- `false`: no read timestamp guard.

If a file changed externally after it was read, read it again before editing.

## Agent Tools Fail

`dispatch_agent`, `architect`, and `code_critique` may require API keys and model config.

Check:

```bash
ANTHROPIC_API_KEY
OPENAI_API_KEY
GEMINI_API_KEY
```

Also check `.clojure-mcp/config.edn` `:models` and `:tools-config`.

## Too Many or Too Few Tools

Use profile and filters:

```bash
clojure -Tmcp start :config-profile :cli-assist
clojure -Tmcp start :enable-tools '[:clojure_eval :read_file]'
clojure -Tmcp start :disable-tools '[:bash :dispatch_agent]'
```

Remember environment variables `ENABLE_TOOLS` and `DISABLE_TOOLS` override other filtering.
