# Delete Multiple Memories

**Source:** https://docs.agno.com/reference-api/schema/memory/delete-multiple-memories.md
**Section:** Docs

**Description:** Delete multiple user memories by their IDs in a single operation. This action cannot be undone and all specified memories will be permanently removed.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Multiple Memories

> Delete multiple user memories by their IDs in a single operation. This action cannot be undone and all specified memories will be permanently removed.



## OpenAPI

````yaml delete /memories
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /memories:
    delete:
      tags:
        - Memory
      summary: Delete Multiple Memories
      description: >-
        Delete multiple user memories by their IDs in a single operation. This
        action cannot be undone and all specified memories will be permanently
        removed.
      operationId: delete_memories
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for deletion
            title: Db Id
          description: Database ID to use for deletion
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to use for deletion
            title: Table
          description: Table to use for deletion
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/DeleteMemoriesRequest'
      responses:
        '204':
          description: Memories deleted successfully
        '400':
          description: Invalid request - empty memory_ids list
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
          description: Failed to delete memories
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    DeleteMemoriesRequest:
      properties:
        memory_ids:
          items:
            type: string
          type: array
          minItems: 1
          title: Memory Ids
          description: List of memory IDs to delete
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID to filter memories for deletion
      type: object
      required:
        - memory_ids
      title: DeleteMemoriesRequest
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