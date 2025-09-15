# AGENTS

This file defines how agents must behave in my coding environment.

## Purpose

Provide explicit behavioral guidance for AI coding agents to ensure consistency, quality, and adherence to established patterns across all development activities.

## General Rules

### Code Quality Standards
- **Write no comments** in code
- **Use strict types only** - never use `any`, `unknown`, or untyped values
- **Disallow magic numbers** - use explicit constants with descriptive names
- **Eliminate duplication** - follow DRY principle strictly
- **Write the simplest code possible** that solves the problem
- **Avoid double negatives** in conditions and variable names
- **Use long, readable variable names** that reveal intent

### File and Function Limits
- **Keep functions under 30 lines**
- **Limit function parameters to 5 maximum**
- **Keep files under 300 lines**
- **Limit folders to 10 sub-files maximum**
- **One responsibility per file**
- **No flag parameters** in functions

### Error Handling
- **Fail fast** - throw errors early
- **Use custom domain errors** with specific types
- **Translate errors to user language** for display
- **Log errors in English** with error codes
- **Never swallow exceptions** - handle or propagate appropriately
- **Add context** to error messages

## Coding Guidelines

### Architecture Patterns

#### Backend (Clean Architecture)
- **Separate by layers**: Domain, Application, Infrastructure, Presentation
- **Direct dependencies inward only** - outer layers depend on inner layers
- **Keep domain layer framework-agnostic**
- **Define interfaces at layer boundaries**
- **Place business logic in domain layer**
- **Implement use cases as orchestrators** in application layer
- **Isolate external systems** in infrastructure layer
- **Handle HTTP logic** in presentation layer

#### Frontend (Feature-Based Architecture)
- **Organize code by business feature** in `features/` directory
- **Co-locate components, hooks, and state** per feature
- **Use shared folders** for common code only
- **Apply smart/dumb component pattern**
- **Use global state only for app-wide concerns**

### Naming Conventions

#### General
- **Use descriptive names** that reveal intent
- **No single-letter names** except loop counters
- **No abbreviations** except widely recognized ones
- **Use consistent terminology** throughout codebase
- **Use plural for arrays/collections**

#### TypeScript/JavaScript
- **PascalCase** for classes and interfaces
- **camelCase** for functions, methods, and variables
- **UPPER_SNAKE_CASE** for constants
- **Prefix booleans** with `is`, `has`, `should`
- **Use verbs for actions**, nouns for value-returning functions

### Type Systems

#### TypeScript
- **Type everything explicitly**
- **Never use `any` or `unknown`**
- **Avoid `as` for type conversion** - use type guards
- **Use `interface` for extensible objects**
- **Use `type` for unions and primitives**
- **Prefer string literal unions to enums**
- **Avoid `null` and `undefined` in returns**
- **Catch errors as `unknown | Error`**

## Framework-Specific Guidelines

### React
- **Use functional components** exclusively
- **Keep components light and small**
- **Strongly type props** with interfaces
- **Split by responsibility** into sub-components
- **Delegate state to smart components**
- **Return `null` if mandatory props missing**
- **One component per file** (except tiny private components)
- **Think mobile-first** for styling
- **Use semantic HTML elements**
- **Ensure keyboard navigation**

### React Router v7.5
- **Search for generated types** in `.react-router/types/app/routes`
- **Use Route.LoaderArgs** for loader parameters
- **Use Route.ComponentProps** for component props
- **Import types from generated paths**

### NestJS
- **Use modular structure**
- **Import new files in parent module**
- **Use dependency injection** for external interactions
- **Controllers only handle HTTP layer**
- **Use DTOs for input/output**
- **Call use-cases, not repositories** from controllers
- **Validate with class-validator**
- **Return domain objects only** from repositories

### MobX
- **Group stores by domain feature**
- **Use class-based store structure**
- **Disallow MobX decorators**
- **Use `makeAutoObservable` in constructor**
- **Use `get` for computed values**
- **Use `action.bound` for callbacks**
- **Use `runInAction` for async mutations**
- **Prefer `reaction` over `autorun`**

