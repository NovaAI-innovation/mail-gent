# Building Agents

**Source:** https://docs.agno.com/agents/building-agents.md
**Section:** Docs

**Description:** Start simple: a model, tools, and instructions.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Building Agents

> Start simple: a model, tools, and instructions.

To build effective agents, start simple: a model, tools, and instructions. Once that works, layer in more functionality as needed. For example, here's the simplest possible agent with access to `HackerNews`:

```python hackernews_agent.py theme={null}
from agno.agent import Agent
from agno.models.anthropic import Claude
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=Claude(id="claude-sonnet-4-5"),
    tools=[HackerNewsTools()],
    instructions="Write a report on the topic. Output only the report.",
    markdown=True,
)
agent.print_response("Trending startups and products.", stream=True)
```

## Run your Agent

Use `Agent.print_response()` for development. It prints the response in a readable format in your terminal.

For production, use `Agent.run()` or `Agent.arun()`:

```python  theme={null}
from typing import Iterator
from agno.agent import Agent, RunOutputEvent, RunEvent
from agno.models.anthropic import Claude
from agno.tools.hackernews import HackerNewsTools

agent = Agent(
    model=Claude(id="claude-sonnet-4-5"),
    tools=[HackerNewsTools()],
    instructions="Write a report on the topic. Output only the report.",
    markdown=True,
)

# Stream the response
stream: Iterator[RunOutputEvent] = agent.run("Trending products", stream=True)
for chunk in stream:
    if chunk.event == RunEvent.run_content:
        print(chunk.content)
```

## Next Steps

After getting familiar with the basics, add functionality as needed:

| Task                               | Guide                                        |
| ---------------------------------- | -------------------------------------------- |
| Run agents                         | [Running agents](/agents/running-agents)     |
| Debug agents                       | [Debugging agents](/agents/debugging-agents) |
| Manage sessions                    | [Agent sessions](/sessions/overview)         |
| Handle input/output                | [Input and output](/input-output/overview)   |
| Add tools                          | [Tools](/tools/overview)                     |
| Manage context                     | [Context engineering](/context/overview)     |
| Add knowledge                      | [Knowledge](/knowledge/overview)             |
| Handle images, audio, video, files | [Multimodal](/multimodal/overview)           |
| Add guardrails                     | [Guardrails](/guardrails/overview)           |
| Cache responses during development | [Response caching](/models/cache-response)   |
