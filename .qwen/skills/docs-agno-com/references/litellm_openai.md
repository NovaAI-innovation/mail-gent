# LiteLLM OpenAI

**Source:** https://docs.agno.com/models/providers/gateways/litellm-openai/overview.md
**Section:** Docs

**Description:** Use LiteLLM with Agno with an openai-compatible proxy server.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# LiteLLM OpenAI

> Use LiteLLM with Agno with an openai-compatible proxy server.

## Proxy Server Integration

LiteLLM can also be used as an OpenAI-compatible proxy server, allowing you to route requests to different models through a unified API.

### Starting the Proxy Server

First, install LiteLLM with proxy support:

```shell  theme={null}
uv pip install 'litellm[proxy]'
```

Start the proxy server:

```shell  theme={null}
litellm --model gpt-5-mini --host 127.0.0.1 --port 4000
```

### Using the Proxy

The `LiteLLMOpenAI` class connects to the LiteLLM proxy using an OpenAI-compatible interface:

```python  theme={null}
from agno.agent import Agent
from agno.models.litellm import LiteLLMOpenAI

agent = Agent(
    model=LiteLLMOpenAI(
        id="gpt-5-mini",  # Model ID to use
    ),
    markdown=True,
)

agent.print_response("Share a 2 sentence horror story")
```

### Configuration Options

The `LiteLLMOpenAI` class accepts the following parameters:

| Parameter  | Type | Description                                                    | Default                                      |
| ---------- | ---- | -------------------------------------------------------------- | -------------------------------------------- |
| `id`       | str  | Model identifier                                               | "gpt-5-mini"                                 |
| `name`     | str  | Display name for the model                                     | "LiteLLM"                                    |
| `provider` | str  | Provider name                                                  | "LiteLLM"                                    |
| `api_key`  | str  | API key (falls back to LITELLM\_API\_KEY environment variable) | None                                         |
| `base_url` | str  | URL of the LiteLLM proxy server                                | "[http://0.0.0.0:4000](http://0.0.0.0:4000)" |

`LiteLLMOpenAI` is a subclass of the [OpenAILike](/models/providers/openai-like) class and has access to the same params.

## Examples

Check out these examples in the cookbook:

### Proxy Examples

<Note> View more examples [here](/models/providers/gateways/litellm-openai/usage/basic-stream). </Note>
