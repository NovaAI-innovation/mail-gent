# Create New Session

**Source:** https://docs.agno.com/reference-api/schema/sessions/create-new-session.md
**Section:** Docs

**Description:** Create a new empty session with optional configuration. Useful for pre-creating sessions with specific session_state, metadata, or other properties before running any agent/team/workflow interactions. The session can later be used by providing its session_id in run requests.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create New Session

> Create a new empty session with optional configuration. Useful for pre-creating sessions with specific session_state, metadata, or other properties before running any agent/team/workflow interactions. The session can later be used by providing its session_id in run requests.



## OpenAPI

````yaml post /sessions
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions:
    post:
      tags:
        - Sessions
      summary: Create New Session
      description: >-
        Create a new empty session with optional configuration. Useful for
        pre-creating sessions with specific session_state, metadata, or other
        properties before running any agent/team/workflow interactions. The
        session can later be used by providing its session_id in run requests.
      operationId: create_session
      parameters:
        - name: type
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/SessionType'
            description: Type of session to create (agent, team, or workflow)
            default: agent
          description: Type of session to create (agent, team, or workflow)
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to create session in
            title: Db Id
          description: Database ID to create session in
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateSessionRequest'
              description: Session configuration data
              default: {}
      responses:
        '201':
          description: Session created successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/AgentSessionDetailSchema'
                  - $ref: '#/components/schemas/TeamSessionDetailSchema'
                  - $ref: '#/components/schemas/WorkflowSessionDetailSchema'
                title: Response Create Session
              examples:
                agent_session_example:
                  summary: Example created agent session
                  value:
                    user_id: user-123
                    agent_session_id: new-session-id
                    session_id: new-session-id
                    session_name: New Session
                    session_state:
                      key: value
                    metadata:
                      key: value
                    agent_id: agent-1
                    created_at: '2025-10-21T12:00:00Z'
                    updated_at: '2025-10-21T12:00:00Z'
        '400':
          description: Invalid request parameters
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
          description: Validation error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '500':
          description: Failed to create session
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
    CreateSessionRequest:
      properties:
        session_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Id
          description: Optional session ID (generated if not provided)
        session_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Name
          description: Name for the session
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Initial session state
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the session
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID if this is an agent session
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID if this is a team session
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Workflow ID if this is a workflow session
      type: object
      title: CreateSessionRequest
    AgentSessionDetailSchema:
      properties:
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the session
        agent_session_id:
          type: string
          title: Agent Session Id
          description: Unique agent session identifier
        session_id:
          type: string
          title: Session Id
          description: Session identifier
        session_name:
          type: string
          title: Session Name
          description: Human-readable session name
        session_summary:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session Summary
          description: Summary of session interactions
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Current state of the session
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID used in this session
        total_tokens:
          anyOf:
            - type: integer
            - type: 'null'
          title: Total Tokens
          description: Total tokens used in this session
        agent_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Agent Data
          description: Agent-specific data
        metrics:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metrics
          description: Session metrics
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata
        chat_history:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Chat History
          description: Complete chat history
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Session creation timestamp
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Last update timestamp
      type: object
      required:
        - agent_session_id
        - session_id
        - session_name
      title: AgentSessionDetailSchema
    TeamSessionDetailSchema:
      properties:
        session_id:
          type: string
          title: Session Id
          description: Unique session identifier
        session_name:
          type: string
          title: Session Name
          description: Human-readable session name
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the session
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID used in this session
        session_summary:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session Summary
          description: Summary of team interactions
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Current state of the session
        metrics:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metrics
          description: Session metrics
        team_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Team Data
          description: Team-specific data
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata
        chat_history:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Chat History
          description: Complete chat history
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Session creation timestamp
        updated_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Updated At
          description: Last update timestamp
        total_tokens:
          anyOf:
            - type: integer
            - type: 'null'
          title: Total Tokens
          description: Total tokens used in this session
      type: object
      required:
        - session_id
        - session_name
      title: TeamSessionDetailSchema
    WorkflowSessionDetailSchema:
      properties:
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the session
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Workflow ID used in this session
        workflow_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Name
          description: Name of the workflow
        session_id:
          type: string
          title: Session Id
          description: Unique session identifier
        session_name:
          type: string
          title: Session Name
          description: Human-readable session name
        session_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session Data
          description: Complete session data
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Current workflow state
        workflow_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Workflow Data
          description: Workflow-specific data
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Additional metadata
        created_at:
          anyOf:
            - type: integer
            - type: 'null'
          title: Created At
          description: Unix timestamp of session creation
        updated_at:
          anyOf:
            - type: integer
            - type: 'null'
          title: Updated At
          description: Unix timestamp of last update
      type: object
      required:
        - session_id
        - session_name
      title: WorkflowSessionDetailSchema
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