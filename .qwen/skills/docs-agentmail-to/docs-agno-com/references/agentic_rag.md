# Agentic RAG

**Source:** https://docs.agno.com/cookbook/streamlit/agentic-rag.md
**Section:** Docs

**Description:** Document Q&A with knowledge base, citations, and conversation memory.

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agentic RAG

> Document Q&A with knowledge base, citations, and conversation memory.

A sophisticated RAG (Retrieval Augmented Generation) system that leverages search of a knowledge base with LLMs to provide deep insights into the data.

## The agent can:

* Process and understand documents from multiple sources (PDFs, websites, text files)
* Build a searchable knowledge base using vector embeddings
* Maintain conversation context and memory across sessions
* Provide relevant citations and sources for its responses
* Generate summaries and extract key insights
* Answer follow-up questions and clarifications

## The agent uses:

* Vector similarity search for relevant document retrieval
* Conversation memory for contextual responses
* Citation tracking for source attribution
* Dynamic knowledge base updates

<video autoPlay muted controls className="w-full aspect-video" src="https://mintcdn.com/agno-v2/yeT29TzCG5roT0hQ/videos/agentic_rag.mp4?fit=max&auto=format&n=yeT29TzCG5roT0hQ&q=85&s=9a09224f674692a82548532f375a6b38" data-path="videos/agentic_rag.mp4" />

## Example queries to try:

* "What are the key points from this document?"
* "Can you summarize the main arguments and supporting evidence?"
* "What are the important statistics and findings?"
* "How does this relate to \[topic X]?"
* "What are the limitations or gaps in this analysis?"
* "Can you explain \[concept X] in more detail?"
* "What other sources support or contradict these claims?"

## Code

The complete code is available in the [Agno repository](https://github.com/agno-agi/agno).

## Usage

<Steps>
  <Step title="Clone the repository">
    ```bash  theme={null}
    git clone https://github.com/agno-agi/agno.git
    cd agno
    ```
  </Step>

  <Step title="Create virtual environment">
    ```bash  theme={null}
    python3 -m venv .venv
    source .venv/bin/activate
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    uv pip install -r cookbook/02_examples/streamlit_apps/agentic_rag/requirements.txt
    ```
  </Step>

  <Step title="Run PgVector">
    First, install [Docker Desktop](https://docs.docker.com/desktop/install/mac-install/).

    Then run either using the helper script:

    ```bash  theme={null}
    ./cookbook/scripts/run_pgvector.sh
    ```

    Or directly with Docker:

    ```bash  theme={null}
    docker run -d \
      -e POSTGRES_DB=ai \
      -e POSTGRES_USER=ai \
      -e POSTGRES_PASSWORD=ai \
      -e PGDATA=/var/lib/postgresql/data/pgdata \
      -v pgvolume:/var/lib/postgresql/data \
      -p 5532:5432 \
      --name pgvector \
      agnohq/pgvector:16
    ```
  </Step>

  <Step title="Set up API keys">
    ```bash  theme={null}
    # Required
    export OPENAI_API_KEY=***
    # Optional
    export ANTHROPIC_API_KEY=***
    export GOOGLE_API_KEY=***

    ```

    We recommend using gpt-5-mini for optimal performance.
  </Step>

  <Step title="Launch the app">
    ```bash  theme={null}
    streamlit run cookbook/02_examples/streamlit_apps/agentic_rag/app.py
    ```

    Open localhost:8501 to start using the Agentic RAG.
  </Step>
</Steps>

Need help? Join our [Discourse community](https://community.agno.com) for support!
