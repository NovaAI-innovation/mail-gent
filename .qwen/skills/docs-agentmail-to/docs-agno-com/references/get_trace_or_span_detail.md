# Get Trace or Span Detail

**Source:** https://docs.agno.com/reference-api/schema/traces/get-trace-or-span-detail.md
**Section:** Docs

**Description:** Retrieve detailed trace information with hierarchical span tree, or a specific span within the trace.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Trace or Span Detail

> Retrieve detailed trace information with hierarchical span tree, or a specific span within the trace.

**Without span_id parameter:**
Returns the full trace with hierarchical span tree:
- Trace metadata (ID, status, duration, context)
- Hierarchical tree of all spans
- Each span includes timing, status, and type-specific metadata

**With span_id parameter:**
Returns details for a specific span within the trace:
- Span metadata (ID, name, type, timing)
- Status and error information
- Type-specific attributes (model, tokens, tool params, etc.)

**Span Hierarchy (full trace):**
The `tree` field contains root spans, each with potential `children`.
This recursive structure represents the execution flow:
```
Agent.run (root)
  ├─ LLM.invoke
  ├─ Tool.execute
  │   └─ LLM.invoke (nested)
  └─ LLM.invoke
```

**Span Types:**
- `AGENT`: Agent execution with input/output
- `LLM`: Model invocations with tokens and prompts
- `TOOL`: Tool calls with parameters and results



## OpenAPI

````yaml get /traces/{trace_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /traces/{trace_id}:
    get:
      tags:
        - Traces
        - Traces
      summary: Get Trace or Span Detail
      description: >-
        Retrieve detailed trace information with hierarchical span tree, or a
        specific span within the trace.


        **Without span_id parameter:**

        Returns the full trace with hierarchical span tree:

        - Trace metadata (ID, status, duration, context)

        - Hierarchical tree of all spans

        - Each span includes timing, status, and type-specific metadata


        **With span_id parameter:**

        Returns details for a specific span within the trace:

        - Span metadata (ID, name, type, timing)

        - Status and error information

        - Type-specific attributes (model, tokens, tool params, etc.)


        **Span Hierarchy (full trace):**

        The `tree` field contains root spans, each with potential `children`.

        This recursive structure represents the execution flow:

        ```

        Agent.run (root)
          ├─ LLM.invoke
          ├─ Tool.execute
          │   └─ LLM.invoke (nested)
          └─ LLM.invoke
        ```


        **Span Types:**

        - `AGENT`: Agent execution with input/output

        - `LLM`: Model invocations with tokens and prompts

        - `TOOL`: Tool calls with parameters and results
      operationId: get_trace
      parameters:
        - name: trace_id
          in: path
          required: true
          schema:
            type: string
            title: Trace Id
        - name: span_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: 'Optional: Span ID to retrieve specific span'
            title: Span Id
          description: 'Optional: Span ID to retrieve specific span'
        - name: run_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: 'Optional: Run ID to retrieve trace for'
            title: Run Id
          description: 'Optional: Run ID to retrieve trace for'
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query trace from
            title: Db Id
          description: Database ID to query trace from
      responses:
        '200':
          description: Trace or span detail retrieved successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/TraceDetail'
                  - $ref: '#/components/schemas/TraceNode'
                title: Response Get Trace
              examples:
                full_trace:
                  summary: Full trace with hierarchy (no span_id)
                  value:
                    trace_id: a1b2c3d4
                    name: Stock_Price_Agent.run
                    status: OK
                    duration: 1.2s
                    start_time: '2025-11-19T10:30:00.000000+00:00'
                    end_time: '2025-11-19T10:30:01.200000+00:00'
                    total_spans: 4
                    error_count: 0
                    input: What is Tesla stock price?
                    output: The current price of Tesla (TSLA) is $245.67.
                    run_id: run123
                    session_id: session456
                    user_id: user789
                    agent_id: stock_agent
                    created_at: '2025-11-19T10:30:00+00:00'
                    tree:
                      - id: span1
                        name: Stock_Price_Agent.run
                        type: AGENT
                        duration: 1.2s
                        status: OK
                        spans: []
                single_span:
                  summary: Single span detail (with span_id)
                  value:
                    id: span2
                    name: gpt-4o-mini.invoke
                    type: LLM
                    duration: 800ms
                    status: OK
                    metadata:
                      model: gpt-4o-mini
                      input_tokens: 120
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
          description: Trace or span not found
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
    TraceDetail:
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
          description: Overall status (OK, ERROR)
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
          description: Input to the agent/workflow
        output:
          anyOf:
            - type: string
            - type: 'null'
          title: Output
          description: Output from the agent/workflow
        error:
          anyOf:
            - type: string
            - type: 'null'
          title: Error
          description: Error message if status is ERROR
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
        tree:
          items:
            $ref: '#/components/schemas/TraceNode'
          type: array
          title: Tree
          description: Hierarchical tree of spans (root nodes)
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
        - tree
      title: TraceDetail
      description: Detailed trace information with hierarchical span tree
    TraceNode:
      properties:
        id:
          type: string
          title: Id
          description: Span ID
        name:
          type: string
          title: Name
          description: Span name (e.g., 'agent.run', 'llm.invoke')
        type:
          type: string
          title: Type
          description: Span kind (AGENT, TEAM, WORKFLOW, LLM, TOOL)
        duration:
          type: string
          title: Duration
          description: Human-readable duration (e.g., '123ms', '1.5s')
        start_time:
          type: string
          format: date-time
          title: Start Time
          description: Start time (Pydantic auto-serializes to ISO 8601)
        end_time:
          type: string
          format: date-time
          title: End Time
          description: End time (Pydantic auto-serializes to ISO 8601)
        status:
          type: string
          title: Status
          description: Status code (OK, ERROR)
        input:
          anyOf:
            - type: string
            - type: 'null'
          title: Input
          description: Input to the span
        output:
          anyOf:
            - type: string
            - type: 'null'
          title: Output
          description: Output from the span
        error:
          anyOf:
            - type: string
            - type: 'null'
          title: Error
          description: Error message if status is ERROR
        spans:
          anyOf:
            - items:
                $ref: '#/components/schemas/TraceNode'
              type: array
            - type: 'null'
          title: Spans
          description: Child spans in the trace hierarchy
        step_type:
          anyOf:
            - type: string
            - type: 'null'
          title: Step Type
          description: Workflow step type (Step, Condition, function, Agent, Team)
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional span attributes and data
        extra_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Extra Data
          description: Flexible field for custom attributes and additional data
      type: object
      required:
        - id
        - name
        - type
        - duration
        - start_time
        - end_time
        - status
      title: TraceNode
      description: Recursive node structure for rendering trace hierarchy in the frontend
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