# Image Transcribe Document Agent

**Source:** https://docs.agno.com/models/providers/native/mistral/usage/image-transcribe-document-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Image Transcribe Document Agent

## Code

```python cookbook/11_models/mistral/image_transcribe_document_agent.py theme={null}
from agno.agent import Agent
from agno.media import Image
from agno.models.mistral.mistral import MistralChat

agent = Agent(
    model=MistralChat(id="pixtral-12b-2409"),
    markdown=True,
)

agent.print_response(
    "Transcribe this document.",
    images=[
        Image(url="https://ciir.cs.umass.edu/irdemo/hw-demo/page_example.jpg"),
    ],
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
    python cookbook/11_models/mistral/image_transcribe_document_agent.py
    ```
  </Step>
</Steps>
