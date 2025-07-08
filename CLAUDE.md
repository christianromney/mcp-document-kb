# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`mcp-document-kb` is a Clojure-based project that provides semantic search capabilities for Emacs org-mode notes. It integrates with local Ollama embedding models and a Qdrant vector database to enable semantic search beyond simple pattern matching. These capabilities should be exposed as an MCP (Model Context Protocol) server to enable any tool-capable LLM to consult the knowledgebase.

## Development Commands

### Testing
```bash
# Run all tests
clojure -M:test -m cognitect.test-runner

# Run tests via build script
clojure -T:build test
```

### Building
```bash
# Build uberjar
clojure -T:build ci

# Clean build artifacts
rm -rf target/
```

### Running
```bash
# Run via main function
clojure -M:run-m

# Run with exec function
clojure -X:run-x

# Run with custom name
clojure -M:run-m "YourName"
```

### REPL Development
```bash
# Start REPL with test dependencies
clojure -M:test

# Start REPL with all aliases
clojure -M:test:build
```

## Architecture

The system follows a layered architecture:

1. **Note Ingestion Layer**: Processes Emacs org-mode files
2. **Embedding Layer**: Integrates with local Ollama models for vector generation
3. **Vector Storage**: Uses Qdrant for semantic search indexing
4. **MCP Server Layer**: Exposes JSON-RPC 2.0 API over HTTP with Server-Sent Events

### Key Components

- **Core Namespace**: `christianromney.mcp-document-kb` - Main application logic
- **Build System**: `build.clj` - Contains CI pipeline and build tasks
- **Configuration**: `deps.edn` - Dependency management and aliases

### External Dependencies

- **Qdrant**: Local vector database for semantic search
- **Ollama**: Local embedding model management
- **Clojure**: Core runtime (v1.12.0)
- **tools.build**: Build automation

## Code Structure

The codebase is currently in early development with:
- Minimal core functionality in `src/christianromney/mcp_document_kb.clj`
- Test scaffold in `test/christianromney/mcp_document_kb_test.clj`
- Build configuration in `build.clj`
- Dependencies in `deps.edn`

## Development Notes

- The project uses Clojure 1.12.0
- Tests use `clojure.test` and `test.check` for property-based testing
- Documentation lives in the `docs` folder and should be written in org-mode format.
  - The `docs/claude-plan.org` file contains a high-level architectural plan for this system. 
  - The `docs/architecture.org` file should summarize the system architecture and follow the conventions in `docs/templates/architecture.org`.
- Always ensure org-tangle works and that output directories exist.
- Diagrams should use Mermaid syntax and be output as PNG. 
- The system is designed to run locally for privacy and cost benefits.
