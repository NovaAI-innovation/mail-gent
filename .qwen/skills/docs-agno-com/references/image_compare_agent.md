# Image Compare Agent

**Source:** https://docs.agno.com/models/providers/native/mistral/usage/image-compare-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Image Compare Agent

## Code

```python cookbook/11_models/mistral/image_compare_agent.py theme={null}
from agno.agent import Agent
from agno.media import Image
from agno.models.mistral.mistral import MistralChat

agent = Agent(
    model=MistralChat(id="pixtral-12b-2409"),
    markdown=True,
)

agent.print_response(
    "what are the differences between two images?",
    images=[
        Image(
            url="https://tripfixers.com/wp-content/uploads/2019/11/eiffel-tower-with-snow.jpeg"
        ),
        Image(
            url="https://assets.visitorscoverage.com/production/wp-content/uploads/2024/04/AdobeStock_626542468-min-1024x683.jpeg"
        ),
    ],
    stream=True,
)

```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export MISTRAL_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U mistralai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/mistral/image_compare_agent.py
    ```
  </Step>
</Steps>
