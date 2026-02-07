# Get User Memory Statistics

**Source:** https://docs.agno.com/reference-api/schema/memory/get-user-memory-statistics.md
**Section:** Docs

**Description:** Retrieve paginated statistics about memory usage by user. Provides insights into user engagement and memory distribution across users.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get User Memory Statistics

> Retrieve paginated statistics about memory usage by user. Provides insights into user engagement and memory distribution across users.



## OpenAPI

````yaml get /user_memory_stats
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /user_memory_stats:
    get:
      tags:
        - Memory
      summary: Get User Memory Statistics
      description: >-
        Retrieve paginated statistics about memory usage by user. Provides
        insights into user engagement and memory distribution across users.
      operationId: get_user_memory_stats
      parameters:
        - name: limit
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Number of user statistics to return per page
            default: 20
            title: Limit
          description: Number of user statistics to return per page
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
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to query statistics from
            title: Table
          description: Table to query statistics from
      responses:
        '200':
          description: User memory statistics retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_UserStatsSchema_'
              example:
                data:
                  - user_id: '123'
                    total_memories: 3
                    last_memory_updated_at: '2025-09-01T07:53:17Z'
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
          description: Failed to retrieve user statistics
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    PaginatedResponse_UserStatsSchema_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/UserStatsSchema'
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
      title: PaginatedResponse[UserStatsSchema]
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
    UserStatsSchema:
      properties:
        user_id:
          type: string
          title: User Id
          description: User ID
        total_memories:
          type: integer
          minimum: 0
          title: Total Memories
          description: Total number of memories for this user
        last_memory_updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Last Memory Updated At
          description: Timestamp of the most recent memory update
      type: object
      required:
        - user_id
        - total_memories
      title: UserStatsSchema
      description: Schema for user memory statistics
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