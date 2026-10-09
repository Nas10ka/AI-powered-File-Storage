# Coding Guidelines

> **Purpose**: This file documents the coding conventions that every contributor must follow to ensure a maintainable, testable, and high‑quality codebase.

## 1. TypeScript Best Practices
- **Strict mode** – `tsconfig.json` must have `strict: true`, `noImplicitAny: true`, and `noUnusedLocals: true`.
- **No `any`** – The `any` type is forbidden. Use `unknown` + type guards when you must.
- **Prefer `readonly`** – Use `readonly` for immutable data structures.
- **Interfaces over `type`** – Prefer `interface` for public contracts; use `type` for local, complex unions.
- **Never cast away types** – Avoid `as any` or `as unknown as T` except in very controlled, unit‑tested helper functions.

## 2. SOLID Principles
| Principle | What it means for this project | Example |
|---|---|---|
| **Single Responsibility** | Each module/class should have one reason to change. | `UserService` handles user data only, not UI formatting. |
| **Open/Closed** | Extend behaviour via interfaces, not by modifying existing classes. | Add a new `StorageAdapter` without touching `UserService`. |
| **Liskov Substitution** | Subtypes can replace their base types without breaking consumers. | `FileStorageAdapter` implements `StorageAdapter`. |
| **Interface Segregation** | Small, specific interfaces rather than fat ones. | Separate `IUserRepository` into `IUserReadRepository` & `IUserWriteRepository`. |
| **Dependency Inversion** | Depend on abstractions, not concretes. | Inject `ILogger` into services. |

## 3. Separation of Concerns
- **Domain Layer** – Pure business logic, no framework imports.
- **Service Layer** – Orchestrates domain logic and external dependencies.
- **Controller / Router Layer** – Handles HTTP request/response plumbing.
- **UI Layer** – React components, hooks, and presentation logic.
- **Infrastructure Layer** – Database access, file I/O, third‑party APIs.

## 4. Testability
- **Pure functions** – Functions should be deterministic; avoid side effects.
- **Dependency Injection** – Pass dependencies via constructor or function parameters.
- **Mockable Interfaces** – Define interfaces for external services (e.g., `IChatModel`).
- **Test‑Only Exports** – Export helper functions to aid unit tests.
- **Coverage** – Aim for ≥90 % statement coverage on critical paths; run `npm test -- --coverage`.

## 5. Naming & Structure
- **File names** – snake_case for utilities, PascalCase for classes/components.
- **Component props** – Use descriptive names; avoid generic `data` or `props`.
- **Action verbs** – Prefix service methods with `get`, `create`, `update`, `delete`.

## 6. Linting & Formatting
- Use ESLint with the `@typescript-eslint` plugin.
- Prettier is configured to enforce consistent formatting.
- All PRs must pass `npm run lint`.

## 7. Documentation
- Public APIs must include JSDoc comments.
- Complex logic should be accompanied by a short explanatory comment.
- Keep README up to date with build/run instructions.

---

> **Purpose**: This file formalizes the coding standards that enable the team to write clear, robust, and testable code while adhering to SOLID and separation principles.
