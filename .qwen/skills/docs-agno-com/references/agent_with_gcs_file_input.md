# Agent with GCS File Input

**Source:** https://docs.agno.com/models/providers/native/google/usage/gcs-file-input.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Agent with GCS File Input

## Code

```python cookbook/11_models/google/gemini/gcs_file_input.py theme={null}
"""GCS file input with Gemini.

Pass files directly from Google Cloud Storage (gs://) without downloading.
Supports files up to 2GB. Requires Vertex AI authentication.
"""

from agno.agent import Agent
from agno.media import File
from agno.models.google import Gemini

agent = Agent(
    model=Gemini(
        id="gemini-2.0-flash",
        vertexai=True,
    ),
    markdown=True,
)

agent.print_response(
    "Summarize this document and extract key insights.",
    files=[
        File(
            url="gs://cloud-samples-data/generative-ai/pdf/2312.11805v3.pdf",
            mime_type="application/pdf",
        )
    ],
)
```

## Usage

<Steps>
  <Snippet file="create-venv-step.mdx" />

  <Step title="Set up Vertex AI">
    ```bash  theme={null}
    gcloud auth application-default login
    export GOOGLE_CLOUD_PROJECT="your-project-id"
    export GOOGLE_CLOUD_LOCATION="us-central1"
    ```
  </Step>

  <Step title="Install dependencies">
    ```bash  theme={null}
    pip install -U google-genai agno
    ```
  </Step>

  <Step title="Run Agent">
    ```bash  theme={null}
    python cookbook/11_models/google/gemini/gcs_file_input.py
    ```
  </Step>
</Steps>
