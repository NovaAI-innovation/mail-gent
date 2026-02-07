# Cerebras OpenAI

**Source:** https://docs.agno.com/models/providers/gateways/cerebras-openai/overview.md
**Section:** Docs

**Description:** Use Cerebras via OpenAI-compatible interface in Agno agents.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Cerebras OpenAI

> Use Cerebras via OpenAI-compatible interface in Agno agents.

## OpenAI-Compatible Integration

Cerebras can also be used via an OpenAI-compatible interface, making it easy to integrate with tools and libraries that expect the OpenAI API.

### Using the OpenAI-Compatible Class

The `CerebrasOpenAI` class provides an OpenAI-style interface for Cerebras models:

First, install openai:

```shell  theme={null}
uv pip install openai
```

```python  theme={null}
from agno.agent import Agent
from agno.models.cerebras import CerebrasOpenAI

agent = Agent(
    model=CerebrasOpenAI(
        id="llama-4-scout-17b-16e-instruct",  # Model ID to use
        # base_url="https://api.cerebras.ai", # Optional: default endpoint for Cerebras
    ),
    markdown=True,
)

# Print the response in the terminal
agent.print_response("write a two sentence horror story")
```

### Configuration Options

The `CerebrasOpenAI` class accepts the following parameters:

| Parameter  | Type | Description                                                     | Default                                              |
| ---------- | ---- | --------------------------------------------------------------- | ---------------------------------------------------- |
| `id`       | str  | Model identifier (e.g., "llama-4-scout-17b-16e-instruct")       | **Required**                                         |
| `name`     | str  | Display name for the model                                      | "Cerebras"                                           |
| `provider` | str  | Provider name                                                   | "Cerebras"                                           |
| `api_key`  | str  | API key (falls back to CEREBRAS\_API\_KEY environment variable) | None                                                 |
| `base_url` | str  | URL of the Cerebras OpenAI-compatible endpoint                  | "[https://api.cerebras.ai](https://api.cerebras.ai)" |

`CerebrasOpenAI` also supports the parameters of [OpenAI](/reference/models/openai).

### Examples

* View more examples [here](/models/providers/gateways/cerebras-openai/usage/basic-stream).
