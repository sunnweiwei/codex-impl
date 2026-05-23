# API_SURFACE

Every symbol below will be imported or accessed during evaluation. Treat this as a lower bound: signatures are not strict — assume every class/function implicitly allows extra `*args, **kwargs` and may have additional methods/attributes. Add whatever else you need; just don't break or rename what's listed. Behavior must match `upstream/openai-codex/`.

## `codex`

### class `CodexConfig`
```python
CodexConfig(
    model: 'str' = <factory>,
    cwd: 'Path | str' = <factory>,
    sandbox: 'SandboxMode' = 'workspace-write',
    approval_policy: 'ApprovalPolicy' = 'never',
    writable_roots: 'tuple[Path | str, ...]' = (),
    codex_home: 'Path | str | None' = None,
    skip_git_repo_check: 'bool' = False,
    ephemeral: 'bool' = False,
    max_iterations: 'int | None' = None,
    model_auto_compact_token_limit: 'int | None' = None,
    agent_depth: 'int' = 0,
    web_search_external_web_access: 'bool' = False,
    web_search_filters: 'dict[str, Any] | None' = None,
    web_search_user_location: 'dict[str, Any] | None' = None,
    web_search_context_size: "Literal['low', 'medium', 'high'] | None" = None,
    web_search_content_types: 'tuple[str, ...] | None' = None,
    collaboration_mode: 'CollaborationMode' = 'Default',
    approval_provider: 'Any | None' = None,
    hook_provider: 'Any | None' = None,
    request_user_input_answers: 'dict[str, Any] | None' = None,
    request_user_input_provider: 'Any | None' = None,
    model_supports_image_input: 'bool | None' = None,
    model_supports_image_detail_original: 'bool | None' = None,
    memory_tool_enabled: 'bool' = False,
    memory_disable_on_external_context: 'bool' = False,
    use_memories: 'bool' = True,
    memory_state_store: 'Any | None' = None,
    memory_startup_background: 'bool' = True,
    memory_run_phase2_on_startup: 'bool' = True,
    memory_max_rollout_age_days: 'int' = 10,
    memory_min_rollout_idle_hours: 'int' = 6,
    model_stream_max_retries: 'int | None' = None,
    model_stream_retry_base_delay_ms: 'int' = 200,
    output_schema: 'dict[str, Any] | None' = None,
    input_images: 'tuple[Path | str, ...]' = (),
    remote_compaction: 'RemoteCompactionMode' = <factory>,
    current_date: 'str | None' = None,
    timezone: 'str | None' = None,
)
```
- `resolved_auto_compact_token_limit(self) -> 'int | None'`
- `resolved_codex_home(self) -> 'Path'`
- `resolved_cwd(self) -> 'Path'`
- `resolved_model_context_window(self) -> 'int | None'`
- `resolved_model_stream_max_retries(self) -> 'int'`
- `resolved_model_stream_retry_base_delay_ms(self) -> 'int'`
- `resolved_output_last_message(self) -> 'Path | None'`
- `resolved_parallel_tool_calls(self) -> 'bool'`
- `resolved_reasoning(self) -> 'dict[str, str | None] | None'`
- `resolved_supports_image_input(self) -> 'bool'`
- `resolved_tool_output_truncation_tokens(self) -> 'int'`
- `resolved_verbosity(self) -> 'str | None'`

### class `CodexSession`
```python
CodexSession(config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None)
```
- `compact(self, prompt: 'str | None' = None) -> 'CodexResult'`
- `config`
- `fork_from_rollout(cls, rollout_path: 'str | Path', config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None) -> "'CodexSession'"`
- `has_pending_input(self) -> 'bool'`
- `inject_response_items(self, items: 'list[dict[str, Any]]', *, expected_turn_id: 'str | None' = None) -> 'str'`
- `interrupt(self) -> 'None'`
- `memory_startup_result`
- `model_client`
- `prepend_pending_input(self, items: 'list[dict[str, Any]]') -> 'None'`
- `queue_input_for_next_turn(self, prompt: 'str') -> 'None'`
- `resume_from_rollout(cls, rollout_path: 'str | Path', config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None) -> "'CodexSession'"`
- `run(self, prompt: 'str') -> 'CodexResult'`
- `state`
- `steer_input(self, prompt: 'str', *, expected_turn_id: 'str | None' = None) -> 'str'`
- `stream(self, prompt: 'str') -> 'Iterator[CodexEvent]'`
- `stream_compact(self, prompt: 'str | None' = None) -> 'Iterator[CodexEvent]'`
- `tools`

- `cli: module`

## `codex.types`

