# Video Input

**Source:** https://docs.agno.com/multimodal/agent/usage/video_input.md
**Section:** Docs

**Description:** Process video as input with Agno agents.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Video Input

> Process video as input with Agno agents.

In this example we will create an agent that can understand video input.

```python video_agent.py theme={null}
from pathlib import Path

from agno.agent import Agent
from agno.media import Video
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash-001"),
    markdown=True,
)

# Please download "GreatRedSpot.mp4" using
# wget https://storage.googleapis.com/generativeai-downloads/images/GreatRedSpot.mp4
video_path = Path(__file__).parent.joinpath("GreatRedSpot.mp4")

agent.print_response("Tell me about this video", videos=[Video(filepath=video_path)])
```
