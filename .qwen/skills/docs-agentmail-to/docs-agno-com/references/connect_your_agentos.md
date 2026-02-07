# Connect Your AgentOS

**Source:** https://docs.agno.com/agent-os/connect-your-os.md
**Section:** Docs

**Description:** Connect your AgentOS to the control plane for monitoring and management.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Connect Your AgentOS

> Connect your AgentOS to the control plane for monitoring and management.

## Connect Your AgentOS

1. Open [os.agno.com](https://os.agno.com) and sign in
2. Click **"Add new OS"**

<Frame>
  <video autoPlay muted loop playsInline controls style={{ borderRadius: "0.5rem", width: "100%", height: "auto" }}>
    <source src="https://mintcdn.com/agno-v2/Ug_UAH9jtxYdgRC4/videos/agent-os-connect-os.mp4?fit=max&auto=format&n=Ug_UAH9jtxYdgRC4&q=85&s=b8c1a9ae5f1c8380f6aeff833493c9eb" type="video/mp4" data-path="videos/agent-os-connect-os.mp4" />
  </video>
</Frame>

## Configure Connection

| Field            | Description                                              |
| ---------------- | -------------------------------------------------------- |
| **Environment**  | Local (`http://localhost:8000`) or Live (your HTTPS URL) |
| **Endpoint URL** | Where your AgentOS is running                            |
| **OS Name**      | A descriptive name, e.g. "Development OS"                |
| **Tags**         | Optional. Organize with labels like `dev`, `stg`, `prd`  |

Click **"CONNECT"**. If successful, your OS appears in the dashboard.

## Verify Connection

| Indicator | Expected                                       |
| --------- | ---------------------------------------------- |
| Status    | "Running"                                      |
| Features  | Chat, Knowledge, Memory, Sessions accessible   |
| Agents    | Configured agents appear in the chat interface |
