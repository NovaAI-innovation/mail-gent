# What are Teams?

**Source:** https://docs.agno.com/teams/overview.md
**Section:** Docs

**Description:** Groups of agents that collaborate to solve complex tasks.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# What are Teams?

> Groups of agents that collaborate to solve complex tasks.

A Team is a collection of agents (or sub-teams) that work together. The team leader delegates tasks to members based on their roles.

<img className="block dark:hidden" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=0bbb6a84e04b9201746b0ff3495243e3" alt="Team structure" data-og-width="2610" width="2610" data-og-height="1413" height="1413" data-path="images/teams/team-structure-light.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=d9ca1e24c2099dffd88f2578e270dfa3 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=2a02ea12563bb86e4abb675612f9798a 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=638794030f685b82d26b434bb29e965f 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=6af9acfb6c2a82818deb979daee38365 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=5b3eaa00ec569867483b304a98d6be0d 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-light.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=5a153a9a9cd31794ab9f53a82324537f 2500w" />

<img className="hidden dark:block" src="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c4a60d21db7ffcd568b1d40c6eeb6866" alt="Team structure" data-og-width="2610" width="2610" data-og-height="1413" height="1413" data-path="images/teams/team-structure-dark.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=280&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=c44983dd9d8421469118ab7754a31852 280w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=560&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=6737f538162e1f95fffc78f71de32ae4 560w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=840&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=53c06595fc0177b71e828771431ff9c7 840w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=1100&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=7874c16f789718d6dd7333d40bf36290 1100w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=1650&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=d83b756d8d1effc8825882a5f39ce86f 1650w, https://mintcdn.com/agno-v2/i4nXCaAsJR5zgHQd/images/teams/team-structure-dark.png?w=2500&fit=max&auto=format&n=i4nXCaAsJR5zgHQd&q=85&s=08ae74854289473571437318aee88b55 2500w" />

```python  theme={null}
from agno.team import Team
from agno.agent import Agent

team = Team(members=[
    Agent(name="English Agent", role="You answer questions in English"),
    Agent(name="Chinese Agent", role="You answer questions in Chinese"),
    Team(
        name="Germanic Team",
        role="You coordinate the team members to answer questions in German and Dutch",
        members=[
            Agent(name="German Agent", role="You answer questions in German"),
            Agent(name="Dutch Agent", role="You answer questions in Dutch"),
        ],
    ),
])
```

## Why Teams?

Single agents hit limits fast. Context windows fill up, decision-making gets muddy, debugging becomes impossible.

Teams distribute work across specialized agents:

| Benefit             | Description                                                           |
| ------------------- | --------------------------------------------------------------------- |
| Specialization      | Each agent masters one domain instead of being mediocre at everything |
| Parallel processing | Multiple agents work simultaneously on independent subtasks           |
| Maintainability     | When something breaks, you know exactly which agent to fix            |
| Scalability         | Add capabilities by adding agents, not rewriting everything           |

The tradeoff: coordination overhead. Agents need to communicate and share state. Get this wrong and you've built a more expensive failure mode.

## When to Use Teams

**Use a team when:**

* A task requires multiple specialized agents with different tools or expertise
* A single agent's context window gets exceeded
* You want each agent focused on a narrow scope

**Use a single agent when:**

* The task fits one domain of expertise
* Minimizing token costs matters
* You're not sure yet (start simple, add agents when you hit limits)

## Team Patterns

| Pattern        | Configuration                                                | Use case                                       |
| -------------- | ------------------------------------------------------------ | ---------------------------------------------- |
| **Supervisor** | Default                                                      | Task decomposition, quality control, synthesis |
| **Router**     | `respond_directly=True`, `determine_input_for_members=False` | Route to specialists without synthesis         |
| **Broadcast**  | `delegate_to_all_members=True`                               | Parallel research, multiple perspectives       |

See [Delegation](/teams/delegation) for details.

## Guides

<CardGroup cols={3}>
  <Card title="Build Teams" icon="wrench" iconType="duotone" href="/teams/building-teams">
    Define members, roles, and structure.
  </Card>

  <Card title="Run Teams" icon="user-robot" iconType="duotone" href="/teams/running-teams">
    Execute teams and handle responses.
  </Card>

  <Card title="Debug Teams" icon="bug" iconType="duotone" href="/teams/debugging-teams">
    Inspect and troubleshoot team behavior.
  </Card>
</CardGroup>

## Resources

* [Examples](/cookbook/teams/overview)
* [Reference](/reference/teams/team)
