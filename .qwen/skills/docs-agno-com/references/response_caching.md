# Response Caching

**Source:** https://docs.agno.com/models/providers/native/openai/completion/usage/cache-response.md
**Section:** Docs

**Description:** Cache model responses to reduce API calls and costs.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Response Caching

> Cache model responses to reduce API calls and costs.

<Note>
  For a conceptual overview of response caching, see [Response Caching](/models/cache-response).
</Note>

Response caching allows you to cache model responses, which can significantly improve response times and reduce API costs during development and testing.

## Basic Usage

Enable caching by setting `cache_response=True` when initializing the model. The first call will hit the API and cache the response, while subsequent identical calls will return the cached result.

```python cache_model_response.py theme={null}
import time

from agno.agent import Agent
from agno.models.openai import OpenAIResponses

agent = Agent(model=OpenAIResponses(id="gpt-5.2", cache_response=True))

# Run the same query twice to demonstrate caching
for i in range(1, 3):
    print(f"\n{'=' * 60}")
    print(
        f"Run {i}: {'Cache Miss (First Request)' if i == 1 else 'Cache Hit (Cached Response)'}"
    )
    print(f"{'=' * 60}\n")

    response = agent.run(
        "Write me a short story about a cat that can talk and solve problems."
    )
    print(response.content)
    print(f"\n Elapsed time: {response.metrics.duration:.3f}s")

    # Small delay between iterations for clarity
    if i == 1:
        time.sleep(0.5)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cache_model_response.py
    ```
  </Step>
</Steps>
