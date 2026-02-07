# List Memories

**Source:** https://docs.agno.com/reference-api/schema/memory/list-memories.md
**Section:** Docs

**Description:** Retrieve paginated list of user memories with filtering and search capabilities. Filter by user, agent, team, topics, or search within memory content.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Memories

> Retrieve paginated list of user memories with filtering and search capabilities. Filter by user, agent, team, topics, or search within memory content.



## OpenAPI

````yaml get /memories
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /memories:
    get:
      tags:
        - Memory
      summary: List Memories
      description: >-
        Retrieve paginated list of user memories with filtering and search
        capabilities. Filter by user, agent, team, topics, or search within
        memory content.
      operationId: get_memories
      parameters:
        - name: user_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter memories by user ID
            title: User Id
          description: Filter memories by user ID
        - name: agent_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter memories by agent ID
            title: Agent Id
          description: Filter memories by agent ID
        - name: team_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Filter memories by team ID
            title: Team Id
          description: Filter memories by team ID
        - name: search_content
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Fuzzy search within memory content
            title: Search Content
          description: Fuzzy search within memory content
        - name: limit
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Number of memories to return per page
            default: 20
            title: Limit
          description: Number of memories to return per page
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
            description: Field to sort memories by
            default: updated_at
            title: Sort By
          description: Field to sort memories by
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
            description: Database ID to query memories from
            title: Db Id
          description: Database ID to query memories from
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
        - name: topics
          in: query
          required: false
          schema:
            anyOf:
              - items:
                  type: string
                type: array
              - type: 'null'
            description: Comma-separated list of topics to filter by
            examples:
              - preferences,technical,communication_style
            title: Topics
          description: Comma-separated list of topics to filter by
      responses:
        '200':
          description: Memories retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_UserMemorySchema_'
              example:
                data:
                  - memory_id: f9361a69-2997-40c7-ae4e-a5861d434047
                    memory: User likes coffee.
                    topics:
                      - preferences
                    user_id: '123'
                    updated_at: '2025-09-01T07:53:17Z'
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
    SortOrder:
      type: string
      enum:
        - asc
        - desc
      title: SortOrder
    PaginatedResponse_UserMemorySchema_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/UserMemorySchema'
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
      title: PaginatedResponse[UserMemorySchema]
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
    UserMemorySchema:
      properties:
        memory_id:
          type: string
          title: Memory Id
          description: Unique identifier for the memory
        memory:
          type: string
          title: Memory
          description: Memory content text
        topics:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Topics
          description: Topics or tags associated with the memory
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID associated with this memory
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID associated with this memory
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID who owns this memory
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Timestamp when memory was last updated
      type: object
      required:
        - memory_id
        - memory
      title: UserMemorySchema
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