# List Traces

**Source:** https://docs.agno.com/reference-api/schema/traces/list-traces.md
**Section:** Docs

**Description:** Retrieve a paginated list of execution traces with optional filtering.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Traces

> Retrieve a paginated list of execution traces with optional filtering.

**Traces provide observability into:**
- Agent execution flows
- Model invocations and token usage
- Tool calls and their results
- Errors and performance bottlenecks

**Filtering Options:**
- By run, session, user, or agent ID
- By status (OK, ERROR)
- By time range

**Pagination:**
- Use `page` (1-indexed) and `limit` parameters
- Response includes pagination metadata (total_pages, total_count, etc.)

**Response Format:**
Returns summary information for each trace. Use GET `/traces/{trace_id}` for detailed hierarchy.



## OpenAPI

````yaml get /traces
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /traces:
    get:
      tags:
        - Traces
        - Traces
      summary: List Traces
      description: >-
        Retrieve a paginated list of execution traces with optional filtering.


        **Traces provide observability into:**

        - Agent execution flows

        - Model invocations and token usage

        - Tool calls and their results

        - Errors and performance bottlenecks


        **Filtering Options:**

        - By run, session, user, or agent ID

        - By status (OK, ERROR)

        - By time range


        **Pagination:**

        - Use `page` (1-indexed) and `limit` parameters

        - Response includes pagination metadata (total_pages, total_count, etc.)


        **Response Format:**

        Returns summary information for each trace. Use GET `/traces/{trace_id}`
        for detailed hierarchy.
      operationId: get_traces
      parameters:
        - name: run_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by run ID
            title: Run Id
          description: Filter by run ID
        - name: session_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by session ID
            title: Session Id
          description: Filter by session ID
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
        - name: status
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter by status (OK, ERROR)
            title: Status
          description: Filter by status (OK, ERROR)
        - name: start_time
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: >-
              Filter traces starting after this time (ISO 8601 format with
              timezone, e.g., '2025-11-19T10:00:00Z' or
              '2025-11-19T15:30:00+05:30'). Times are converted to UTC for
              comparison.
            title: Start Time
          description: >-
            Filter traces starting after this time (ISO 8601 format with
            timezone, e.g., '2025-11-19T10:00:00Z' or
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
              Filter traces ending before this time (ISO 8601 format with
              timezone, e.g., '2025-11-19T11:00:00Z' or
              '2025-11-19T16:30:00+05:30'). Times are converted to UTC for
              comparison.
            title: End Time
          description: >-
            Filter traces ending before this time (ISO 8601 format with
            timezone, e.g., '2025-11-19T11:00:00Z' or
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
            description: Number of traces per page
            default: 20
            title: Limit
          description: Number of traces per page
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query traces from
            title: Db Id
          description: Database ID to query traces from
      responses:
        '200':
          description: List of traces retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_TraceSummary_'
              example:
                data:
                  - trace_id: a1b2c3d4
                    name: Stock_Price_Agent.run
                    status: OK
                    duration: 1.2s
                    start_time: '2025-11-19T10:30:00.000000+00:00'
                    total_spans: 4
                    error_count: 0
                    input: What is the stock price of NVDA?
                    run_id: run123
                    session_id: session456
                    user_id: user789
                    agent_id: agent_stock
                    created_at: '2025-11-19T10:30:00+00:00'
                meta:
                  page: 1
                  limit: 20
                  total_pages: 5
                  total_count: 95
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
    PaginatedResponse_TraceSummary_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/TraceSummary'
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
      title: PaginatedResponse[TraceSummary]
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
    TraceSummary:
      properties:
        trace_id:
          type: string
          title: Trace Id
          description: Unique trace identifier
        name:
          type: string
          title: Name
          description: Trace name (usually root span name)
        status:
          type: string
          title: Status
          description: Overall status (OK, ERROR, UNSET)
        duration:
          type: string
          title: Duration
          description: Human-readable total duration
        start_time:
          type: string
          format: date-time
          title: Start Time
          description: Trace start time (Pydantic auto-serializes to ISO 8601)
        end_time:
          type: string
          format: date-time
          title: End Time
          description: Trace end time (Pydantic auto-serializes to ISO 8601)
        total_spans:
          type: integer
          title: Total Spans
          description: Total number of spans in this trace
        error_count:
          type: integer
          title: Error Count
          description: Number of spans with errors
        input:
          anyOf:
            - type: string
            - type: 'null'
          title: Input
          description: Input to the agent
        run_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Id
          description: Associated run ID
        session_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Id
          description: Associated session ID
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: Associated user ID
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Associated agent ID
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Associated team ID
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Associated workflow ID
        created_at:
          type: string
          format: date-time
          title: Created At
          description: Time when trace was created (Pydantic auto-serializes to ISO 8601)
      type: object
      required:
        - trace_id
        - name
        - status
        - duration
        - start_time
        - end_time
        - total_spans
        - error_count
        - created_at
      title: TraceSummary
      description: Summary information for trace list view
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