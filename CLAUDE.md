# AI‑Document‑Studio

## Project Overview
The **AI‑Document‑Studio** is a learning project that demonstrates how to build an AI‑powered document processing application using the following stack:
- **Front‑end**: React + TypeScript (Vite)
- **Back‑end**: Express + TypeScript (Node.js)
- **AI**: Ollama local server exposing the `gpt-oss:20b` model
- **Testing**: Vitest (Jest‑compatible, focused on unit/feature tests)

The goal is to learn best practices in software architecture, code quality, and AI‑assisted engineering. The following document outlines the *architecture* and *engineering rules* that govern the codebase.

---

## 1. Project Architecture
```
┌───────────────────────┐
│   Web Browser         │  ← React + Vite (client)
└─────┬─────────────────┘
      │
      ▼
┌───────────────────────┐
│  Node.js Server       │  ← Express + TS (API, file ingestion)
└─────┬─────────────────┘
      │
      ▼
┌───────────────────────┐
│  Ollama Local AI      │  ← gpt-oss:20b for all NLP tasks
└───────────────────────┘
```
* All business logic lives in the **Express** API.
* **React** consumes the API and displays the UI; data flows are strictly typed with TypeScript.
* **Ollama** runs locally; no external network calls are made to an LLM provider.
* **Vitest** runs unit tests for both the client and server.

## 2. Engineering Rules
1. **Commit Discipline** – Follow Conventional Commits (feat:, fix:, docs:, style:, refactor:, test:, chore:).
2. **CI / Lint** – Every PR must pass the lint‑and‑test pipeline (`npm test` + `npm run lint`).
3. **Code Reviews** – All PRs require at least one approving review *and* a run of the `frontend-reviewer` subagent on affected React/TS files.
4. **Type Safety** – `tsconfig.json` is set to `strict`, `noImplicitAny`, and `noUnusedLocals`.
5. **SOLID & Separation** – Code is organized into layers: domain → service → controller → routes. UI components are pure and stateless where possible.
6. **Testability** – Services expose interfaces for dependency injection; no global state or hidden side‑effects.
7. **Documentation** – All public APIs, utilities, and complex logic are documented in JSDoc comments.
8. **Subagents** – The project ships a read‑only `frontend-reviewer` subagent (see `./.claude/agents/frontend-reviewer.md`) that enforces the guidelines above.

## 3. Subagent Usage
- To run the React/TS reviewer on a folder:
  ```bash
  /run-agent frontend-reviewer src/components
  ```
- The agent returns a Markdown report following the format described in its file.

## 4. File‑Level Roles
- **`CLAUDE.md`** – Project architecture + engineering rules.
- **`coding-guidelines.md`** – Detailed coding conventions and testability practices.
- **`.claude/agents/frontend-reviewer.md`** – Read‑only custom agent for code reviews.

> **Note**: These files are part of the *engineering setup* and do not scaffold the application itself.

---

> **Purpose**: The `CLAUDE.md` file serves as the single source of truth for project structure, engineering conventions, and subagent usage. It guides developers and reviewers on how to interact with the codebase and enforce quality standards.
