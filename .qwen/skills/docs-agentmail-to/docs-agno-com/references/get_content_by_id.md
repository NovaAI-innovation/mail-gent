# Get Content by ID

**Source:** https://docs.agno.com/reference-api/schema/knowledge/get-content-by-id.md
**Section:** Docs

**Description:** Retrieve detailed information about a specific content item including processing status and metadata.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Content by ID

> Retrieve detailed information about a specific content item including processing status and metadata.



## OpenAPI

````yaml get /knowledge/content/{content_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/content/{content_id}:
    get:
      tags:
        - Knowledge
      summary: Get Content by ID
      description: >-
        Retrieve detailed information about a specific content item including
        processing status and metadata.
      operationId: get_content_by_id
      parameters:
        - name: content_id
          in: path
          required: true
          schema:
            type: string
            title: Content Id
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
          description: Content details retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ContentResponseSchema'
              example:
                id: 3c2fc685-d451-4d47-b0c0-b9a544c672b7
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
          description: Content not found
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