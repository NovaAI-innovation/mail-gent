# High Fidelity Image Input

**Source:** https://docs.agno.com/multimodal/agent/usage/image-input-high-fidelity.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# High Fidelity Image Input

This example demonstrates how to use high fidelity image analysis with an AI agent by setting the detail parameter.

## Code

```python image_input_high_fidelity.py theme={null}
from agno.agent import Agent
from agno.media import Image
from agno.models.openai import OpenAIResponses

agent = Agent(
    model=OpenAIResponses(id="gpt-5.2"),
    markdown=True,
)

agent.print_response(
    "What's in these images",
    images=[
        Image(
            url="https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/Gfp-wisconsin-madison-the-nature-boardwalk.jpg/2560px-Gfp-wisconsin-madison-the-nature-boardwalk.jpg",
            detail="high",
        )
    ],
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
    python image_input_high_fidelity.py
    ```
  </Step>
</Steps>
