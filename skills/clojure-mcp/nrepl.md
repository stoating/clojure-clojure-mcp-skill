# nREPL

## Basic nREPL Alias

For deps.edn projects:

```clojure
{:aliases
 {:nrepl
  {:extra-paths ["test"]
   :extra-deps {nrepl/nrepl {:mvn/version "1.3.1"}}
   :main-opts ["-m" "nrepl.cmdline" "--port" "7888"]}}}
```

Start it:

```bash
clojure -M:nrepl
```

For Leiningen:

```bash
lein repl :headless :port 7888
```

## ClojureMCP CLI Arguments

Values passed to `clojure -Tmcp start` are EDN values.

```bash
clojure -Tmcp start :port 7888
clojure -Tmcp start :host '"localhost"' :port 7888
clojure -Tmcp start :project-dir '"/path/to/project"'
```

Important options:

| Option | Use |
|--------|-----|
| `:port` | nREPL port to connect to |
| `:host` | nREPL host, defaults to localhost |
| `:not-cwd true` | Discover project dir through nREPL instead of MCP process cwd |
| `:project-dir` | Explicit project directory |
| `:start-nrepl-cmd` | Start an nREPL process automatically |
| `:nrepl-env-type` | Force environment type such as `:clj`, `:bb`, `:basilisp`, `:scittle` |
| `:shadow-cljs-repl-message false` | Suppress shadow-cljs REPL status message |

## Auto-Start nREPL

For CLI assistants launched from the project directory:

```bash
clojure -Tmcp start :start-nrepl-cmd '["clojure" "-M:nrepl"]'
clojure -Tmcp start :start-nrepl-cmd '["lein" "repl" ":headless"]'
```

Without `:port`, ClojureMCP parses the port from command output. With `:port`, it uses the fixed port.

Claude Desktop does not launch from the project directory, so pair auto-start with `:project-dir`:

```bash
clojure -Tmcp start \
  :project-dir '"/path/to/project"' \
  :start-nrepl-cmd '["clojure" "-M:nrepl"]'
```

## Multiple REPLs

Use ClojureMCP's `list_nrepl_ports` tool to discover running nREPL servers, including shadow-cljs instances. `clojure_eval` accepts a `port` parameter when the assistant needs to target a specific REPL.

For shadow-cljs, ensure the REPL is in the expected build/runtime context before evaluating code.
