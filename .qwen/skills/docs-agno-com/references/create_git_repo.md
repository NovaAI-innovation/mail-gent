# Create Git Repo

**Source:** https://docs.agno.com/production/aws/git-repo.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Create Git Repo

Create a git repository to share your application with your team.

<Steps>
  <Step title="Create a git repository">
    Create a new [git repository](https://github.com/new).
  </Step>

  <Step title="Push your code">
    Push your code to the git repository.

    ```bash terminal theme={null}
    git init
    git add .
    git commit -m "Init LLM App"
    git branch -M main
    git remote add origin https://github.com/[YOUR_GIT_REPO].git
    git push -u origin main
    ```
  </Step>

  <Step title="Ask your team to join">
    Ask your team to follow the [setup steps for new users](/templates/infra-management/new-users) to use this workspace.
  </Step>
</Steps>
