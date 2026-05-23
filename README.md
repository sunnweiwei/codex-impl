# codex-impl

Re-implement [openai/codex](https://github.com/openai/codex) (originally Rust) as a pure-Python package named `codex`. The goal is a **100% faithful port of the upstream code at `upstream/openai-codex/`**, not a fresh design inspired by the description below. When the description and the upstream source disagree, the upstream source wins.

## What you're building (overview of the upstream tool)

This section is just orientation — read `upstream/openai-codex/` for the actual behavior to reproduce. Do not treat the paragraphs below as a spec to interpret freely.

Codex is a **terminal-based coding agent**: a user runs `codex` in a shell, types prompts in natural language, and an LLM drives tool calls (run shell commands, edit files via `apply_patch`, view images, search the web, spawn sub-agents, etc.) to satisfy the request. The Python port must reproduce the full end-to-end experience:

- **Single CLI entry point: `python -m codex`.** With no args it opens an interactive TUI chat REPL — the user types messages, the agent streams its reasoning + tool calls + final answer back, and the loop continues until exit. Slash commands like `/resume`, `/fork`, `/new`, `/clear`, `/model`, `/ps`, `/stop`, `/theme` work the way upstream does.
- **Subcommands under the same entry.** `python -m codex exec <prompt>` for one-shot non-interactive runs; `python -m codex exec resume <rollout>` / `python -m codex exec fork <rollout>` to continue or branch a past session. Conversations are recorded as JSONL rollouts under `$CODEX_HOME`, and the interactive rollout picker lets the user browse them.
- **Tool runtime.** Shell exec (sandboxed via seatbelt on macOS), `apply_patch`, `update_plan`, `request_user_input`, `view_image`, hosted web search, and multi-agent spawn/wait/close/resume — all dispatched by the model and reported back to it in upstream-compatible shapes.
- **Memory pipeline.** Two-stage memory (per-rollout stage-1 extraction + global stage-2 consolidation) runs in the background on startup, writes consolidated memories under `$CODEX_HOME/memories/`, and feeds them into future prompts.
- **Model client.** Talks to the OpenAI Responses API (and an in-memory `ScriptedResponsesModel` for tests), streams events back as a typed `CodexEvent` sequence, retries on transient stream failures, and supports auto-compaction when the context window fills up.

Every one of these behaviors must match `upstream/openai-codex/` (Rust) at the level of CLI output bytes, prompt assets, event shapes, tool call protocol, rollout file format, and memory file layout. The Python port is a translation, not a reinterpretation — if a feature exists in upstream, port it; if a feature doesn't exist in upstream, don't invent it. When in doubt, read upstream.

**Faithfulness covers names, not just behavior.** Keep upstream's exact field names, tool argument keys, event type strings, output/error text, and formatting details. A renamed field or paraphrased message that "means the same thing" still fails evaluation. Don't pick your own names — go read what upstream uses.

## What's in this repo

- `SPEC.md` — module layout and the two hard rules (behavior + surface).
- `API_SURFACE.md` — every symbol that will be imported during evaluation, with signatures. Lower bound, not an exhaustive enumeration — see SPEC.md.
- `upstream/openai-codex/` — full upstream source at pinned commit `392e94e9ea756cffd89f35941e881d29b2a81a6e`. Read it for anything not spelled out here.

## Output layout

```
your-solution/
└── codex/
    ├── __init__.py
    ├── types.py / prompts.py / state.py / model.py / tools.py / core.py / memory.py / cli.py
    └── assets/
```

All nine of the listed `.py` files (the package `__init__.py` plus eight submodules) are required — evaluation imports from each. Asset paths under `codex/assets/` are enumerated in `SPEC.md` (§ Required assets).

## Constraints

Python ≥ 3.11, stdlib only (Pillow optional). Do not shell out to the official `codex` binary.

## Delivery requirements (read carefully)

These are the most common ways previous submissions have failed. Verify all of them before submitting.

1. **`python3 -m codex` must launch the interactive CLI.** That means `codex/__main__.py` must call into `codex/cli.py:main()` (or equivalent) and open the upstream-style TUI chat REPL. A submission where `python3 -m codex` prints a help message, errors out with "no main function", or just exits silently is not a delivery — it's broken. Test this yourself before submitting:
   ```bash
   cd your-solution
   OPENAI_API_KEY=sk-... python3 -m codex      # should open chat REPL
   OPENAI_API_KEY=sk-... python3 -m codex exec "hello"   # one-shot mode
   ```

2. **The shipped CLI must call the real OpenAI Responses API by default.** Your development environment may not have an `OPENAI_API_KEY`, but the *delivered* code must, when run by a user with a valid `OPENAI_API_KEY` set, send real requests to OpenAI and stream real responses back — exactly the way upstream codex does. Do not ship a CLI that returns hardcoded strings, template responses, or placeholder messages. The `ScriptedResponsesModel` class is a testing-only stub and must only be selected when the relevant test env variable (`PY_CODEX_FAKE_RESPONSES`) is set; the default path must be the live API.

3. **`import codex` must succeed cleanly.** No `NameError`, no missing typing imports, no circular import explosion. `python3 -c "import codex"` is the absolute minimum smoke test — run it before submitting.

4. **Every symbol listed in `API_SURFACE.md` must be importable.** Grep your code: every `def X` / `class X` named in `API_SURFACE.md` should exist at the listed module path. Missing entries fail the test that imports them.