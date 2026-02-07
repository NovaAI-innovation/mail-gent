# List Sessions

**Source:** https://docs.agno.com/reference-api/schema/sessions/list-sessions.md
**Section:** Docs

**Description:** Retrieve paginated list of sessions with filtering and sorting options. Supports filtering by session type (agent, team, workflow), component, user, and name. Sessions represent conversation histories and execution contexts.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Sessions

> Retrieve paginated list of sessions with filtering and sorting options. Supports filtering by session type (agent, team, workflow), component, user, and name. Sessions represent conversation histories and execution contexts.



## OpenAPI

````yaml get /sessions
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions:
    get:
      tags:
        - Sessions
      summary: List Sessions
      description: >-
        Retrieve paginated list of sessions with filtering and sorting options.
        Supports filtering by session type (agent, team, workflow), component,
        user, and name. Sessions represent conversation histories and execution
        contexts.
      operationId: get_sessions
      parameters:
        - name: type
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/SessionType'
            description: Type of sessions to retrieve (agent, team, or workflow)
            default: agent
          description: Type of sessions to retrieve (agent, team, or workflow)
        - name: component_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter sessions by component ID (agent/team/workflow ID)
            title: Component Id
          description: Filter sessions by component ID (agent/team/workflow ID)
        - name: user_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter sessions by user ID
            title: User Id
          description: Filter sessions by user ID
        - name: session_name
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter sessions by name (partial match)
            title: Session Name
          description: Filter sessions by name (partial match)
        - name: limit
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Number of sessions to return per page
            default: 20
            title: Limit
          description: Number of sessions to return per page
        - name: page
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Page number for pagination
            default: 1
            title: Page
          description: Page number for pagination
        - name: sort_by
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Field to sort sessions by
            default: created_at
            title: Sort By
          description: Field to sort sessions by
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
            description: Database ID to query sessions from
            title: Db Id
          description: Database ID to query sessions from
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
          description: Sessions retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_SessionSchema_'
              example:
                session_example:
                  summary: Example session response
                  value:
                    data:
                      - session_id: 6f6cfbfd-9643-479a-ae47-b8f32eb4d710
                        session_name: What tools do you have?
                        session_state: {}
                        created_at: '2025-09-05T16:02:09Z'
                        updated_at: '2025-09-05T16:02:09Z'
        '400':
          description: Invalid session type or filter parameters
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
          description: Not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/NotFoundResponse'
        '422':
          description: Validation error in query parameters
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
    SessionType:
      type: string
      enum:
        - agent
        - team
        - workflow
      title: SessionType
    SortOrder:
      type: string
      enum:
        - asc
        - desc
      title: SortOrder
    PaginatedResponse_SessionSchema_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/SessionSchema'
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
      title: PaginatedResponse[SessionSchema]
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
    SessionSchema:
      properties:
        session_id:
          type: string
          title: Session Id
          description: Unique identifier for the session
        session_name:
          type: string
          title: Session Name
          description: Human-readable name for the session
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Current state data of the session
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Timestamp when session was created
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Timestamp when session was last updated
      type: object
      required:
        - session_id
        - session_name
      title: SessionSchema
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