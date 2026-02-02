# Module 5: RULES

Rules are guidelines that define how Claude should write code in your project.

## What Are Rules?

Rules tell Claude:
- How to format code
- Where to put files
- What patterns to follow
- What standards to enforce

**Simple example:**
```markdown
# Rules
- Use TypeScript
- Put tests in __tests__/
- Use async/await (not .then)
```

Now Claude follows these rules automatically!

## Rules vs Other Features

```
MEMORY   → Facts (Tech: Express, DB: PostgreSQL)
RULES    → Standards (Use semicolons, 2 spaces)
SKILLS   → Workflows (/commit, /review)
CONTEXT  → What Claude sees right now
```

## Where to Define Rules

### Option 1: `.claude/rules.md` (Best)
```markdown
# Claude Rules for This Project

## Code Style
- 2 spaces for indentation
- Single quotes for strings
- Semicolons required

## Architecture
- Controllers in src/controllers/
- Services in src/services/
- Models in src/models/

## Testing
- Jest with describe/it
- Tests must be in __tests__/
- Minimum 80% coverage
```

### Option 2: Project README
```markdown
# My Project

## Development Guidelines
- Use TypeScript strict mode
- All functions need JSDoc
- Max function length: 50 lines
```

### Option 3: CONTRIBUTING.md
```markdown
# Contributing

Before submitting:
1. Run `npm test`
2. Run `npm run lint`
3. Update documentation
```

## Why Rules Matter

### Without Rules
```
You: "Add login endpoint"
Claude: [Creates in random location, random style]

You: "Add signup endpoint"
Claude: [Different location, different style]

Result: Inconsistent mess 😞
```

### With Rules
```markdown
# .claude/rules.md
## API Endpoints
- Location: src/api/
- Pattern: controller-service-repository
- Validation: Joi schemas
```

```
You: "Add login endpoint"
Claude: [Creates in src/api/, follows pattern]

You: "Add signup endpoint"
Claude: [Same location, same pattern]

Result: Consistent codebase 😊
```

## Types of Rules

### 1. Code Style
```markdown
- Use 2 spaces (not tabs)
- Single quotes for strings
- Trailing commas in objects
```

### 2. File Organization
```markdown
- Feature-based folders
- One component per file
- Tests colocated with source
```

### 3. Naming Conventions
```markdown
- camelCase for variables
- PascalCase for classes
- UPPER_SNAKE_CASE for constants
- kebab-case for file names
```

### 4. Architecture
```markdown
- 3-layer pattern (API, Service, Data)
- No business logic in controllers
- All API calls through service layer
```

### 5. Testing
```markdown
- Unit tests for all services
- Integration tests for endpoints
- Minimum 80% coverage
```

### 6. Documentation
```markdown
- JSDoc for all exported functions
- README for each feature
- Inline comments for complex logic
```

### 7. Security
```markdown
- Never log passwords
- Validate all user input
- Use parameterized queries
```

### 8. Performance
```markdown
- Lazy load routes
- Memoize expensive calculations
- Bundle size < 250KB
```

## Creating Effective Rules

### ✅ DO: Be Specific
```markdown
❌ Bad: "Write good tests"
✅ Good: "All services must have unit tests with 80%+ coverage"

❌ Bad: "Keep functions small"
✅ Good: "Functions should not exceed 50 lines"
```

### ✅ DO: Provide Examples
```markdown
Rule: Prefer async/await over .then()

❌ Bad:
fetchData().then(data => process(data));

✅ Good:
const data = await fetchData();
process(data);
```

### ✅ DO: Explain Why
```markdown
❌ Bad: "Use TypeScript"
✅ Good: "Use TypeScript for type safety and better IDE support"
```

### ❌ DON'T: Be Vague
```markdown
❌ "Write clean code"
❌ "Follow best practices"
❌ "Use meaningful names"
```
These mean nothing without specifics!

### ❌ DON'T: Create Too Many Rules
```markdown
❌ 50 micro-rules about formatting
✅ Use ESLint/Prettier instead
```

### ❌ DON'T: Make Conflicting Rules
```markdown
❌ Rule 1: "Write concise code"
❌ Rule 2: "Add detailed comments everywhere"
```
These conflict!

## Rule Specificity Levels

**Level 1: Vague (Bad)**
```markdown
- Write clean code
- Follow best practices
```
Problem: Too vague

**Level 2: Specific (Good)**
```markdown
- Functions max 50 lines
- Use camelCase for variables
- Imports at top of file
```
Better: Concrete, measurable

**Level 3: Enforced (Best)**
```markdown
- ESLint must pass (.eslintrc.js)
- TypeScript strict mode enabled
- Test coverage minimum: 80%
```
Best: Automated, non-negotiable

## Enforcing Rules

### Manual (Checklist)
```markdown
Pre-commit:
- [ ] Tests pass
- [ ] No console.log
- [ ] JSDoc added
```

### Automated (Best)
```json
// package.json
{
  "scripts": {
    "lint": "eslint src/",
    "test": "jest --coverage",
    "pre-commit": "npm run lint && npm run test"
  }
}
```

### Git Hooks
```bash
# .husky/pre-commit
npm run lint
npm run test
```

## Common Rules by Project Type

### React Projects
```markdown
- Functional components only
- Use hooks (not classes)
- Props interface for each component
- Custom hooks start with 'use'
```

### Node.js APIs
```markdown
- Express for routing
- Controllers handle HTTP only
- Services handle business logic
- Async/await for all async code
```

### Full-Stack Apps
```markdown
- Shared types in /shared
- API routes under /api
- Frontend in /components
- No business logic in components
```

## Rules Anti-Patterns

### ❌ Too Many Rules
```markdown
1. Use semicolons
2. Use 2 spaces
3. Use single quotes
... (50 more)
```
Solution: Use ESLint/Prettier

### ❌ Contradictory Rules
```markdown
Rule 1: Keep code concise
Rule 2: Add detailed comments everywhere
```
Solution: Clarify when each applies

### ❌ Unenforced Rules
```markdown
"All code must have tests"
[But no CI check]
```
Solution: Automate enforcement

## Key Takeaways

1. **Rules ensure consistency** across your codebase
2. **Rules guide Claude** to write code your way
3. **Rules should be specific** (not vague)
4. **Rules should be enforced** (automate when possible)
5. **Rules evolve** as your project grows

## Examples & Practice

**→ [EXAMPLES.md](EXAMPLES.md) - Complete practical guide:**
- Copy-paste `.claude/rules.md` templates
- Real examples for React, Node.js, Full-stack
- Before/after comparisons
- Exercise: Create rules for your project

## Next Steps

1. Read [EXAMPLES.md](EXAMPLES.md) for hands-on practice
2. Create `.claude/rules.md` for your project
3. Test rules with Claude
4. Move to [START-REPO](../START-REPO/README.md)

---

**Remember: Good rules = Consistent code!** 📋✨
