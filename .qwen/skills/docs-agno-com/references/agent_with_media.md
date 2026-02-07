# Agent with Media

**Source:** https://docs.agno.com/integrations/discord/usage/agent-with-media.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with Media

## Code

```python cookbook/13_integrations/discord/agent_with_media.py theme={null}
from agno.agent import Agent
from agno.integrations.discord import DiscordClient
from agno.models.google import Gemini

media_agent = Agent(
    name="Media Agent",
    model=Gemini(id="gemini-2.0-flash"),
    description="A Media processing agent",
    instructions="Analyze images, audios and videos sent by the user",
    add_history_to_context=True,
    num_history_runs=3,
    add_datetime_to_context=True,
    markdown=True,
)

discord_agent = DiscordClient(media_agent)
if __name__ == "__main__":
     discord_agent.serve()
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set your API keys">
    ```bash  theme={null}
    export GOOGLE_API_KEY=xxx
    export DISCORD_BOT_TOKEN=xxx
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno google-generativeai discord.py
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/13_integrations/discord/agent_with_media.py
    ```
  </Step>
</Steps>
