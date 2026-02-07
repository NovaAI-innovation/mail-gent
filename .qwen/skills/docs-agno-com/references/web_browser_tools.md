# Web Browser Tools

**Source:** https://docs.agno.com/tools/toolkits/others/web-browser.md
**Section:** Docs

**Description:** WebBrowser Tools enable an Agent to open a URL in a web browser.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Web Browser Tools

> WebBrowser Tools enable an Agent to open a URL in a web browser.

## Example

```python cookbook/14_tools/webbrowser_tools.py theme={null}
from agno.agent import Agent
from agno.models.google import Gemini
from agno.tools.hackernews import HackerNewsTools
from agno.tools.webbrowser import WebBrowserTools

agent = Agent(
    model=Gemini("gemini-2.0-flash"),
    tools=[WebBrowserTools(), HackerNewsTools()],
    instructions=[
        "Find related articles using HackerNews",
        "Use web browser to open the site",
    ],
        markdown=True,
)
agent.print_response("Find an article explaining MCP and open it in the web browser.")
```

## Toolkit Params

| Parameter          | Type   | Default | Description                                   |
| ------------------ | ------ | ------- | --------------------------------------------- |
| `enable_open_page` | `bool` | `True`  | Enables functionality to open URLs in browser |
| `all`              | `bool` | `False` | Enables all functionality when set to True    |

## Toolkit Functions

| Function    | Description                  |
| ----------- | ---------------------------- |
| `open_page` | Opens a URL in a web browser |
