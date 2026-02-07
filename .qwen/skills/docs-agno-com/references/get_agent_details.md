# Get Agent Details

**Source:** https://docs.agno.com/reference-api/schema/agents/get-agent-details.md
**Section:** Docs

**Description:** Retrieve detailed configuration and capabilities of a specific agent.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Agent Details

> Retrieve detailed configuration and capabilities of a specific agent.

**Returns comprehensive agent information including:**
- Model configuration and provider details
- Complete tool inventory and configurations
- Session management settings
- Knowledge base and memory configurations
- Reasoning capabilities and settings
- System prompts and response formatting options



## OpenAPI

````yaml get /agents/{agent_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /agents/{agent_id}:
    get:
      tags:
        - Agents
      summary: Get Agent Details
      description: |-
        Retrieve detailed configuration and capabilities of a specific agent.

        **Returns comprehensive agent information including:**
        - Model configuration and provider details
        - Complete tool inventory and configurations
        - Session management settings
        - Knowledge base and memory configurations
        - Reasoning capabilities and settings
        - System prompts and response formatting options
      operationId: get_agent
      parameters:
        - name: agent_id
          in: path
          required: true
          schema:
            type: string
            title: Agent Id
      responses:
        '200':
          description: Agent details retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AgentResponse'
              example:
                id: main-agent
                name: Main Agent
                db_id: 9e064c70-6821-4840-a333-ce6230908a70
                model:
                  name: OpenAIChat
                  model: gpt-4o
                  provider: OpenAI
                sessions:
                  session_table: agno_sessions
                knowledge:
                  knowledge_table: main_knowledge
                system_message:
                  markdown: true
                  add_datetime_to_context: true
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
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````