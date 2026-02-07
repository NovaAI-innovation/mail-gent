# Format & Validate

**Source:** https://docs.agno.com/production/aws/format-and-validate.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Format & Validate

## Format

Formatting the codebase using a set standard saves us time and mental energy. Agno templates are pre-configured with [ruff](https://docs.astral.sh/ruff/) that you can run using a helper script or directly.

<CodeGroup>
  ```bash terminal theme={null}
  ./scripts/format.sh
  ```

  ```bash ruff theme={null}
  ruff format .
  ```
</CodeGroup>

## Validate

Linting and Type Checking add an extra layer of protection to the codebase. We highly recommending running the validate script before pushing any changes.

Agno templates are pre-configured with [ruff](https://docs.astral.sh/ruff/) and [mypy](https://mypy.readthedocs.io/en/stable/) that you can run using a helper script or directly. Checkout the `pyproject.toml` file for the configuration.

<CodeGroup>
  ```bash terminal theme={null}
  ./scripts/validate.sh
  ```

  ```bash ruff theme={null}
  ruff check .
  ```

  ```bash mypy theme={null}
  mypy .
  ```
</CodeGroup>
