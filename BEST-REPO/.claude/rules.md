# Claude Development Rules

This document defines the coding standards and conventions for Claude AI assistance in this project.

## Architecture Patterns

### Layered Architecture
Follow strict separation of concerns:

1. **API Layer** (`src/api/endpoints/`)
   - Handle HTTP requests/responses only
   - Validate request format
   - Call service layer
   - Format responses
   - Never contain business logic

2. **Service Layer** (`src/services/`)
   - Implement all business logic
   - No HTTP knowledge (no Request/Response types)
   - Return data or throw errors
   - Reusable across endpoints

3. **Data Layer** (`prisma/`)
   - Database access only
   - Use Prisma client
   - No business logic

### File Organization
```
feature-name/
├── endpoints/feature-name.ts    # HTTP handlers
├── services/feature-name-service.ts   # Business logic
└── tests/feature-name.test.ts   # Tests
```

## Coding Standards

### TypeScript

**Strict Mode Required:**
```typescript
// tsconfig.json must have:
"strict": true
"noImplicitAny": true
"strictNullChecks": true
```

**Type Annotations:**
- All function parameters must be typed
- All function return types must be explicit
- No `any` types without justification comment
- Prefer interfaces over types for objects

**Example:**
```typescript
// ✅ Good
function processTask(taskId: string, userId: string): Promise<Task> {
  // implementation
}

// ❌ Bad
function processTask(taskId, userId) {
  // implementation
}
```

### Naming Conventions

| Type | Convention | Example |
|------|-----------|---------|
| Files | kebab-case | `user-service.ts` |
| Classes | PascalCase | `UserService` |
| Interfaces | PascalCase with I prefix | `IUser` |
| Functions | camelCase | `getUserById` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_ATTEMPTS` |
| Variables | camelCase | `userName` |
| Private methods | _camelCase | `_validateInput` |

### Code Style

**Enforced by ESLint & Prettier:**
- 2 spaces indentation
- Single quotes for strings
- Semicolons required
- Trailing commas in multiline
- Max line length: 100 characters
- Max function length: 50 lines

**Async Operations:**
```typescript
// ✅ Always use async/await
async function fetchUser(id: string): Promise<IUser> {
  const user = await prisma.user.findUnique({ where: { id } });
  return user;
}

// ❌ Never use .then()
function fetchUser(id: string): Promise<IUser> {
  return prisma.user.findUnique({ where: { id } })
    .then(user => user);
}
```

## API Endpoint Structure

### Template
```typescript
import { Request, Response } from 'express';
import { ServiceName } from '../../services/service-name';

/**
 * Description of what this endpoint does
 * @route HTTP_METHOD /api/resource
 */
export async function endpointName(
  req: Request,
  res: Response
): Promise<Response> {
  try {
    // 1. Extract and validate parameters
    const { param } = req.params;
    const { field } = req.body;

    // 2. Call service layer
    const result = await ServiceName.method(param, field);

    // 3. Return formatted response
    return res.status(200).json({
      success: true,
      data: result
    });
  } catch (error) {
    // 4. Handle errors
    return res.status(error.statusCode || 500).json({
      success: false,
      error: {
        message: error.message,
        code: error.code || 'INTERNAL_ERROR'
      }
    });
  }
}
```

### Error Response Format
**Always use consistent error responses:**
```typescript
{
  "success": false,
  "error": {
    "message": "User-friendly error message",
    "code": "ERROR_CODE",
    "details": {} // optional
  }
}
```

### Success Response Format
```typescript
{
  "success": true,
  "data": {
    // response data
  },
  "meta": { // optional, for pagination etc
    "page": 1,
    "totalPages": 10
  }
}
```

## Service Structure

### Template
```typescript
import { prisma } from '../config/database';
import { NotFoundError, ValidationError } from '../utils/errors';
import type { IResource } from '../models/resource';

/**
 * Service for resource management
 */
