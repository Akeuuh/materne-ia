# AGENTS.md - Complete Coding Guidelines for AI Agents

This file contains comprehensive coding guidelines and standards that must be followed by all AI agents working on this codebase. These rules are derived from the complete rules directory and must be applied contextually based on file locations and operations.

## CRITICAL RULES - ALWAYS APPLY

### Code Quality Standards

- **NO COMMENTS** - Write self-explanatory code only
- Use strict types everywhere, never `any` or `unknown`
- No magic numbers - use explicit constants
- Maximum 30 lines per function
- Maximum 5 parameters per function
- Maximum 300 lines per file
- One responsibility per file
- Eliminate all duplication (DRY)
- Fail fast, throw errors early
- Use custom domain errors
- Prefer one-line early returns

### TypeScript Requirements

- **Always use TypeScript** for all JavaScript code
- **Always use arrow functions**, even for components
- Classes only for singletons
- Type everything explicitly
- Use `interface` for extensible objects
- Use `type` for unions and primitives
- Prefer string literal unions over enums
- Use generics for reusable functions
- Avoid `as` for type conversion
- Use type guards for assertions

### Naming Conventions

#### TypeScript/JavaScript

- Classes/Interfaces: PascalCase, use nouns
- Functions/Methods: camelCase, verbs for actions, nouns for values
- Boolean prefixes: `is`, `has`, `should`
- Variables: camelCase, plural for arrays/collections
- Constants: UPPER_SNAKE_CASE
- Long descriptive names, reveal intent
- No single-letter names except loops
- No abbreviations except common ones

## ARCHITECTURE PATTERNS

### Backend - Clean Architecture

**Applied to:** `apps/backend/**`

- Layers: Domain → Application → Infrastructure → Presentation
- Dependencies point inward only
- Domain layer is framework-agnostic
- Use DTOs for all data transfer
- Validate input at boundaries
- Repository interfaces in domain, implementations in infrastructure
- Use cases orchestrate business logic
- Controllers handle HTTP only

### Frontend - Feature-Based Architecture

**Applied to:** `apps/frontend/**`

- Organize by business feature in `features/` directory
- Co-locate components, hooks, state per feature
- Use shared folders for common code
- Global state only for app-wide concerns

## FRAMEWORK-SPECIFIC RULES

### React Development

**Applied to:** `apps/frontend/**/*.tsx`

- Functional components only, no classes
- Smart/dumb component pattern
- Smart components handle data/logic
- Dumb components display only
- Strongly type all props
- Return `null` if mandatory props missing
- One component per file
- Place `displayName` at bottom
- No default exports
- Think mobile-first
- Use semantic HTML and ARIA attributes

### React Libraries

- **axios** for HTTP requests (not fetch)
- **react-query** for all API calls
- **react-hook-form + yup** for forms
- Use path aliasing for imports
- Prefer `condition ? <Component/> : null`

### React Router v7.5

**Applied to:** `apps/frontend/app/routes/**/*.tsx`

- Import types from `.react-router/types/app/routes`
- Use `Route.LoaderArgs` and `Route.ComponentProps`
- Example:

```typescript
import type { Route } from "apps/frontend/.react-router/types/app/routes/+types/groups";
export async function loader({ params }: Route.LoaderArgs) {
  /* ... */
}
export default function Groups({ loaderData }: Route.ComponentProps) {
  /* ... */
}
```

### NestJS Backend

**Applied to:** `apps/backend/src/**/*.ts`

- Modular structure, import new files in parent module
- Controllers handle HTTP only, call use-cases not repositories
- Use DTOs for input/output
- Domain services: no DB access
- Use cases: use commands/queries for DB
- Repositories: implement domain interface, return domain objects only
- Keep Prisma types internal
- Use DI for mappers
- Jest for testing

### MobX State Management

**Applied to:** `apps/frontend/app/**/*.store.ts`

