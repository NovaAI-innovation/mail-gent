# Transcription Agent

**Source:** https://docs.agno.com/models/providers/gateways/groq/usage/transcription-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Transcription Agent

## Code

```python cookbook/11_models/groq/transcription_agent.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.models.groq import GroqTools

url = "https://agno-public.s3.amazonaws.com/demo_data/sample_conversation.wav"

agent = Agent(
    name="Groq Transcription Agent",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[GroqTools(exclude_tools=["generate_speech"])],
)

agent.print_response(f"Please transcribe the audio file located at '{url}' to English")
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GROQ_API_KEY=xxx
    export OPENAI_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U groq openai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/groq/transcription_agent.py
    ```
  </Step>
</Steps>
