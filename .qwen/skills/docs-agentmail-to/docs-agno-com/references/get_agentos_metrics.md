# Get AgentOS Metrics

**Source:** https://docs.agno.com/reference-api/schema/metrics/get-agentos-metrics.md
**Section:** Docs

**Description:** Retrieve AgentOS metrics and analytics data for a specified date range. If no date range is specified, returns all available metrics.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get AgentOS Metrics

> Retrieve AgentOS metrics and analytics data for a specified date range. If no date range is specified, returns all available metrics.



## OpenAPI

````yaml get /metrics
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /metrics:
    get:
      tags:
        - Metrics
      summary: Get AgentOS Metrics
      description: >-
        Retrieve AgentOS metrics and analytics data for a specified date range.
        If no date range is specified, returns all available metrics.
      operationId: get_metrics
      parameters:
        - name: starting_date
          in: query
          required: false
          schema:
            anyOf:
              - type: string
                format: date
              - type: 'null'
            description: Starting date for metrics range (YYYY-MM-DD format)
            title: Starting Date
          description: Starting date for metrics range (YYYY-MM-DD format)
        - name: ending_date
          in: query
          required: false
          schema:
            anyOf:
              - type: string
                format: date
              - type: 'null'
            description: Ending date for metrics range (YYYY-MM-DD format)
            title: Ending Date
          description: Ending date for metrics range (YYYY-MM-DD format)
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query metrics from
            title: Db Id
          description: Database ID to query metrics from
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
      responses:
        '200':
          description: Metrics retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/MetricsResponse'
              example:
                metrics:
                  - id: 7bf39658-a00a-484c-8a28-67fd8a9ddb2a
                    agent_runs_count: 5
                    agent_sessions_count: 5
                    team_runs_count: 0
                    team_sessions_count: 0
                    workflow_runs_count: 0
                    workflow_sessions_count: 0
                    users_count: 1
                    token_metrics:
                      input_tokens: 448
                      output_tokens: 148
                      total_tokens: 596
                      audio_tokens: 0
                      input_audio_tokens: 0
                      output_audio_tokens: 0
                      cached_tokens: 0
                      cache_write_tokens: 0
                      reasoning_tokens: 0
                    model_metrics:
                      - model_id: gpt-4o
                        model_provider: OpenAI
                        count: 5
                    date: '2025-07-31T00:00:00'
                    created_at: 1753993132
                    updated_at: 1753993741
        '400':
          description: Invalid date range parameters
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
          description: Failed to retrieve metrics
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    MetricsResponse:
      properties:
        metrics:
          items:
            $ref: '#/components/schemas/DayAggregatedMetrics'
          type: array
          title: Metrics
          description: List of daily aggregated metrics
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Timestamp of the most recent metrics update
      type: object
      required:
        - metrics
      title: MetricsResponse
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
    DayAggregatedMetrics:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the metrics record
        agent_runs_count:
          type: integer
          minimum: 0
          title: Agent Runs Count
          description: Total number of agent runs
        agent_sessions_count:
          type: integer
          minimum: 0
          title: Agent Sessions Count
          description: Total number of agent sessions
        team_runs_count:
          type: integer
          minimum: 0
          title: Team Runs Count
          description: Total number of team runs
        team_sessions_count:
          type: integer
          minimum: 0
          title: Team Sessions Count
          description: Total number of team sessions
        workflow_runs_count:
          type: integer
          minimum: 0
          title: Workflow Runs Count
          description: Total number of workflow runs
        workflow_sessions_count:
          type: integer
          minimum: 0
          title: Workflow Sessions Count
          description: Total number of workflow sessions
        users_count:
          type: integer
          minimum: 0
          title: Users Count
          description: Total number of unique users
        token_metrics:
          additionalProperties: true
          type: object
          title: Token Metrics
          description: Token usage metrics (input, output, cached, etc.)
        model_metrics:
          items:
            additionalProperties: true
            type: object
          type: array
          title: Model Metrics
          description: Metrics grouped by model (model_id, provider, count)
        date:
          type: string
          format: date-time
          title: Date
          description: Date for which these metrics are aggregated
        created_at:
          type: integer
          minimum: 0
          title: Created At
          description: Unix timestamp when metrics were created
        updated_at:
          type: integer
          minimum: 0
          title: Updated At
          description: Unix timestamp when metrics were last updated
      type: object
      required:
        - id
        - agent_runs_count
        - agent_sessions_count
        - team_runs_count
        - team_sessions_count
        - workflow_runs_count
        - workflow_sessions_count
        - users_count
        - token_metrics
        - model_metrics
        - date
        - created_at
        - updated_at
      title: DayAggregatedMetrics
      description: Aggregated metrics for a given day
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````