### Tailwind CSS v4.1
- **Use CSS-based configuration** in `tailwind.css`
- **Use CSS variables for theme values**: `var(--color-red-500)`
- **Register custom utilities with `@utility`**
- **Apply variants left-to-right**: `*:first:pt-0`
- **Use parentheses for arbitrary CSS variables**: `bg-(--brand-color)`
- **Scope hover styles** with `@media (hover: hover)`
- **Import theme with `@reference`** in component frameworks
- **Prefer direct CSS variables over `@apply`**

## Testing Standards

### General Testing Principles
- **Organize test files by feature**
- **Group related tests** using `describe`
- **Write tests in English**
- **Follow Arrange-Act-Assert (AAA) pattern**
- **Use descriptive test names**
- **Use existing types for tests**
- **Keep tests independent and focused**

### Unit Testing
- **Test one functional unit only**
- **Mock all external dependencies**
- **Keep tests fast and independent**
- **Test edge cases thoroughly**
- **Verify error handling conditions**
- **Avoid brittle assertion checks**

### Integration Testing
- **Define input data clearly** using DTOs
- **Specify expected output data**
- **Verify data transformation** through components
- **Mock external API calls**
- **Assert external calls receive valid data**
- **Verify asynchronous operations**

### Frontend Testing
- **Mock only external dependencies** (API, browser)
- **Test error throwing mechanisms**
- **Do not test presentational components**
- **Test state stores thoroughly**
- **Test container/smart components**
- **Assert state changes**

### Backend Testing
- **Use setup hooks** (`beforeEach`, `beforeAll`)
- **Use teardown hooks** (`afterEach`, `afterAll`)
- **Avoid code repetition in tests**
- **Import all modules for integration tests**
- **No DB mock for integration tests**

## Communication Guidelines

### With Users
- **Never install packages directly** - always ask first
- **Check existing packages** before proposing new ones
- **Prefer stable versions** of dependencies
- **Explain changes clearly** when asked
- **Provide confidence levels** when diagnosing issues

### Code Comments and Documentation
- **Write no comments in code** - code should be self-documenting
- **Use descriptive names** instead of comments
- **Document APIs and interfaces** when necessary
- **Keep documentation close to code**

## Project-Specific Conventions

### Git and Version Control
- **Write small, focused commits**
- **Use clear commit messages** explaining "why" not "what"
- **Follow repository's commit style**
- **Never commit secrets or keys**

### Package Management
- **Never install new packages directly**
- **Always ask user before installing**
- **Check existing packages first**
- **Prefer stable versions**
- **Document package purpose**

## Workflow Processes

### Bug Finding Process
1. **Summarize issue** in your own words
2. **List action paths** between files in mermaid
3. **Examine relevant files** based on issue description
4. **List top 3 potential causes** with confidence levels
5. **Wait for user confirmation** before proceeding
6. **Provide top 3 best steps** to fix the issue
7. **Wait for user confirmation** before implementing

### Development Workflow
1. **Understand requirements** before coding
2. **Check existing patterns** in codebase
3. **Follow established conventions**
4. **Test changes thoroughly**
5. **Verify no regressions**
6. **Document significant changes**

## Do / Don't Examples

### DO ✅
```typescript
// Use explicit types
interface UserData {
  id: string;
  name: string;
  email: string;
}

// Use descriptive names
const isUserAuthenticated = checkAuthStatus();

// Use constants for magic values
const MAX_RETRY_ATTEMPTS = 3;

// Handle errors properly
try {
  await saveUser(userData);
} catch (error) {
  logger.error('Failed to save user', { error, userId: userData.id });
  throw new UserSaveError('Unable to save user data', error);
}
```

### DON'T ❌
```typescript
// Don't use any
let data: any = fetchData();

// Don't use single letters
const u = getUser();

// Don't use magic numbers
if (retries > 3) { /* ... */ }

// Don't swallow errors
try {
  await saveUser(userData);
} catch (error) {
  // Silent fail
}

// Don't use flag parameters
function createUser(data, isAdmin) { /* ... */ }
```

## References

- Clean Architecture principles for backend organization
- Feature-based architecture for frontend structure
- PSR-12 and PSR-4 standards for PHP development
- PEP 8 for Python code style
- React best practices for component development
- Testing pyramid principles for test strategy
- SOLID principles for object-oriented design
- DRY, KISS, and YAGNI principles for code simplicity

---

**Remember**: Write code that is simple, explicit, and maintainable. When in doubt, favor clarity over cleverness.