export class ResourceService {
  /**
   * Method description
   * @param param - Parameter description
   * @returns Promise<ReturnType>
   * @throws NotFoundError when resource not found
   * @throws ValidationError when validation fails
   */
  static async methodName(param: string): Promise<IResource> {
    // 1. Validate input
    if (!param) {
      throw new ValidationError('Parameter is required');
    }

    // 2. Fetch data
    const resource = await prisma.resource.findUnique({
      where: { id: param }
    });

    // 3. Handle not found
    if (!resource) {
      throw new NotFoundError('Resource not found');
    }

    // 4. Return data
    return resource;
  }
}
```

### Service Rules
- All methods are `static` (services are stateless)
- All async methods use `async/await`
- All methods have JSDoc comments
- All methods have explicit return types
- Services throw errors, never handle HTTP

## Error Handling

### Custom Error Classes
```typescript
// Use these custom errors:
class NotFoundError extends Error {
  statusCode = 404;
  code = 'NOT_FOUND';
}

class ValidationError extends Error {
  statusCode = 400;
  code = 'VALIDATION_ERROR';
}

class UnauthorizedError extends Error {
  statusCode = 401;
  code = 'UNAUTHORIZED';
}

class ForbiddenError extends Error {
  statusCode = 403;
  code = 'FORBIDDEN';
}
```

### When to Use Which Error
- `NotFoundError`: Resource doesn't exist
- `ValidationError`: Invalid input data
- `UnauthorizedError`: Not authenticated
- `ForbiddenError`: Authenticated but not authorized
- Generic `Error`: Unexpected errors

### Error Handling Pattern
```typescript
// In services: throw errors
if (!user) {
  throw new NotFoundError(`User ${id} not found`);
}

// In endpoints: catch and format
try {
  const result = await UserService.getById(id);
  return res.json({ success: true, data: result });
} catch (error) {
  return res.status(error.statusCode || 500).json({
    success: false,
    error: { message: error.message, code: error.code }
  });
}
```

## Testing

### Test Structure
```typescript
import { ServiceName } from '../services/service-name';

describe('ServiceName', () => {
  describe('methodName', () => {
    it('should return result when input is valid', async () => {
      // Arrange
      const input = 'test';

      // Act
      const result = await ServiceName.methodName(input);

      // Assert
      expect(result).toBeDefined();
      expect(result.field).toBe('expected');
    });

    it('should throw ValidationError when input is invalid', async () => {
      // Arrange
      const input = '';

      // Act & Assert
      await expect(ServiceName.methodName(input))
        .rejects.toThrow(ValidationError);
    });
  });
});
```

### Testing Requirements
- **Coverage**: Minimum 80% code coverage
- **Unit Tests**: All service methods
- **Integration Tests**: All API endpoints
- **Test Files**: Named `*.test.ts`, colocated with source
- **Test Structure**: Use `describe` and `it` blocks
- **Test Pattern**: Arrange-Act-Assert

### What to Test
✅ Happy paths
✅ Error conditions
✅ Edge cases
✅ Validation logic
✅ Business rules

❌ Don't test:
- External libraries
- Trivial getters/setters
- Type definitions

## Documentation

### JSDoc Requirements
All exported functions require JSDoc:

```typescript
/**
 * Brief description of what the function does
 *
 * Longer description if needed, explaining complex logic,
 * business rules, or important considerations.
 *
 * @param paramName - Description of parameter and its constraints
 * @param optionalParam - Optional parameter (optional)
 * @returns Description of return value and what it represents
 * @throws ErrorType - Describe when this error is thrown
 *
 * @example
 * const result = await functionName('example', true);
 */
```

### Inline Comments
Add comments for:
- Complex algorithms
- Non-obvious business logic
- Workarounds for known issues
- Performance optimizations

```typescript
// ✅ Good comment
// Calculate tax based on user's state and product category
// (special handling for digital products in California)
const tax = calculateTax(price, state, category);

// ❌ Bad comment
// Get user
const user = await getUser(id);
```

### API Documentation
- All endpoints documented in `docs/API.md`
- Include request/response examples
- Document all error codes
- Provide curl examples

## Security Rules

### Never Log Sensitive Data
```typescript
// ❌ Never log these
console.log('Login:', { email, password });
console.log('Token:', token);
console.log('Credit card:', ccNumber);

// ✅ Log safely
console.log('Login attempt:', { email });
console.log('Token issued for user:', userId);
```

### Input Validation
Always validate user input:

```typescript
// Use Joi for validation
import Joi from 'joi';

