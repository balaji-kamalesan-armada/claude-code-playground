# Rules Examples

## Example 1: Without Rules (Chaos) ❌

### Session 1 - Add Login Endpoint
```
You: Add a login endpoint

Claude: [Creates endpoint]
```

**Claude's code:**
```javascript
// login.js in root folder
const express = require('express')
const router = express.Router()

router.post('/login', function(req, res) {
  const {username, password} = req.body
  // login logic
  res.json({token: 'abc123'})
})

module.exports = router
```

### Session 2 - Add Signup Endpoint (NEW SESSION)
```
You: Add a signup endpoint

Claude: [Creates in different style]
```

**Claude's code:**
```typescript
// src/routes/signup.ts (different location!)
import { Router } from 'express';

export const signupRouter = Router();

signupRouter.post('/signup', async (req, res) => {
  const { username, password } = req.body;
  // signup logic
  return res.json({ success: true });
});
```

### Session 3 - Add Password Reset
```
You: Add password reset endpoint

Claude: [Yet another style]
```

**Claude's code:**
```javascript
// api/reset-password.js (third location!)
module.exports = (req, res) => {
  let email = req.body.email
  // reset logic
  res.send("Email sent")
}
```

**Result: 3 endpoints, 3 different patterns, 3 different locations** 😞

---

## Example 2: With Rules (Consistency) ✅

### Create `.claude/rules.md`
```markdown
# Claude Rules for This Project

## API Endpoints

### Location
- All endpoints in `src/api/endpoints/`
- One file per resource (users.ts, posts.ts)

### Structure
- Use Express Router
- TypeScript with proper types
- Controller-Service-Repository pattern
- Controllers in endpoints/ (handle HTTP only)
- Services in src/services/ (business logic)

### Code Style
- Async/await (not .then or callbacks)
- Destructure request body
- Return JSON with consistent format
- TypeScript interfaces for request/response

### Validation
- Use Joi schemas
- Validate in controller before calling service
- Return 400 for validation errors

### Error Handling
- Try-catch in all async functions
- Custom error classes
- Return appropriate HTTP status codes

### Testing
- Jest with supertest
- Test file in __tests__/ folder
- Minimum 80% coverage

### Example
\`\`\`typescript
// src/api/endpoints/users.ts
import { Router } from 'express';
import { UserService } from '../../services/user.service';
import { loginSchema } from '../../validation/user.schema';

export const userRouter = Router();

userRouter.post('/login', async (req, res) => {
  try {
    const { error, value } = loginSchema.validate(req.body);
    if (error) {
      return res.status(400).json({ error: error.message });
    }

    const result = await UserService.login(value);
    return res.json(result);
  } catch (err) {
    return res.status(500).json({ error: 'Internal server error' });
  }
});
\`\`\`
```

### Session 1 - Add Login Endpoint
```
You: Add a login endpoint

Claude: [Reads .claude/rules.md, follows pattern]
```

**Claude's code:**
```typescript
// src/api/endpoints/users.ts
import { Router } from 'express';
import { UserService } from '../../services/user.service';
import { loginSchema } from '../../validation/user.schema';

export const userRouter = Router();

userRouter.post('/login', async (req, res) => {
  try {
    const { error, value } = loginSchema.validate(req.body);
    if (error) {
      return res.status(400).json({ error: error.message });
    }

    const result = await UserService.login(value);
    return res.json(result);
  } catch (err) {
    return res.status(500).json({ error: 'Internal server error' });
  }
});

// src/services/user.service.ts
export class UserService {
  static async login(credentials: LoginCredentials) {
    // business logic here
  }
}

// src/validation/user.schema.ts
import Joi from 'joi';

export const loginSchema = Joi.object({
  username: Joi.string().required(),
  password: Joi.string().required()
});
```

### Session 2 - Add Signup Endpoint (NEW SESSION)
```
You: Add a signup endpoint

Claude: [Still follows rules from .claude/rules.md]
```