### class `CodexConfig`
```python
CodexConfig(
    model: 'str' = <factory>,
    cwd: 'Path | str' = <factory>,
    sandbox: 'SandboxMode' = 'workspace-write',
    approval_policy: 'ApprovalPolicy' = 'never',
    writable_roots: 'tuple[Path | str, ...]' = (),
    codex_home: 'Path | str | None' = None,
    skip_git_repo_check: 'bool' = False,
    ephemeral: 'bool' = False,
    max_iterations: 'int | None' = None,
    model_auto_compact_token_limit: 'int | None' = None,
    agent_depth: 'int' = 0,
    web_search_external_web_access: 'bool' = False,
    web_search_filters: 'dict[str, Any] | None' = None,
    web_search_user_location: 'dict[str, Any] | None' = None,
    web_search_context_size: "Literal['low', 'medium', 'high'] | None" = None,
    web_search_content_types: 'tuple[str, ...] | None' = None,
    collaboration_mode: 'CollaborationMode' = 'Default',
    approval_provider: 'Any | None' = None,
    hook_provider: 'Any | None' = None,
    request_user_input_answers: 'dict[str, Any] | None' = None,
    request_user_input_provider: 'Any | None' = None,
    model_supports_image_input: 'bool | None' = None,
    model_supports_image_detail_original: 'bool | None' = None,
    memory_tool_enabled: 'bool' = False,
    memory_disable_on_external_context: 'bool' = False,
    use_memories: 'bool' = True,
    memory_state_store: 'Any | None' = None,
    memory_startup_background: 'bool' = True,
    memory_run_phase2_on_startup: 'bool' = True,
    memory_max_rollout_age_days: 'int' = 10,
    memory_min_rollout_idle_hours: 'int' = 6,
    model_stream_max_retries: 'int | None' = None,
    model_stream_retry_base_delay_ms: 'int' = 200,
    output_schema: 'dict[str, Any] | None' = None,
    input_images: 'tuple[Path | str, ...]' = (),
    remote_compaction: 'RemoteCompactionMode' = <factory>,
    current_date: 'str | None' = None,
    timezone: 'str | None' = None,
)
```
- `resolved_auto_compact_token_limit(self) -> 'int | None'`
- `resolved_codex_home(self) -> 'Path'`
- `resolved_cwd(self) -> 'Path'`
- `resolved_model_context_window(self) -> 'int | None'`
- `resolved_model_stream_max_retries(self) -> 'int'`
- `resolved_model_stream_retry_base_delay_ms(self) -> 'int'`
- `resolved_output_last_message(self) -> 'Path | None'`
- `resolved_parallel_tool_calls(self) -> 'bool'`
- `resolved_reasoning(self) -> 'dict[str, str | None] | None'`
- `resolved_supports_image_input(self) -> 'bool'`
- `resolved_tool_output_truncation_tokens(self) -> 'int'`
- `resolved_verbosity(self) -> 'str | None'`

### class `CodexEvent`
```python
CodexEvent(
    type: 'str',
    payload: 'dict[str, Any]' = <factory>,
)
```
- `to_dict(self) -> 'dict[str, Any]'`
- `to_json(self) -> 'str'`

### class `CodexResult`
```python
CodexResult(
    final_message: 'str',
    events: 'list[CodexEvent]',
    thread_id: 'str',
    turn_id: 'str',
    history: 'list[dict[str, Any]]',
    memory_citations: 'list[dict[str, Any]]' = <factory>,
)
```

### class `LifecycleStep`
```python
LifecycleStep(
    name: 'str',
    event_type: 'str',
    phase: 'LifecyclePhase',
    terminal: 'bool' = False,
    mutates_history: 'bool' = False,
)
```

### class `ModelResponse`
```python
ModelResponse(
    id: 'str',
    output: 'list[dict[str, Any]]',
    raw: 'dict[str, Any]' = <factory>,
)
```

### class `PromptRequest`
```python
PromptRequest(
    model: 'str',
    instructions: 'str',
    input: 'list[dict[str, Any]]',
    tools: 'list[dict[str, Any]]',
    parallel_tool_calls: 'bool' = True,
    prompt_cache_key: 'str | None' = None,
    reasoning: 'dict[str, Any] | None' = None,
    include: 'list[str]' = <factory>,
    output_schema: 'dict[str, Any] | None' = None,
    output_schema_strict: 'bool' = True,
    verbosity: 'str | None' = None,
    service_tier: 'str | None' = None,
    client_metadata: 'dict[str, str] | None' = None,
)
```
- `to_compact_payload(self) -> 'dict[str, Any]'`
- `to_responses_kwargs(self) -> 'dict[str, Any]'`

- `KNOWN_EVENT_TYPES: frozenset`
- `TERMINAL_TURN_EVENT_TYPES: frozenset`
- `_MODEL_CATALOG_CACHE: NoneType`

## `codex.prompts`

