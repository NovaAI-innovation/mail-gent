# List Content

**Source:** https://docs.agno.com/reference-api/schema/knowledge/list-content.md
**Section:** Docs

**Description:** Retrieve paginated list of all content in the knowledge base with filtering and sorting options. Filter by status, content type, or metadata properties.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# List Content

> Retrieve paginated list of all content in the knowledge base with filtering and sorting options. Filter by status, content type, or metadata properties.



## OpenAPI

````yaml get /knowledge/content
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/content:
    get:
      tags:
        - Knowledge
      summary: List Content
      description: >-
        Retrieve paginated list of all content in the knowledge base with
        filtering and sorting options. Filter by status, content type, or
        metadata properties.
      operationId: get_content
      parameters:
        - name: limit
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Number of content entries to return
            default: 20
            title: Limit
          description: Number of content entries to return
        - name: page
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: Page number
            default: 1
            title: Page
          description: Page number
        - name: sort_by
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Field to sort by
            default: created_at
            title: Sort By
          description: Field to sort by
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
            description: The ID of the database to use
            title: Db Id
          description: The ID of the database to use
      responses:
        '200':
          description: Content list retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_ContentResponseSchema_'
              example:
                data:
                  - id: 3c2fc685-d451-4d47-b0c0-b9a544c672b7
                    name: example.pdf
                    description: ''
                    type: application/pdf
                    size: '251261'
                    metadata: {}
                    access_count: 1
                    status: completed
                    status_message: ''
                    created_at: '2025-09-08T15:22:53Z'
                    updated_at: '2025-09-08T15:22:54Z'
                meta:
                  page: 1
                  limit: 20
                  total_pages: 1
                  total_count: 2
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
    PaginatedResponse_ContentResponseSchema_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/ContentResponseSchema'
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
      title: PaginatedResponse[ContentResponseSchema]
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
    ContentResponseSchema:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the content
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the content
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the content
        type:
          anyOf:
            - type: string
            - type: 'null'
          title: Type
          description: MIME type of the content
        size:
          anyOf:
            - type: string
            - type: 'null'
          title: Size
          description: Size of the content in bytes
        linked_to:
          anyOf:
            - type: string
            - type: 'null'
          title: Linked To
          description: ID of related content if linked
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata as key-value pairs
        access_count:
          anyOf:
            - type: integer
              minimum: 0
            - type: 'null'
          title: Access Count
          description: Number of times content has been accessed
        status:
          anyOf:
            - $ref: '#/components/schemas/ContentStatus'
            - type: 'null'
          description: Processing status of the content
        status_message:
          anyOf:
            - type: string
            - type: 'null'
          title: Status Message
          description: Status message or error details
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Timestamp when content was created
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Timestamp when content was last updated
      type: object
      required:
        - id
      title: ContentResponseSchema
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
    ContentStatus:
      type: string
      enum:
        - processing
        - completed
        - failed
      title: ContentStatus
      description: Enumeration of possible content processing statuses.
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````