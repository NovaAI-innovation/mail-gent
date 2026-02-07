# Image Agent with Bytes

**Source:** https://docs.agno.com/models/providers/native/dashscope/usage/image-agent-bytes.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Image Agent with Bytes

## Code

```python cookbook/11_models/dashscope/image_agent_bytes.py theme={null}
from pathlib import Path

from agno.agent import Agent
from agno.media import Image
from agno.models.dashscope import DashScope
from agno.tools.hackernews import HackerNewsTools
from agno.utils.media import download_image

agent = Agent(
    model=DashScope(id="qwen-vl-plus"),
    tools=[HackerNewsTools()],
    markdown=True,
)

image_path = Path(__file__).parent.joinpath("sample.jpg")

download_image(
    url="https://upload.wikimedia.org/wikipedia/commons/a/a7/Camponotus_flavomarginatus_ant.jpg",
    output_path=str(image_path),
)

# Read the image file content as bytes
image_bytes = image_path.read_bytes()

agent.print_response(
    "Analyze this image of an ant. Describe its features, species characteristics, and search for more information about this type of ant.",
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
    export DASHSCOPE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/dashscope/image_agent_bytes.py
    ```
  </Step>
</Steps>