- Class-based stores, group by domain feature
- Use `makeAutoObservable` in constructor
- No decorators
- Use `get` for computed values
- Use `action.bound` for callbacks
- Use `runInAction` for async mutations
- Prefer `reaction` over `autorun`
- Unit test every store

### Tailwind CSS v4.1

**Applied to:** CSS files and component files

- CSS-based configuration in `tailwind.css`
- Use CSS variables: `var(--color-red-500)`
- Register custom utilities with `@utility`
- Apply variants left-to-right: `*:first:pt-0`
- Use parentheses for arbitrary CSS: `bg-(--brand-color)`
- Scope hover with `@media (hover: hover)`
- Import theme with `@reference`
- Prefer CSS variables over `@apply`

## TESTING STANDARDS

### General Testing Rules

**Applied to:** `**/*.spec.*`, `**/*.test.*`

- Write tests in English
- Follow AAA pattern (Arrange-Act-Assert)
- Organize by feature
- Group with `describe`
- Use descriptive test names
- Prefer action-based user interaction tests

### Unit Tests

- Test one functional unit only
- Mock all external dependencies
- Keep tests fast and independent
- Test edge cases thoroughly
- Verify error handling

### Integration Tests

- Define input/output data clearly
- Mock external API calls
- Verify data transformation
- Assert async operations

### Frontend Testing

- Mock only external dependencies (API, browser)
- Test state stores thoroughly
- Test smart/container components
- Don't test presentational components
- Assert state changes

### Backend Testing

- Use setup/teardown hooks
- Avoid code repetition
- Keep tests independent
- Import all modules for integration
- No DB mock for integration tests

## WORKFLOW PROCESSES

### Package Installation

- **NEVER install packages directly**
- Always ask user first
- Check existing packages before proposing
- Prefer stable versions

### Bug Finding Process

1. Summarize issue in own words
2. List action paths between files in mermaid
3. Examine relevant files
4. List top 3 potential causes with confidence
5. Wait for user confirmation
6. Provide top 3 best fix steps
7. Wait for user confirmation

### Multi-Project Setup

- Use Turborepo for projects with frontend and backend
- Maintain consistent tooling across projects

## ERROR HANDLING

- Fail fast, throw errors early
- Use custom domain errors
- Translate errors to user language
- Log errors in English with error codes
- Catch errors as `unknown | Error` (TypeScript)
- Use specific exceptions (Python)
- Centralize error handling (Presentation layer)


**Applied to:** `**/*.py`

- Type hints for all function arguments
- Avoid `Any` type
- Use `Type | None` for nullable
- Use `dict` and `list` for hints
- Use dataclasses for simple structures
- Use NamedTuple for immutable data
- Use Enum for enumerations
- Follow PEP 8
- Use TypeVar for generics

## PHP-SPECIFIC RULES

**Applied to:** `**/*.php`

- PSR-12 coding standards
- PSR-4 autoloading
- Unix LF line endings
- 4 spaces indentation
- One statement per line
- Soft limit 120 chars per line
- Lowercase keywords
- PascalCase class names
- Declare visibility always
- Abstract/final before visibility
- Static after visibility

## IMPORTANT REMINDERS

1. **Never add comments** - code must be self-documenting
2. **Ask before installing packages**
3. **Use existing UI components and patterns**
4. **Follow established code style in existing files**
5. **Maintain consistency with surrounding code**
6. **Test all changes appropriately**
7. **Handle errors properly with domain-specific exceptions**
8. **Keep functions small and focused**
9. **Use descriptive names that reveal intent**
10. **Apply rules contextually based on file location and type**

## FILE ORGANIZATION

- `/apps/frontend/` - React frontend with TypeScript
- `/apps/backend/` - NestJS or Symfony backend
- `/features/` - Feature-based modules (frontend)
- `/src/` - Source code (backend)
- `*.spec.*`, `*.test.*` - Test files
- `*.store.ts` - MobX stores
- `/routes/` - React Router pages

This document should be referenced for every code change to ensure consistency and quality across the entire codebase.
