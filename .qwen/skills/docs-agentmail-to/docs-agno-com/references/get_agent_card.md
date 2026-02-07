# Get Agent Card

**Source:** https://docs.agno.com/reference-api/schema/a2a/get-agent-card.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Agent Card



## OpenAPI

````yaml get /a2a/agents/{id}/.well-known/agent-card.json
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /a2a/agents/{id}/.well-known/agent-card.json:
    get:
      tags:
        - A2A
      summary: Get Agent Card
      operationId: get_agent_card_a2a_agents__id___well_known_agent_card_json_get
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
            title: Id
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}
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