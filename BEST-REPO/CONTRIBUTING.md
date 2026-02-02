# Contributing to Task Management API

Thank you for your interest in contributing! This document provides guidelines for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Submitting Changes](#submitting-changes)
- [Review Process](#review-process)

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inspiring community for all.

### Our Standards

**Positive behaviors:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behaviors:**
- Harassment or discriminatory language
- Trolling or insulting comments
- Public or private harassment
- Publishing others' private information
- Other conduct which could reasonably be considered inappropriate

## Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL 14+
- Git
- Code editor (VS Code recommended)

### Initial Setup

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/task-api.git
   cd task-api
   ```

3. Add upstream remote:
   ```bash
   git remote add upstream https://github.com/original/task-api.git
   ```

4. Install dependencies:
   ```bash
   npm install
   ```

5. Set up environment:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

6. Set up database:
   ```bash
   npm run db:migrate
   npm run db:seed
   ```

7. Verify setup:
   ```bash
   npm test
   npm run lint
   ```

## Development Workflow

### Branch Strategy

- `main`: Production-ready code
- `develop`: Development branch
- `feature/*`: New features
- `fix/*`: Bug fixes
- `docs/*`: Documentation updates

### Starting New Work

1. Update your fork:
   ```bash
   git checkout develop
   git pull upstream develop
   ```

2. Create feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Make your changes

4. Run tests frequently:
   ```bash
   npm test -- --watch
   ```

### Commit Messages

Follow conventional commits format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code refactoring
- `test`: Tests
- `chore`: Maintenance

**Example:**
```
feat(tasks): add task filtering by status

Implement filtering functionality allowing users to filter
tasks by their current status (todo, in_progress, done).

Closes #123
```

## Coding Standards

### TypeScript

- Use TypeScript strict mode
- Explicit types for all function parameters and returns
- No `any` types without justification
- Prefer interfaces for objects

### Code Style

Enforced automatically by ESLint and Prettier:
- 2 spaces indentation
- Single quotes
- Semicolons required
- Trailing commas
- Max line length: 100 characters

Run formatters before committing:
```bash
npm run lint       # Check for issues
npm run lint:fix   # Auto-fix issues
npm run format     # Format code
```

### Architecture

Follow the layered architecture:

1. **API Endpoints** (`src/api/endpoints/`)
   - Handle HTTP only
   - Call services
   - Return responses

2. **Services** (`src/services/`)
   - Business logic
   - No HTTP knowledge
   - Throw errors

3. **Database** (Prisma)
   - Data access only

### Testing

All contributions must include tests:

**Required:**
- Unit tests for services
- Integration tests for endpoints
- Minimum 80% coverage

**Test Structure:**
```typescript
describe('FeatureName', () => {
  describe('methodName', () => {
    it('should do something when condition', async () => {
      // Arrange
      const input = 'test';

      // Act
      const result = await method(input);

      // Assert
      expect(result).toBe('expected');
    });
  });
});
```

Run tests:
```bash
npm test                    # Run all tests
npm test -- --watch         # Watch mode
npm run test:coverage       # With coverage
```

### Documentation

- Add JSDoc comments to all exported functions
- Update API documentation in `docs/API.md`
- Update README if needed
- Add inline comments for complex logic

**JSDoc Format:**
```typescript
/**
 * Brief description
 *
 * @param param - Parameter description
 * @returns Return value description
 * @throws ErrorType - When error occurs
 *
 * @example
 * const result = await function(param);
 */
```

## Submitting Changes

### Before Submitting

Run the full checklist:

```bash
# 1. Run tests
npm test

# 2. Check coverage
npm run test:coverage

# 3. Lint code
npm run lint

# 4. Format code
npm run format

# 5. Type check
npm run type-check

# 6. Build
npm run build
```

All must pass before submitting.

### Creating Pull Request

1. Push to your fork:
   ```bash
   git push origin feature/your-feature-name
   ```

2. Open pull request on GitHub

3. Fill out the PR template:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] All tests passing
- [ ] Coverage maintained/improved

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] No new warnings
- [ ] Tests added
- [ ] All tests pass
- [ ] Coverage > 80%
```

4. Link related issues: `Closes #123`

### Pull Request Guidelines

**Good PR:**
- Focused on single feature/fix
- Clear description
- Tests included
- Documentation updated
- Small and reviewable (< 400 lines)

**Avoid:**
- Multiple unrelated changes
- Missing tests
- Breaking existing tests
- Mixing features and refactoring
- Large PRs (> 800 lines)

## Review Process

### What Reviewers Check

1. **Code Quality**
   - Follows coding standards
   - Well-structured and readable
   - Appropriate abstractions
   - No code smells

2. **Testing**
   - Adequate test coverage
   - Tests actually test the functionality
   - Edge cases covered
   - Tests are maintainable

3. **Documentation**
   - JSDoc comments present
   - API docs updated
   - Complex logic explained
   - README updated if needed

4. **Security**
   - No security vulnerabilities
   - Input validation present
   - No sensitive data exposed
   - Error handling appropriate

5. **Performance**
   - Efficient database queries
   - No obvious performance issues
   - Appropriate caching if needed

### Review Timeline

- Initial review: Within 2 business days
- Follow-up reviews: Within 1 business day
- Merge: After approval from 2 reviewers

### Addressing Feedback

1. Read all comments thoroughly
2. Ask questions if unclear
3. Make requested changes
4. Push new commits (don't force push)
5. Reply to comments when addressed
6. Request re-review

### After Merge

1. Delete your feature branch:
   ```bash
   git branch -d feature/your-feature-name
   git push origin --delete feature/your-feature-name
   ```

2. Update your fork:
   ```bash
   git checkout develop
   git pull upstream develop
   git push origin develop
   ```

## Common Mistakes

### ❌ Don't
- Commit directly to main/develop
- Force push to shared branches
- Leave `console.log` statements
- Skip writing tests
- Ignore linting errors
- Make PRs too large
- Mix unrelated changes

### ✅ Do
- Work on feature branches
- Write tests first (TDD)
- Run linters before committing
- Keep PRs focused and small
- Update documentation
- Respond to review comments
- Squash commits if asked

## Getting Help

### Resources

- **Documentation**: Check `docs/` folder
- **Issues**: [GitHub Issues](https://github.com/org/repo/issues)
- **Discussions**: [GitHub Discussions](https://github.com/org/repo/discussions)
- **Code Examples**: Look at existing code

### Questions

If you have questions:

1. Check documentation first
2. Search existing issues
3. Ask in discussions
4. Create new issue if needed

Tag questions appropriately:
- `question`: General questions
- `help wanted`: Need assistance
- `good first issue`: For newcomers

## Development Tips

### VS Code Setup

Recommended extensions:
- ESLint
- Prettier
- TypeScript
- Prisma
- Jest Runner

### Database Tips

```bash
# Reset database
npm run db:reset

# Create migration
npm run db:migrate:dev

# View database
npm run db:studio
```

### Debugging

```bash
# Debug tests
npm test -- --verbose

# Debug single test
npm test -- path/to/test.ts

# Debug with breakpoints
npm run test:debug
```

### Performance

- Use `select` in Prisma queries
- Add indexes for frequently queried fields
- Paginate large result sets
- Profile slow queries

## Recognition

Contributors are recognized in:
- README.md contributors section
- Release notes
- Annual contributor highlights

Top contributors may be invited to:
- Join core team
- Participate in roadmap planning
- Review architectural decisions

## Questions?

Open an issue with the `question` label or start a discussion!

Thank you for contributing! 🎉
