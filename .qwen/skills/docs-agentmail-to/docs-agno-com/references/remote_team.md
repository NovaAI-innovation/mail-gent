# Remote Team

**Source:** https://docs.agno.com/agent-os/usage/remote-execution/remote-team.md
**Section:** Docs

**Description:** Execute teams hosted on a remote AgentOS instance

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Remote Team

> Execute teams hosted on a remote AgentOS instance

<Steps>
  <Step title="Create a Python file">
    ```python remote_team.py theme={null}
    import asyncio

    from agno.team import RemoteTeam


    async def remote_team_example():
        """Call a remote team hosted on another AgentOS instance."""
        team = RemoteTeam(
            base_url="http://localhost:7777",
            team_id="research-team",
        )

        response = await team.arun(
            "What is the capital of France?",
            user_id="user-123",
            session_id="session-456",
        )
        print(response.content)


    async def remote_streaming_example():
        """Stream responses from a remote team."""
        team = RemoteTeam(
            base_url="http://localhost:7777",
            team_id="research-team",
        )

        async for chunk in team.arun(
            "Tell me about Python programming",
            session_id="session-456",
            user_id="user-123",
            stream=True,
        ):
            if hasattr(chunk, "content") and chunk.content:
                print(chunk.content, end="", flush=True)


    if __name__ == "__main__":
        print("=" * 60)
        print("RemoteTeam Examples")
        print("=" * 60)

        print("\n1. Remote Team Example:")
        asyncio.run(remote_team_example())

        print("\n\n2. Remote Streaming Example:")
        asyncio.run(remote_streaming_example())
    ```
  </Step>

  <Snippet file="create-venv-step.mdx" />

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -U agno openai
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

  <Step title="Start an AgentOS Server">
    Make sure you have an AgentOS server running with a team that has `id="research-team"`. See [Creating Your First OS](/agent-os/run-your-os) for setup instructions.
  </Step>

  <Step title="Run the Client">
    <CodeGroup>
      ```bash Mac theme={null}
      python remote_team.py
      ```

      ```bash Windows theme={null}
      python remote_team.py
      ```
    </CodeGroup>
  </Step>
</Steps>