- `build_base_instructions(*, prompt_asset: 'str', model: 'str | None' = None, cwd: 'Path', sandbox: 'SandboxMode', approval_policy: 'ApprovalPolicy', codex_home: 'Path | None' = None, memory_tool_enabled: 'bool' = False, use_memories: 'bool' = True) -> 'str'`
- `build_environment_context(cwd: 'Path', *, shell: 'str | None' = None, current_date: 'str | None' = None, timezone: 'str | None' = None) -> 'str'`
- `build_initial_context_items(config: 'CodexConfig', *, cwd: 'Path | None' = None) -> 'list[dict[str, Any]]'`
- `build_memory_consolidation_prompt(memory_root: 'Path | str') -> 'str'`
- `build_memory_stage_one_input_message(*, rollout_path: 'Path | str', rollout_cwd: 'Path | str', rollout_contents: 'str', model_context_window: 'int | None' = None, effective_context_window_percent: 'int' = 95) -> 'str'`
- `build_permissions_instructions(*, cwd: 'Path', sandbox: 'SandboxMode', approval_policy: 'ApprovalPolicy', network_access: 'NetworkAccess' = 'restricted', writable_roots: 'tuple[Path | str, ...]' = ()) -> 'str'`
- `collect_agents_md(cwd: 'Path') -> 'str'`
- `memory_stage_one_rollout_token_limit(*, model_context_window: 'int | None' = None, effective_context_window_percent: 'int' = 95) -> 'int'`
- `memory_stage_one_system_prompt() -> 'str'`
- `read_model_catalog_instructions(model: 'str') -> 'str | None'`
- `verify_asset_hashes() -> 'dict[str, bool]'`
- `ASSETS_DIR: PosixPath`

## `codex.state`

### class `CodexState`
```python
CodexState(
    config: 'CodexConfig',
    thread_id: 'str' = <factory>,
    turn_id: 'str' = <factory>,
    installation_id: 'str' = <factory>,
    forked_from_id: 'str | None' = None,
    history: 'list[dict]' = <factory>,
    events: 'list[CodexEvent]' = <factory>,
    memory_citations: 'list[dict]' = <factory>,
    previous_turn_settings: 'dict[str, Any] | None' = None,
    reference_context_item: 'dict[str, Any] | None' = None,
    last_token_usage: 'dict[str, Any] | None' = None,
    total_token_usage: 'int' = 0,
    session_reasoning_tokens: 'int' = 0,
    context_carryover_tokens: 'int' = 0,
    context_carryover_estimated: 'bool' = False,
)
```
- `active_context_token_status(self) -> 'tuple[int | None, bool]'`
- `active_context_tokens(self) -> 'int'`
- `append_history(self, item: 'dict') -> 'None'`
- `approx_history_tokens(self) -> 'int'`
- `compact_with_remote_history(self, compacted_history: 'list[dict[str, Any]]', initial_context: 'list[dict] | None' = None) -> 'list[dict]'`
- `compact_with_summary(self, summary_suffix: 'str', initial_context: 'list[dict] | None' = None) -> 'list[dict]'`
- `emit(self, event_type: 'str', **payload: 'object') -> 'CodexEvent'`
- `estimate_token_count_with_base_instructions(self) -> 'int'`
- `prompt_history(self) -> 'list[dict[str, Any]]'`
- `read_rollout_records(self) -> 'list[dict[str, Any]]'`
- `recompute_token_usage_from_history(self) -> 'None'`
- `record_apply_patch_turn_diff(self, metadata: 'Any') -> 'str | None'`
- `record_memory_citation(self, citation: 'dict') -> 'None'`
- `record_token_usage(self, usage: 'dict[str, Any] | None') -> 'None'`
- `rollout_path(self) -> 'Path'`
- `session_context_token_status(self) -> 'tuple[int | None, bool]'`
- `session_reasoning_usage_tokens(self) -> 'int | None'`
- `session_usage_tokens(self) -> 'int | None'`
- `start_new_context_epoch(self, carryover_tokens: 'int | None' = None, *, estimated: 'bool' = False) -> 'None'`
- `start_turn(self) -> 'None'`
- `token_usage_info(self) -> 'dict[str, Any] | None'`
- `write_last_message(self, message: 'str') -> 'None'`

### class `RolloutReconstruction`
```python
RolloutReconstruction(
    history: 'list[dict[str, Any]]',
    previous_turn_settings: 'dict[str, Any] | None',
    reference_context_item: 'dict[str, Any] | None',
    session_meta: 'dict[str, Any] | None' = None,
    legacy_compaction_without_replacement_history: 'bool' = False,
)
```

- `build_compacted_history(initial_context: 'list[dict]', user_messages: 'list[str]', summary_text: 'str', max_tokens: 'int' = 20000) -> 'list[dict]'`
- `build_compaction_summary_text(summary_suffix: 'str') -> 'str'`
- `extract_proposed_plan_text(text: 'str') -> 'str | None'`
- `parse_command_actions(command: 'str') -> 'list[dict[str, Any]]'`
- `parse_memory_citation(citations: 'list[str]') -> 'dict | None'`
- `prepare_prompt_history(history: 'list[dict[str, Any]]', config: 'CodexConfig') -> 'list[dict[str, Any]]'`
- `reconstruct_history_from_rollout(source: 'Path | str | list[dict[str, Any]]') -> 'RolloutReconstruction'`
- `strip_memory_citations(text: 'str') -> 'tuple[str, list[str]]'`
- `strip_proposed_plan_blocks(text: 'str') -> 'str'`
- `summarization_prompt() -> 'str'`
- `CODEX_ROLLOUT_ITEM_TYPES: frozenset`

