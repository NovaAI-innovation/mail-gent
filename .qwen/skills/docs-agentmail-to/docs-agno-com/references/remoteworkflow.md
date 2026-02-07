# RemoteWorkflow

**Source:** https://docs.agno.com/reference/workflows/remote-workflow.md
**Section:** Docs

**Description:** Execute workflows hosted on a remote AgentOS instance

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# RemoteWorkflow

> Execute workflows hosted on a remote AgentOS instance

`RemoteWorkflow` allows you to run workflows that are hosted on a remote AgentOS instance. It provides the same interface as a local workflow, making it easy to integrate remote workflows into your applications.

## Installation

```bash  theme={null}
pip install agno
```

## Basic Usage

```python  theme={null}
from agno.workflow import RemoteWorkflow

# Create a remote workflow pointing to a remote AgentOS instance
workflow = RemoteWorkflow(
    base_url="http://localhost:7777",
    workflow_id="qa-workflow",
)

# Run the workflow (async)
response = await workflow.arun("What are the benefits of Python?")
print(response.content)
```

## Parameters

| Parameter     | Type    | Default  | Description                                                               |
| ------------- | ------- | -------- | ------------------------------------------------------------------------- |
| `base_url`    | `str`   | Required | Base URL of the remote AgentOS instance (e.g., `"http://localhost:7777"`) |
| `workflow_id` | `str`   | Required | ID of the remote workflow to execute                                      |
| `timeout`     | `float` | `300.0`  | Request timeout in seconds                                                |
| `config_ttl`  | `float` | `300.0`  | Time-to-live for cached configuration in seconds                          |

## Properties

### `id`

Returns the workflow ID.

```python  theme={null}
print(workflow.id)  # "qa-workflow"
```

### `name`

Returns the workflow's name from the remote configuration.

```python  theme={null}
print(workflow.name)  # "QA Workflow"
```

### `description`

Returns the workflow's description from the remote configuration.

```python  theme={null}
print(workflow.description)  # "A Q&A workflow for answering questions"
```

### `db`

Returns a `RemoteDb` instance if the workflow has a database configured.

```python  theme={null}
if workflow.db:
    print(f"Database ID: {workflow.db.id}")
```

## Methods

### `arun`

Execute the remote workflow asynchronously.

```python  theme={null}
# Non-streaming
response = await workflow.arun(
    "Explain machine learning",
    user_id="user-123",
    session_id="session-456",
)
print(response.content)
print(f"Status: {response.status}")

# Streaming
async for event in workflow.arun(
    "Generate a report",
    stream=True,
    user_id="user-123",
):
    if event.event == "RunContent" and hasattr(event, "content"):
        print(event.content, end="", flush=True)
```

**Parameters:**

| Parameter         | Type                               | Default  | Description                             |
| ----------------- | ---------------------------------- | -------- | --------------------------------------- |
| `input`           | `str \| Dict \| List \| BaseModel` | Required | The input for the workflow              |
| `additional_data` | `Optional[Dict]`                   | `None`   | Additional data to pass to the workflow |
| `user_id`         | `Optional[str]`                    | `None`   | User ID for the run                     |
| `run_id`          | `Optional[str]`                    | `None`   | Custom run ID                           |
| `session_id`      | `Optional[str]`                    | `None`   | Session ID for context persistence      |
| `session_state`   | `Optional[Dict]`                   | `None`   | Session state dictionary                |
| `images`          | `Optional[List[Image]]`            | `None`   | Images to include                       |
| `audio`           | `Optional[List[Audio]]`            | `None`   | Audio to include                        |
| `videos`          | `Optional[List[Video]]`            | `None`   | Videos to include                       |
| `files`           | `Optional[List[File]]`             | `None`   | Files to include                        |
| `stream`          | `bool`                             | `False`  | Whether to stream the response          |
| `stream_events`   | `Optional[bool]`                   | `None`   | Whether to stream events                |
| `auth_token`      | `Optional[str]`                    | `None`   | JWT token for authentication            |

