# Audio to Text Transcription

**Source:** https://docs.agno.com/multimodal/agent/usage/audio-to-text.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Audio to Text Transcription

This example demonstrates how to create an agent that can transcribe audio conversations, identifying different speakers and providing accurate transcriptions.

## Code

```python audio_to_text.py theme={null}
import requests
from agno.agent import Agent
from agno.media import Audio
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash-exp"),
    markdown=True,
)

url = "https://agno-public.s3.us-east-1.amazonaws.com/demo_data/QA-01.mp3"

response = requests.get(url)
audio_content = response.content

# Give a transcript of this audio conversation. Use speaker A, speaker B to identify speakers.

agent.print_response(
    "Give a transcript of this audio conversation. Use speaker A, speaker B to identify speakers.",
    audio=[Audio(content=audio_content)],
    stream=True,
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno google-generativeai requests
    ```
  </Step>

  <Step title="Export your GOOGLE API key">
    <CodeGroup>
      ```bash Mac/Linux theme={null}
        export GOOGLE_API_KEY="your_google_api_key_here"
      ```

      ```bash Windows theme={null}
        $Env:GOOGLE_API_KEY="your_google_api_key_here"
      ```
    </CodeGroup>
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python audio_to_text.py
    ```
  </Step>
</Steps>
