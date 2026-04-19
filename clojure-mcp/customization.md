# Customization

ClojureMCP can be customized by composing tools, prompts, resources, models, and filters in config or by building a custom server.

## Component Types

| Component | Shape | Callback result |
|-----------|-------|-----------------|
| Tool | `{:name :description :schema :tool-fn}` | `(callback result-vector error?)` |
| Prompt | `{:name :description :arguments :prompt-fn}` | `(callback {:description ... :messages [...]})` |
| Resource | `{:url :name :description :mime-type :resource-fn}` | `(callback ["content..."])` |

Parameter maps passed to component functions use string keys.

## Custom Tools

Use ClojureMCP's multimethod system when you want validation, formatting, and integration benefits inside the ClojureMCP ecosystem.

Use simple tool maps when you want standalone, portable MCP components that do not depend deeply on ClojureMCP internals.

Practical guidance:

- Keep tool schemas narrow and explicit.
- Return structured data where possible.
- Make side effects obvious in tool descriptions.
- Keep destructive or external-network operations opt-in.
- Test tool functions directly before wiring them into a server.

## Prompts

Prompts generate reusable conversation context. Good prompts:

- Describe when the prompt should be used.
- Accept a small, explicit argument list.
- Load project resources only when they are relevant.
- Produce task-specific instructions rather than generic advice.

## Resources

Resources expose read-only content such as:

- `PROJECT_SUMMARY.md`
- `LLM_CODE_STYLE.md`
- generated project info
- architecture notes
- API docs

Prefer resources for stable project context that assistants should read, not for mutable task state.

## Custom MCP Server

Create a custom server when configuration alone is not enough:

- You need a focused tool/resource set.
- You want project-specific prompts.
- You need custom tools.
- You want stricter security boundaries.

During customization, keep a minimal server profile for normal development and separate higher-risk tools into explicit opt-in profiles.
