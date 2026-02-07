# Generate output image using DALL-E

**Source:** https://docs.agno.com/multimodal/agent/usage/generate-image.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Generate output image using DALL-E

This example demonstrates how Agno agents can be used to create images using DALL-E.

## Code

```python  theme={null}
from typing import Iterator

from agno.agent import Agent, RunOutput
from agno.models.openai import OpenAIResponses
from agno.tools.dalle import DalleTools
from agno.utils.common import dataclass_to_dict
from rich.pretty import pprint

image_agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[DalleTools()],
    description="You are an AI agent that can create images using DALL-E.",
    instructions=[
        "When the user asks you to create an image, use the DALL-E tool to create an image.",
        "The DALL-E tool will return an image URL.",
        "Return the image URL in your response in the following format: `![image description](image URL)`",
    ],
    markdown=True,
)

run_stream: Iterator[RunOutputEvent] = image_agent.run(
    "Create an image of a yellow siamese cat",
    stream=True,
    stream_events=True,
)
for chunk in run_stream:
    pprint(dataclass_to_dict(chunk, exclude={"messages"}))
    print("---" * 20)
```

## Deploy

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai rich agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/agent_basics/multimodal/generate_image_with_intermediate_steps.py
    ```
  </Step>
</Steps>