## `codex.model`

### class `ModelClient`
```python
ModelClient()
```
- `create(self, request: 'PromptRequest') -> 'ModelResponse'`
- `stream(self, request: 'PromptRequest') -> 'Iterable[ModelStreamEvent]'`

### class `ModelStreamEvent`
```python
ModelStreamEvent(
    type: 'str',
    payload: 'dict[str, Any]',
)
```

### class `OpenAIResponsesModel`
```python
OpenAIResponsesModel()
```
- `compact(self, request: 'PromptRequest', *, session_id: 'str | None' = None, thread_id: 'str | None' = None, installation_id: 'str | None' = None) -> 'list[dict[str, Any]]'`
- `create(self, request: 'PromptRequest') -> 'ModelResponse'`
- `stream(self, request: 'PromptRequest') -> 'Iterable[ModelStreamEvent]'`

### class `RemoteCompactionError`
```python
RemoteCompactionError(...)
```

### class `ScriptedResponsesModel`
```python
ScriptedResponsesModel(responses: 'Sequence[dict[str, Any]]')
```
- `create(self, request: 'PromptRequest') -> 'ModelResponse'`
- `from_env(cls) -> "'ScriptedResponsesModel | None'"`
- `requests`
- `stream(self, request: 'PromptRequest') -> 'Iterable[ModelStreamEvent]'`

- `collect_stream_response(events: 'Iterable[Any]') -> 'ModelResponse'`
- `iter_model_stream_events(events: 'Iterable[Any]') -> 'Iterable[ModelStreamEvent]'`
- `load_env_file(path: 'Path') -> 'dict[str, str]'`

## `codex.tools`

### class `AgentRuntime`
```python
AgentRuntime()
```
- `close_agent(self, arguments: 'dict[str, Any]') -> 'ToolResult'`
- `resume_agent(self, arguments: 'dict[str, Any]') -> 'ToolResult'`
- `send_input(self, arguments: 'dict[str, Any]') -> 'ToolResult'`
- `spawn_agent(self, arguments: 'dict[str, Any]') -> 'ToolResult'`
- `wait_agent(self, arguments: 'dict[str, Any]') -> 'ToolResult'`

### class `ApplyPatchShellInvocation`
```python
ApplyPatchShellInvocation(
    patch: 'str',
    workdir: 'str | None' = None,
)
```

### class `RunningCommand`
```python
RunningCommand()
```
- `interrupt(self) -> 'None'`
- `snapshot(self, start: 'float', max_output_tokens: 'int') -> 'dict[str, Any]'`
- `start_readers(self) -> 'None'`
- `write_stdin(self, chars: 'str') -> 'None'`

### class `SandboxedProcessArgv`
```python
SandboxedProcessArgv(
    argv: 'list[str]',
    metadata: 'dict[str, Any]',
)
```

### class `ToolDefinition`
```python
ToolDefinition(
    name: 'str',
    spec: 'dict[str, Any]',
    handler: 'Callable[[Any], ToolResult]',
    freeform: 'bool' = False,
    supports_parallel: 'bool' = False,
)
```

### class `ToolResult`
```python
ToolResult(
    ok: 'bool',
    output: 'str',
    metadata: 'dict[str, Any]',
)
```

### class `ToolRuntime`
```python
ToolRuntime(config: 'CodexConfig')
```
- `apply_patch(self, arguments: 'Any') -> 'ToolResult'`
- `close_agent(self, arguments: 'Any') -> 'ToolResult'`
- `definitions(self) -> 'list[ToolDefinition]'`
- `dispatch(self, name: 'str', arguments: 'Any', *, call_id: 'str | None' = None) -> 'ToolResult'`
- `drain_runtime_events(self) -> 'list[dict[str, Any]]'`
- `exec_command(self, arguments: 'Any') -> 'ToolResult'`
- `hosted_web_search(self, arguments: 'Any') -> 'ToolResult'`
- `interrupt_all(self) -> 'None'`
- `multi_agent_unavailable(self, arguments: 'Any') -> 'ToolResult'`
- `normalize_tool_call(self, call: 'dict[str, Any]') -> 'dict[str, Any]'`
- `request_user_input(self, arguments: 'Any') -> 'ToolResult'`
- `resume_agent(self, arguments: 'Any') -> 'ToolResult'`
- `send_input(self, arguments: 'Any') -> 'ToolResult'`
- `shell_command(self, arguments: 'Any') -> 'ToolResult'`
- `spawn_agent(self, arguments: 'Any') -> 'ToolResult'`
- `specs(self) -> 'list[dict[str, Any]]'`
- `supports_parallel(self, name: 'str') -> 'bool'`
- `update_plan(self, arguments: 'Any') -> 'ToolResult'`
- `view_image(self, arguments: 'Any') -> 'ToolResult'`
- `wait_agent(self, arguments: 'Any') -> 'ToolResult'`
- `write_stdin(self, arguments: 'Any') -> 'ToolResult'`

