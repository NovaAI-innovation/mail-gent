# Chat History

**Source:** https://docs.agno.com/history/overview.md
**Section:** Docs

**Description:** Persist and access conversation history for multi-turn interactions.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Chat History

> Persist and access conversation history for multi-turn interactions.

Chat History enables your agents, teams, and workflows to remember and reference previous conversations, creating intelligent and context-aware interactions.

Instead of starting fresh with each interaction, Chat History allows you to:

* **Maintain conversation continuity** - Build on previous exchanges within a session
* **Provide personalized responses** - Reference past interactions to tailor outputs
* **Avoid repetitive questions** - Access previously provided information
* **Enable long-running conversations** - Support multi-turn dialogues with persistent memory

<Note>
  All history features require a database configured on your agent, team, or workflow. See [Database](/database/overview) for setup details.
</Note>

## Learn more

<CardGroup cols={3}>
  <Card title="Chat History in Agents" icon="robot" iconType="duotone" href="/history/agent/overview">
    Configure history storage and retrieval for agents.
  </Card>

  <Card title="Chat History in Teams" icon="users" iconType="duotone" href="/history/team/overview">
    Share conversation context across team members.
  </Card>

  <Card title="Chat History in Workflows" icon="diagram-project" iconType="duotone" href="/history/workflow/overview">
    Enable history for workflow steps.
  </Card>
</CardGroup>
