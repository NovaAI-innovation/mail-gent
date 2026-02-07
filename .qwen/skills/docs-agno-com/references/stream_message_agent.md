# Stream Message Agent

**Source:** https://docs.agno.com/reference-api/schema/a2a/stream-message-agent.md
**Section:** Docs

**Description:** Stream a message to an Agno Agent (streaming). The Agent is identified via the path parameter '{id}'. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata. Returns real-time updates as newline-delimited JSON (NDJSON).

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Stream Message Agent

> Stream a message to an Agno Agent (streaming). The Agent is identified via the path parameter '{id}'. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata. Returns real-time updates as newline-delimited JSON (NDJSON).



## OpenAPI

````yaml post /a2a/agents/{id}/v1/message:stream
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /a2a/agents/{id}/v1/message:stream:
    post:
      tags:
        - A2A
      summary: Stream Message Agent
      description: >-
        Stream a message to an Agno Agent (streaming). The Agent is identified
        via the path parameter '{id}'. Optional: Pass user ID via X-User-ID
        header (recommended) or 'userId' in params.message.metadata. Returns
        real-time updates as newline-delimited JSON (NDJSON).
      operationId: stream_message_agent
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            title: Id
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
          description: Invalid request
        '404':
          description: Agent not found
        '422':
          description: Validation Error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/HTTPValidationError'
components:
  schemas:
    HTTPValidationError:
      properties:
        detail:
          items:
            $ref: '#/components/schemas/ValidationError'
          type: array
          title: Detail
      type: object
      title: HTTPValidationError
    ValidationError:
      properties:
        loc:
          items:
            anyOf:
              - type: string
              - type: integer
          type: array
          title: Location
        msg:
          type: string
          title: Message
        type:
          type: string
          title: Error Type
      type: object
      required:
        - loc
        - msg
        - type
      title: ValidationError

````