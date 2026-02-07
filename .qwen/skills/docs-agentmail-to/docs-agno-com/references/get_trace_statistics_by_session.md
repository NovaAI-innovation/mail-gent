# Get Trace Statistics by Session

**Source:** https://docs.agno.com/reference-api/schema/traces/get-trace-statistics-by-session.md
**Section:** Docs

**Description:** Retrieve aggregated trace statistics grouped by session ID with pagination.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Trace Statistics by Session

> Retrieve aggregated trace statistics grouped by session ID with pagination.

**Provides insights into:**
- Total traces per session
- First and last trace timestamps per session
- Associated user and agent information

**Filtering Options:**
- By user ID
- By agent ID

**Use Cases:**
- Monitor session-level activity
- Track conversation flows
- Identify high-activity sessions
- Analyze user engagement patterns



## OpenAPI

````yaml get /trace_session_stats
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /trace_session_stats:
    get:
      tags:
        - Traces
        - Traces
      summary: Get Trace Statistics by Session
      description: >-
        Retrieve aggregated trace statistics grouped by session ID with
        pagination.


        **Provides insights into:**

        - Total traces per session

        - First and last trace timestamps per session

        - Associated user and agent information


        **Filtering Options:**

        - By user ID

        - By agent ID


        **Use Cases:**

        - Monitor session-level activity

        - Track conversation flows

        - Identify high-activity sessions

        - Analyze user engagement patterns
      operationId: get_trace_stats
      parameters:
        - name: user_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by user ID
            title: User Id
          description: Filter by user ID
        - name: agent_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by agent ID
            title: Agent Id
          description: Filter by agent ID
        - name: team_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by team ID
            title: Team Id
          description: Filter by team ID
        - name: workflow_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by workflow ID
            title: Workflow Id
          description: Filter by workflow ID
        - name: start_time
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: >-
              Filter sessions with traces created after this time (ISO 8601
              format with timezone, e.g., '2025-11-19T10:00:00Z' or
              '2025-11-19T15:30:00+05:30'). Times are converted to UTC for
              comparison.
            title: Start Time
          description: >-
            Filter sessions with traces created after this time (ISO 8601 format
            with timezone, e.g., '2025-11-19T10:00:00Z' or
            '2025-11-19T15:30:00+05:30'). Times are converted to UTC for
            comparison.
        - name: end_time
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: >-
              Filter sessions with traces created before this time (ISO 8601
              format with timezone, e.g., '2025-11-19T11:00:00Z' or
              '2025-11-19T16:30:00+05:30'). Times are converted to UTC for
              comparison.
            title: End Time
          description: >-
            Filter sessions with traces created before this time (ISO 8601
            format with timezone, e.g., '2025-11-19T11:00:00Z' or
            '2025-11-19T16:30:00+05:30'). Times are converted to UTC for
            comparison.
        - name: page
          in: query
          required: false
          schema:
            type: integer
            minimum: 1
            description: Page number (1-indexed)
            default: 1
            title: Page
          description: Page number (1-indexed)
        - name: limit
          in: query
          required: false
          schema:
            type: integer
            maximum: 100
            minimum: 1
            description: Number of sessions per page
            default: 20
            title: Limit
          description: Number of sessions per page
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query statistics from
            title: Db Id
          description: Database ID to query statistics from
      responses:
        '200':
          description: Trace statistics retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_TraceSessionStats_'
              example:
                data:
                  - session_id: 37029bc6-1794-4ba8-a629-1efedc53dcad
                    user_id: kaustubh@agno.com
                    agent_id: hackernews-agent
                    total_traces: 5
                    first_trace_at: '2025-11-19T10:15:16+00:00'
                    last_trace_at: '2025-11-19T10:21:30+00:00'
                meta:
                  page: 1
                  limit: 20
                  total_pages: 3
                  total_count: 45
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
          description: Failed to retrieve statistics
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    PaginatedResponse_TraceSessionStats_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/TraceSessionStats'
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
      title: PaginatedResponse[TraceSessionStats]
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
    TraceSessionStats:
      properties:
        session_id:
          type: string
          title: Session Id
          description: Session identifier
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the session
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID(s) used in the session
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID associated with the session
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Workflow ID associated with the session
        total_traces:
          type: integer
          title: Total Traces
          description: Total number of traces in this session
        first_trace_at:
          type: string
          format: date-time
          title: First Trace At
          description: Time of first trace (Pydantic auto-serializes to ISO 8601)
        last_trace_at:
          type: string
          format: date-time
          title: Last Trace At
          description: Time of last trace (Pydantic auto-serializes to ISO 8601)
      type: object
      required:
        - session_id
        - total_traces
        - first_trace_at
        - last_trace_at
      title: TraceSessionStats
      description: Aggregated trace statistics grouped by session
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
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````