# Install & Setup

**Source:** https://docs.agno.com/production/aws/install.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Install & Setup

## Install Agno

We highly recommend:

* Installing `agno` using `pip` in a python virtual environment.
* Creating an `ai` directory for your ai infra

<Steps>
  <Step title="Create a virtual environment">
    Open the `Terminal` and create an `ai` directory with a python virtual environment.

    <CodeGroup>
      ```bash Mac theme={null}
      mkdir ai && cd ai

      python3 -m venv aienv
      source aienv/bin/activate
      ```

      ```bash Windows theme={null}
      mkdir ai; cd ai

      python3 -m venv aienv
      aienv/scripts/activate
      ```
    </CodeGroup>
  </Step>

  <Step title="Install Agno">
    Install `agno` using pip

    <CodeGroup>
      ```bash Mac theme={null}
      pip install -U agno
      ```

      ```bash Windows theme={null}
      pip install -U agno
      ```
    </CodeGroup>
  </Step>

  <Step title="Install Docker">
    Install [docker desktop](https://docs.docker.com/desktop/install/mac-install/) to run apps locally
  </Step>
</Steps>

<br />

<Note>
  If you encounter errors, try updating pip using `python -m pip install --upgrade pip`
</Note>

***

## Upgrade Agno

To upgrade `agno`, run this in your virtual environment

```bash  theme={null}
pip install -U agno --no-cache-dir
```
