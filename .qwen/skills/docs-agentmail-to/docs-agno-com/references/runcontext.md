# RunContext

**Source:** https://docs.agno.com/reference/run/run-context.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# RunContext

The `RunContext` is an object that can be referenced in pre- and post-hooks, tools, and other parts of the run.

See [Agent State](/state/agent/overview) for examples of how to use the `RunContext` in your code.

## RunContext Attributes

| Attribute           | Type             | Description                      |
| ------------------- | ---------------- | -------------------------------- |
| `run_id`            | `str`            | Run ID                           |
| `session_id`        | `str`            | Session ID for the run           |
| `user_id`           | `Optional[str]`  | User ID associated with the run  |
| `dependencies`      | `Dict[str, Any]` | Dependencies for the run         |
| `knowledge_filters` | `Dict[str, Any]` | Knowledge filters for the run    |
| `metadata`          | `Dict[str, Any]` | Metadata associated with the run |
| `session_state`     | `Dict[str, Any]` | Session state for the run        |
