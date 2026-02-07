# Audio Input (Bytes Content)

**Source:** https://docs.agno.com/models/providers/native/google/usage/audio-input-bytes-content.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Audio Input (Bytes Content)

## Code

```python cookbook/11_models/google/gemini/audio_input_bytes_content.py theme={null}
import requests
from agno.agent import Agent
from agno.media import Audio
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash-exp"),
    markdown=True,
)

url = "https://openaiassets.blob.core.windows.net/$web/API/docs/audio/alloy.wav"

# Download the audio file from the URL as bytes
response = requests.get(url)
audio_content = response.content

agent.print_response(
    "Tell me about this audio",
    audio=[Audio(content=audio_content)],
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API key">
    ```bash  theme={null}
    export GOOGLE_API_KEY=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U google-genai requests agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/audio_input_bytes_content.py
    ```
  </Step>
</Steps>
