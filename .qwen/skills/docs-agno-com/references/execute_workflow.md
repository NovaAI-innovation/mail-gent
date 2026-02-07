# Execute Workflow

**Source:** https://docs.agno.com/reference-api/schema/workflows/execute-workflow.md
**Section:** Docs

**Description:** Execute a workflow with the provided input data. Workflows can run in streaming or batch mode.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Execute Workflow

> Execute a workflow with the provided input data. Workflows can run in streaming or batch mode.

**Execution Modes:**
- **Streaming (`stream=true`)**: Real-time step-by-step execution updates via SSE
- **Non-Streaming (`stream=false`)**: Complete workflow execution with final result

**Workflow Execution Process:**
1. Input validation against workflow schema
2. Sequential or parallel step execution based on workflow design
3. Data flow between steps with transformation
4. Error handling and automatic retries where configured
5. Final result compilation and response

**Session Management:**
Workflows support session continuity for stateful execution across multiple runs.



## OpenAPI

````yaml post /workflows/{workflow_id}/runs
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /workflows/{workflow_id}/runs:
    post:
      tags:
        - Workflows
      summary: Execute Workflow
      description: >-
        Execute a workflow with the provided input data. Workflows can run in
        streaming or batch mode.


        **Execution Modes:**

        - **Streaming (`stream=true`)**: Real-time step-by-step execution
        updates via SSE

        - **Non-Streaming (`stream=false`)**: Complete workflow execution with
        final result


        **Workflow Execution Process:**

        1. Input validation against workflow schema

        2. Sequential or parallel step execution based on workflow design

        3. Data flow between steps with transformation

        4. Error handling and automatic retries where configured

        5. Final result compilation and response


        **Session Management:**

        Workflows support session continuity for stateful execution across
        multiple runs.
      operationId: create_workflow_run
      parameters:
        - name: workflow_id
          in: path
          required: true
          schema:
            type: string
            title: Workflow Id
      requestBody:
        required: true
        content:
          application/x-www-form-urlencoded:
            schema:
              $ref: '#/components/schemas/Body_create_workflow_run'
      responses:
        '200':
          description: Workflow executed successfully
          content:
            application/json:
              schema: {}
            text/event-stream:
              example: |+
                event: RunStarted
                data: {"content": "Hello!", "run_id": "123..."}

        '400':
          description: Invalid input data or workflow configuration
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
          description: Workflow not found
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
          description: Workflow execution error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/InternalServerErrorResponse'
      security:
        - HTTPBearer: []
components:
  schemas:
    Body_create_workflow_run:
      properties:
        message:
          type: string
          title: Message
        stream:
          type: boolean
          title: Stream
          default: true
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
      type: object
      required:
        - message
      title: Body_create_workflow_run
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