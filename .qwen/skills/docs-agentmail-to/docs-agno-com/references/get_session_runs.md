# Get Session Runs

**Source:** https://docs.agno.com/reference-api/schema/sessions/get-session-runs.md
**Section:** Docs

**Description:** Retrieve all runs (executions) for a specific session with optional timestamp filtering. Runs represent individual interactions or executions within a session. Response schema varies based on session type.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Session Runs

> Retrieve all runs (executions) for a specific session with optional timestamp filtering. Runs represent individual interactions or executions within a session. Response schema varies based on session type.



## OpenAPI

````yaml get /sessions/{session_id}/runs
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions/{session_id}/runs:
    get:
      tags:
        - Sessions
      summary: Get Session Runs
      description: >-
        Retrieve all runs (executions) for a specific session with optional
        timestamp filtering. Runs represent individual interactions or
        executions within a session. Response schema varies based on session
        type.
      operationId: get_session_runs
      parameters:
        - name: session_id
          in: path
          required: true
          schema:
            type: string
            description: Session ID to get runs from
            title: Session Id
          description: Session ID to get runs from
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
            description: User ID to query runs from
            title: User Id
          description: User ID to query runs from
        - name: created_after
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: >-
              Filter runs created after this Unix timestamp (epoch time in
              seconds)
            title: Created After
          description: >-
            Filter runs created after this Unix timestamp (epoch time in
            seconds)
        - name: created_before
          in: query
          required: false
          schema:
            anyOf:
              - type: integer
              - type: 'null'
            description: >-
              Filter runs created before this Unix timestamp (epoch time in
              seconds)
            title: Created Before
          description: >-
            Filter runs created before this Unix timestamp (epoch time in
            seconds)
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query runs from
            title: Db Id
          description: Database ID to query runs from
        - name: table
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Table to query runs from
            title: Table
          description: Table to query runs from
      responses:
        '200':
          description: Session runs retrieved successfully
          content:
            application/json:
              schema:
                type: array
                items:
                  anyOf:
                    - $ref: '#/components/schemas/RunSchema'
                    - $ref: '#/components/schemas/TeamRunSchema'
                    - $ref: '#/components/schemas/WorkflowRunSchema'
                title: Response Get Session Runs
              examples:
                completed_run:
                  summary: Example completed run
                  value:
                    run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                    parent_run_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                    agent_id: basic-agent
                    user_id: ''
                    run_input: Which tools do you have access to?
                    content: >-
                      I don't have access to external tools or the internet.
                      However, I can assist you with a wide range of topics by
                      providing information, answering questions, and offering
                      suggestions based on the knowledge I've been trained on.
                      If there's anything specific you need help with, feel free
                      to ask!
                    run_response_format: text
                    reasoning_content: ''
                    metrics:
                      input_tokens: 82
                      output_tokens: 56
                      total_tokens: 138
                      time_to_first_token: 0.047505500027909875
                      duration: 4.840060166025069
                    messages:
                      - content: >-
                          <additional_information>

                          - Use markdown to format your answers.

                          - The current time is 2025-09-08 17:52:10.101003.

                          </additional_information>


                          You have the capability to retain memories from
                          previous interactions with the user, but have not had
                          any interactions with the user yet.
                        from_history: false
                        stop_after_tool_call: false
                        role: system
                        created_at: 1757346730
                      - content: Which tools do you have access to?
                        from_history: false
                        stop_after_tool_call: false
                        role: user
                        created_at: 1757346730
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
                          input_tokens: 82
                          output_tokens: 56
                          total_tokens: 138
                        created_at: 1757346730
                    events:
                      - created_at: 1757346730
                        event: RunStarted
                        agent_id: basic-agent
                        agent_name: Basic Agent
                        run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                        session_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                        model: gpt-4o
                        model_provider: OpenAI
                      - created_at: 1757346733
                        event: MemoryUpdateStarted
                        agent_id: basic-agent
                        agent_name: Basic Agent
                        run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                        session_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                      - created_at: 1757346734
                        event: MemoryUpdateCompleted
                        agent_id: basic-agent
                        agent_name: Basic Agent
                        run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                        session_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                      - created_at: 1757346734
                        event: RunCompleted
                        agent_id: basic-agent
                        agent_name: Basic Agent
                        run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                        session_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                        content: >-
                          I don't have access to external tools or the internet.
                          However, I can assist you with a wide range of topics
                          by providing information, answering questions, and
                          offering suggestions based on the knowledge I've been
                          trained on. If there's anything specific you need help
                          with, feel free to ask!
                        content_type: str
                        metrics:
                          input_tokens: 82
                          output_tokens: 56
                          total_tokens: 138
                          time_to_first_token: 0.047505500027909875
                          duration: 4.840060166025069
                    created_at: '2025-09-08T15:52:10Z'
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
          description: Session not found or has no runs
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/NotFoundResponse'
        '422':
          description: Invalid session type
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
    RunSchema:
      properties:
        run_id:
          type: string
          title: Run Id
          description: Unique identifier for the run
        parent_run_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Parent Run Id
          description: Parent run ID if this is a nested run
        agent_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Agent Id
          description: Agent ID that executed this run
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the run
        run_input:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Input
          description: Input provided to the run
        content:
          anyOf:
            - type: string
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Content
          description: Output content from the run
        run_response_format:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Response Format
          description: Format of the response (text/json)
        reasoning_content:
          anyOf:
            - type: string
            - type: 'null'
          title: Reasoning Content
          description: Reasoning content if reasoning was enabled
        reasoning_steps:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Steps
          description: List of reasoning steps
        metrics:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metrics
          description: Performance and usage metrics
        messages:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Messages
          description: Message history for the run
        tools:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Tools
          description: Tools used in the run
        events:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Events
          description: Events generated during the run
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Run creation timestamp
        references:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: References
          description: References cited in the run
        citations:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Citations
          description: Citations from the model (e.g., from Gemini grounding/search)
        reasoning_messages:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Messages
          description: Reasoning process messages
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Session state at the end of the run
        images:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Images
          description: Images included in the run
        videos:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Videos
          description: Videos included in the run
        audio:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Audio
          description: Audio files included in the run
        files:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Files
          description: Files included in the run
        response_audio:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Response Audio
          description: Audio response if generated
        input_media:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Input Media
          description: Input media attachments
      type: object
      required:
        - run_id
      title: RunSchema
    TeamRunSchema:
      properties:
        run_id:
          type: string
          title: Run Id
          description: Unique identifier for the team run
        parent_run_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Parent Run Id
          description: Parent run ID if this is a nested run
        team_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Team Id
          description: Team ID that executed this run
        content:
          anyOf:
            - type: string
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Content
          description: Output content from the team run
        reasoning_content:
          anyOf:
            - type: string
            - type: 'null'
          title: Reasoning Content
          description: Reasoning content if reasoning was enabled
        reasoning_steps:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Steps
          description: List of reasoning steps
        run_input:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Input
          description: Input provided to the run
        run_response_format:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Response Format
          description: Format of the response (text/json)
        metrics:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metrics
          description: Performance and usage metrics
        tools:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Tools
          description: Tools used in the run
        messages:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Messages
          description: Message history for the run
        events:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Events
          description: Events generated during the run
        created_at:
          anyOf:
            - type: string
              format: date-time
            - type: 'null'
          title: Created At
          description: Run creation timestamp
        references:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: References
          description: References cited in the run
        citations:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Citations
          description: Citations from the model (e.g., from Gemini grounding/search)
        reasoning_messages:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Messages
          description: Reasoning process messages
        session_state:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Session State
          description: Session state at the end of the run
        input_media:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Input Media
          description: Input media attachments
        images:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Images
          description: Images included in the run
        videos:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Videos
          description: Videos included in the run
        audio:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Audio
          description: Audio files included in the run
        files:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Files
          description: Files included in the run
        response_audio:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Response Audio
          description: Audio response if generated
      type: object
      required:
        - run_id
      title: TeamRunSchema
    WorkflowRunSchema:
      properties:
        run_id:
          type: string
          title: Run Id
          description: Unique identifier for the workflow run
        run_input:
          anyOf:
            - type: string
            - type: 'null'
          title: Run Input
          description: Input provided to the workflow
        events:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Events
          description: Events generated during the workflow
        workflow_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Workflow Id
          description: Workflow ID that was executed
        user_id:
          anyOf:
            - type: string
            - type: 'null'
          title: User Id
          description: User ID associated with the run
        content:
          anyOf:
            - type: string
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Content
          description: Output content from the workflow
        content_type:
          anyOf:
            - type: string
            - type: 'null'
          title: Content Type
          description: Type of content returned
        status:
          anyOf:
            - type: string
            - type: 'null'
          title: Status
          description: Status of the workflow run
        step_results:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Step Results
          description: Results from each workflow step
        step_executor_runs:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Step Executor Runs
          description: Executor runs for each step
        metrics:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metrics
          description: Performance and usage metrics
        created_at:
          anyOf:
            - type: integer
            - type: 'null'
          title: Created At
          description: Unix timestamp of run creation
        reasoning_content:
          anyOf:
            - type: string
            - type: 'null'
          title: Reasoning Content
          description: Reasoning content if reasoning was enabled
        reasoning_steps:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Steps
          description: List of reasoning steps
        references:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: References
          description: References cited in the workflow
        citations:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Citations
          description: Citations from the model (e.g., from Gemini grounding/search)
        reasoning_messages:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Reasoning Messages
          description: Reasoning process messages
        images:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Images
          description: Images included in the workflow
        videos:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Videos
          description: Videos included in the workflow
        audio:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Audio
          description: Audio files included in the workflow
        files:
          anyOf:
            - items:
                additionalProperties: true
                type: object
              type: array
            - type: 'null'
          title: Files
          description: Files included in the workflow
        response_audio:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Response Audio
          description: Audio response if generated
      type: object
      required:
        - run_id
      title: WorkflowRunSchema
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