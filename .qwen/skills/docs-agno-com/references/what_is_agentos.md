# What is AgentOS?

**Source:** https://docs.agno.com/agent-os/introduction.md
**Section:** Docs

**Description:** The runtime and control plane for multi-agent systems.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# What is AgentOS?

> The runtime and control plane for multi-agent systems.

**AgentOS turns your agents into a production API you can deploy anywhere.** It gives you a pre-built backend for your AI product, so all you need to do is add your agent logic, build your frontend and your product is live.

You bring the agents and AgentOS turns it into a product:

* 50+ API endpoints with SSE-compatible streaming. Ready for production on day one.
* Sessions, memory, knowledge stored in your database. Your data stays in your system.
* Request-level isolation. No state bleed between users, agents and sessions.
* JWT-based RBAC with hierarchical scopes. Enterprise-ready from day one.
* Tracing built-in, stored in your database. No third-party egress. No vendor lock-in.
* Guardrails, human in the loop, learning machines. The full Agno framework.

Here's an example of an AgentOS serving an Agent with memory, state, and MCP tools:

```python agno_agent.py theme={null}
from agno.os import AgentOS
from agno.agent import Agent
from agno.db.sqlite import SqliteDb
from agno.models.anthropic import Claude

agent = Agent(
    name="Agno Agent",
    model=Claude(id="claude-sonnet-4-5"),
    db=SqliteDb(db_file="agno.db"),
    add_history_to_context=True,
    markdown=True,
)

agent_os = AgentOS(agents=[agent])
app = agent_os.get_app()

if __name__ == "__main__":
    agent_os.serve(app="agno_agent:app", reload=True)
```

<Check>
  AgentOS runs on FastAPI. Add middleware, custom routes, background tasks, or any FastAPI feature without extra configuration.
</Check>

## Control Plane

AgentOS comes with a built-in [control plane](https://os.agno.com) that connects directly to your runtime from your browser. Monitor sessions. Debug with full traces. Manage users and permissions.

<Frame>
  <video autoPlay muted loop playsInline controls style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-agent-chat.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=26712acdfbce08e725b75f6618f925c8" type="video/mp4" data-path="videos/agentos-agent-chat.mp4" />
  </video>
</Frame>

## Private by Design

Most AI tooling stores your data on their servers. You pay retention costs, deal with egress fees, and depend on their security.

AgentOS runs entirely in your infrastructure:

* **Your database**: Sessions, memory, knowledge, traces. All stored where you control it.
* **Zero transmission**: No conversations, logs, or metrics sent to Agno.
* **Nothing stored on our end**: The control plane reads from your database, displays in your browser, stores nothing. When you close the tab, there's no trace of your data anywhere but your own systems.

See [AgentOS Security](/agent-os/security) for more details.

<Frame>
  <img src="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=b13db5d4b3c25eb5508752f7d3474b51" alt="AgentOS Security and Privacy Architecture" style={{ borderRadius: "0.5rem" }} data-og-width="3258" width="3258" data-og-height="1938" height="1938" data-path="images/agentos-secure-infra-illustration.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=280&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=c548641b352030a8fee914cd49919417 280w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=560&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=9640bb14a9d22619973e7efb20ab1be5 560w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=840&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=82645dfaae8f0155bc3912cdfaf656cc 840w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=1100&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=ba5cf9921c1b389d58216ba71ef38515 1100w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=1650&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=d7ca28c6e75259c18b08783224c1a2e4 1650w, https://mintcdn.com/agno-v2/Is_2Bv3MNVYdZh1v/images/agentos-secure-infra-illustration.png?w=2500&fit=max&auto=format&n=Is_2Bv3MNVYdZh1v&q=85&s=122528a3dc3ecf7789fb1b076be48f08 2500w" />
</Frame>

## Architecture

Your AgentOS runs as a container in your cloud. The control plane connects directly from your browser. No proxy servers, no data relay.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=f43be65c03f2748f0ff92d3364320710" alt="AgentOS Architecture" data-og-width="2457" width="2457" data-og-height="2670" height="2670" data-path="images/agent-os/agentos-architecture-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=280&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=3c3b34f5715a58a03cd418fca5c9d61d 280w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=560&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=dddec0a884981a4bbe38df78bb56f290 560w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=840&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=9a36a1d01fe9c99ee72fd6800db5dd4a 840w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=1100&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=5fa9f78d2d2d3916618f21f247359f99 1100w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=1650&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=fa14e46ffc87ec61a324e271cce902f7 1650w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-light.png?w=2500&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=fa2599183cd388f9ae9f5530287a696c 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=3d18950e38a502536c29b8ed8ccf5167" alt="AgentOS Architecture" data-og-width="2457" width="2457" data-og-height="2670" height="2670" data-path="images/agent-os/agentos-architecture-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=280&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=d10c6ceba4910b2501d00b50c54c1cb0 280w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=560&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=57f6af8eeb3b95f3379fda459adbcb9b 560w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=840&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=5f1b8690c72839a7482301c9cb3d5fbb 840w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=1100&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=db57cea0efc161a7299ef01a15d9dfce 1100w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=1650&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=63619b386d33e39880d3fb573d695ee8 1650w, https://mintcdn.com/agno-v2/c_Z_N0EWC5Kqg1t4/images/agent-os/agentos-architecture-dark.png?w=2500&fit=max&auto=format&n=c_Z_N0EWC5Kqg1t4&q=85&s=bf05a1453481dac2f1f8199383390b41 2500w" />

## Get Started

<CardGroup cols={2}>
  <Card title="Run Your First AgentOS" icon="plus" href="/agent-os/run-your-os">
    Create and run your first AgentOS
  </Card>

  <Card title="Connect Your AgentOS" icon="link" href="/agent-os/connect-your-os">
    Connect your AgentOS to the UI
  </Card>

  <Card title="Control Plane" icon="desktop" href="/agent-os/control-plane">
    Monitor and manage your AgentOS
  </Card>

  <Card title="Overview" icon="book" href="/agent-os/overview">
    Learn more about AgentOS
  </Card>
</CardGroup>