**Returns:**

* `WorkflowRunOutput` when `stream=False`
* `AsyncIterator[WorkflowRunOutputEvent]` when `stream=True`

### `cancel_run`

Cancel a running workflow execution.

```python  theme={null}
success = await workflow.cancel_run(run_id="run-123")
if success:
    print("Run cancelled")
```

**Parameters:**

| Parameter    | Type            | Default  | Description                  |
| ------------ | --------------- | -------- | ---------------------------- |
| `run_id`     | `str`           | Required | ID of the run to cancel      |
| `auth_token` | `Optional[str]` | `None`   | JWT token for authentication |

**Returns:** `bool` - True if successfully cancelled

### `get_workflow_config`

Get the workflow configuration from the remote server (always fetches fresh).

```python  theme={null}
config = await workflow.get_workflow_config()
print(f"Workflow name: {config.name}")
print(f"Steps: {config.steps}")
```

**Returns:** `WorkflowResponse`

### `refresh_config`

Force refresh the cached workflow configuration.

```python  theme={null}
config = workflow.refresh_config()
```

**Returns:** `WorkflowResponse`

## A2A Protocol Support

`RemoteWorkflow` can connect to any A2A-compatible server using the `protocol="a2a"` parameter:

### Connecting to Agno A2A Servers

```python  theme={null}
from agno.team import RemoteTeam

# Connect to an Agno AgentOS with A2A interface
workflow = RemoteWorkflow(
    base_url="http://localhost:7001/a2a/workflows/my-workflow",
    workflow_id="my-workflow",
    protocol="a2a",
)

response = await workflow.arun("Hello!")
print(response.content)
```

### Protocol Options

| Protocol    | a2a\_protocol | Use Case                                           |
| ----------- | ------------- | -------------------------------------------------- |
| `"agentos"` | N/A           | Default. Connect to Agno AgentOS REST API          |
| `"a2a"`     | `"rest"`      | Connect to A2A servers using REST endpoints        |
| `"a2a"`     | `"json-rpc"`  | Connect to Google ADK or pure JSON-RPC A2A servers |

## Using in AgentOS Gateway

Remote workflows can be registered in a local AgentOS to create a gateway:

```python  theme={null}
from agno.workflow import RemoteWorkflow
from agno.os import AgentOS

agent_os = AgentOS(
    workflows=[
        RemoteWorkflow(base_url="http://server-1:7777", workflow_id="qa-workflow"),
        RemoteWorkflow(base_url="http://server-2:7777", workflow_id="analysis-workflow"),
    ],
)
```

See [AgentOS Gateway](/agent-os/remote-execution/gateway) for more details.

## Streaming Example

```python  theme={null}
from agno.workflow import RemoteWorkflow

workflow = RemoteWorkflow(
    base_url="http://localhost:7777",
    workflow_id="story-workflow",
)

print("Response: ", end="", flush=True)
async for event in workflow.arun(
    "Write a story about space exploration",
    stream=True,
    user_id="user-123",
):
    # Handle content from agent events or workflow completion
    if event.event == "RunContent" and hasattr(event, "content"):
        print(event.content, end="", flush=True)
    elif event.event == "WorkflowAgentCompleted" and hasattr(event, "content"):
        print(event.content, end="", flush=True)
```

## Error Handling

```python  theme={null}
from agno.exceptions import RemoteServerUnavailableError

try:
    response = await workflow.arun("Hello")
except RemoteServerUnavailableError as e:
    print(f"Remote server unavailable: {e.message}")
```

## Authentication

For authenticated AgentOS instances, pass the `auth_token` parameter:

```python  theme={null}
response = await workflow.arun(
    "Process this request",
    auth_token="your-jwt-token",
)
```

## Notes

<Warning>
  Remote Workflows via WebSocket are not yet supported. Use HTTP streaming instead.
</Warning>
