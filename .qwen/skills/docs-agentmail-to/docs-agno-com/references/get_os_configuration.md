# Get OS Configuration

**Source:** https://docs.agno.com/reference-api/schema/core/get-os-configuration.md
**Section:** Docs

**Description:** Retrieve the complete configuration of the AgentOS instance, including:

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get OS Configuration

> Retrieve the complete configuration of the AgentOS instance, including:

- Available models and databases
- Registered agents, teams, and workflows
- Chat, session, memory, knowledge, and evaluation configurations
- Available interfaces and their routes



## OpenAPI

````yaml get /config
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /config:
    get:
      tags:
        - Core
      summary: Get OS Configuration
      description: |-
        Retrieve the complete configuration of the AgentOS instance, including:

        - Available models and databases
        - Registered agents, teams, and workflows
        - Chat, session, memory, knowledge, and evaluation configurations
        - Available interfaces and their routes
      operationId: get_config
      responses:
        '200':
          description: OS configuration retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ConfigResponse'
              example:
                id: demo
                description: Example AgentOS configuration
                available_models: []
                databases:
                  - 9c884dc4-9066-448c-9074-ef49ec7eb73c
                session:
                  dbs:
                    - db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                      domain_config:
                        display_name: Sessions
                metrics:
                  dbs:
                    - db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                      domain_config:
                        display_name: Metrics
                memory:
                  dbs:
                    - db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                      domain_config:
                        display_name: Memory
                knowledge:
                  dbs:
                    - db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                      domain_config:
                        display_name: Knowledge
                evals:
                  dbs:
                    - db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                      domain_config:
                        display_name: Evals
                agents:
                  - id: main-agent
                    name: Main Agent
                    db_id: 9c884dc4-9066-448c-9074-ef49ec7eb73c
                teams: []
                workflows: []
                interfaces: []
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
          description: Not Found
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
    ConfigResponse:
      properties:
        os_id:
          type: string
          title: Os Id
          description: Unique identifier for the OS instance
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the OS instance
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the OS instance
        available_models:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Available Models
          description: List of available models
        databases:
          items:
            type: string
          type: array
          title: Databases
          description: List of database IDs
        chat:
          anyOf:
            - $ref: '#/components/schemas/ChatConfig'
            - type: 'null'
          description: Chat configuration
        session:
          anyOf:
            - $ref: '#/components/schemas/SessionConfig'
            - type: 'null'
          description: Session configuration
        metrics:
          anyOf:
            - $ref: '#/components/schemas/MetricsConfig'
            - type: 'null'
          description: Metrics configuration
        memory:
          anyOf:
            - $ref: '#/components/schemas/MemoryConfig'
            - type: 'null'
          description: Memory configuration
        knowledge:
          anyOf:
            - $ref: '#/components/schemas/KnowledgeConfig'
            - type: 'null'
          description: Knowledge configuration
        evals:
          anyOf:
            - $ref: '#/components/schemas/EvalsConfig'
            - type: 'null'
          description: Evaluations configuration
        traces:
          anyOf:
            - $ref: '#/components/schemas/TracesConfig'
            - type: 'null'
          description: Traces configuration
        agents:
          items:
            $ref: '#/components/schemas/AgentSummaryResponse'
          type: array
          title: Agents
          description: List of registered agents
        teams:
          items:
            $ref: '#/components/schemas/TeamSummaryResponse'
          type: array
          title: Teams
          description: List of registered teams
        workflows:
          items:
            $ref: '#/components/schemas/WorkflowSummaryResponse'
          type: array
          title: Workflows
          description: List of registered workflows
        interfaces:
          items:
            $ref: '#/components/schemas/InterfaceResponse'
          type: array
          title: Interfaces
          description: List of available interfaces
      type: object
      required:
        - os_id
        - databases
        - agents
        - teams
        - workflows
        - interfaces
      title: ConfigResponse
      description: Response schema for the general config endpoint
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
    ChatConfig:
      properties:
        quick_prompts:
          additionalProperties:
            items:
              type: string
            type: array
          type: object
          title: Quick Prompts
      type: object
      required:
        - quick_prompts
      title: ChatConfig
      description: Configuration for the Chat page of the AgentOS
    SessionConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_SessionDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: SessionConfig
      description: Configuration for the Session domain of the AgentOS
    MetricsConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_MetricsDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: MetricsConfig
      description: Configuration for the Metrics domain of the AgentOS
    MemoryConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_MemoryDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: MemoryConfig
      description: Configuration for the Memory domain of the AgentOS
    KnowledgeConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_KnowledgeDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: KnowledgeConfig
      description: Configuration for the Knowledge domain of the AgentOS
    EvalsConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        available_models:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Available Models
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_EvalsDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: EvalsConfig
      description: Configuration for the Evals domain of the AgentOS
    TracesConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/DatabaseConfig_TracesDomainConfig_'
              type: array
            - type: 'null'
          title: Dbs
      type: object
      title: TracesConfig
      description: Configuration for the Traces domain of the AgentOS
    AgentSummaryResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
          description: Unique identifier for the agent
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the agent
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the agent
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: Database identifier
      type: object
      title: AgentSummaryResponse
    TeamSummaryResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
          description: Unique identifier for the team
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the team
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the team
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: Database identifier
      type: object
      title: TeamSummaryResponse
    WorkflowSummaryResponse:
      properties:
        id:
          anyOf:
            - type: string
            - type: 'null'
          title: Id
          description: Unique identifier for the workflow
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the workflow
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the workflow
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: Database identifier
      type: object
      title: WorkflowSummaryResponse
    InterfaceResponse:
      properties:
        type:
          type: string
          title: Type
          description: Type of the interface
        version:
          type: string
          title: Version
          description: Version of the interface
        route:
          type: string
          title: Route
          description: API route path
      type: object
      required:
        - type
        - version
        - route
      title: InterfaceResponse
    DatabaseConfig_SessionDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/SessionDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[SessionDomainConfig]
    DatabaseConfig_MetricsDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/MetricsDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[MetricsDomainConfig]
    DatabaseConfig_MemoryDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/MemoryDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[MemoryDomainConfig]
    DatabaseConfig_KnowledgeDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/KnowledgeDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[KnowledgeDomainConfig]
    DatabaseConfig_EvalsDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/EvalsDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[EvalsDomainConfig]
    DatabaseConfig_TracesDomainConfig_:
      properties:
        db_id:
          type: string
          title: Db Id
        domain_config:
          anyOf:
            - $ref: '#/components/schemas/TracesDomainConfig'
            - type: 'null'
        tables:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Tables
      type: object
      required:
        - db_id
      title: DatabaseConfig[TracesDomainConfig]
    SessionDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
      type: object
      title: SessionDomainConfig
      description: Configuration for the Session domain of the AgentOS
    MetricsDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
      type: object
      title: MetricsDomainConfig
      description: Configuration for the Metrics domain of the AgentOS
    MemoryDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
      type: object
      title: MemoryDomainConfig
      description: Configuration for the Memory domain of the AgentOS
    KnowledgeDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
      type: object
      title: KnowledgeDomainConfig
      description: Configuration for the Knowledge domain of the AgentOS
    EvalsDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
        available_models:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Available Models
      type: object
      title: EvalsDomainConfig
      description: Configuration for the Evals domain of the AgentOS
    TracesDomainConfig:
      properties:
        display_name:
          anyOf:
            - type: string
            - type: 'null'
          title: Display Name
      type: object
      title: TracesDomainConfig
      description: Configuration for the Traces domain of the AgentOS
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````