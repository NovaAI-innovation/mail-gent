# Search Knowledge

**Source:** https://docs.agno.com/reference-api/schema/knowledge/search-knowledge.md
**Section:** Docs

**Description:** Search the knowledge base for relevant documents using query, filters and search type.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Search Knowledge

> Search the knowledge base for relevant documents using query, filters and search type.



## OpenAPI

````yaml post /knowledge/search
openapi: 3.1.0
info:
  title: Agno AgentOS
  description: An agent operating system.
  version: 1.0.0
servers: []
security: []
paths:
  /knowledge/search:
    post:
      tags:
        - Knowledge
      summary: Search Knowledge
      description: >-
        Search the knowledge base for relevant documents using query, filters
        and search type.
      operationId: search_knowledge
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/VectorSearchRequestSchema'
        required: true
      responses:
        '200':
          description: Search results retrieved successfully
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PaginatedResponse_VectorSearchResult_'
              example:
                data:
                  - id: doc_123
                    content: >-
                      Jordan Mitchell - Software Engineer with skills in
                      JavaScript, React, Python
                    name: cv_1
                    meta_data:
                      page: 1
                      chunk: 1
                    usage:
                      total_tokens: 14
                    reranking_score: 0.95
                    content_id: content_456
                meta:
                  page: 1
                  limit: 20
                  total_pages: 2
                  total_count: 35
        '400':
          description: Invalid search parameters
        '401':
          description: Unauthorized
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UnauthenticatedResponse'
        '404':
          description: No documents found
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
    VectorSearchRequestSchema:
      properties:
        query:
          type: string
          title: Query
          description: The search query text
        db_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Db Id
          description: The content database ID to search in
        vector_db_ids:
          anyOf:
            - items:
                type: string
              type: array
            - type: 'null'
          title: Vector Db Ids
          description: List of vector database IDs to search in
        search_type:
          anyOf:
            - type: string
            - type: 'null'
          title: Search Type
          description: The type of search to perform (vector, keyword, hybrid)
        max_results:
          anyOf:
            - type: integer
              maximum: 1000
              minimum: 1
            - type: 'null'
          title: Max Results
          description: The maximum number of results to return
        filters:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Filters
          description: Filters to apply to the search results
        meta:
          anyOf:
            - $ref: '#/components/schemas/Meta'
            - type: 'null'
          description: >-
            Pagination metadata. Limit and page number to return a subset of
            results.
      type: object
      required:
        - query
      title: VectorSearchRequestSchema
      description: Schema for vector search request.
    PaginatedResponse_VectorSearchResult_:
      properties:
        data:
          items:
            $ref: '#/components/schemas/VectorSearchResult'
          type: array
          title: Data
          description: List of items for the current page
        meta:
          $ref: '#/components/schemas/PaginationInfo'
          description: Pagination metadata
      type: object
      required:
        - data
        - meta
      title: PaginatedResponse[VectorSearchResult]
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
    Meta:
      properties:
        limit:
          type: integer
          maximum: 100
          minimum: 1
          title: Limit
          description: Number of results per page
          default: 20
        page:
          type: integer
          minimum: 1
          title: Page
          description: Page number
          default: 1
      type: object
      title: Meta
      description: Inline metadata schema for pagination.
    VectorSearchResult:
      properties:
        id:
          type: string
          title: Id
          description: Unique identifier for the search result document
        content:
          type: string
          title: Content
          description: Content text of the document
        name:
          anyOf:
            - type: string
            - type: 'null'
          title: Name
          description: Name of the document
        meta_data:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Meta Data
          description: Metadata associated with the document
        usage:
          anyOf:
            - additionalProperties: true
              type: object
            - type: 'null'
          title: Usage
          description: Usage statistics (e.g., token counts)
        reranking_score:
          anyOf:
            - type: number
              maximum: 1
              minimum: 0
            - type: 'null'
          title: Reranking Score
          description: Reranking score for relevance
        content_id:
          anyOf:
            - type: string
            - type: 'null'
          title: Content Id
          description: ID of the source content
        content_origin:
          anyOf:
            - type: string
            - type: 'null'
          title: Content Origin
          description: Origin URL or source of the content
        size:
          anyOf:
            - type: integer
              minimum: 0
            - type: 'null'
          title: Size
          description: Size of the content in bytes
      type: object
      required:
        - id
        - content
      title: VectorSearchResult
      description: Schema for search result documents.
    PaginationInfo:
      properties:
        page:
          type: integer
          minimum: 0
          title: Page
          description: Current page number (0-indexed)
          default: 0
        limit:
          type: integer
          maximum: 100
          minimum: 1
          title: Limit
          description: Number of items per page
          default: 20
        total_pages:
          type: integer
          minimum: 0
          title: Total Pages
          description: Total number of pages
          default: 0
        total_count:
          type: integer
          minimum: 0
          title: Total Count
          description: Total count of items
          default: 0
        search_time_ms:
          type: number
          minimum: 0
          title: Search Time Ms
          description: Search execution time in milliseconds
          default: 0
      type: object
      title: PaginationInfo
  securitySchemes:
    HTTPBearer:
      type: http
      scheme: bearer

````