# AgentOS on Docker

**Source:** https://docs.agno.com/production/templates/docker.md
**Section:** Docs

**Description:** Run AgentOS locally using Docker.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentOS on Docker

> Run AgentOS locally using Docker.

This template includes AgentOS and PostgreSQL with pgvector. Run locally for development, or deploy to any cloud that supports Docker.

## Step-by-step Guide

<Steps>
  <Step title="Install tools">
    * Install [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/)
    * Install [uv](https://docs.astral.sh/uv/) (Python package manager)
  </Step>

  <Step title="Create and activate a virtual environment">
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

  <Step title="Create your codebase">
    ```bash  theme={null}
    ag infra create --template agentos-docker --name agentos-docker

    cd agentos-docker
    ```

    <Tip>
      Or clone directly: `git clone https://github.com/agno-agi/agentos-docker-template.git`
    </Tip>
  </Step>

  <Step title="Export your API key">
    ```bash  theme={null}
    export OPENAI_API_KEY=sk-***
    ```

    <Tip>
      Agno works with any model provider. Just update the agents in your codebase.
    </Tip>
  </Step>

  <Step title="Start your AgentOS">
    ```bash  theme={null}
    docker compose up -d --build
    ```
  </Step>

  <Step title="Verify it works">
    Open [http://localhost:8000/docs](http://localhost:8000/docs) to see your AgentOS API:

    <Frame>
      <img src="https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=b29f0058c6920a5f8c286642b800ebcb" alt="AgentOS FastAPI endpoints" data-og-width="3064" width="3064" data-og-height="2272" height="2272" data-path="images/agentos-endpoints.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=280&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=499a4bdc9e1bdd275a5bc9d9929a8c9f 280w, https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=560&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=5b45fc3c8db8848287025e048043cfcc 560w, https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=840&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=f4113206dea30b3cb54b474af3de51b4 840w, https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=1100&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=8997cfd1d55fb3e8cd7ad4432d01af4e 1100w, https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=1650&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=d0f92a98e1e8494d45400c4a44fa6e1b 1650w, https://mintcdn.com/agno-v2/NGh0J86bCmPKi7an/images/agentos-endpoints.png?w=2500&fit=max&auto=format&n=NGh0J86bCmPKi7an&q=85&s=3c4dbfeb8837d895039ffd745b49f6d4 2500w" />
    </Frame>
  </Step>

  <Step title="Connect your AgentOS to the control plane">
    1. Open [os.agno.com](https://os.agno.com)
    2. Click "Connect OS" and select "Local"
    3. Enter `http://localhost:8000`

    <Frame>
      <img src="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=dace555ba53468d3b5d8c8a3a50f9acb" alt="AgentOS connection dialog" data-og-width="2472" width="2472" data-og-height="2408" height="2408" data-path="images/agent-os-connection-dialog.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=280&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=0a6df0f8e440140f73eb1d6b5a9600eb 280w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=560&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=97967d6ed45c07eb13d81eeb39cae267 560w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=840&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=419ccf4c560b3fae2e56fc85659fb8d6 840w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=1100&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=ee04e8acffb1ca82c4091447c6f0e871 1100w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=1650&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=8e647d974cc5b1a1916cc976a86c131a 1650w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agent-os-connection-dialog.png?w=2500&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=e9dcbbeb8274cb21e5dcdc91f3b5d7e7 2500w" />
    </Frame>
  </Step>
</Steps>

## Tips

**Hot reload**: Changes to agents, teams, and workflows are reflected automatically.

**Environment variables**: Restart containers when updating environment variables.

**Common commands:**

| ag infra           | docker compose                 | Description        |
| ------------------ | ------------------------------ | ------------------ |
| `ag infra up`      | `docker compose up -d --build` | Start containers   |
| `ag infra down`    | `docker compose down`          | Stop containers    |
| `ag infra restart` | `docker compose restart`       | Restart containers |
|                    | `docker compose logs -f`       | View logs          |

**Project structure:**

```
agentos-docker/
├── agents/              # Your agents
├── teams/               # Your teams
├── workflows/           # Your workflows
├── app/                 # AgentOS directory
├── db/                  # Database tables
├── compose.yml          # Docker Compose configuration
├── Dockerfile           # Container build
├── pyproject.toml       # Python dependencies
└── scripts/             # Helper scripts
```

## Deploy to Production

You can deploy this template to any cloud that supports Docker.

**Cloud providers:** [AWS ECS](https://aws.amazon.com/ecs/), [Google Cloud Compute Engine](https://cloud.google.com/compute-engine/), [Azure Virtual Machines](https://azure.microsoft.com/en-us/products/virtual-machines/)

**Platforms:** [Railway](https://railway.app/), [Render](https://render.com/), [DigitalOcean](https://digitalocean.com/), [Fly.io](https://fly.io/), [Modal](https://modal.com/)

## Troubleshooting

<AccordionGroup>
  <Accordion title="Port already in use">
    Modify `compose.yml`:

    ```yaml  theme={null}
        ports:
          - "8080:8000"  # Change 8000 to 8080
    ```
  </Accordion>

  <Accordion title="Database connection issues">
    Ensure PostgreSQL is running:

    ```bash  theme={null}
        docker compose ps
    ```

    If the database isn't ready, wait a few seconds and try again.
  </Accordion>
</AccordionGroup>
