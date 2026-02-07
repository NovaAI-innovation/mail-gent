# List All Workflows

**Source:** https://docs.agno.com/reference-api/schema/workflows/list-all-workflows.md
**Section:** Docs

**Description:** Retrieve a comprehensive list of all workflows configured in this OS instance.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List All Workflows

> Retrieve a comprehensive list of all workflows configured in this OS instance.

**Return Information:**
- Workflow metadata (ID, name, description)
- Input schema requirements
- Step sequence and execution flow
- Associated agents and teams



## OpenAPI

````yaml get /workflows
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /workflows:
    get:
      tags:
        - Workflows
      summary: List All Workflows
      description: >-
        Retrieve a comprehensive list of all workflows configured in this OS
        instance.


        **Return Information:**

        - Workflow metadata (ID, name, description)

        - Input schema requirements

        - Step sequence and execution flow

        - Associated agents and teams
      operationId: get_workflows
      responses:
        '200':
          description: List of workflows retrieved successfully
          content:
            application/json:
              schema:
                items:
                  $ref: '#/components/schemas/WorkflowSummaryResponse'
                type: array
                title: Response Get Workflows
              example:
                - id: content-creation-workflow
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
          description: Not Found
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
    WorkflowSummaryResponse:
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
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the workflow
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: Database identifier
      type: object
      title: WorkflowSummaryResponse
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