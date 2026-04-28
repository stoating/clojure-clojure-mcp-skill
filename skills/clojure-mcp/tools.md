# Tools

## Tool Categories

Read-only tools:

- `LS` - recursive tree view
- `read_file` - smart Clojure-aware file reader with collapsed view and pattern search
- `grep` - content search
- `glob_files` - file pattern search

REPL and shell:

- `clojure_eval` - evaluate forms through nREPL, with optional port selection
- `list_nrepl_ports` - discover running nREPL servers
- `bash` - run shell commands, locally or over nREPL depending on config

Editing:

- `clojure_edit` - structure-aware form replacement/insertion
- `clojure_edit_replace_sexp` - replace an expression inside a form
- `file_edit` - string replacement with parinfer repair where useful
- `file_write` - write files with safety checks

Agent tools:

- `dispatch_agent` - read-only autonomous exploration
- `architect` - technical planning
- `code_critique` - iterative code review

Experimental:

- `scratch_pad` - structured session workspace with optional persistence

## CLI Assist Profile

Use `:config-profile :cli-assist` for CLI coding assistants. It disables redundant tools and describes `clojure_edit` as a fallback when native edit fails.

```bash
clojure -Tmcp start :config-profile :cli-assist
```

Good default division of labor:

- Use the assistant's native file edit and shell tools for normal edits.
- Use ClojureMCP for `clojure_eval`, `list_nrepl_ports`, delimiter repair, and structural edit fallback.
- Use `dispatch_agent`, `architect`, or `code_critique` only when API keys and token costs are intentional.

## Smart File Reading

`read_file` provides Clojure-aware collapsed views for large files and supports pattern-focused reads.

Use collapsed reads for orientation. Use full reads before editing when the config requires full-read write guards or when exact surrounding context matters.

## Structural Editing

`clojure_edit` targets forms by type and name instead of fragile text ranges. It is useful when:

- Text replacement does not match due to formatting.
- You need to replace or insert a `defn`, `defmethod`, `def`, or similar top-level form.
- Parentheses need repair after an edit.

Prefer native edits for straightforward changes in CLI agents; use structural edits as fallback or when form targeting is more reliable.

## Bash Tool

The `bash` tool can run over nREPL or locally. Over-nREPL mode is useful for sandboxing the nREPL process and matching project context. Local mode is useful for non-CLJ runtimes or when the nREPL is not a normal JVM process.
