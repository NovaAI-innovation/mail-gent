# List Evaluation Runs

**Source:** https://docs.agno.com/reference-api/schema/evals/list-evaluation-runs.md
**Section:** Docs

**Description:** Retrieve paginated evaluation runs with filtering and sorting options. Filter by agent, team, workflow, model, or evaluation type.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Evaluation Runs

> Retrieve paginated evaluation runs with filtering and sorting options. Filter by agent, team, workflow, model, or evaluation type.



## OpenAPI

````yaml get /eval-runs
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /eval-runs:
    get:
      tags:
        - Evals
      summary: List Evaluation Runs
      description: >-
        Retrieve paginated evaluation runs with filtering and sorting options.
        Filter by agent, team, workflow, model, or evaluation type.
      operationId: get_eval_runs
      parameters:
        - name: agent_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Agent ID
            title: Agent Id
          description: Agent ID
        - name: team_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Team ID
            title: Team Id
          description: Team ID
        - name: workflow_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Workflow ID
            title: Workflow Id
          description: Workflow ID
        - name: model_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Model ID
            title: Model Id
          description: Model ID
        - name: type
          in: query
          required: false
          schema:
            anyOf:
              - $ref: '#/components/schemas/EvalFilterType'
              - type: 'null'
            description: Filter type
            title: Type
          description: Filter type
        - name: limit
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Number of eval runs to return
            default: 20
            title: Limit
          description: Number of eval runs to return
        - name: page
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Page number
            default: 1
            title: Page
          description: Page number
        - name: sort_by
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Field to sort by
            default: created_at
            title: Sort By
          description: Field to sort by
        - name: sort_order
          in: query
          required: false
          schema:
            anyOf:
              - $ref: '#/components/schemas/SortOrder'
              - type: 'null'
            description: Sort order (asc or desc)
            default: desc
            title: Sort Order
          description: Sort order (asc or desc)
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: The ID of the database to use
            title: Db Id
          description: The ID of the database to use
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: The database table to use
            title: Table
          description: The database table to use
        - name: eval_types
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: >-
              Comma-separated eval types
              (accuracy,agent_as_judge,performance,reliability)
            examples:
              - accuracy,agent_as_judge,performance,reliability
            title: Eval Types
          description: >-
            Comma-separated eval types
            (accuracy,agent_as_judge,performance,reliability)
      responses:
        '200':
          description: Evaluation runs retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_EvalSchema_'
              example:
                data:
                  - id: a03fa2f4-900d-482d-afe0-470d4cd8d1f4
                    agent_id: basic-agent
                    model_id: gpt-4o
                    model_provider: OpenAI
                    name: 'Test '
                    eval_type: reliability
                    eval_data:
                      eval_status: PASSED
                      failed_tool_calls: []
                      passed_tool_calls:
                        - multiply
                    eval_input:
                      expected_tool_calls:
                        - multiply
                    created_at: '2025-08-27T15:41:59Z'
                    updated_at: '2025-08-27T15:41:59Z'
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
    EvalFilterType:
      type: string
      enum:
        - agent
        - team
        - workflow
      title: EvalFilterType
    SortOrder:
      type: string
      enum:
        - asc
        - desc
      title: SortOrder
    PaginatedResponse_EvalSchema_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/EvalSchema'
          type: array
          title: Data
          description: List of items for the current page
        meta:
          $ref: '#/components/schemas/PaginationInfo'
          description: Pagination metadata
      type: object
      required:
        - data
        - meta
      title: PaginatedResponse[EvalSchema]
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
    EvalSchema:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the evaluation run
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID that was evaluated
        model_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Model Id
          description: Model ID used in evaluation
        model_provider:
          anyOf:
            - type: string
            - type: 'null'
          title: Model Provider
          description: Model provider name
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID that was evaluated
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Workflow ID that was evaluated
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the evaluation run
        evaluated_component_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Evaluated Component Name
          description: Name of the evaluated component
        eval_type:
          $ref: '#/components/schemas/EvalType'
          description: Type of evaluation (accuracy, performance, or reliability)
        eval_data:
          additionalProperties: true
          type: object
          title: Eval Data
          description: Evaluation results and metrics
        eval_input:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Eval Input
          description: Input parameters used for the evaluation
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Timestamp when evaluation was created
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Timestamp when evaluation was last updated
      type: object
      required:
        - id
        - eval_type
        - eval_data
      title: EvalSchema
    PaginationInfo:
      properties:
        page:
          type: integer
          minimum: 0
          title: Page
          description: Current page number (0-indexed)
          default: 0
        limit:
          type: integer
          maximum: 100
          minimum: 1
          title: Limit
          description: Number of items per page
          default: 20
        total_pages:
          type: integer
          minimum: 0
          title: Total Pages
          description: Total number of pages
          default: 0
        total_count:
          type: integer
          minimum: 0
          title: Total Count
          description: Total count of items
          default: 0
        search_time_ms:
          type: number
          minimum: 0
          title: Search Time Ms
          description: Search execution time in milliseconds
          default: 0
      type: object
      title: PaginationInfo
    EvalType:
      type: string
      enum:
        - accuracy
        - agent_as_judge
        - performance
        - reliability
      title: EvalType
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````