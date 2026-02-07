# Get Team Details

**Source:** https://docs.agno.com/reference-api/schema/teams/get-team-details.md
**Section:** Docs

**Description:** Retrieve detailed configuration and member information for a specific team.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Team Details

> Retrieve detailed configuration and member information for a specific team.



## OpenAPI

````yaml get /teams/{team_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /teams/{team_id}:
    get:
      tags:
        - Teams
      summary: Get Team Details
      description: >-
        Retrieve detailed configuration and member information for a specific
        team.
      operationId: get_team
      parameters:
        - name: team_id
          in: path
          required: true
          schema:
            type: string
            title: Team Id
      responses:
        '200':
          description: Team details retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/TeamResponse'
              example:
                team_id: basic-team
                name: Basic Team
                mode: coordinate
                model:
                  name: OpenAIChat
                  model: gpt-4o
                  provider: OpenAI
                tools:
                  - name: transfer_task_to_member
                    description: >-
                      Use this function to transfer a task to the selected team
                      member.

                      You must provide a clear and concise description of the
                      task the member should achieve AND the expected output.
                    parameters:
                      type: object
                      properties:
                        member_id:
                          type: string
                          description: >-
                            (str) The ID of the member to transfer the task to.
                            Use only the ID of the member, not the ID of the
                            team followed by the ID of the member.
                        task_description:
                          type: string
                          description: >-
                            (str) A clear and concise description of the task
                            the member should achieve.
                        expected_output:
                          type: string
                          description: >-
                            (str) The expected output from the member
                            (optional).
                      additionalProperties: false
                      required:
                        - member_id
                        - task_description
                members:
                  - agent_id: basic-agent
                    name: Basic Agent
                    model:
                      name: OpenAIChat
                      model: gpt-4o
                      provider: OpenAI gpt-4o
                    memory:
                      app_name: Memory
                      model:
                        name: OpenAIChat
                        model: gpt-4o
                        provider: OpenAI
                    session_table: agno_sessions
                    memory_table: agno_memories
                enable_agentic_context: false
                memory:
                  app_name: Memory
                  model:
                    name: OpenAIChat
                    model: gpt-4o
                    provider: OpenAI
                async_mode: false
                session_table: agno_sessions
                memory_table: agno_memories
        '400':
          description: Bad Request
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
          description: Team not found
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
    TeamResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
        model:
          anyOf:
            - $ref: '#/components/schemas/ModelResponse'
            - type: 'null'
        tools:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Tools
        sessions:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Sessions
        knowledge:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Knowledge
        memory:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Memory
        reasoning:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Reasoning
        default_tools:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Default Tools
        system_message:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: System Message
        response_settings:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Response Settings
        introduction:
          anyOf:
            - type: string
            - type: 'null'
          title: Introduction
        streaming:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Streaming
        members:
          anyOf:
            - items:
                anyOf:
                  - $ref: '#/components/schemas/AgentResponse'
                  - $ref: '#/components/schemas/TeamResponse'
              type: array
            - type: 'null'
          title: Members
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        input_schema:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Input Schema
      type: object
      title: TeamResponse
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
    ModelResponse:
      properties:
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the model
        model:
          anyOf:
            - type: string
            - type: 'null'
          title: Model
          description: Model identifier
        provider:
          anyOf:
            - type: string
            - type: 'null'
          title: Provider
          description: Model provider name
      type: object
      title: ModelResponse
    AgentResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
        model:
          anyOf:
            - $ref: '#/components/schemas/ModelResponse'
            - type: 'null'
        tools:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Tools
        sessions:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Sessions
        knowledge:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Knowledge
        memory:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Memory
        reasoning:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Reasoning
        default_tools:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Default Tools
        system_message:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: System Message
        extra_messages:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Extra Messages
        response_settings:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Response Settings
        introduction:
          anyOf:
            - type: string
            - type: 'null'
          title: Introduction
        streaming:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Streaming
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        input_schema:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Input Schema
      type: object
      title: AgentResponse
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````