# Agent with URL Context

**Source:** https://docs.agno.com/models/providers/native/google/usage/url-context.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with URL Context

## Code

```python cookbook/11_models/google/gemini/url_context.py theme={null}
from agno.agent import Agent
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(id="gemini-2.5-flash", url_context=True),
    markdown=True,
)

url1 = "https://www.foodnetwork.com/recipes/ina-garten/perfect-roast-chicken-recipe-1940592"
url2 = "https://www.allrecipes.com/recipe/83557/juicy-roasted-chicken/"

agent.print_response(
    f"Compare the ingredients and cooking times from the recipes at {url1} and {url2}"
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
    uv pip install -U google-genai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/url_context.py
    ```
  </Step>
</Steps>
