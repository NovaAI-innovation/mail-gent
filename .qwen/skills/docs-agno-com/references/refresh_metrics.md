# Refresh Metrics

**Source:** https://docs.agno.com/reference-api/schema/metrics/refresh-metrics.md
**Section:** Docs

**Description:** Manually trigger recalculation of system metrics from raw data. This operation analyzes system activity logs and regenerates aggregated metrics. Useful for ensuring metrics are up-to-date or after system maintenance.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Refresh Metrics

> Manually trigger recalculation of system metrics from raw data. This operation analyzes system activity logs and regenerates aggregated metrics. Useful for ensuring metrics are up-to-date or after system maintenance.



## OpenAPI

````yaml post /metrics/refresh
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /metrics/refresh:
    post:
      tags:
        - Metrics
      summary: Refresh Metrics
      description: >-
        Manually trigger recalculation of system metrics from raw data. This
        operation analyzes system activity logs and regenerates aggregated
        metrics. Useful for ensuring metrics are up-to-date or after system
        maintenance.
      operationId: refresh_metrics
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for metrics calculation
            title: Db Id
          description: Database ID to use for metrics calculation
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to use for metrics calculation
            title: Table
          description: Table to use for metrics calculation
      responses:
        '200':
          description: Metrics refreshed successfully
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/DayAggregatedMetrics'
                title: Response Refresh Metrics
              example:
                - id: e77c9531-818b-47a5-99cd-59fed61e5403
                  agent_runs_count: 2
                  agent_sessions_count: 2
                  team_runs_count: 0
                  team_sessions_count: 0
                  workflow_runs_count: 0
                  workflow_sessions_count: 0
                  users_count: 1
                  token_metrics:
                    input_tokens: 256
                    output_tokens: 441
                    total_tokens: 697
                    audio_total_tokens: 0
                    audio_input_tokens: 0
                    audio_output_tokens: 0
                    cache_read_tokens: 0
                    cache_write_tokens: 0
                    reasoning_tokens: 0
                  model_metrics:
                    - model_id: gpt-4o
                      model_provider: OpenAI
                      count: 2
                  date: '2025-08-12T00:00:00'
                  created_at: 1755016907
                  updated_at: 1755016907
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
          description: Failed to refresh metrics
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
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