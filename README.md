# mcp-document-kb

An [MCP server](https://modelcontextprotocol.io) for semantic search of a
knowledge base built from a local collection of notes.

## Motivation

I take notes nearly every day. I want to use my notes as a "second brain,"
allowing me to instantly recall things I've written in the past and relevant
related content.

I create these notes using Emacs [org-mode](https://orgmode.org/) and
[org-roam](https://www.orgroam.com/). While these tools have some great
features, they notably lack a powerful search facility, providing only a simple
pattern matching search via [grep](https://man7.org/linux/man-pages/man1/grep.1.html) or
[ripgrep](https://github.com/BurntSushi/ripgrep). In the age of vector databases and [powerful embedding models](https://ollama.com/library/mxbai-embed-large), we can do better.


Such a system should support the following use-cases and capabilities:

- I want to find notes I've written based on semantic search. A search for "AI"
  should find notes about "LLMs", for example. This search should return the
  most relevant document fragments related to my query, along with important
  metadata like file path and last-modified timestamp. 
- These results will often be given as context to an LLM for summarization or citation.
- I want to extract the main semantic topics or concepts from a note to support
  the construction, visualization, and traversal of a knowledge graph.
- I want the cost, privacy and security benefits of a local knowledge base
  without a lots of required maintenance.
- I want knowledge to be automatically added, updated, deleted, or linked to
  other knowledge in the knowledgebase whenever a source note document is added,
  modified, or deleted, as appropriate.

## Technology Choices

- I want the system to be written in Clojure, because I value its power,
  elegance, and simplicity.
- I want to use a local [qdrant](https://qdrant.tech/) database to
  provide search vector.
- I want to expose these capabilities to tool-capable LLMs as an MCP server.
- using [JSON-RPC 2.0](https://www.jsonrpc.org/specification) over an HTTP
  transport layer with Server-Sent Events for streaming. 
- I want to use local LLMs like gemma3n and local embedding models via Ollama.
- I prefer documentation to be written in org-mode whenever possible.
- Diagrams should be written as [mermaid](mermaid.js.org) source code and
  embedded as source blocks in org-mode documents.

## Documentation

- README documentation should follow this [architectural briefing format](docs/templates/architecture.org).
- All Clojure code should have good docstrings favoring usage semantics over
  mechanics. Clojure's own docstrings are the best example.

## License

Copyright © 2025 Christian Romney. Distributed under the [Eclipse Public License v1.0](LICENSE.md).

