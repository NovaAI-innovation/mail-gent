# Semantic Chunking

**Source:** https://docs.agno.com/reference/knowledge/chunking/semantic.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Semantic Chunking

Semantic chunking is a method of splitting documents into smaller chunks by analyzing semantic similarity between text segments using embeddings.
It uses the chonkie library to identify natural breakpoints where the semantic meaning changes significantly, based on a configurable similarity threshold.
This helps preserve context and meaning better than fixed-size chunking by ensuring semantically related content stays together in the same chunk, while splitting occurs at meaningful topic transitions.

<Snippet file="chunking-semantic.mdx" />
