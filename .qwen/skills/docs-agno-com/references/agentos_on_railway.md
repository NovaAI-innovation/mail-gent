# AgentOS on Railway

**Source:** https://docs.agno.com/production/templates/railway.md
**Section:** Docs

**Description:** Deploy AgentOS to Railway.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentOS on Railway

> Deploy AgentOS to Railway.

This template deploys AgentOS and PostgreSQL with pgvector to Railway. Automatic HTTPS and public domain included.

## What's Included

| Component           | Description                           |
| ------------------- | ------------------------------------- |
| **AgentOS**         | FastAPI server running your AI agents |
| **PostgreSQL**      | Database with pgvector for embeddings |
| **Automatic HTTPS** | Railway handles TLS certificates      |
| **Public Domain**   | your-app.up.railway.app               |

## Prerequisites

You'll need:

* [Docker Desktop](https://docker.com/desktop)
* [uv](https://docs.astral.sh/uv) (Python package manager)
* [Railway account](https://railway.app) (free tier works)
* [OpenAI API key](https://platform.openai.com)

**Install Railway CLI:**

<CodeGroup>
  ```bash Mac theme={null}
  brew install railway
  ```

  ```bash Windows/Linux theme={null}
  npm install -g @railway/cli
  ```
</CodeGroup>

## Deploy

Let's start by creating the project

### Create Your Project

<Steps>
  <Step title="Set up Python environment">
    ```bash  theme={null}
    uv venv --python 3.12
    source .venv/bin/activate
    ```
  </Step>

  <Step title="Install Agno">
    ```bash  theme={null}
    uv pip install -U 'agno[infra]'
    ```
  </Step>

  <Step title="Create from template">
    ```bash  theme={null}
    ag infra create --template agentos-railway --name my-agentos
    cd my-agentos
    ```
  </Step>

  <Step title="Set your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=sk-***
    ```
  </Step>
</Steps>

### Included Agents

These agents are ready to use once deployed:

<CardGroup cols={3}>
  <Card title="Pal" icon="graduation-cap">
    Personal assistant that learns from you. Stores notes, bookmarks, and research findings.
  </Card>

  <Card title="Knowledge Agent" icon="book">
    RAG agent that answers questions from your documents. Pre-loaded with Agno docs.
  </Card>

  <Card title="MCP Agent" icon="plug">
    Connects to external tools via MCP. Extensible with any MCP-compatible service.
  </Card>
</CardGroup>

### Deploy to Railway

<Steps titleSize="h3">
  <Step title="Login and deploy" stepNumber={5}>
    ```bash  theme={null}
    railway login
    ./scripts/railway_up.sh
    ```

    This creates the project, provisions PostgreSQL with pgvector, and deploys your AgentOS. Takes \~2 minutes.
  </Step>

  <Step title="Get your domain" stepNumber={6}>
    ```bash  theme={null}
    railway open
    ```

    Find your URL in the dashboard (e.g., `my-agentos.up.railway.app`). Navigate to `<railway-domain>/docs` to see your AgentOS API.
  </Step>
</Steps>

### Connect to Control Plane

<Steps titleSize="h3">
  <Step title="Connect your AgentOS" stepNumber={7}>
    1. Go to [os.agno.com](https://os.agno.com)
    2. Click "Connect OS" → Select "Live"
    3. Paste your Railway domain

    <Frame>
      <img className="block dark:hidden" src="https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=60338a1404ecc414aa72dd8a0d71c024" alt="AgentOS connection dialog" data-og-width="1232" width="1232" data-og-height="1478" height="1478" data-path="images/agent-os-connection-railway-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=280&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=a0df287cf716b0b302ef0db0441306bb 280w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=560&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=a3b1805ad04b9088880e07ea6204d41b 560w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=840&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=fd1a7d64aa5cd9e132f3d9e14572f42c 840w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=1100&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=85e47dde525ce43c69cdde38c6909822 1100w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=1650&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=47abda12d872a2e4af663bd444676944 1650w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway-light.png?w=2500&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=fdd49a86e4270218b947c745df461b04 2500w" />

      <img className="hidden dark:block" src="https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=14f29c8dd1a884c11e9402b12dd72598" alt="AgentOS connection dialog" data-og-width="1232" width="1232" data-og-height="1464" height="1464" data-path="images/agent-os-connection-railway.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=280&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=911fc620e131e638e6fe69089821582e 280w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=560&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=c18fbc3a8d8ae1945f4469b75dc5976e 560w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=840&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=5ab095e24722c86822f5db3f32b08623 840w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=1100&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=d627d883c7aa4fdbb9c66162ec2a99be 1100w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=1650&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=301a304c85b17047b819dfc1fbfb87eb 1650w, https://mintcdn.com/agno-v2/ACGFg1IKv6IfuEMR/images/agent-os-connection-railway.png?w=2500&fit=max&auto=format&n=ACGFg1IKv6IfuEMR&q=85&s=433f9db0bd73b0955b1899a529df37d0 2500w" />
    </Frame>
  </Step>
</Steps>

<Check>
  Your AgentOS is live! Manage it from os.agno.com
</Check>

## Next Steps

<CardGroup cols={2}>
  <Card title="Build Custom Agents" icon="robot" href="/agents/building-agents">
    Create agents with your own tools and prompts.
  </Card>

  <Card title="Add Tools" icon="wrench" href="/tools/overview">
    Slack, GitHub, databases, and 100+ integrations.
  </Card>

  <Card title="Add Knowledge" icon="database" href="/knowledge/overview">
    Load documents, websites, and databases for RAG.
  </Card>

  <Card title="Add Interfaces" icon="comments" href="/production/interfaces/overview">
    Deploy to Slack, Discord, WhatsApp, or expose via MCP.
  </Card>
</CardGroup>

## Reference

| Task             | Command                                               |
| ---------------- | ----------------------------------------------------- |
| Deploy updates   | `railway up --service agent_os -d`                    |
| View logs        | `railway logs --service agent_os`                     |
| Open dashboard   | `railway open`                                        |
| Set env variable | `railway variables set KEY=value`                     |
| Stop service     | `railway down --service agent_os`                     |
| Scale replicas   | Edit `railway.json`: `{"deploy": {"numReplicas": 2}}` |
| Switch model     | `railway variables set ANTHROPIC_API_KEY=sk-ant-***`  |

## Troubleshooting

<AccordionGroup>
  <Accordion title="'railway: command not found'">
    Install: `brew install railway` (Mac) or `npm install -g @railway/cli`
  </Accordion>

  <Accordion title="Deployment fails">
    Run `railway init` first, then `./scripts/railway_up.sh` again.
  </Accordion>

  <Accordion title="Database timeout">
    PostgreSQL takes \~30s. Check: `railway logs --service pgvector`
  </Accordion>

  <Accordion title="502 error">
    Container starting. Wait 1-2 min. Check: `railway logs --service agent_os`
  </Accordion>
</AccordionGroup>