**Claude's code:**
```typescript
// src/api/endpoints/users.ts (same file, consistent!)
userRouter.post('/signup', async (req, res) => {
  try {
    const { error, value } = signupSchema.validate(req.body);
    if (error) {
      return res.status(400).json({ error: error.message });
    }

    const result = await UserService.signup(value);
    return res.json(result);
  } catch (err) {
    return res.status(500).json({ error: 'Internal server error' });
  }
});

// src/services/user.service.ts (same pattern)
export class UserService {
  static async signup(userData: SignupData) {
    // business logic here
  }
}

// src/validation/user.schema.ts (same location)
export const signupSchema = Joi.object({
  username: Joi.string().min(3).required(),
  email: Joi.string().email().required(),
  password: Joi.string().min(8).required()
});
```

### Session 3 - Add Password Reset
```
You: Add password reset endpoint

Claude: [Still consistent!]
```

**Claude's code:**
```typescript
// src/api/endpoints/users.ts (same file!)
userRouter.post('/reset-password', async (req, res) => {
  try {
    const { error, value } = resetPasswordSchema.validate(req.body);
    if (error) {
      return res.status(400).json({ error: error.message });
    }

    const result = await UserService.resetPassword(value);
    return res.json(result);
  } catch (err) {
    return res.status(500).json({ error: 'Internal server error' });
  }
});
```

**Result: Perfect consistency across all sessions!** ✨

---

## Copy-Paste Templates

### Template 1: React Project
```markdown
# .claude/rules.md

# Claude Rules for [Project Name]

## Tech Stack
- React 18 with TypeScript
- Vite for build
- React Router for routing
- TanStack Query for data fetching
- Tailwind CSS for styling

## Component Structure

### Location
- All components in `src/components/`
- Feature folders: `src/features/[feature-name]/`
- Shared components in `src/components/shared/`

### Component Format
- Functional components only (no classes)
- TypeScript with proper prop types
- Named exports (not default)
- Props interface named `[ComponentName]Props`

### Example
\`\`\`tsx
// src/components/Button.tsx
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  return (
    <button
      onClick={onClick}
      className={variant === 'primary' ? 'btn-primary' : 'btn-secondary'}
    >
      {label}
    </button>
  );
}
\`\`\`

## Hooks

### Custom Hooks
- All custom hooks in `src/hooks/`
- Must start with 'use'
- TypeScript return types required

### Example
\`\`\`tsx
// src/hooks/useAuth.ts
export function useAuth() {
  const [user, setUser] = useState<User | null>(null);
  // ... hook logic
  return { user, login, logout };
}
\`\`\`

## State Management
- Use React hooks for local state
- TanStack Query for server state
- Context for global UI state only
- No Redux/MobX

## Styling
- Tailwind CSS utility classes
- Custom classes in component.module.css if needed
- No inline styles (except dynamic values)

## Testing
- Vitest + React Testing Library
- Test files: `[ComponentName].test.tsx`
- Tests colocated with components
- Minimum 80% coverage

## File Naming
- Components: PascalCase (Button.tsx)
- Hooks: camelCase with 'use' prefix (useAuth.ts)
- Utils: camelCase (formatDate.ts)
- Types: PascalCase (User.ts)

## Imports
- Group: React, external libs, internal, relative
- Sort alphabetically within groups
- Use absolute imports with @ alias

## Error Handling
- Error boundaries for component errors
- Try-catch in async functions
- Show user-friendly error messages
```

---

