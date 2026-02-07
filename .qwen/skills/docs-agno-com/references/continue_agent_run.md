# Continue Agent Run

**Source:** https://docs.agno.com/reference-api/schema/agents/continue-agent-run.md
**Section:** Docs

**Description:** Continue a paused or incomplete agent run with updated tool results.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Continue Agent Run

> Continue a paused or incomplete agent run with updated tool results.

**Use Cases:**
- Resume execution after tool approval/rejection
- Provide manual tool execution results

**Tools Parameter:**
JSON string containing array of tool execution objects with results.



## OpenAPI

````yaml post /agents/{agent_id}/runs/{run_id}/continue
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /agents/{agent_id}/runs/{run_id}/continue:
    post:
      tags:
        - Agents
      summary: Continue Agent Run
      description: |-
        Continue a paused or incomplete agent run with updated tool results.

        **Use Cases:**
        - Resume execution after tool approval/rejection
        - Provide manual tool execution results

        **Tools Parameter:**
        JSON string containing array of tool execution objects with results.
      operationId: continue_agent_run
      parameters:
        - name: agent_id
          in: path
          required: true
          schema:
            type: string
            title: Agent Id
        - name: run_id
          in: path
          required: true
          schema:
            type: string
            title: Run Id
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              $ref: '#/components/schemas/Body_continue_agent_run'
      responses:
        '200':
          description: Agent run continued successfully
          content:
            application/json:
              schema: {}
            text/event-stream:
              example: |+
                event: RunContent
                data: {"created_at": 1757348314, "run_id": "123..."}

        '400':
          description: Invalid JSON in tools field or invalid tool structure
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/BadRequestResponse'
        '401':
          description: Unauthorized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UnauthenticatedResponse'
        '404':
          description: Agent not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/NotFoundResponse'
        '422':
          description: Validation Error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '500':
          description: Internal Server Error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    Body_continue_agent_run:
      properties:
        tools:
          type: string
          title: Tools
        session_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Id
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
        stream:
          type: boolean
          title: Stream
          default: true
      type: object
      required:
        - tools
      title: Body_continue_agent_run
    BadRequestResponse:
      properties:
        detail:
          type: string
          title: Detail
          description: Error detail message
        error_code:
          anyOf:
            - type: string
            - type: 'null'
          title: Error Code
          description: Error code for categorization
      type: object
      required:
        - detail
      title: BadRequestResponse
      example:
        detail: Bad request
        error_code: BAD_REQUEST
    UnauthenticatedResponse:
      properties:
        detail:
          type: string
          title: Detail
          description: Error detail message
        error_code:
          anyOf:
            - type: string
            - type: 'null'
          title: Error Code
          description: Error code for categorization
      type: object
      required:
        - detail
      title: UnauthenticatedResponse
      example:
        detail: Unauthenticated access
        error_code: UNAUTHENTICATED
    NotFoundResponse:
      properties:
        detail:
          type: string
          title: Detail
          description: Error detail message
        error_code:
          anyOf:
            - type: string
            - type: 'null'
          title: Error Code
          description: Error code for categorization
      type: object
      required:
        - detail
      title: NotFoundResponse
      example:
        detail: Not found
        error_code: NOT_FOUND
    ValidationErrorResponse:
      properties:
        detail:
          type: string
          title: Detail
          description: Error detail message
        error_code:
          anyOf:
            - type: string
            - type: 'null'
          title: Error Code
          description: Error code for categorization
      type: object
      required:
        - detail
      title: ValidationErrorResponse
      example:
        detail: Validation error
        error_code: VALIDATION_ERROR
    InternalServerErrorResponse:
      properties:
        detail:
          type: string
          title: Detail
          description: Error detail message
        error_code:
          anyOf:
            - type: string
            - type: 'null'
          title: Error Code
          description: Error code for categorization
      type: object
      required:
        - detail
      title: InternalServerErrorResponse
      example:
        detail: Internal server error
        error_code: INTERNAL_SERVER_ERROR
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````