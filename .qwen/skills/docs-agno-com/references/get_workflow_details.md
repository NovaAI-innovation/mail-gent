# Get Workflow Details

**Source:** https://docs.agno.com/reference-api/schema/workflows/get-workflow-details.md
**Section:** Docs

**Description:** Retrieve detailed configuration and step information for a specific workflow.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Workflow Details

> Retrieve detailed configuration and step information for a specific workflow.



## OpenAPI

````yaml get /workflows/{workflow_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /workflows/{workflow_id}:
    get:
      tags:
        - Workflows
      summary: Get Workflow Details
      description: >-
        Retrieve detailed configuration and step information for a specific
        workflow.
      operationId: get_workflow
      parameters:
        - name: workflow_id
          in: path
          required: true
          schema:
            type: string
            title: Workflow Id
      responses:
        '200':
          description: Workflow details retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/WorkflowResponse'
              example:
                id: content-creation-workflow
                name: Content Creation Workflow
                description: Automated content creation from blog posts to social media
                db_id: '123'
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
          description: Workflow not found
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
    WorkflowResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
          description: Unique identifier for the workflow
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the workflow
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: Database identifier
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the workflow
        input_schema:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Input Schema
          description: Input schema for the workflow
        steps:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Steps
          description: List of workflow steps
        agent:
          anyOf:
            - $ref: '#/components/schemas/AgentResponse'
            - type: 'null'
          description: Agent configuration if used
        team:
          anyOf:
            - $ref: '#/components/schemas/TeamResponse'
            - type: 'null'
          description: Team configuration if used
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata
        workflow_agent:
          type: boolean
          title: Workflow Agent
          description: Whether this workflow uses a WorkflowAgent
          default: false
      type: object
      title: WorkflowResponse
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