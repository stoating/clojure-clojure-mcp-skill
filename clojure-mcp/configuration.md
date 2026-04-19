# Configuration

Default config path:

```text
.clojure-mcp/config.edn
```

Override with:

```bash
clojure -Tmcp start :config-file '"/path/to/config.edn"'
```

## Core Settings

```clojure
{:allowed-directories ["src" "test" "resources"]
 :cljfmt true
 :write-file-guard :partial-read
 :bash-over-nrepl true
 :scratch-pad-load false
 :scratch-pad-file "scratch_pad.edn"}
```

| Key | Use |
|-----|-----|
| `:allowed-directories` | Restrict filesystem access |
| `:cljfmt` | `true`, `:partial`, or `false` for edit formatting |
| `:write-file-guard` | `:partial-read`, `:full-read`, or `false` |
| `:start-nrepl-cmd` | Auto-start nREPL command vector |
| `:bash-over-nrepl` | Run bash over nREPL instead of locally |
| `:scratch-pad-load` | Load scratch pad on startup |
| `:scratch-pad-file` | Scratch pad persistence filename under `.clojure-mcp/` |
| `:dispatch-agent-context` | Include project summary/code index in agent context |

## Tool Filtering

Filter exposed components with enable/disable lists.

```clojure
{:enable-tools [:clojure_eval :read_file :grep]
 :disable-tools [:bash :dispatch_agent]}
```

CLI overrides:

```bash
clojure -Tmcp start :enable-tools '[:clojure_eval :read_file]'
clojure -Tmcp start :disable-tools '[:bash]'
clojure -Tmcp start :config-profile :cli-assist :add-tools '[:architect]'
clojure -Tmcp start :config-profile :cli-assist :remove-tools '[:clojure_eval]'
```

Application order:

1. Home/project/profile config merge.
2. CLI `:enable-tools` and `:disable-tools` replace config values.
3. `:remove-tools` force-disables.
4. `:add-tools` force-enables and wins on overlap.
5. `ENABLE_TOOLS` and `DISABLE_TOOLS` environment variables still win.

## Tool-Specific Config

```clojure
{:tools-config
 {:dispatch_agent {:model :openai/my-o3}
  :architect {:model :anthropic/my-claude}
  :bash {:default-timeout-ms 60000
         :working-dir "/path/to/project"
         :bash-over-nrepl false}}

 :models
 {:openai/my-o3 {:model-name "o3-mini"
                 :temperature 0.2
                 :api-key [:env "OPENAI_API_KEY"]}
  :anthropic/my-claude {:model-name "claude-3-haiku-20240307"
                        :api-key [:env "ANTHROPIC_API_KEY"]}}}
```

Only configure model-backed tools when the required API key and token budget are intentional.
