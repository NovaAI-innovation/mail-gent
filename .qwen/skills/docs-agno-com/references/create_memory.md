# Create Memory

**Source:** https://docs.agno.com/reference-api/schema/memory/create-memory.md
**Section:** Docs

**Description:** Create a new user memory with content and associated topics. Memories are used to store contextual information for users across conversations.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Memory

> Create a new user memory with content and associated topics. Memories are used to store contextual information for users across conversations.



## OpenAPI

````yaml post /memories
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /memories:
    post:
      tags:
        - Memory
      summary: Create Memory
      description: >-
        Create a new user memory with content and associated topics. Memories
        are used to store contextual information for users across conversations.
      operationId: create_memory
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for memory storage
            title: Db Id
          description: Database ID to use for memory storage
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to use for memory storage
            title: Table
          description: Table to use for memory storage
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserMemoryCreateSchema'
      responses:
        '200':
          description: Memory created successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserMemorySchema'
              example:
                memory_id: mem-123
                memory: User prefers technical explanations with code examples
                topics:
                  - preferences
                  - communication_style
                  - technical
                user_id: user-456
                created_at: '2024-01-15T10:30:00Z'
                updated_at: '2024-01-15T10:30:00Z'
        '400':
          description: Invalid request data
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
          description: Validation error in payload
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '500':
          description: Failed to create memory
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    UserMemoryCreateSchema:
      properties:
        memory:
          type: string
          maxLength: 5000
          minLength: 1
          title: Memory
          description: Memory content text
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID who owns this memory
        topics:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Topics
          description: Topics or tags to categorize the memory
      type: object
      required:
        - memory
      title: UserMemoryCreateSchema
      description: Define the payload expected for creating a new user memory
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