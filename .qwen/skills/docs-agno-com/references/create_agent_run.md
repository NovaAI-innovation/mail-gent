# Create Agent Run

**Source:** https://docs.agno.com/reference-api/schema/agents/create-agent-run.md
**Section:** Docs

**Description:** Execute an agent with a message and optional media files. Supports both streaming and non-streaming responses.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Agent Run

> Execute an agent with a message and optional media files. Supports both streaming and non-streaming responses.

**Features:**
- Text message input with optional session management
- Multi-media support: images (PNG, JPEG, WebP), audio (WAV, MP3), video (MP4, WebM, etc.)
- Document processing: PDF, CSV, DOCX, TXT, JSON
- Real-time streaming responses with Server-Sent Events (SSE)
- User and session context preservation

**Streaming Response:**
When `stream=true`, returns SSE events with `event` and `data` fields.



## OpenAPI

````yaml post /agents/{agent_id}/runs
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /agents/{agent_id}/runs:
    post:
      tags:
        - Agents
      summary: Create Agent Run
      description: >-
        Execute an agent with a message and optional media files. Supports both
        streaming and non-streaming responses.


        **Features:**

        - Text message input with optional session management

        - Multi-media support: images (PNG, JPEG, WebP), audio (WAV, MP3), video
        (MP4, WebM, etc.)

        - Document processing: PDF, CSV, DOCX, TXT, JSON

        - Real-time streaming responses with Server-Sent Events (SSE)

        - User and session context preservation


        **Streaming Response:**

        When `stream=true`, returns SSE events with `event` and `data` fields.
      operationId: create_agent_run
      parameters:
        - name: agent_id
          in: path
          required: true
          schema:
            type: string
            title: Agent Id
      requestBody:
        required: true
        content:
          multipart/form-data:
            schema:
              $ref: '#/components/schemas/Body_create_agent_run'
      responses:
        '200':
          description: Agent run executed successfully
          content:
            application/json:
              schema: {}
            text/event-stream:
              examples:
                event_stream:
                  summary: Example event stream response
                  value: |+
                    event: RunStarted
                    data: {"content": "Hello!", "run_id": "123..."}

        '400':
          description: Invalid request or unsupported file type
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
          description: Agent not found
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
    Body_create_agent_run:
      properties:
        message:
          type: string
          title: Message
        stream:
          type: boolean
          title: Stream
          default: false
        session_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Id
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
        files:
          anyOf:
            - items:
                type: string
                format: binary
              type: array
            - type: 'null'
          title: Files
      type: object
      required:
        - message
      title: Body_create_agent_run
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