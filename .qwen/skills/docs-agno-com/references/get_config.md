# Get Config

**Source:** https://docs.agno.com/reference-api/schema/knowledge/get-config.md
**Section:** Docs

**Description:** Retrieve available readers, chunkers, and configuration options for content processing. This endpoint provides metadata about supported file types, processing strategies, and filters.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Get Config

> Retrieve available readers, chunkers, and configuration options for content processing. This endpoint provides metadata about supported file types, processing strategies, and filters.



## OpenAPI

````yaml get /knowledge/config
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/config:
    get:
      tags:
        - Knowledge
      summary: Get Config
      description: >-
        Retrieve available readers, chunkers, and configuration options for
        content processing. This endpoint provides metadata about supported file
        types, processing strategies, and filters.
      operationId: get_knowledge_config
      parameters:
        - name: db_id
          in: query
          required: false
          schema:
            anyOf:
              - type: string
              - type: 'null'
            description: The ID of the database to use
            title: Db Id
          description: The ID of the database to use
      responses:
        '200':
          description: Knowledge configuration retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ConfigResponseSchema'
              example:
                readers:
                  website:
                    id: website
                    name: WebsiteReader
                    description: Reads website files
                    chunkers:
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                      - FixedSizeChunker
                  firecrawl:
                    id: firecrawl
                    name: FirecrawlReader
                    description: Reads firecrawl files
                    chunkers:
                      - SemanticChunker
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                  youtube:
                    id: youtube
                    name: YoutubeReader
                    description: Reads youtube files
                    chunkers:
                      - RecursiveChunker
                      - AgenticChunker
                      - DocumentChunker
                      - SemanticChunker
                      - FixedSizeChunker
                  web_search:
                    id: web_search
                    name: WebSearchReader
                    description: Reads web_search files
                    chunkers:
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                      - FixedSizeChunker
                  arxiv:
                    id: arxiv
                    name: ArxivReader
                    description: Reads arxiv files
                    chunkers:
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                  csv:
                    id: csv
                    name: CsvReader
                    description: Reads csv files
                    chunkers:
                      - RowChunker
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                  docx:
                    id: docx
                    name: DocxReader
                    description: Reads docx files
                    chunkers:
                      - DocumentChunker
                      - FixedSizeChunker
                      - SemanticChunker
                      - AgenticChunker
                      - RecursiveChunker
                  gcs:
                    id: gcs
                    name: GcsReader
                    description: Reads gcs files
                    chunkers:
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                  json:
                    id: json
                    name: JsonReader
                    description: Reads json files
                    chunkers:
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                  markdown:
                    id: markdown
                    name: MarkdownReader
                    description: Reads markdown files
                    chunkers:
                      - MarkdownChunker
                      - DocumentChunker
                      - AgenticChunker
                      - RecursiveChunker
                      - SemanticChunker
                      - FixedSizeChunker
                  pdf:
                    id: pdf
                    name: PdfReader
                    description: Reads pdf files
                    chunkers:
                      - DocumentChunker
                      - FixedSizeChunker
                      - AgenticChunker
                      - SemanticChunker
                      - RecursiveChunker
                  text:
                    id: text
                    name: TextReader
                    description: Reads text files
                    chunkers:
                      - FixedSizeChunker
                      - AgenticChunker
                      - DocumentChunker
                      - RecursiveChunker
                      - SemanticChunker
                readersForType:
                  url:
                    - url
                    - website
                    - firecrawl
                    - youtube
                    - web_search
                    - gcs
                  youtube:
                    - youtube
                  text:
                    - web_search
                  topic:
                    - arxiv
                  file:
                    - csv
                    - gcs
                  .csv:
                    - csv
                  .xlsx:
                    - csv
                  .xls:
                    - csv
                  .docx:
                    - docx
                  .doc:
                    - docx
                  .json:
                    - json
                  .md:
                    - markdown
                  .pdf:
                    - pdf
                  .txt:
                    - text
                chunkers:
                  AgenticChunker:
                    key: AgenticChunker
                    name: AgenticChunker
                    description: >-
                      Chunking strategy that uses an LLM to determine natural
                      breakpoints in the text
                    metadata:
                      chunk_size: 5000
                  DocumentChunker:
                    key: DocumentChunker
                    name: DocumentChunker
                    description: >-
                      A chunking strategy that splits text based on document
                      structure like paragraphs and sections
                    metadata:
                      chunk_size: 5000
                      chunk_overlap: 0
                  FixedSizeChunker:
                    key: FixedSizeChunker
                    name: FixedSizeChunker
                    description: >-
                      Chunking strategy that splits text into fixed-size chunks
                      with optional overlap
                    metadata:
                      chunk_size: 5000
                      chunk_overlap: 0
                  MarkdownChunker:
                    key: MarkdownChunker
                    name: MarkdownChunker
                    description: >-
                      A chunking strategy that splits markdown based on
                      structure like headers, paragraphs and sections
                    metadata:
                      chunk_size: 5000
                      chunk_overlap: 0
                  RecursiveChunker:
                    key: RecursiveChunker
                    name: RecursiveChunker
                    description: >-
                      Chunking strategy that recursively splits text into chunks
                      by finding natural break points
                    metadata:
                      chunk_size: 5000
                      chunk_overlap: 0
                  RowChunker:
                    key: RowChunker
                    name: RowChunker
                    description: RowChunking chunking strategy
                    metadata: {}
                  SemanticChunker:
                    key: SemanticChunker
                    name: SemanticChunker
                    description: >-
                      Chunking strategy that splits text into semantic chunks
                      using chonkie
                    metadata:
                      chunk_size: 5000
                vector_dbs:
                  - id: vector_db_1
                    name: Vector DB 1
                    description: Vector DB 1 description
                    search_types:
                      - vector
                      - keyword
                      - hybrid
                filters:
                  - filter_tag_1
                  - filter_tag2
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
    ConfigResponseSchema:
      properties:
        readers:
          anyOf:
            - additionalProperties:
                $ref: '#/components/schemas/ReaderSchema'
              type: object
            - type: 'null'
          title: Readers
          description: Available content readers
        readersForType:
          anyOf:
            - additionalProperties:
                items:
                  type: string
                type: array
              type: object
            - type: 'null'
          title: Readersfortype
          description: Mapping of content types to reader IDs
        chunkers:
          anyOf:
            - additionalProperties:
                $ref: '#/components/schemas/ChunkerSchema'
              type: object
            - type: 'null'
          title: Chunkers
          description: Available chunking strategies
        filters:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Filters
          description: Available filter tags
        vector_dbs:
          anyOf:
            - items:
                $ref: '#/components/schemas/VectorDbSchema'
              type: array
            - type: 'null'
          title: Vector Dbs
          description: Configured vector databases
      type: object
      title: ConfigResponseSchema
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
    ReaderSchema:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the reader
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the reader
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the reader's capabilities
        chunkers:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Chunkers
          description: List of supported chunking strategies
      type: object
      required:
        - id
      title: ReaderSchema
    ChunkerSchema:
      properties:
        key:
          type: string
          title: Key
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
        metadata:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Metadata
      type: object
      required:
        - key
      title: ChunkerSchema
    VectorDbSchema:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the vector database
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the vector database
        description:
          anyOf:
            - type: string
            - type: 'null'
          title: Description
          description: Description of the vector database
        search_types:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Search Types
          description: List of supported search types (vector, keyword, hybrid)
      type: object
      required:
        - id
      title: VectorDbSchema
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````