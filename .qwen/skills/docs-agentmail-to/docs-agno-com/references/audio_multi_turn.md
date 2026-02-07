# Audio Multi Turn

**Source:** https://docs.agno.com/multimodal/agent/usage/audio-multi-turn.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Audio Multi Turn

This example demonstrates how to create an agent that can handle multi-turn audio conversations, maintaining context between audio interactions while generating both text and audio responses.

## Code

```python audio_multi_turn.py theme={null}
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.openai import OpenAIResponses
from agno.utils.audio import write_audio_to_file
from rich.pretty import pprint

agent = Agent(
    model=OpenAIResponses(
        id="gpt-5.2-audio-preview",
        modalities=["text", "audio"],
        audio={"voice": "sage", "format": "wav"},
    ),
    add_history_to_context=True,
    db=SqliteDb(
        session_table="audio_multi_turn_sessions", db_file="tmp/audio_multi_turn.db"
    ),
)

run_response = agent.run("Is a golden retriever a good family dog?")
pprint(run_response.content)
if run_response.response_audio is not None:
    write_audio_to_file(
        audio=run_response.response_audio.content, filename="tmp/answer_1.wav"
    )

run_response = agent.run("What breed are we talking about?")
pprint(run_response.content)
if run_response.response_audio is not None:
    write_audio_to_file(
        audio=run_response.response_audio.content, filename="tmp/answer_2.wav"
    )
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U openai agno
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
    python audio_multi_turn.py
    ```
  </Step>
</Steps>
