# Skills Examples

## Complete Skill Templates

### Template 1: API Endpoint Creator

**File: `.claude/skills/endpoint/skill.md`**

```markdown
---
name: endpoint
description: Create complete API endpoint with tests and documentation
---

# API Endpoint Creator

When user types `/endpoint <name> <method>`:

## Workflow

1. **Validate Input**
   - Check name is valid identifier
   - Check method is GET, POST, PUT, DELETE, or PATCH

2. **Create Endpoint File**
   - Path: `src/api/endpoints/<name>.ts`
   - Include:
     - Express router setup
     - Route handler
     - Input validation (Joi schema)
     - Error handling
     - JSDoc documentation

3. **Create Service File**
   - Path: `src/services/<name>-service.ts`
   - Include:
     - Business logic functions
     - Type definitions
     - Error handling
     - JSDoc documentation

4. **Create Test File**
   - Path: `src/api/endpoints/<name>.test.ts`
   - Include:
     - Happy path tests
     - Error case tests
     - Validation tests
     - Use Supertest for API testing

5. **Update Documentation**
   - Add endpoint to `docs/API.md`
   - Include method, path, parameters, responses

6. **Verify**
   - Run tests to ensure everything works
   - Report success or errors

## Parameters

- `name`: Endpoint name (e.g., "users", "products")
- `method`: HTTP method (GET, POST, PUT, DELETE, PATCH)

## Examples

```bash
/endpoint users GET
/endpoint products POST
/endpoint orders PUT
```

## Notes

- Follows project's 3-layer architecture
- Uses ESLint Airbnb style
- Requires Joi validation for all inputs
- Test coverage must be >80%
```

---

### Template 2: Code Review Skill

**File: `.claude/skills/review/skill.md`**

```markdown
---
name: review
description: Comprehensive code review with security, performance, and style checks
---

# Code Review Skill

When user types `/review <file>`:

## Workflow

1. **Read File**
   - Load the specified file
   - Parse the code structure

2. **Security Check**
   - SQL injection vulnerabilities
   - XSS vulnerabilities
   - Authentication/authorization issues
   - Secrets or credentials in code
   - Unsafe dependencies

3. **Performance Check**
   - N+1 queries
   - Missing database indexes
   - Inefficient algorithms
   - Memory leaks
   - Unnecessary re-renders (React)

4. **Code Style Check**
   - ESLint compliance
   - Naming conventions
   - Function length
   - Code complexity
   - Documentation completeness

5. **Testing Check**
   - Test coverage
   - Missing test cases
   - Test quality

6. **Generate Report**
   - Issues by priority (High/Medium/Low)
   - Line numbers for each issue
   - Suggested fixes
   - Praise for good practices

## Parameters

- `file`: Path to file to review

## Example

```bash
/review src/services/auth-service.ts
```

## Output Format

```
# Code Review: auth-service.ts

## High Priority Issues
1. [Line 45] SQL injection vulnerability in query
   Fix: Use parameterized queries

## Medium Priority Issues
1. [Line 78] Missing error handling
   Fix: Add try-catch block

## Low Priority Issues
1. [Line 23] Variable name could be more descriptive
   Suggestion: Rename 'x' to 'userId'

## Good Practices Found
- Excellent JSDoc documentation
- Proper input validation
- Good test coverage (87%)
```
```

---

### Template 3: Database Migration Skill

**File: `.claude/skills/migrate/skill.md`**