### Template 2: Node.js API Project
```markdown
# .claude/rules.md

# Claude Rules for [Project Name]

## Tech Stack
- Node.js with TypeScript
- Express for routing
- PostgreSQL with Prisma
- Jest for testing

## Architecture

### 3-Layer Pattern
1. **API Layer** (`src/api/endpoints/`) - HTTP handling only
2. **Service Layer** (`src/services/`) - Business logic
3. **Data Layer** (`src/repositories/`) - Database access

### Never
- ❌ Business logic in controllers
- ❌ Database queries in controllers
- ❌ HTTP handling in services

## API Endpoints

### Location
- All endpoints in `src/api/endpoints/`
- One file per resource (users.ts, posts.ts)

### Structure
\`\`\`typescript
// src/api/endpoints/users.ts
import { Router } from 'express';
import { UserService } from '../../services/user.service';
import { createUserSchema } from '../../validation/user.schema';

export const userRouter = Router();

userRouter.post('/users', async (req, res) => {
  try {
    // 1. Validate
    const { error, value } = createUserSchema.validate(req.body);
    if (error) {
      return res.status(400).json({ error: error.message });
    }

    // 2. Call service
    const user = await UserService.createUser(value);

    // 3. Return response
    return res.status(201).json(user);
  } catch (err) {
    // 4. Handle errors
    if (err instanceof ValidationError) {
      return res.status(400).json({ error: err.message });
    }
    return res.status(500).json({ error: 'Internal server error' });
  }
});
\`\`\`

## Services

### Location
- All services in `src/services/`
- Named: `[resource].service.ts`
- Export class with static methods

### Structure
\`\`\`typescript
// src/services/user.service.ts
import { UserRepository } from '../repositories/user.repository';
import { CreateUserDto } from '../types/user.dto';

export class UserService {
  static async createUser(data: CreateUserDto) {
    // 1. Validate business rules
    // 2. Call repository
    // 3. Return result
    return UserRepository.create(data);
  }
}
\`\`\`

## Repositories

### Location
- All repositories in `src/repositories/`
- Named: `[resource].repository.ts`

### Structure
\`\`\`typescript
// src/repositories/user.repository.ts
import { prisma } from '../lib/prisma';

export class UserRepository {
  static async create(data: CreateUserData) {
    return prisma.user.create({ data });
  }

  static async findById(id: string) {
    return prisma.user.findUnique({ where: { id } });
  }
}
\`\`\`

## Validation
- Joi for all request validation
- Schemas in `src/validation/[resource].schema.ts`
- Validate in controller, not service

## Error Handling
- Custom error classes in `src/errors/`
- Always use try-catch in async functions
- Log errors with Winston
- Never expose internal errors to client

## Testing
- Jest with supertest
- Test files in `__tests__/`
- Unit tests for services
- Integration tests for endpoints
- Minimum 80% coverage

## Code Style
- TypeScript strict mode
- Async/await (never callbacks or .then)
- Destructure function parameters
- No abbreviations in names
```

---

### Template 3: Full-Stack App
```markdown
# .claude/rules.md

# Claude Rules for [Project Name]

## Tech Stack
- Frontend: Next.js 14 (App Router)
- Backend: Next.js API Routes
- Database: PostgreSQL with Prisma
- Auth: NextAuth.js

## Folder Structure
\`\`\`
src/
├── app/              # Next.js app router pages
├── components/       # React components
├── lib/             # Utilities, DB client
├── services/        # Business logic
├── types/           # TypeScript types
└── api/             # API route handlers
\`\`\`

## Frontend Rules

### Components
- Server Components by default
- 'use client' only when needed (interactivity, hooks)
- Props interface for every component
- Tailwind CSS for styling

### Data Fetching
- Server Components: Fetch directly
- Client Components: Use TanStack Query
- Never fetch in useEffect

## Backend Rules

### API Routes
- Location: `src/app/api/[resource]/route.ts`
- Export: GET, POST, PUT, DELETE functions
- Validate request body
- Return NextResponse

### Example
\`\`\`typescript
// src/app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { UserService } from '@/services/user.service';

export async function POST(req: NextRequest) {
  try {
    const body = await req.json();
    const user = await UserService.createUser(body);
    return NextResponse.json(user, { status: 201 });
  } catch (err) {
    return NextResponse.json(
      { error: 'Failed to create user' },
      { status: 500 }
    );
  }
}
\`\`\`

## Database
- Prisma for all database access
- Models in `prisma/schema.prisma`
- Repositories in `src/repositories/`
- Never use Prisma directly in components/API routes

## Types
- Shared types in `src/types/`
- DTOs for API requests/responses
- Entities for database models

## Testing
- Vitest for unit tests
- Playwright for E2E tests
- Test files colocated with source
```

