# Audio Generation Tools

**Source:** https://docs.agno.com/multimodal/agent/usage/audio_generation.md
**Section:** Docs

**Description:** Generate audio with text-to-speech tools in Agno agents.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Audio Generation Tools

> Generate audio with text-to-speech tools in Agno agents.

The following example demonstrates how to generate an audio using the ElevenLabs tool with an agent. See [Eleven Labs](https://elevenlabs.io/) for more details.

## Prerequisites

You need to install the `elevenlabs` library and an API key which can be obtained from [Eleven Labs](https://elevenlabs.io/)

```bash  theme={null}
uv pip install elevenlabs
```

Set the `ELEVEN_LABS_API_KEY` environment variable.

```bash  theme={null}
export ELEVEN_LABS_API_KEY=****
```

```python audio_agent.py theme={null}
import base64

from agno.agent import Agent
from agno.models.google import Gemini
from agno.tools.eleven_labs import ElevenLabsTools
from agno.utils.media import save_base64_data

audio_agent = Agent(
    model=Gemini(id="gemini-2.5-pro"),
    tools=[
        ElevenLabsTools(
            voice_id="21m00Tcm4TlvDq8ikWAM",
            model_id="eleven_multilingual_v2",
            target_directory="audio_generations",
        )
    ],
    description="You are an AI agent that can generate audio using the ElevenLabs API.",
    instructions=[
        "When the user asks you to generate audio, use the `generate_audio` tool to generate the audio.",
        "You'll generate the appropriate prompt to send to the tool to generate audio.",
        "You don't need to find the appropriate voice first, I already specified the voice to user."
        "Return the audio file name in your response. Don't convert it to markdown.",
        "The audio should be long and detailed.",
    ],
    markdown=True,
)

response = audio_agent.run(
    "Generate a very long audio of history of french revolution and tell me which subject it belongs to.",
    debug_mode=True,
)

if response.audio:
    print("Agent response:", response.content)
    base64_audio = base64.b64encode(response.audio[0].content).decode("utf-8")
    save_base64_data(base64_audio, "tmp/french_revolution.mp3")
    print("Successfully saved generated speech to tmp/french_revolution.mp3")


audio_agent.print_response("Generate a kick sound effect")
```
