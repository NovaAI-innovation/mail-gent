# Update Evaluation Run

**Source:** https://docs.agno.com/reference-api/schema/evals/update-evaluation-run.md
**Section:** Docs

**Description:** Update the name or other properties of an existing evaluation run.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Evaluation Run

> Update the name or other properties of an existing evaluation run.



## OpenAPI

````yaml patch /eval-runs/{eval_run_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /eval-runs/{eval_run_id}:
    patch:
      tags:
        - Evals
      summary: Update Evaluation Run
      description: Update the name or other properties of an existing evaluation run.
      operationId: update_eval_run
      parameters:
        - name: eval_run_id
          in: path
          required: true
          schema:
            type: string
            title: Eval Run Id
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
            description: Table to use for rename operation
            title: Table
          description: Table to use for rename operation
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UpdateEvalRunRequest'
      responses:
        '200':
          description: Evaluation run updated successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/EvalSchema'
              example:
                id: a03fa2f4-900d-482d-afe0-470d4cd8d1f4
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
          description: Evaluation run not found
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
          description: Failed to update evaluation run
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    UpdateEvalRunRequest:
      properties:
        name:
          type: string
          maxLength: 255
          minLength: 1
          title: Name
          description: New name for the evaluation run
      type: object
      required:
        - name
      title: UpdateEvalRunRequest
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