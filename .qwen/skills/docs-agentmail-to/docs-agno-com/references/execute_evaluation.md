# Execute Evaluation

**Source:** https://docs.agno.com/reference-api/schema/evals/execute-evaluation.md
**Section:** Docs

**Description:** Run evaluation tests on agents or teams. Supports accuracy, agent-as-judge, performance, and reliability evaluations. Requires either agent_id or team_id, but not both.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Execute Evaluation

> Run evaluation tests on agents or teams. Supports accuracy, agent-as-judge, performance, and reliability evaluations. Requires either agent_id or team_id, but not both.



## OpenAPI

````yaml post /eval-runs
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /eval-runs:
    post:
      tags:
        - Evals
      summary: Execute Evaluation
      description: >-
        Run evaluation tests on agents or teams. Supports accuracy,
        agent-as-judge, performance, and reliability evaluations. Requires
        either agent_id or team_id, but not both.
      operationId: run_eval
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for evaluation
            title: Db Id
          description: Database ID to use for evaluation
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to use for evaluation
            title: Table
          description: Table to use for evaluation
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/EvalRunInput'
      responses:
        '200':
          description: Evaluation executed successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/EvalSchema'
              example:
                id: f2b2d72f-e9e2-4f0e-8810-0a7e1ff58614
                agent_id: basic-agent
                model_id: gpt-4o
                model_provider: OpenAI
                eval_type: reliability
                eval_data:
                  eval_status: PASSED
                  failed_tool_calls: []
                  passed_tool_calls:
                    - multiply
                created_at: '2025-08-27T15:41:59Z'
                updated_at: '2025-08-27T15:41:59Z'
        '400':
          description: Invalid request - provide either agent_id or team_id
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
          description: Agent or team not found
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
    EvalRunInput:
      properties:
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID to evaluate
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID to evaluate
        model_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Model Id
          description: Model ID to use for evaluation
        model_provider:
          anyOf:
            - type: string
            - type: 'null'
          title: Model Provider
          description: Model provider name
        eval_type:
          $ref: '#/components/schemas/EvalType'
          description: Type of evaluation to run (accuracy, performance, or reliability)
        input:
          type: string
          minLength: 1
          title: Input
          description: Input text/query for the evaluation
        additional_guidelines:
          anyOf:
            - type: string
            - type: 'null'
          title: Additional Guidelines
          description: Additional guidelines for the evaluation
        additional_context:
          anyOf:
            - type: string
            - type: 'null'
          title: Additional Context
          description: Additional context for the evaluation
        num_iterations:
          type: integer
          maximum: 100
          minimum: 1
          title: Num Iterations
          description: Number of times to run the evaluation
          default: 1
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name for this evaluation run
        expected_output:
          anyOf:
            - type: string
            - type: 'null'
          title: Expected Output
          description: Expected output for accuracy evaluation
        criteria:
          anyOf:
            - type: string
            - type: 'null'
          title: Criteria
          description: Evaluation criteria for agent-as-judge evaluation
        scoring_strategy:
          anyOf:
            - type: string
              enum:
                - numeric
                - binary
            - type: 'null'
          title: Scoring Strategy
          description: >-
            Scoring strategy: 'numeric' (1-10 with threshold) or 'binary'
            (PASS/FAIL)
          default: binary
        threshold:
          anyOf:
            - type: integer
              maximum: 10
              minimum: 1
            - type: 'null'
          title: Threshold
          description: Score threshold for pass/fail (1-10), only used with numeric scoring
          default: 7
        warmup_runs:
          type: integer
          maximum: 10
          minimum: 0
          title: Warmup Runs
          description: Number of warmup runs before measuring performance
          default: 0
        expected_tool_calls:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Expected Tool Calls
          description: Expected tool calls for reliability evaluation
      type: object
      required:
        - eval_type
        - input
      title: EvalRunInput
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