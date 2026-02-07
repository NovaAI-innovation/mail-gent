# Google

**Source:** https://docs.agno.com/cookbook/models/google.md
**Section:** Docs

**Description:** Use Gemini models with video, audio, search, and Imagen generation.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Google

> Use Gemini models with video, audio, search, and Imagen generation.

Gemini models with native multimodal support. Handles text, images, video, and audio with built-in Google Search.

```python  theme={null}
from agno.agent import Agent
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash"),
    markdown=True,
)

agent.print_response("Explain the theory of relativity", stream=True)
```

## Tool Use

```python  theme={null}
from agno.agent import Agent
from agno.models.google import Gemini
from agno.tools.yfinance import YFinanceTools

agent = Agent(
    model=Gemini(id="gemini-2.0-flash"),
    tools=[YFinanceTools(stock_price=True)],
    markdown=True,
)

agent.print_response("What's GOOGL's stock price?", stream=True)
```

## Video Input

```python  theme={null}
from agno.agent import Agent
from agno.media import Video
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash"),
    markdown=True,
)

agent.print_response(
    "Tell me about this video",
    videos=[Video(url="https://www.youtube.com/watch?v=XinoY2LDdA0")],
)
```

## Google Search

```python  theme={null}
from agno.agent import Agent
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.0-flash", search=True),
    markdown=True,
)

agent.print_response("What are the latest developments in AI this week?")
```

## Structured Output

```python  theme={null}
from pydantic import BaseModel, Field
from agno.agent import Agent
from agno.models.google import Gemini

class Recipe(BaseModel):
    name: str = Field(..., description="Recipe name")
    ingredients: list[str] = Field(..., description="List of ingredients")
    instructions: list[str] = Field(..., description="Cooking instructions")

agent = Agent(
    model=Gemini(id="gemini-2.0-flash"),
    output_schema=Recipe,
)

agent.print_response("Give me a recipe for pasta carbonara")
```

## Run Examples

```bash  theme={null}
export GOOGLE_API_KEY=xxx

# Clone and run
git clone https://github.com/agno-agi/agno.git
cd agno/cookbook/90_models/google/gemini

python basic.py
python tool_use.py
python video_input_youtube.py
python search.py
```