```markdown
---
name: migrate
description: Create and run database migration safely
---

# Database Migration Skill

When user types `/migrate <action> <name>`:

## Workflow

### For `/migrate create <name>`:

1. **Generate Migration File**
   - Timestamp-based filename
   - Include up() and down() methods
   - Add template based on migration type

2. **Open for Editing**
   - Show file to user for review

### For `/migrate run`:

1. **Safety Checks**
   - Verify database connection
   - Check for pending migrations
   - If production: Require confirmation

2. **Backup Database**
   - Create backup before migration
   - Store backup location

3. **Run Migrations**
   - Execute pending migrations in order
   - Log each migration

4. **Verify**
   - Check migration was applied
   - Run tests if available

5. **Report**
   - Show what was migrated
   - Provide backup location

### For `/migrate rollback`:

1. **Confirm Action**
   - Ask for confirmation
   - Show which migration will be rolled back

2. **Backup**
   - Create backup before rollback

3. **Rollback**
   - Run down() method
   - Verify rollback succeeded

## Parameters

- `action`: create, run, or rollback
- `name`: Migration name (for create only)

## Examples

```bash
/migrate create add-users-table
/migrate run
/migrate rollback
```
```

---

## Exercise 1: Use Built-in Skills

### Task:
Try the `/commit` skill

### Steps:
1. Make some changes to files
2. Type: `/commit`
3. Observe the workflow
4. See the generated commit message

### What to Notice:
- Claude analyzes all changes
- Follows conventional commit format
- Asks for confirmation
- No manual git commands needed

---

## Exercise 2: Create Your First Skill

### Task:
Create a skill for your common workflow

### Example: "Test Runner" Skill

**File: `.claude/skills/test/skill.md`**

```markdown
---
name: test
description: Run tests with coverage report
---

When user types `/test`:

1. Run all unit tests
2. Run integration tests
3. Generate coverage report
4. Check coverage meets 80% threshold
5. If failed: Show which tests failed
6. If passed: Show coverage summary

Example: /test
```

### Test It:
1. Save the file
2. Type `/test` in Claude
3. See if it works as expected

---

## Exercise 3: Create Team Skill

### Task:
Create a skill your whole team can use

### Example: "Feature Setup" Skill

**File: `.claude/skills/feature/skill.md`**

```markdown
---
name: feature
description: Set up new feature with boilerplate
---

When user types `/feature <name>`:

1. Create feature branch: `feature/<name>`
2. Create folder: `src/features/<name>/`
3. Create files:
   - `index.ts` (main export)
   - `<name>.service.ts` (business logic)
   - `<name>.test.ts` (tests)
   - `README.md` (documentation)
4. Add feature to main router
5. Create initial test
6. Run tests to verify setup

Parameters:
- name: Feature name (e.g., "user-profile")

Example: /feature user-profile
```

---

## Real-World Skill Ideas

### For Web Development:
```bash
/component <name>       # Create React/Vue component
/page <route>           # Create new page with routing
/api <endpoint>         # Create API endpoint
/style <component>      # Add styled-components
```

### For Backend:
```bash
/model <name>           # Create database model
/controller <name>      # Create controller
/service <name>         # Create service layer
/middleware <name>      # Create middleware
```

### For DevOps:
```bash
/deploy <env>           # Deploy to environment
/rollback               # Rollback deployment
/logs <service>         # Fetch and analyze logs
/health                 # Check system health
```

### For Testing:
```bash
/test-unit              # Run unit tests only
/test-e2e               # Run end-to-end tests
/coverage               # Generate coverage report
/benchmark              # Run performance benchmarks
```

---

## Skill Template (Copy-Paste)

```markdown
---
name: your-skill-name
description: Brief description
---

# Your Skill Title

When user types `/your-skill-name <args>`:

## Workflow

1. First step
2. Second step
3. Third step

## Parameters

- `arg1`: Description
- `arg2`: Description

## Examples

```bash
/your-skill-name value1 value2
```

## Notes

- Any special requirements
- Prerequisites
- Limitations
```

---

## Key Takeaways

1. **Skills save time**
   - Automate repetitive workflows
   - One command instead of many steps

2. **Skills ensure consistency**
   - Same process every time
   - Team follows same standards

3. **Skills are simple to create**
   - Just a markdown file
   - Clear instructions for Claude

4. **Skills are shareable**
   - Check into version control
   - Whole team benefits

---

**Create skills for your repetitive tasks!** ⚡
