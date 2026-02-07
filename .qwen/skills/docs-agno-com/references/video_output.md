# Video Output

**Source:** https://docs.agno.com/multimodal/agent/usage/video_generation.md
**Section:** Docs

**Description:** Generate videos with AI tools in Agno agents.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Video Output

> Generate videos with AI tools in Agno agents.

This example demonstrates how to generate a video using [FAL](https://fal.ai/video) in an Agno agent.

## Prerequisites

You'll need to have the following:

* `fal_client` library installed
* An API key from [Fal](https://fal.ai/)

## Setup

```shell  theme={null}
uv pip install -U fal_client
```

```shell  theme={null}
export FAL_KEY=***
```

## Code

```python video_agent.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.tools.fal import FalTools

fal_agent = Agent(
    name="Fal Video Generator Agent",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[
        FalTools(
            model="fal-ai/hunyuan-video",
            enable_generate_media=True,
        )
    ],
    description="You are an AI agent that can generate videos using the Fal API.",
    instructions=[
        "When the user asks you to create a video, use the `generate_media` tool to create the video.",
        "Return the URL as raw to the user.",
        "Don't convert video URL to markdown or anything else.",
    ],
    markdown=True,
)

fal_agent.print_response("Generate video of balloon in the ocean")

```
