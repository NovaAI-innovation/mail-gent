# Delete Multiple Sessions

**Source:** https://docs.agno.com/reference-api/schema/sessions/delete-multiple-sessions.md
**Section:** Docs

**Description:** Delete multiple sessions by their IDs in a single operation. This action cannot be undone and will permanently remove all specified sessions and their runs.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Delete Multiple Sessions

> Delete multiple sessions by their IDs in a single operation. This action cannot be undone and will permanently remove all specified sessions and their runs.



## OpenAPI

````yaml delete /sessions
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions:
    delete:
      tags:
        - Sessions
      summary: Delete Multiple Sessions
      description: >-
        Delete multiple sessions by their IDs in a single operation. This action
        cannot be undone and will permanently remove all specified sessions and
        their runs.
      operationId: delete_sessions
      parameters:
        - name: type
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/SessionType'
            description: Default session type filter
            default: agent
          description: Default session type filter
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
              $ref: '#/components/schemas/DeleteSessionRequest'
      responses:
        '204':
          description: Sessions deleted successfully
        '400':
          description: Invalid request - session IDs and types length mismatch
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
          description: Failed to delete sessions
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
    DeleteSessionRequest:
      properties:
        session_ids:
          items:
            type: string
          type: array
          minItems: 1
          title: Session Ids
          description: List of session IDs to delete
        session_types:
          items:
            $ref: '#/components/schemas/SessionType'
          type: array
          minItems: 1
          title: Session Types
          description: Types of sessions to delete
      type: object
      required:
        - session_ids
        - session_types
      title: DeleteSessionRequest
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