# Upload Content

**Source:** https://docs.agno.com/reference-api/schema/knowledge/upload-content.md
**Section:** Docs

**Description:** Upload content to the knowledge base. Supports file uploads, text content, or URLs. Content is processed asynchronously in the background. Supports custom readers and chunking strategies.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Upload Content

> Upload content to the knowledge base. Supports file uploads, text content, or URLs. Content is processed asynchronously in the background. Supports custom readers and chunking strategies.



## OpenAPI

````yaml post /knowledge/content
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/content:
    post:
      tags:
        - Knowledge
      summary: Upload Content
      description: >-
        Upload content to the knowledge base. Supports file uploads, text
        content, or URLs. Content is processed asynchronously in the background.
        Supports custom readers and chunking strategies.
      operationId: upload_content
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for content storage
            title: Db Id
          description: Database ID to use for content storage
      requestBody:
        content:
          multipart/form-data:
            schema:
              $ref: '#/components/schemas/Body_upload_content'
      responses:
        '202':
          description: Content upload accepted for processing
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ContentResponseSchema'
              example:
                id: content-123
                name: example-document.pdf
                description: Sample document for processing
                metadata:
                  category: documentation
                  priority: high
                status: processing
        '400':
          description: Invalid request - malformed metadata or missing content
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
          description: Validation error in form data
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
    Body_upload_content:
      properties:
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Content name (auto-generated from file/URL if not provided)
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Content description for context
        url:
          anyOf:
            - type: string
            - type: 'null'
          title: Url
          description: URL to fetch content from (JSON array or single URL string)
        metadata:
          anyOf:
            - type: string
            - type: 'null'
          title: Metadata
          description: JSON metadata object for additional content properties
        file:
          anyOf:
            - type: string
              format: binary
            - type: 'null'
          title: File
          description: File to upload for processing
        text_content:
          anyOf:
            - type: string
            - type: 'null'
          title: Text Content
          description: Raw text content to process
        reader_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Reader Id
          description: ID of the reader to use for content processing
        chunker:
          anyOf:
            - type: string
            - type: 'null'
          title: Chunker
          description: Chunking strategy to apply during processing
        chunk_size:
          anyOf:
            - type: integer
            - type: 'null'
          title: Chunk Size
          description: Chunk size to use for processing
        chunk_overlap:
          anyOf:
            - type: integer
            - type: 'null'
          title: Chunk Overlap
          description: Chunk overlap to use for processing
      type: object
      title: Body_upload_content
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