- `_platform_sandbox_available() -> 'bool'`
- `_sandboxed_process_argv(argv: 'list[str]', *, config: 'CodexConfig', cwd: 'Path', workdir: 'Path', bypass_sandbox: 'bool') -> 'SandboxedProcessArgv'`
- `MACOS_SANDBOX_EXEC: str`
- `_PLATFORM_SANDBOX_AVAILABLE_CACHE: NoneType`

## `codex.memory`

### class `MemoryBackgroundTask`
```python
MemoryBackgroundTask()
```
- `done(self) -> 'bool'`
- `join(self, timeout: 'float | None' = None) -> 'Any | None'`

### class `MemoryJobClaim`
```python
MemoryJobClaim(
    outcome: 'str',
    ownership_token: 'str | None' = None,
    input_watermark: 'int | None' = None,
)
```

### class `MemoryPhase2Result`
```python
MemoryPhase2Result(
    status: 'str',
    selected: 'list[MemoryStageOneRecord]',
    memory_root: 'Path',
    workspace_changed: 'bool' = False,
    final_message: 'str' = '',
)
```

### class `MemoryRollout`
```python
MemoryRollout(
    thread_id: 'str',
    rollout_path: 'Path',
    cwd: 'Path',
    source_updated_at: 'datetime',
    git_branch: 'str | None',
    source: 'str',
    memory_mode: 'str',
    items: 'list[dict[str, Any]]',
    serialized_contents: 'str',
)
```

### class `MemoryStageOneOutput`
```python
MemoryStageOneOutput(
    raw_memory: 'str',
    rollout_summary: 'str',
    rollout_slug: 'str | None',
)
```

### class `MemoryStageOneRecord`
```python
MemoryStageOneRecord(
    thread_id: 'str',
    source_updated_at: 'datetime',
    raw_memory: 'str',
    rollout_summary: 'str',
    rollout_slug: 'str | None',
    rollout_path: 'Path | str',
    cwd: 'Path | str',
    usage_count: 'int' = 0,
    last_usage: 'datetime | None' = None,
    selected_for_phase2: 'bool' = False,
)
```

### class `MemoryStageOneStartupClaim`
```python
MemoryStageOneStartupClaim(
    thread_id: 'str',
    rollout_path: 'Path',
    source_updated_at: 'datetime',
    ownership_token: 'str',
)
```

### class `MemoryStartupResult`
```python
MemoryStartupResult(
    records: 'list[MemoryStageOneRecord]',
    skipped: 'list[Path]',
    memory_root: 'Path',
    status: 'str' = 'completed',
    phase2_result: 'Any | None' = None,
    rate_limit_allowed: 'bool | None' = None,
)
```

