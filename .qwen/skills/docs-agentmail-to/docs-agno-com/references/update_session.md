# Update Session

**Source:** https://docs.agno.com/reference-api/schema/sessions/update-session.md
**Section:** Docs

**Description:** Update session properties such as session_name, session_state, metadata, or summary. Use this endpoint to modify the session name, update state, add metadata, or update the session summary.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Update Session

> Update session properties such as session_name, session_state, metadata, or summary. Use this endpoint to modify the session name, update state, add metadata, or update the session summary.



## OpenAPI

````yaml patch /sessions/{session_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions/{session_id}:
    patch:
      tags:
        - Sessions
      summary: Update Session
      description: >-
        Update session properties such as session_name, session_state, metadata,
        or summary. Use this endpoint to modify the session name, update state,
        add metadata, or update the session summary.
      operationId: update_session
      parameters:
        - name: session_id
          in: path
          required: true
          schema:
            type: string
            description: Session ID to update
            title: Session Id
          description: Session ID to update
        - name: type
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/SessionType'
            description: Session type (agent, team, or workflow)
            default: agent
          description: Session type (agent, team, or workflow)
        - name: user_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: User ID
            title: User Id
          description: User ID
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for update operation
            title: Db Id
          description: Database ID to use for update operation
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UpdateSessionRequest'
              description: Session update data
      responses:
        '200':
          description: Session updated successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/AgentSessionDetailSchema'
                  - $ref: '#/components/schemas/TeamSessionDetailSchema'
                  - $ref: '#/components/schemas/WorkflowSessionDetailSchema'
                title: Response Update Session
              examples:
                update_summary:
                  summary: Update session summary
                  value:
                    summary:
                      summary: The user discussed project planning with the agent.
                      updated_at: '2025-10-21T14:30:00Z'
                update_metadata:
                  summary: Update session metadata
                  value:
                    metadata:
                      tags:
                        - planning
                        - project
                      priority: high
                update_session_name:
                  summary: Update session name
                  value:
                    session_name: Updated Session Name
                update_session_state:
                  summary: Update session state
                  value:
                    session_state:
                      step: completed
                      context: Project planning finished
                      progress: 100
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
          description: Session not found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/NotFoundResponse'
        '422':
          description: Invalid request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '500':
          description: Failed to update session
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
    UpdateSessionRequest:
      properties:
        session_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Session Name
          description: Updated session name
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Updated session state
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
          description: Updated metadata
        summary:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Summary
          description: Session summary
      type: object
      title: UpdateSessionRequest
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