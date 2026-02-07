# Generate output image using DALL-E with intermediate steps

**Source:** https://docs.agno.com/multimodal/agent/usage/generate-image-with-intermediate-steps.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Generate output image using DALL-E with intermediate steps

This example demonstrates how to create an Agno agent that generates images using DALL-E while streaming during the image creation process.

## Code

```python generate_image_with_intermediate_steps.py theme={null}
from typing import Iterator

from agno.agent import Agent, RunOutputEvent
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

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai rich
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export OPENAI_API_KEY="your_openai_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:OPENAI_API_KEY="your_openai_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python generate_image_with_intermediate_steps.py
    ```
  </Step>
</Steps>
