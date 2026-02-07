# AgentOS Control Plane

**Source:** https://docs.agno.com/agent-os/control-plane.md
**Section:** Docs

**Description:** A web interface for testing, monitoring, and managing your multi-agent system.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# AgentOS Control Plane

> A web interface for testing, monitoring, and managing your multi-agent system.

The control plane is where you chat with agents, view traces, manage knowledge, track sessions, and monitor performance.

<Frame>
  <img src="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=34b84b1f2871d4fa922400f3d501289a" alt="AgentOS Control Plane Dashboard" style={{ borderRadius: "0.5rem" }} data-og-width="3448" width="3448" data-og-height="1986" height="1986" data-path="images/agentos-full-screenshot.png" data-optimize="true" data-opv="3" srcset="https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=280&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=3993b3b083c75893dfcb76f9256b1326 280w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=560&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=40010697aa349249a4afb941a1fe8199 560w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=840&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=31001298552fd8b06b684679478790fd 840w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=1100&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=4c22bd89a17d4c16c8d256be4ebf7de5 1100w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=1650&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=65143b02ef4e3f1c9ea25d6952527476 1650w, https://mintcdn.com/agno-v2/tBgqL1LeYUKpZTuS/images/agentos-full-screenshot.png?w=2500&fit=max&auto=format&n=tBgqL1LeYUKpZTuS&q=85&s=88d82e38cb1f205e5b41e102b568d29b 2500w" />
</Frame>

<Tip>
  It connects directly from your browser to your AgentOS runtime. No data is sent to Agno.
</Tip>

## Chat Interface

Chat with agents, collaborate with teams, and run workflows from one screen.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-chat.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=e8aedec10c87f6395efabd0779d96e7d" type="video/mp4" data-path="videos/agentos-chat.mp4" />
  </video>
</Frame>

### Agents

Select an agent from the right panel and start a conversation. Each agent maintains its own history, tools, and instructions. Switching agents won't mix contexts.

### Teams

Switch the toggle to Teams. Use the chat stream to watch how the team divides and solves the task.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-teams-chat.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=f2b735935b10d29a44b42cdc8df3e303" type="video/mp4" data-path="videos/agentos-teams-chat.mp4" />
  </video>
</Frame>

### Workflows

Switch to Workflows. Provide input (plain text or structured, depending on the workflow) and watch execution live as steps stream, produce output, and finish.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-workflows-chat.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=5b789c65083ea5ab933641499ba876ac" type="video/mp4" data-path="videos/agentos-workflows-chat.mp4" />
  </video>
</Frame>

## Tracing

Traces capture the complete execution flow of agents and teams. Each trace contains spans representing individual operations (LLM calls, tool executions, etc.) with token usage, latency, and error information.

### Tree View

Displays spans in a hierarchical structure showing parent-child relationships between operations. Useful for understanding how teams delegate to agents and how agents invoke tools.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/trace-tree.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=41802e996d1e1f3f211268bc7202e83a" type="video/mp4" data-path="videos/trace-tree.mp4" />
  </video>
</Frame>

### Waterfall View

Visualizes spans on a time axis showing when each operation started, how long it took, and which operations ran in parallel. Helps identify bottlenecks and optimize performance.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/traces-timeline-view.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=3b84b3cdb021a4a75abc2853f4e89aae" type="video/mp4" data-path="videos/traces-timeline-view.mp4" />
  </video>
</Frame>

## Session Tracking

Sessions group related runs under a single `session_id`. Each session captures messages, tool calls, metrics, and summaries for a single conversation. Sessions are stored in your database and can be queried and managed from the control plane.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-session-management.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=b267c3a4e943dc115e18459806df5ca4" type="video/mp4" data-path="videos/agentos-session-management.mp4" />
  </video>
</Frame>

## Knowledge

Knowledge bases provide agents with domain-specific information through RAG (Retrieval-Augmented Generation). Manage multiple knowledge bases, add content from URLs, files, or text, and monitor embedding status. Each knowledge base stores documents, chunks them, generates embeddings, and makes them searchable for agents.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-knowledge.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=5537ad713cf54f943f150b589bf9d3ba" type="video/mp4" data-path="videos/agentos-knowledge.mp4" />
  </video>
</Frame>

## Memories

Memories store information that agents learn about users across conversations. Each memory is tied to a user ID and contains content, topics, timestamps, and the input that generated it. You can view, create, edit, or delete memories from the control plane.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/memory-table-usage.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=49a1a912d1f8891b1de4c01b05714669" type="video/mp4" data-path="videos/memory-table-usage.mp4" />
  </video>
</Frame>

## Managing Your AgentOS

Connect and inspect your AgentOS runtimes from a single interface. Switch between local development and production instances and monitor connection health.

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-select-os.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=42354ecc2e4d22c8d8833a4bbf7802b3" type="video/mp4" data-path="videos/agentos-select-os.mp4" />
  </video>
</Frame>

## User Management

Invite team members by entering their email addresses. Separate multiple emails with commas or press Enter/Tab between addresses.

| Role       | Access                                                             |
| ---------- | ------------------------------------------------------------------ |
| **Owner**  | Full administrative access including billing and member management |
| **Member** | Access to AgentOS features and collaboration                       |

<Frame>
  <video autoPlay muted loop playsInline style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/BGdFF6H0EnnnI92k/videos/agentos-invite-member.mp4?fit=max&auto=format&n=BGdFF6H0EnnnI92k&q=85&s=287f70aec11e01946bf7d2d1eaaef275" type="video/mp4" data-path="videos/agentos-invite-member.mp4" />
  </video>
</Frame>
