# Workflows

## CLI Assistant Workflow

1. Start the coding assistant from the project directory.
2. Add ClojureMCP with `:config-profile :cli-assist`.
3. Let the assistant use native file editing and shell tools.
4. Use ClojureMCP for REPL evaluation, port discovery, and Clojure-aware fallback edits.

```bash
codex mcp add clojure-mcp -- clojure -Tmcp start :config-profile :cli-assist
```

## Desktop Workflow

1. Start nREPL in the target project.
2. Configure desktop client to run ClojureMCP with `:not-cwd true :port PORT`.
3. Restart the desktop client.
4. Add `PROJECT_SUMMARY.md`, `Clojure Project Info`, `LLM_CODE_STYLE.md`, and the REPL coding prompt from the ClojureMCP menu when starting a session.

## Project Summary

ClojureMCP includes prompts for maintaining `PROJECT_SUMMARY.md`.

Use `create-update-project-summary`:

- At project onboarding.
- After meaningful feature or architecture changes.
- Before starting a long follow-up session.

The summary helps assistants avoid rediscovering the same project structure each session.

## Chat Session Resume

Use the prompt pair:

- `chat-session-summarize` at the end of a session.
- `chat-session-resume` when continuing.

By default scratch pad data is memory-only. Enable scratch pad persistence if summaries must survive server restarts.

Custom keys allow parallel contexts:

```text
feature-auth-system
debug-memory-leak
```

## REPL-Driven Development

Ask the assistant to validate ideas in the REPL before committing larger edits:

- Evaluate small expressions.
- Inspect vars and namespaces.
- Load changed namespaces.
- Run focused tests.
- Use multiple nREPL ports for CLJ and shadow-cljs when needed.

Keep commits frequent when using an AI assistant over a large change set.
