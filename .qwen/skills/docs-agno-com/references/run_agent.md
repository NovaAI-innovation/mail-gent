# Run Agent

**Source:** https://docs.agno.com/reference-api/schema/agui/run-agent.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Run Agent



## OpenAPI

````yaml post /agui
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /agui:
    post:
      tags:
        - AGUI
      summary: Run Agent
      operationId: run_agent_agui_post
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RunAgentInput'
        required: true
      responses:
        '200':
          description: Successful Response
          content:
            application/json:
              schema: {}
        '422':
          description: Validation Error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/HTTPValidationError'
components:
  schemas:
    RunAgentInput:
      properties:
        threadId:
          type: string
          title: Threadid
        runId:
          type: string
          title: Runid
        state:
          title: State
        messages:
          items:
            oneOf:
              - $ref: '#/components/schemas/DeveloperMessage'
              - $ref: '#/components/schemas/SystemMessage'
              - $ref: '#/components/schemas/AssistantMessage'
              - $ref: '#/components/schemas/UserMessage'
              - $ref: '#/components/schemas/ToolMessage'
            discriminator:
              propertyName: role
              mapping:
                assistant: '#/components/schemas/AssistantMessage'
                developer: '#/components/schemas/DeveloperMessage'
                system: '#/components/schemas/SystemMessage'
                tool: '#/components/schemas/ToolMessage'
                user: '#/components/schemas/UserMessage'
          type: array
          title: Messages
        tools:
          items:
            $ref: '#/components/schemas/Tool'
          type: array
          title: Tools
        context:
          items:
            $ref: '#/components/schemas/Context'
          type: array
          title: Context
        forwardedProps:
          title: Forwardedprops
      additionalProperties: false
      type: object
      required:
        - threadId
        - runId
        - state
        - messages
        - tools
        - context
        - forwardedProps
      title: RunAgentInput
      description: Input for running an agent.
    HTTPValidationError:
      properties:
        detail:
          items:
            $ref: '#/components/schemas/ValidationError'
          type: array
          title: Detail
      type: object
      title: HTTPValidationError
    DeveloperMessage:
      properties:
        id:
          type: string
          title: Id
        role:
          type: string
          const: developer
          title: Role
        content:
          type: string
          title: Content
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
      additionalProperties: false
      type: object
      required:
        - id
        - role
        - content
      title: DeveloperMessage
      description: A developer message.
    SystemMessage:
      properties:
        id:
          type: string
          title: Id
        role:
          type: string
          const: system
          title: Role
        content:
          type: string
          title: Content
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
      additionalProperties: false
      type: object
      required:
        - id
        - role
        - content
      title: SystemMessage
      description: A system message.
    AssistantMessage:
      properties:
        id:
          type: string
          title: Id
        role:
          type: string
          const: assistant
          title: Role
        content:
          anyOf:
            - type: string
            - type: 'null'
          title: Content
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        toolCalls:
          anyOf:
            - items:
                $ref: '#/components/schemas/ToolCall'
              type: array
            - type: 'null'
          title: Toolcalls
      additionalProperties: false
      type: object
      required:
        - id
        - role
      title: AssistantMessage
      description: An assistant message.
    UserMessage:
      properties:
        id:
          type: string
          title: Id
        role:
          type: string
          const: user
          title: Role
        content:
          type: string
          title: Content
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
      additionalProperties: false
      type: object
      required:
        - id
        - role
        - content
      title: UserMessage
      description: A user message.
    ToolMessage:
      properties:
        id:
          type: string
          title: Id
        role:
          type: string
          const: tool
          title: Role
        content:
          type: string
          title: Content
        toolCallId:
          type: string
          title: Toolcallid
      additionalProperties: false
      type: object
      required:
        - id
        - role
        - content
        - toolCallId
      title: ToolMessage
      description: A tool result message.
    Tool:
      properties:
        name:
          type: string
          title: Name
        description:
          type: string
          title: Description
        parameters:
          title: Parameters
      additionalProperties: false
      type: object
      required:
        - name
        - description
        - parameters
      title: Tool
      description: A tool definition.
    Context:
      properties:
        description:
          type: string
          title: Description
        value:
          type: string
          title: Value
      additionalProperties: false
      type: object
      required:
        - description
        - value
      title: Context
      description: Additional context for the agent.
    ValidationError:
      properties:
        loc:
          items:
            anyOf:
              - type: string
              - type: integer
          type: array
          title: Location
        msg:
          type: string
          title: Message
        type:
          type: string
          title: Error Type
      type: object
      required:
        - loc
        - msg
        - type
      title: ValidationError
    ToolCall:
      properties:
        id:
          type: string
          title: Id
        type:
          type: string
          const: function
          title: Type
        function:
          $ref: '#/components/schemas/FunctionCall'
      additionalProperties: false
      type: object
      required:
        - id
        - type
        - function
      title: ToolCall
      description: A tool call, modelled after OpenAI tool calls.
    FunctionCall:
      properties:
        name:
          type: string
          title: Name
        arguments:
          type: string
          title: Arguments
      additionalProperties: false
      type: object
      required:
        - name
        - arguments
      title: FunctionCall
      description: Name and arguments of a function call.

````