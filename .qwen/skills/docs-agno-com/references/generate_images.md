# Generate Images

**Source:** https://docs.agno.com/models/providers/native/openai/completion/usage/generate-images.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Generate Images

## Code

```python cookbook/11_models/openai/chat/generate_images.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.dalle import DalleTools

image_agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[DalleTools()],
    description="You are an AI agent that can generate images using DALL-E.",
    instructions="When the user asks you to create an image, use the `create_image` tool to create the image.",
    markdown=True,
)

image_agent.print_response("Generate an image of a white siamese cat")

images = image_agent.get_images()
if images and isinstance(images, list):
    for image_response in images:
        image_url = image_response.url
        print(image_url)
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
    python cookbook/11_models/openai/chat/generate_images.py
    ```
  </Step>
</Steps>
