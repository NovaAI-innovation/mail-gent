# Rename Session

**Source:** https://docs.agno.com/reference-api/schema/sessions/rename-session.md
**Section:** Docs

**Description:** Update the name of an existing session. Useful for organizing and categorizing sessions with meaningful names for better identification and management.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Rename Session

> Update the name of an existing session. Useful for organizing and categorizing sessions with meaningful names for better identification and management.



## OpenAPI

````yaml post /sessions/{session_id}/rename
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions/{session_id}/rename:
    post:
      tags:
        - Sessions
      summary: Rename Session
      description: >-
        Update the name of an existing session. Useful for organizing and
        categorizing sessions with meaningful names for better identification
        and management.
      operationId: rename_session
      parameters:
        - name: session_id
          in: path
          required: true
          schema:
            type: string
            description: Session ID to rename
            title: Session Id
          description: Session ID to rename
        - name: type
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/SessionType'
            description: Session type (agent, team, or workflow)
            default: agent
          description: Session type (agent, team, or workflow)
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to use for rename operation
            title: Db Id
          description: Database ID to use for rename operation
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to use for rename operation
            title: Table
          description: Table to use for rename operation
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Body_rename_session'
      responses:
        '200':
          description: Session renamed successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/AgentSessionDetailSchema'
                  - $ref: '#/components/schemas/TeamSessionDetailSchema'
                  - $ref: '#/components/schemas/WorkflowSessionDetailSchema'
                title: Response Rename Session
              examples:
                agent_session_example:
                  summary: Example agent session response
                  value:
                    user_id: '123'
                    agent_session_id: 6f6cfbfd-9643-479a-ae47-b8f32eb4d710
                    session_id: 6f6cfbfd-9643-479a-ae47-b8f32eb4d710
                    session_name: What tools do you have?
                    session_summary:
                      summary: >-
                        The user and assistant engaged in a conversation about
                        the tools the agent has available.
                      updated_at: '2025-09-05T18:02:12.269392'
                    session_state: {}
                    agent_id: basic-agent
                    total_tokens: 160
                    agent_data:
                      name: Basic Agent
                      agent_id: basic-agent
                      model:
                        provider: OpenAI
                        name: OpenAIChat
                        id: gpt-4o
                    metrics:
                      input_tokens: 134
                      output_tokens: 26
                      total_tokens: 160
                      audio_input_tokens: 0
                      audio_output_tokens: 0
                      audio_total_tokens: 0
                      cache_read_tokens: 0
                      cache_write_tokens: 0
                      reasoning_tokens: 0
                    chat_history:
                      - content: >-
                          <additional_information>

                          - Use markdown to format your answers.

                          - The current time is 2025-09-05 18:02:09.171627.

                          </additional_information>


                          You have access to memories from previous interactions
                          with the user that you can use:


                          <memories_from_previous_interactions>

                          - User really likes Digimon and Japan.

                          - User really likes Japan.

                          - User likes coffee.

                          </memories_from_previous_interactions>


                          Note: this information is from previous interactions
                          and may be updated in this conversation. You should
                          always prefer information from this conversation over
                          the past memories.
                        from_history: false
                        stop_after_tool_call: false
                        role: system
                        created_at: 1757088129
                      - content: What tools do you have?
                        from_history: false
                        stop_after_tool_call: false
                        role: user
                        created_at: 1757088129
                      - content: >-
                          I don't have access to external tools or the internet.
                          However, I can assist you with a wide range of topics
                          by providing information, answering questions, and
                          offering suggestions based on the knowledge I've been
                          trained on. If there's anything specific you need help
                          with, feel free to ask!
                        from_history: false
                        stop_after_tool_call: false
                        role: assistant
                        metrics:
                          input_tokens: 134
                          output_tokens: 26
                          total_tokens: 160
                        created_at: 1757088129
                    created_at: '2025-09-05T16:02:09Z'
                    updated_at: '2025-09-05T16:02:09Z'
        '400':
          description: Invalid session name
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
          description: Invalid session type or validation error
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
    SessionType:
      type: string
      enum:
        - agent
        - team
        - workflow
      title: SessionType
    Body_rename_session:
      properties:
        session_name:
          type: string
          title: Session Name
          description: New name for the session
      type: object
      required:
        - session_name
      title: Body_rename_session
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