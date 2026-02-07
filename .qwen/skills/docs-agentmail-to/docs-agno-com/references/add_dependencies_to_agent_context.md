# Add Dependencies to Agent Context

**Source:** https://docs.agno.com/dependencies/agent/add-dependencies-to-context.md
**Section:** Docs

**Description:** This example demonstrates how to create a context-aware agent that can access real-time HackerNews data through dependency injection, enabling the agent to provide current information.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Add Dependencies to Agent Context

> This example demonstrates how to create a context-aware agent that can access real-time HackerNews data through dependency injection, enabling the agent to provide current information.

<Steps>
  <Step title="Create a Python file">
    ```python add_dependencies_to_context.py theme={null}
    import json

    import httpx

    from agno.agent import Agent
    from agno.models.openai import OpenAIResponses


    def get_top_hackernews_stories(num_stories: int = 5) -> str:
        """Fetch and return the top stories from HackerNews.

        Args:
            num_stories: Number of top stories to retrieve (default: 5)
        Returns:
            JSON string containing story details (title, url, score, etc.)
        """
        stories = [
            {
                k: v
                for k, v in httpx.get(
                    f"https://hacker-news.firebaseio.com/v0/item/{id}.json"
                )
                .json()
                .items()
                if k != "kids"
            }
            for id in httpx.get(
                "https://hacker-news.firebaseio.com/v0/topstories.json"
            ).json()[:num_stories]
        ]
        return json.dumps(stories, indent=4)


    agent = Agent(
        model=OpenAIResponses(id="gpt-5.2"),
        dependencies={"top_hackernews_stories": get_top_hackernews_stories},
        add_dependencies_to_context=True,
        markdown=True,
    )

    agent.print_response(
        "Summarize the top stories on HackerNews and identify any interesting trends.",
        stream=True,
    )
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai httpx
    ```
  </Step>

  <Step title="Export your OpenAI API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=your_openai_api_key_here
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python add_dependencies_to_context.py
    ```
  </Step>
</Steps>
