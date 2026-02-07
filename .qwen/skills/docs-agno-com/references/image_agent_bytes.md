# Image Agent Bytes

**Source:** https://docs.agno.com/models/providers/native/xai/usage/image-agent-bytes.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Image Agent Bytes

## Code

```python cookbook/11_models/xai/image_agent_bytes.py theme={null}
from pathlib import Path

from agno.agent import Agent
from agno.media import Image
from agno.models.xai import xAI
from agno.tools.hackernews import HackerNewsTools
from agno.utils.media import download_image

agent = Agent(
    model=xAI(id="grok-2-vision-latest"),
    tools=[HackerNewsTools()],
    markdown=True,
)

image_path = Path(__file__).parent.joinpath("sample.jpg")

download_image(
    url="https://upload.wikimedia.org/wikipedia/commons/0/0c/GoldenGateBridge-001.jpg",
    output_path=str(image_path),
)

# Read the image file content as bytes
image_bytes = image_path.read_bytes()

agent.print_response(
    "Tell me about this image and give me the latest news about it.",
    images=[
        Image(content=image_bytes),
    ],
    stream=True,
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export XAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U xai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/xai/image_agent_bytes.py
    ```
  </Step>
</Steps>