### class `MemoryStateStore`
```python
MemoryStateStore(path: 'Path | str')
```
- `claim_stage1_jobs_for_startup(self, *, current_thread_id: 'str | None', scan_limit: 'int', max_claimed: 'int', max_age_days: 'int', min_rollout_idle_hours: 'int', allowed_sources: 'set[str] | frozenset[str]', lease_seconds: 'int', max_running_jobs: 'int', now: 'datetime | None' = None) -> 'list[MemoryStageOneStartupClaim]'`
- `clear_memory_data(self) -> 'None'`
- `close(self) -> 'None'`
- `enqueue_global_consolidation(self, input_watermark: 'datetime | int') -> 'None'`
- `get_job(self, kind: 'str', job_key: 'str') -> 'dict[str, Any] | None'`
- `get_phase2_input_selection(self, *, n: 'int', max_unused_days: 'int' = 30, now: 'datetime | None' = None) -> 'list[MemoryStageOneRecord]'`
- `get_stage1_output(self, thread_id: 'str') -> 'dict[str, Any] | None'`
- `heartbeat_global_phase2_job(self, *, ownership_token: 'str', lease_seconds: 'int', now: 'datetime | None' = None) -> 'bool'`
- `list_stage1_outputs_for_global(self, n: 'int') -> 'list[MemoryStageOneRecord]'`
- `mark_global_phase2_job_failed(self, *, ownership_token: 'str', failure_reason: 'str', retry_delay_seconds: 'int', now: 'datetime | None' = None, allow_unowned: 'bool' = False) -> 'bool'`
- `mark_global_phase2_job_succeeded(self, *, ownership_token: 'str', completed_watermark: 'datetime | int', selected_outputs: 'list[MemoryStageOneRecord]', now: 'datetime | None' = None) -> 'bool'`
- `mark_stage1_job_failed(self, *, thread_id: 'str', ownership_token: 'str', failure_reason: 'str', retry_delay_seconds: 'int', now: 'datetime | None' = None) -> 'bool'`
- `mark_stage1_job_succeeded(self, *, thread_id: 'str', ownership_token: 'str', source_updated_at: 'datetime | int', raw_memory: 'str', rollout_summary: 'str', rollout_slug: 'str | None', now: 'datetime | None' = None) -> 'bool'`
- `mark_stage1_job_succeeded_no_output(self, *, thread_id: 'str', ownership_token: 'str', now: 'datetime | None' = None) -> 'bool'`
- `mark_thread_memory_mode_polluted(self, thread_id: 'str', *, now: 'datetime | None' = None) -> 'bool'`
- `open_codex_home(cls, codex_home: 'Path | str') -> "'MemoryStateStore'"`
- `prune_stage1_outputs_for_retention(self, *, max_unused_days: 'int' = 30, limit: 'int' = 100, now: 'datetime | None' = None) -> 'int'`
- `record_stage1_output_usage(self, thread_ids: 'list[str]', *, now: 'datetime | None' = None) -> 'int'`
- `set_thread_memory_mode(self, thread_id: 'str', memory_mode: 'str') -> 'bool'`
- `try_claim_global_phase2_job(self, *, worker_id: 'str', lease_seconds: 'int', now: 'datetime | None' = None) -> 'MemoryJobClaim'`
- `try_claim_stage1_job(self, *, thread_id: 'str', worker_id: 'str', source_updated_at: 'datetime | int', lease_seconds: 'int', max_running_jobs: 'int', now: 'datetime | None' = None) -> 'MemoryJobClaim'`
- `upsert_thread(self, record: 'MemoryThreadRecord') -> 'None'`

### class `MemoryThreadRecord`
```python
MemoryThreadRecord(
    thread_id: 'str',
    rollout_path: 'Path | str',
    cwd: 'Path | str',
    updated_at: 'datetime',
    git_branch: 'str | None' = None,
)
```

### class `MemoryWorkspaceChange`
```python
MemoryWorkspaceChange(
    status: 'str',
    path: 'str',
)
```

