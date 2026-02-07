# Get Content Status

**Source:** https://docs.agno.com/reference-api/schema/knowledge/get-content-status.md
**Section:** Docs

**Description:** Retrieve the current processing status of a content item. Useful for monitoring asynchronous content processing progress and identifying any processing errors.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Content Status

> Retrieve the current processing status of a content item. Useful for monitoring asynchronous content processing progress and identifying any processing errors.



## OpenAPI

````yaml get /knowledge/content/{content_id}/status
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/content/{content_id}/status:
    get:
      tags:
        - Knowledge
      summary: Get Content Status
      description: >-
        Retrieve the current processing status of a content item. Useful for
        monitoring asynchronous content processing progress and identifying any
        processing errors.
      operationId: get_content_status
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
          description: Content status retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ContentStatusResponse'
              examples:
                completed:
                  summary: Example completed content status
                  value:
                    status: completed
                    status_message: ''
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
    ContentStatusResponse:
      properties:
        status:
          $ref: '#/components/schemas/ContentStatus'
          description: Current processing status of the content
        status_message:
          type: string
          title: Status Message
          description: Status message or error details
          default: ''
      type: object
      required:
        - status
      title: ContentStatusResponse
      description: Response model for content status endpoint.
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