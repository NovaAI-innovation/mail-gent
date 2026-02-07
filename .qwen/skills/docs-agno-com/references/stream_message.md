# Stream Message

**Source:** https://docs.agno.com/reference-api/schema/a2a/stream-message.md
**Section:** Docs

**Description:** [DEPRECATED] Stream a message to an Agno Agent, Team, or Workflow. The Agent, Team or Workflow is identified via the 'agentId' field in params.message or X-Agent-ID header. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata. Returns real-time updates as newline-delimited JSON (NDJSON).

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Stream Message

> [DEPRECATED] Stream a message to an Agno Agent, Team, or Workflow. The Agent, Team or Workflow is identified via the 'agentId' field in params.message or X-Agent-ID header. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata. Returns real-time updates as newline-delimited JSON (NDJSON).



## OpenAPI

````yaml post /a2a/message/stream
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /a2a/message/stream:
    post:
      tags:
        - A2A
      summary: Stream Message
      description: >-
        [DEPRECATED] Stream a message to an Agno Agent, Team, or Workflow. The
        Agent, Team or Workflow is identified via the 'agentId' field in
        params.message or X-Agent-ID header. Optional: Pass user ID via
        X-User-ID header (recommended) or 'userId' in params.message.metadata.
        Returns real-time updates as newline-delimited JSON (NDJSON).
      operationId: stream_message
      responses:
        '200':
          description: Streaming response with task updates
          content:
            application/json:
              schema: {}
            text/event-stream:
              example: >+
                event: TaskStatusUpdateEvent

                data:
                {"jsonrpc":"2.0","id":"request-123","result":{"taskId":"task-456","status":"working"}}


                event: Message

                data:
                {"jsonrpc":"2.0","id":"request-123","result":{"messageId":"msg-1","role":"agent","parts":[{"kind":"text","text":"Response"}]}}

        '400':
          description: Invalid request or unsupported method
        '404':
          description: Agent, Team, or Workflow not found

````