- `build_memory_consolidation_config(*, memory_root: 'Path | str', base_config: 'CodexConfig | None' = None) -> 'CodexConfig'`
- `extract_memory_stage_one(*, model_client: 'ModelClient', rollout_path: 'Path | str', rollout_cwd: 'Path | str', rollout_contents: 'str', model_context_window: 'int | None' = None, effective_context_window_percent: 'int' = 95, prompt_cache_key: 'str | None' = None) -> 'MemoryStageOneOutput'`
- `load_memory_rollout(rollout_path: 'Path | str') -> 'MemoryRollout'`
- `memory_extensions_root(root: 'Path | str') -> 'Path'`
- `memory_rate_limit_allows_startup(snapshot: 'Any | None', *, min_remaining_percent: 'int' = 25) -> 'bool'`
- `memory_rollout_candidates(codex_home: 'Path | str', limit: 'int' = 5000) -> 'list[Path]'`
- `memory_rollout_is_stage1_startup_eligible(rollout: 'MemoryRollout', *, current_thread_id: 'str | None' = None, max_rollout_age_days: 'int' = 10, min_rollout_idle_hours: 'int' = 6, allowed_sources: 'set[str] | frozenset[str]' = frozenset({'vscode', 'atlas', 'cli', 'chatgpt'}), now: 'datetime | None' = None) -> 'bool'`
- `memory_stage_one_output_schema() -> 'dict[str, Any]'`
- `memory_workspace_diff(root: 'Path | str') -> 'tuple[list[MemoryWorkspaceChange], str]'`
- `parse_memory_stage_one_output(text: 'str') -> 'MemoryStageOneOutput'`
- `prepare_memory_workspace(root: 'Path | str') -> 'None'`
- `prune_old_extension_resources(memory_root: 'Path | str', *, now: 'datetime | None' = None) -> 'None'`
- `prune_stage1_records_for_retention(memories: 'list[MemoryStageOneRecord]', *, max_unused_days: 'int' = 30, limit: 'int' = 100, now: 'datetime | None' = None) -> 'tuple[list[MemoryStageOneRecord], list[MemoryStageOneRecord]]'`
- `raw_memories_file(root: 'Path | str') -> 'Path'`
- `rebuild_raw_memories_file_from_memories(root: 'Path | str', memories: 'list[MemoryStageOneRecord]', max_raw_memories_for_consolidation: 'int', *, max_unused_days: 'int' = 30, now: 'datetime | None' = None) -> 'None'`
- `render_memory_workspace_diff_file(changes: 'list[MemoryWorkspaceChange]', unified_diff: 'str', max_bytes: 'int' = 4194304) -> 'str'`
- `reset_memory_workspace_baseline(root: 'Path | str') -> 'None'`
- `rollout_summaries_dir(root: 'Path | str') -> 'Path'`
- `rollout_summary_file_stem(memory: 'MemoryStageOneRecord') -> 'str'`
- `run_memory_consolidation_session(*, memory_root: 'Path | str', base_config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None) -> 'CodexResult'`
- `run_memory_phase2_once(*, codex_home: 'Path | str', state_store: 'MemoryStateStore', base_config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None, max_raw_memories_for_consolidation: 'int' = 256, max_unused_days: 'int' = 30, lease_seconds: 'int' = 3600) -> 'MemoryPhase2Result'`
- `run_memory_stage_one_for_rollout(*, model_client: 'ModelClient', rollout_path: 'Path | str', model_context_window: 'int | None' = None, effective_context_window_percent: 'int' = 95) -> 'MemoryStageOneRecord | None'`
- `run_memory_startup_once(*, codex_home: 'Path | str', model_client: 'ModelClient', state_store: 'MemoryStateStore | None' = None, max_rollouts: 'int' = 2, max_raw_memories_for_consolidation: 'int' = 256, max_unused_days: 'int' = 30, max_rollout_age_days: 'int' = 10, min_rollout_idle_hours: 'int' = 6, current_thread_id: 'str | None' = None, allowed_sources: 'set[str] | frozenset[str]' = frozenset({'vscode', 'atlas', 'cli', 'chatgpt'}), model_context_window: 'int | None' = None, sync_phase2_inputs: 'bool' = True) -> 'MemoryStartupResult'`
- `run_memory_startup_pipeline_once(*, codex_home: 'Path | str', model_client: 'ModelClient', state_store: 'MemoryStateStore | None' = None, base_config: 'CodexConfig | None' = None, max_rollouts: 'int' = 2, max_raw_memories_for_consolidation: 'int' = 256, max_unused_days: 'int' = 30, max_rollout_age_days: 'int' = 10, min_rollout_idle_hours: 'int' = 6, current_thread_id: 'str | None' = None, model_context_window: 'int | None' = None, run_phase2: 'bool' = True, rate_limit_snapshot: 'Any | None' = None, min_rate_limit_remaining_percent: 'int' = 25) -> 'MemoryStartupResult'`
- `sanitize_response_item_for_memories(item: 'dict[str, Any]') -> 'dict[str, Any] | None'`
- `seed_extension_instructions(memory_root: 'Path | str') -> 'None'`
- `select_phase2_memory_inputs(memories: 'list[MemoryStageOneRecord]', max_raw_memories_for_consolidation: 'int', *, max_unused_days: 'int' = 30, now: 'datetime | None' = None) -> 'list[MemoryStageOneRecord]'`
- `serialize_filtered_rollout_response_items(items: 'list[dict[str, Any]]') -> 'str'`
- `start_memory_startup_task(*, codex_home: 'Path | str', model_client: 'ModelClient', state_store_path: 'Path | str | None' = None, base_config: 'CodexConfig | None' = None, max_rollouts: 'int' = 2, max_raw_memories_for_consolidation: 'int' = 256, max_unused_days: 'int' = 30, max_rollout_age_days: 'int' = 10, min_rollout_idle_hours: 'int' = 6, current_thread_id: 'str | None' = None, model_context_window: 'int | None' = None, run_phase2: 'bool' = True, rate_limit_snapshot: 'Any | None' = None, min_rate_limit_remaining_percent: 'int' = 25) -> 'MemoryBackgroundTask'`
- `sync_phase2_workspace_inputs(root: 'Path | str', memories: 'list[MemoryStageOneRecord]', max_raw_memories_for_consolidation: 'int', *, max_unused_days: 'int' = 30, now: 'datetime | None' = None) -> 'None'`
- `sync_rollout_summaries_from_memories(root: 'Path | str', memories: 'list[MemoryStageOneRecord]', max_raw_memories_for_consolidation: 'int', *, max_unused_days: 'int' = 30, now: 'datetime | None' = None) -> 'None'`
- `write_current_memory_workspace_diff(root: 'Path | str') -> 'Path'`
- `write_memory_workspace_diff(root: 'Path | str', changes: 'list[MemoryWorkspaceChange]', unified_diff: 'str') -> 'Path'`

## `codex.cli`

