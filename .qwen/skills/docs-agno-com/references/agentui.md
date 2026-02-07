# AgentUI

**Source:** https://docs.agno.com/other/agent-ui.md
**Section:** Docs

**Description:** An Open Source AgentUI for your AgentOS

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentUI

> An Open Source AgentUI for your AgentOS

<Frame>
  <img height="200" src="https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=72cd1f0888dea4f1ec60a67bff5664c4" style={{ borderRadius: '8px' }} data-og-width="5364" data-og-height="2808" data-path="images/agent-ui.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=280&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=8a962c7d75c6fd40d37b696f258b69fc 280w, https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=560&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=729e6c42c46d47f9c56c66451576c53a 560w, https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=840&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=cabb3ed5cb4c1934bd3a5a1cba70a2d1 840w, https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=1100&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=d880656a6c120ed2ef06879bb522b840 1100w, https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=1650&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=55b22efc72db2bbb9e26079d46aea5b5 1650w, https://mintcdn.com/agno-v2/QfHdyhk-tu-JEw8s/images/agent-ui.png?w=2500&fit=max&auto=format&n=QfHdyhk-tu-JEw8s&q=85&s=5331541ccf7abdb289f0e213f65c9649 2500w" />
</Frame>

Agno provides a beautiful UI for interacting with your agents, completely open source, free to use and build on top of. It's a simple interface that allows you to chat with your agents, view their memory, knowledge, and more.

<Note>
  The AgentOS only uses data in your database. No data is sent to Agno.
</Note>

Built with Next.js and TypeScript, the Open Source Agent UI was developed in response to community requests for a self-hosted alternative following the success of [AgentOS](https://github.com/agent-os/introduction).

## Get Started with Agent UI

To clone the Agent UI, run the following command in your terminal:

```bash  theme={null}
npx create-agent-ui@latest
```

Enter `y` to create a new project, install dependencies, then run the agent-ui using:

```bash  theme={null}
cd agent-ui && npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the Agent UI, but remember to connect to your local agents.

<Frame>
  <img height="200" src="https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=02ec5ad7d40581f565548d64fd228fcc" style={{ borderRadius: '8px' }} data-og-width="3452" data-og-height="1910" data-path="images/agent-ui-homepage.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=280&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=09872fba3043aac4475f9d695e485f4d 280w, https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=560&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=71e8e367452dc8a47c043a3f23237711 560w, https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=840&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=bb3309860689377a150fae0c90b4837a 840w, https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=1100&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=68709e16d4ee79f7a0b91df6aab06612 1100w, https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=1650&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=7c8a19d650dea910381443f87f1f2e24 1650w, https://mintcdn.com/agno-v2/JcEPRFr_oNRDYYcC/images/agent-ui-homepage.png?w=2500&fit=max&auto=format&n=JcEPRFr_oNRDYYcC&q=85&s=14b29401ceb62992fed4584ecef540af 2500w" />
</Frame>

<br />

<Accordion title="Clone the repository manually" icon="github">
  You can also clone the repository manually

  ```bash  theme={null}
  git clone https://github.com/agno-agi/agent-ui.git
  ```

  And run the agent-ui using

  ```bash  theme={null}
  cd agent-ui && pnpm install && pnpm dev
  ```
</Accordion>

## Connect your AgentOS

The Agent UI needs to connect to a AgentOS server, which you can run locally or on any cloud provider.

Let's start with a local AgentOS server. Create a file `agentos.py`

```python agentos.py theme={null}
from agno.agent import Agent
from agno.models.openai import OpenAIResponses
from agno.os import AgentOS
from agno.db.sqlite import SqliteDb
from agno.tools.duckduckgo import DuckDuckGoTools
from agno.tools.yfinance import YFinanceTools

agent_storage: str = "tmp/agents.db"

web_agent = Agent(
    name="Web Agent",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[DuckDuckGoTools()],
    instructions=["Always include sources"],
    # Store the agent sessions in a sqlite database
    db=SqliteDb(db_file=agent_storage),
    # Adds the current date and time to the context
    add_datetime_to_context=True,
    # Adds the history of the conversation to the messages
    add_history_to_context=True,
    # Number of history responses to add to the messages
    num_history_runs=5,
    # Adds markdown formatting to the messages
    markdown=True,
)

finance_agent = Agent(
    name="Finance Agent",
    model=OpenAIResponses(id="gpt-5.2"),
    tools=[YFinanceTools()],
    instructions=["Always use tables to display data"],
    db=SqliteDb(db_file=agent_storage),
    add_datetime_to_context=True,
    add_history_to_context=True,
    num_history_runs=5,
    markdown=True,
)

agent_os = AgentOS(agents=[web_agent, finance_agent])
app = agent_os.get_app()

if __name__ == "__main__":
    agent_os.serve("agentos:app", reload=True)
```

In another terminal, run the AgentOS server:

<Steps>
  <Step title="Setup your virtual environment">
    <CodeGroup>
      ```bash Mac theme={null}
      python3 -m venv .venv
      source .venv/bin/activate
      ```

      ```bash Windows theme={null}
      python3 -m venv aienv
      aienv/scripts/activate
      ```
    </CodeGroup>
  </Step>

  <Step title="Install dependencies">
    <CodeGroup>
      ```bash Mac theme={null}
      uv pip install -U openai ddgs yfinance sqlalchemy 'fastapi[standard]' agno
      ```

      ```bash Windows theme={null}
      uv pip install -U openai ddgs yfinance sqlalchemy 'fastapi[standard]' agno
      ```
    </CodeGroup>
  </Step>

  <Step title="Export your OpenAI key">
    <CodeGroup>
      ```bash Mac theme={null}
      export OPENAI_API_KEY=sk-***
      ```

      ```bash Windows theme={null}
      setx OPENAI_API_KEY sk-***
      ```
    </CodeGroup>
  </Step>

  <Step title="Run the AgentOS">
    ```shell  theme={null}
    python agentos.py
    ```
  </Step>
</Steps>

<Tip>Make sure the module path in `agent_os.serve()` matches your filename (e.g., `"agentos:app"` for `agentos.py`).</Tip>

## View the AgentUI

* Open [http://localhost:3000](http://localhost:3000) to view the Agent UI
* Enter the `localhost:7777` endpoint on the left sidebar and start chatting with your agents and teams!

<video autoPlay muted controls className="w-full aspect-video" src="https://mintcdn.com/agno-v2/ZS8LtGag_F9zcKU4/videos/agent-ui-demo.mp4?fit=max&auto=format&n=ZS8LtGag_F9zcKU4&q=85&s=e4d7d59efdd156a677a403baeaa1d1a1" data-path="videos/agent-ui-demo.mp4" />

## Learn more

<CardGroup cols={2}>
  <Card title="AgentOS Introduction" icon="server" href="/agent-os/introduction">
    Learn about AgentOS
  </Card>

  <Card title="Building Agents" icon="robot" href="/agents/building-agents">
    Build your own agents
  </Card>
</CardGroup>