const schema = Joi.object({
  email: Joi.string().email().required(),
  password: Joi.string().min(8).required()
});

const { error, value } = schema.validate(req.body);
if (error) {
  throw new ValidationError(error.message);
}
```

### Environment Variables
Never hardcode secrets:

```typescript
// ❌ Never do this
const apiKey = 'sk-1234567890';
const dbPassword = 'mypassword';

// ✅ Always use environment variables
const apiKey = process.env.API_KEY;
const dbPassword = process.env.DB_PASSWORD;
```

## Import Organization

### Order
1. External packages
2. Internal modules (with aliases)
3. Relative imports
4. Type imports (last)

### Example
```typescript
// 1. External
import express from 'express';
import { Request, Response } from 'express';

// 2. Internal (with @/ alias)
import { UserService } from '@/services/user-service';
import { validateRequest } from '@/utils/validation';

// 3. Relative
import { parseUserData } from './helpers';

// 4. Types
import type { IUser } from '@/models/user';
```

## Database (Prisma)

### Queries
- Always use Prisma client
- Never write raw SQL unless absolutely necessary
- Always handle potential null results
- Use transactions for multi-step operations

```typescript
// ✅ Good
const user = await prisma.user.findUnique({
  where: { id },
  select: { id: true, email: true, name: true }
});

if (!user) {
  throw new NotFoundError('User not found');
}

// ✅ Use transactions for multiple operations
await prisma.$transaction([
  prisma.user.create({ data: userData }),
  prisma.profile.create({ data: profileData })
]);
```

### Migrations
- Generate migration: `npm run db:migrate:dev`
- Always review migration SQL before applying
- Never modify migration files after creation
- Write reversible migrations when possible

## Performance Guidelines

### Database Queries
- Use `select` to limit returned fields
- Use pagination for large result sets
- Add indexes for frequently queried fields
- Avoid N+1 queries (use `include` wisely)

```typescript
// ✅ Good - select only needed fields
const users = await prisma.user.findMany({
  select: { id: true, email: true },
  take: 20,
  skip: (page - 1) * 20
});

// ❌ Bad - fetches all fields
const users = await prisma.user.findMany();
```

### Caching
- Cache expensive computations
- Cache frequently accessed data
- Use appropriate TTL values
- Invalidate cache on data changes

## Git Commit Messages

### Format
```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code refactoring
- `test`: Tests
- `chore`: Maintenance

### Examples
```
feat(auth): add password reset functionality

Implement password reset flow with email verification.
Includes rate limiting and secure token generation.

Closes #123
```

```
fix(tasks): resolve task assignment bug

Fix issue where tasks were not properly assigned to users
when created via the API endpoint.

Fixes #456
```

## Pre-commit Checklist

Before committing:
- [ ] All tests pass (`npm test`)
- [ ] Linting passes (`npm run lint`)
- [ ] Code is formatted (`npm run format`)
- [ ] No console.log statements
- [ ] No TODO comments without issue numbers
- [ ] JSDoc comments added for new functions
- [ ] Tests added for new functionality
- [ ] Documentation updated if needed

## When in Doubt

1. Check existing code for patterns
2. Refer to this rules document
3. Review TypeScript/ESLint errors
4. Ask for clarification
5. Document your decision

## Claude-Specific Instructions

When Claude is assisting with this project:

1. **Always read rules first**: Check this file before starting work
2. **Follow patterns**: Match existing code structure
3. **Be consistent**: Use established conventions
4. **Write tests**: Include tests with new functionality
5. **Document**: Add JSDoc comments
6. **Validate**: Check types and run linters
7. **Ask if unclear**: Request clarification rather than guess

## Key Principles

1. ✅ **Type Safety**: Strict TypeScript, no any
2. ✅ **Separation of Concerns**: Layered architecture
3. ✅ **Testing**: Comprehensive test coverage
4. ✅ **Documentation**: Self-documenting code
5. ✅ **Security**: Never expose sensitive data
6. ✅ **Performance**: Efficient database queries
7. ✅ **Consistency**: Same patterns everywhere
8. ✅ **Quality**: ESLint and Prettier enforced

---

Last updated: 2024