### class `CodexSession`
```python
CodexSession(config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None)
```
- `compact(self, prompt: 'str | None' = None) -> 'CodexResult'`
- `config`
- `fork_from_rollout(cls, rollout_path: 'str | Path', config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None) -> "'CodexSession'"`
- `has_pending_input(self) -> 'bool'`
- `inject_response_items(self, items: 'list[dict[str, Any]]', *, expected_turn_id: 'str | None' = None) -> 'str'`
- `interrupt(self) -> 'None'`
- `memory_startup_result`
- `model_client`
- `prepend_pending_input(self, items: 'list[dict[str, Any]]') -> 'None'`
- `queue_input_for_next_turn(self, prompt: 'str') -> 'None'`
- `resume_from_rollout(cls, rollout_path: 'str | Path', config: 'CodexConfig | None' = None, model_client: 'ModelClient | None' = None) -> "'CodexSession'"`
- `run(self, prompt: 'str') -> 'CodexResult'`
- `state`
- `steer_input(self, prompt: 'str', *, expected_turn_id: 'str | None' = None) -> 'str'`
- `stream(self, prompt: 'str') -> 'Iterator[CodexEvent]'`
- `stream_compact(self, prompt: 'str | None' = None) -> 'Iterator[CodexEvent]'`
- `tools`

### class `_AnsiStyle`
```python
_AnsiStyle(enabled: 'bool')
```
- `bold(self, text: 'str') -> 'str'`
- `cyan(self, text: 'str') -> 'str'`
- `dim(self, text: 'str') -> 'str'`
- `green(self, text: 'str') -> 'str'`
- `italic(self, text: 'str') -> 'str'`
- `magenta(self, text: 'str') -> 'str'`
- `red(self, text: 'str') -> 'str'`
- `strike(self, text: 'str') -> 'str'`
- `yellow(self, text: 'str') -> 'str'`

### class `_HumanEventRenderer`
```python
_HumanEventRenderer(*, color_mode: 'str' = 'auto', line_sink: 'Callable[[str], None] | None' = None)
```
- `finish(self, final_message: 'str', *, print_to_stdout: 'bool' = True) -> 'None'`
- `render(self, event: 'Any') -> 'None'`
- `render_error(self, message: 'str') -> 'None'`
- `render_info_message(self, message: 'str') -> 'None'`
- `render_interrupted(self) -> 'None'`
- `render_pending_input_preview(self, text: 'str', *, active: 'bool') -> 'None'`
- `render_user_message(self, text: 'str') -> 'None'`

### class `_LiveTurnStatusSnapshot`
```python
_LiveTurnStatusSnapshot(
    header: 'str',
    elapsed_seconds: 'int',
    active_context_tokens: 'int | None',
    active_context_estimated: 'bool',
    session_context_tokens: 'int | None',
    session_context_estimated: 'bool',
    session_reasoning_tokens: 'int | None',
    context_window: 'int | None',
)
```

### class `_RolloutPickerRow`
```python
_RolloutPickerRow(
    path: 'Path',
    preview: 'str',
    thread_id: 'str',
    created_at: 'float',
    updated_at: 'float',
    cwd: 'str | None',
    git_branch: 'str | None' = None,
)
```

- `_apply_prompt_escape_sequence(buffer: 'str', cursor: 'int', sequence: 'bytes') -> 'tuple[str, int] | None'`
- `_background_terminal_rows(session: 'CodexSession') -> 'list[tuple[int, str, bool, str]]'`
- `_format_elapsed_compact(elapsed_seconds: 'int') -> 'str'`
- `_format_tokens_compact(value: 'int | float') -> 'str'`
- `_handle_interactive_slash_command(session: 'CodexSession', prompt: 'str', *, color_mode: 'str' = 'auto', queued_prompts: 'deque[str] | None' = None) -> '_InteractiveSlashResult'`
- `_live_status_display_lines(snapshot: '_LiveTurnStatusSnapshot | None', style: "'_AnsiStyle'") -> 'list[str]'`
- `_main_chat(argv: 'list[str]', *, prog: 'str' = 'python -m codex') -> 'int'`
- `_pygments_style_name(name: 'str | None' = None) -> 'str'`
- `_render_markdown_for_terminal(text: 'str', style: '_AnsiStyle', *, emphasis: 'bool' = True, terminal_width: 'int | None' = None) -> 'list[str]'`
- `_rollout_picker_display_lines(rows: 'list[_RolloutPickerRow]', *, title: 'str', style: "'_AnsiStyle'", cwd: 'Path', show_all: 'bool', query: 'str', sort_key: 'str', selected: 'int', offset: 'int', density: 'str', toolbar_focus: 'str', expanded: 'bool') -> 'list[str]'`
- `_rollout_picker_rows(config: 'CodexConfig') -> 'list[_RolloutPickerRow]'`
- `_set_cli_syntax_theme(name: 'str') -> 'bool'`
- `_visible_len(text: 'str') -> 'int'`
- `_wrap_ansi_line(text: 'str', width: 'int') -> 'list[str]'`
- `_ANSI_RE: Pattern`
- `_CLI_SYNTAX_THEME: str`

## `codex.core`

- `_MAX_AGENT_WAIT_TIMEOUT_MS: int`
- `_MIN_AGENT_WAIT_TIMEOUT_MS: int`

