# Get Run by ID

**Source:** https://docs.agno.com/reference-api/schema/sessions/get-run-by-id.md
**Section:** Docs

**Description:** Retrieve a specific run by its ID from a session. Response schema varies based on the run type (agent run, team run, or workflow run).

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Run by ID

> Retrieve a specific run by its ID from a session. Response schema varies based on the run type (agent run, team run, or workflow run).



## OpenAPI

````yaml get /sessions/{session_id}/runs/{run_id}
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /sessions/{session_id}/runs/{run_id}:
    get:
      tags:
        - Sessions
      summary: Get Run by ID
      description: >-
        Retrieve a specific run by its ID from a session. Response schema varies
        based on the run type (agent run, team run, or workflow run).
      operationId: get_session_run
      parameters:
        - name: session_id
          in: path
          required: true
          schema:
            type: string
            description: Session ID to get run from
            title: Session Id
          description: Session ID to get run from
        - name: run_id
          in: path
          required: true
          schema:
            type: string
            description: Run ID to retrieve
            title: Run Id
          description: Run ID to retrieve
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
            description: User ID to query run from
            title: User Id
          description: User ID to query run from
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: Database ID to query run from
            title: Db Id
          description: Database ID to query run from
      responses:
        '200':
          description: Run retrieved successfully
          content:
            application/json:
              schema:
                anyOf:
                  - $ref: '#/components/schemas/RunSchema'
                  - $ref: '#/components/schemas/TeamRunSchema'
                  - $ref: '#/components/schemas/WorkflowRunSchema'
                title: Response Get Session Run
              examples:
                agent_run:
                  summary: Example agent run
                  value:
                    run_id: fcdf50f0-7c32-4593-b2ef-68a558774340
                    parent_run_id: 80056af0-c7a5-4d69-b6a2-c3eba9f040e0
                    agent_id: basic-agent
                    user_id: user_123
                    run_input: Which tools do you have access to?
                    content: I don't have access to external tools.
                    created_at: 1728499200
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
          description: Session or run not found
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