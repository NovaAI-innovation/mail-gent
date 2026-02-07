# Code Chunking

**Source:** https://docs.agno.com/reference/knowledge/chunking/code.md
**Section:** Docs

---

> ## Documentation Index
> Fetch the complete documentation index at: https://docs.agno.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Code Chunking

Code chunking splits code based on its structure, leveraging Abstract Syntax Trees (ASTs) to create contextually relevant segments.
It uses the Chonkie library to identify natural code boundaries like functions, classes, and blocks.
This preserves code semantics better than fixed-size chunking by ensuring related code stays together in the same chunk, while splitting occurs at meaningful structural boundaries.

<Snippet file="chunking-code.mdx" />
