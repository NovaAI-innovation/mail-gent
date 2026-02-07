# Image to Image Generation Agent

**Source:** https://docs.agno.com/multimodal/agent/usage/image-to-image-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Image to Image Generation Agent

This example demonstrates how to create an AI agent that generates images from existing images using the Fal AI API.

## Code

```python image_to_image_agent.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.fal import FalTools

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    id="image-to-image",
    name="Image to Image Agent",
    tools=[FalTools()],
    markdown=True,
    instructions=[
        "You have to use the `image_to_image` tool to generate the image.",
        "You are an AI agent that can generate images using the Fal AI API.",
        "You will be given a prompt and an image URL.",
        "You have to return the image URL as provided, don't convert it to markdown or anything else.",
    ],
)

agent.print_response(
    "a cat dressed as a wizard with a background of a mystic forest. Make it look like 'https://fal.media/files/koala/Chls9L2ZnvuipUTEwlnJC.png'",
    stream=True,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
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
    python image_to_image_agent.py
    ```
  </Step>
</Steps>
