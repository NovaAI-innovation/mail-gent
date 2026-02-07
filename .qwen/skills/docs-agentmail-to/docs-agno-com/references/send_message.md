# Send Message

**Source:** https://docs.agno.com/reference-api/schema/a2a/send-message.md
**Section:** Docs

**Description:** [DEPRECATED] Send a message to an Agno Agent, Team, or Workflow. The Agent, Team or Workflow is identified via the 'agentId' field in params.message or X-Agent-ID header. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Send Message

> [DEPRECATED] Send a message to an Agno Agent, Team, or Workflow. The Agent, Team or Workflow is identified via the 'agentId' field in params.message or X-Agent-ID header. Optional: Pass user ID via X-User-ID header (recommended) or 'userId' in params.message.metadata.



## OpenAPI

````yaml post /a2a/message/send
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /a2a/message/send:
    post:
      tags:
        - A2A
      summary: Send Message
      description: >-
        [DEPRECATED] Send a message to an Agno Agent, Team, or Workflow. The
        Agent, Team or Workflow is identified via the 'agentId' field in
        params.message or X-Agent-ID header. Optional: Pass user ID via
        X-User-ID header (recommended) or 'userId' in params.message.metadata.
      operationId: send_message
      responses:
        '200':
          description: Message sent successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/SendMessageSuccessResponse'
              example:
                jsonrpc: '2.0'
                id: request-123
                result:
                  task:
                    id: task-456
                    context_id: context-789
                    status: completed
                    history:
                      - message_id: msg-1
                        role: agent
                        parts:
                          - kind: text
                            text: Response from agent
        '400':
          description: Invalid request or unsupported method
        '404':
          description: Agent, Team, or Workflow not found
components:
  schemas:
    SendMessageSuccessResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: integer
            - type: 'null'
          title: Id
        jsonrpc:
          type: string
          const: '2.0'
          title: Jsonrpc
          default: '2.0'
        result:
          anyOf:
            - $ref: '#/components/schemas/Task'
            - $ref: '#/components/schemas/Message'
          title: Result
      type: object
      required:
        - result
      title: SendMessageSuccessResponse
      description: Represents a successful JSON-RPC response for the `message/send` method.
    Task:
      properties:
        artifacts:
          anyOf:
            - items:
                $ref: '#/components/schemas/Artifact'
              type: array
            - type: 'null'
          title: Artifacts
        contextId:
          type: string
          title: Contextid
        history:
          anyOf:
            - items:
                $ref: '#/components/schemas/Message'
              type: array
            - type: 'null'
          title: History
        id:
          type: string
          title: Id
        kind:
          type: string
          const: task
          title: Kind
          default: task
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        status:
          $ref: '#/components/schemas/TaskStatus'
      type: object
      required:
        - contextId
        - id
        - status
      title: Task
      description: >-
        Represents a single, stateful operation or conversation between a client
        and an agent.
    Message:
      properties:
        contextId:
          anyOf:
            - type: string
            - type: 'null'
          title: Contextid
        extensions:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Extensions
        kind:
          type: string
          const: message
          title: Kind
          default: message
        messageId:
          type: string
          title: Messageid
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        parts:
          items:
            $ref: '#/components/schemas/Part'
          type: array
          title: Parts
        referenceTaskIds:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Referencetaskids
        role:
          $ref: '#/components/schemas/Role'
        taskId:
          anyOf:
            - type: string
            - type: 'null'
          title: Taskid
      type: object
      required:
        - messageId
        - parts
        - role
      title: Message
      description: >-
        Represents a single message in the conversation between a user and an
        agent.
    Artifact:
      properties:
        artifactId:
          type: string
          title: Artifactid
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
        extensions:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Extensions
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        parts:
          items:
            $ref: '#/components/schemas/Part'
          type: array
          title: Parts
      type: object
      required:
        - artifactId
        - parts
      title: Artifact
      description: >-
        Represents a file, data structure, or other resource generated by an
        agent during a task.
    TaskStatus:
      properties:
        message:
          anyOf:
            - $ref: '#/components/schemas/Message'
            - type: 'null'
        state:
          $ref: '#/components/schemas/TaskState'
        timestamp:
          anyOf:
            - type: string
            - type: 'null'
          title: Timestamp
          examples:
            - '2023-10-27T10:00:00Z'
      type: object
      required:
        - state
      title: TaskStatus
      description: Represents the status of a task at a specific point in time.
    Part:
      anyOf:
        - $ref: '#/components/schemas/TextPart'
        - $ref: '#/components/schemas/FilePart'
        - $ref: '#/components/schemas/DataPart'
      title: Part
    Role:
      type: string
      enum:
        - agent
        - user
      title: Role
      description: >-
        Identifies the sender of the message. `user` for the client, `agent` for
        the service.
    TaskState:
      type: string
      enum:
        - submitted
        - working
        - input-required
        - completed
        - canceled
        - failed
        - rejected
        - auth-required
        - unknown
      title: TaskState
      description: Defines the lifecycle states of a Task.
    TextPart:
      properties:
        kind:
          type: string
          const: text
          title: Kind
          default: text
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
        text:
          type: string
          title: Text
      type: object
      required:
        - text
      title: TextPart
      description: Represents a text segment within a message or artifact.
    FilePart:
      properties:
        file:
          anyOf:
            - $ref: '#/components/schemas/FileWithBytes'
            - $ref: '#/components/schemas/FileWithUri'
          title: File
        kind:
          type: string
          const: file
          title: Kind
          default: file
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
      type: object
      required:
        - file
      title: FilePart
      description: >-
        Represents a file segment within a message or artifact. The file content
        can be

        provided either directly as bytes or as a URI.
    DataPart:
      properties:
        data:
          additionalProperties: true
          type: object
          title: Data
        kind:
          type: string
          const: data
          title: Kind
          default: data
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
      type: object
      required:
        - data
      title: DataPart
      description: >-
        Represents a structured data segment (e.g., JSON) within a message or
        artifact.
    FileWithBytes:
      properties:
        bytes:
          type: string
          title: Bytes
        mimeType:
          anyOf:
            - type: string
            - type: 'null'
          title: Mimetype
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
      type: object
      required:
        - bytes
      title: FileWithBytes
      description: >-
        Represents a file with its content provided directly as a base64-encoded
        string.
    FileWithUri:
      properties:
        mimeType:
          anyOf:
            - type: string
            - type: 'null'
          title: Mimetype
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        uri:
          type: string
          title: Uri
      type: object
      required:
        - uri
      title: FileWithUri
      description: Represents a file with its content located at a specific URI.

````