---

## Before/After Comparison

### Code Style Rules

**Without Rules:**
```javascript
// Inconsistent mess
const x={a:1,b:2}
const y = {
  c: 3,
  d: 4,
}
function foo(){return "bar"}
function baz() {
  return 'qux'
}
```

**With Rules:**
```javascript
// Consistent and clean
const x = { a: 1, b: 2 };
const y = { c: 3, d: 4 };

function foo() {
  return 'bar';
}

function baz() {
  return 'qux';
}
```

---

### Architectural Rules

**Rule:** "All API calls through service layer"

**Without Rule:**
```typescript
// ❌ Direct API call in component
function UserProfile() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch('/api/users/1')
      .then(r => r.json())
      .then(setUser);
  }, []);

  return <div>{user?.name}</div>;
}
```

**With Rule:**
```typescript
// ✅ Through service layer
// src/services/user.service.ts
export class UserService {
  static async getUser(id: string) {
    const response = await fetch(`/api/users/${id}`);
    return response.json();
  }
}

// Component
function UserProfile() {
  const { data: user } = useQuery({
    queryKey: ['user', '1'],
    queryFn: () => UserService.getUser('1')
  });

  return <div>{user?.name}</div>;
}
```

---

## Exercise: Create Rules for Your Project

### Step 1: Identify Patterns
Look at your codebase and answer:
1. What tech stack do you use?
2. How are files organized?
3. What naming conventions exist?
4. Are there inconsistencies?

### Step 2: Write Rules
Create `.claude/rules.md` with:
```markdown
# Claude Rules for [Your Project]

## Tech Stack
- [List your technologies]

## Architecture
- [Describe your patterns]

## Code Style
- [Your conventions]

## File Organization
- [Your folder structure]

## Testing
- [Your testing approach]
```

### Step 3: Test with Claude
Start new session and ask Claude to:
1. Add a new feature
2. Observe if it follows your rules
3. Refine rules based on results

### Step 4: Iterate
- Rules too vague? Make them specific
- Claude not following? Add examples
- Too many rules? Consolidate or automate

---

## Real-World Example

### Scenario: E-commerce API

**Week 1: Without Rules**
```
Monday: Add products endpoint
  → Created in /routes/products.js
  → Used callbacks
  → No validation

Tuesday: Add orders endpoint
  → Created in /api/orders.ts (different location!)
  → Used async/await (different style!)
  → Joi validation (inconsistent!)

Wednesday: Add users endpoint
  → Created in /endpoints/user.js (third location!)
  → Mixed callbacks and promises
  → No validation

Result: Total mess, hard to maintain
```

**Week 2: With Rules**

Created `.claude/rules.md`:
```markdown
## API Endpoints
- Location: src/api/endpoints/
- TypeScript only
- Async/await required
- Joi validation required
- Structure: controller-service-repository
```

```
Monday: Add products endpoint
  → src/api/endpoints/products.ts ✓
  → TypeScript ✓
  → Async/await ✓
  → Joi validation ✓
  → Proper structure ✓

Tuesday: Add orders endpoint
  → src/api/endpoints/orders.ts ✓
  → Same pattern ✓
  → Consistent ✓

Wednesday: Add users endpoint
  → src/api/endpoints/users.ts ✓
  → Same pattern ✓
  → Consistent ✓

Result: Beautiful, maintainable codebase!
```

---

## Key Takeaways

1. **Rules create consistency** - Same pattern every time
2. **Rules persist across sessions** - Claude remembers them
3. **Rules should be specific** - Not vague guidelines
4. **Rules need examples** - Show Claude exactly what you want
5. **Rules save time** - No need to explain patterns repeatedly

**Start with `.claude/rules.md` and watch your codebase transform!** 📋✨
