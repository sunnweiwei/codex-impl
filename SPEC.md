# SPEC

Reproduce openai/codex as a Python package named `codex`. Upstream is at `upstream/openai-codex/` (pinned commit `392e94e9ea756cffd89f35941e881d29b2a81a6e`) — it is the source of truth for every behavior.

Two requirements:

1. **Behavior matches upstream.** Read `upstream/openai-codex/` for everything not spelled out here.
2. **Expose at least the surface in `API_SURFACE.md`.** The listed symbols, parameters, methods, and attributes are a lower bound — treat the signatures as if every class/function implicitly takes extra `*args, **kwargs` and may have additional methods. Add whatever else you need; just don't break or rename what's listed.

Module layout your implementation needs to expose (all 9 are required — evaluation imports from each):

- `codex` (re-exports a subset of `codex.types` and `codex.memory` — see `API_SURFACE.md`)
- `codex.types`
- `codex.prompts`
- `codex.state`
- `codex.model`
- `codex.tools`
- `codex.core`
- `codex.memory`
- `codex.cli` (a handful of rendering/formatting helpers will be imported by name during evaluation, including private `_`-prefixed names — see `API_SURFACE.md`)

## Required assets

Assets live under `codex/assets/`. These specific files must exist at the listed relative paths.

**Byte-checked against upstream (must equal the upstream file byte-for-byte):**

- `grammars/apply_patch.lark`
- `prompts/gpt_5_codex_prompt.md`
- `prompts/gpt_5_2_prompt.md`
- `prompts/gpt-5.2-codex_prompt.md`
- `prompts/prompt_with_apply_patch_instructions.md`
- `prompts/compact/prompt.md`
- `prompts/compact/summary_prefix.md`
- `prompts/memories/read_path.md`
- `prompts/memories/write/stage_one_system.md`
- `prompts/memories/write/stage_one_input.md`
- `prompts/memories/write/consolidation.md`
- `prompts/memories/write/extensions/ad_hoc/instructions.md`

**Loaded at runtime (content reaches the model / sandbox; must match upstream):**

- `models.json` — model catalog
- `seatbelt_base_policy.sbpl` — macOS sandbox policy
- `prompts/permissions/sandbox_mode/read_only.md`
- `prompts/permissions/sandbox_mode/workspace_write.md`
- `prompts/permissions/sandbox_mode/danger_full_access.md`
- `prompts/permissions/approval_policy/never.md`
- `prompts/permissions/approval_policy/on_request.md`
- `prompts/permissions/approval_policy/on_request_rule_request_permission.md`
- `prompts/permissions/approval_policy/on_failure.md`
- `prompts/permissions/approval_policy/unless_trusted.md`

Note: where upstream has multiple files that could plausibly fill a slot (e.g. several `*.sbpl` policies under `codex-rs/sandboxing/`, several model-specific prompt `.md` files under `codex-rs/core/`), the file names above are the ones to use. Shipping additional upstream files alongside them is fine.