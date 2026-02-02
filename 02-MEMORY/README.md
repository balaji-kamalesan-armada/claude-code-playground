# Memory: What Claude Remembers Forever

## What is Memory?

Memory is what Claude remembers **across all sessions**. It's permanent until you remove it.

```
MEMORY = What Claude remembers FOREVER
CONTEXT = What Claude sees RIGHT NOW (temporary)
```

## Key Difference

```
SESSION 1                   SESSION 2
[Talk about Express]        [Claude still remembers Express!]
Close Claude ───────────────> Memory persists
[Context cleared]           [Start fresh, but memory remains]
```

## The `/remember` Command

Use `/remember` to store permanent facts:

```bash
/remember Project: TaskMaster - Team task management API
/remember Tech: Express, TypeScript, PostgreSQL, Prisma
/remember Architecture: 3-layer REST API (API, Service, Data)
/remember Style: ESLint Airbnb + Prettier, camelCase functions
/remember Business: Premium users ($9.99/mo) get 20% discount
```

## Memory vs Context Example

### Without Memory (Every Session):
```
SESSION 1:
You: "Build an API with Express and TypeScript"
Claude: [Builds it]

SESSION 2 (next day):
You: "Add authentication"
Claude: "What's your tech stack?" ← Forgot!
You: "Express and TypeScript" ← Repeat!
Claude: "What database?"
You: "PostgreSQL" ← Repeat again!
```

### With Memory (Once):
```
SESSION 1:
You: "/remember Tech: Express, TypeScript, PostgreSQL"
You: "/remember Architecture: REST API, 3-layer pattern"
You: "Build an API"
Claude: [Builds it]

SESSION 2 (next day):
You: "Add authentication"
Claude: "I'll add auth to your Express/TypeScript API..." ← Remembers!
[No repetition needed]
```

**Time saved: 5+ minutes every session!**

## What to Remember

### ✅ Remember These:

**Tech Stack:**
```bash
/remember Tech: Node.js 18, Express, TypeScript, Prisma, PostgreSQL
/remember Testing: Jest for unit tests, 80% coverage required
```

**Architecture:**
```bash
/remember Architecture: REST API with 3-layer pattern
/remember Folders: src/api/endpoints/, src/services/, src/models/
```

**Conventions:**
```bash
/remember Style: ESLint Airbnb, Prettier, 2 spaces, single quotes
/remember Naming: camelCase functions, PascalCase classes, kebab-case files
/remember Docs: JSDoc required for all exported functions
```

**Business Rules:**
```bash
/remember Business: Premium users get 20% discount
/remember Business: Free shipping over $50, else $10 flat rate
/remember Business: 30-day refund policy with receipt required
```

**Preferences:**
```bash
/remember Preference: Test-driven development (write tests first)
/remember Preference: Detailed comments explaining "why"
```

### ❌ Don't Remember These:

```bash
# ❌ Current work (temporary)
/remember Working on authentication feature

# ❌ File contents (they change)
/remember user.js has getUserById on line 23

# ❌ Bugs (temporary)
/remember Bug in login function on line 45

# ❌ This conversation (already in context)
/remember We discussed using JWT tokens
```

## The Memory Test

Before using `/remember`, ask:

1. **"Will this be true tomorrow?"**
   - ✅ "We use TypeScript" → Remember
   - ❌ "I'm debugging line 45" → Don't remember

2. **"Is this permanent or temporary?"**
   - ✅ "Premium users get 20% off" → Remember
   - ❌ "Working on auth feature" → Don't remember

3. **"Would I want Claude to know this next month?"**
   - ✅ "We use Prisma for database" → Remember
   - ❌ "There's a bug in user.js" → Don't remember

**If YES to all 3: Use `/remember`**

## Quick Start Template

Copy and customize:

```bash
# === CORE ===
/remember Project: [Name] - [Description]
/remember Tech: [Runtime, Framework, Language, Database]
/remember Architecture: [Pattern]

# === CONVENTIONS ===
/remember Style: [Linter, formatter, rules]
/remember Naming: [Conventions]
/remember Docs: [Requirements]

# === BUSINESS ===
/remember Business: [Key rule 1]
/remember Business: [Key rule 2]

# === PREFERENCES ===
/remember Preference: [Your working style]
```

### Example:
```bash
# === CORE ===
/remember Project: ShopAPI - E-commerce REST API
/remember Tech: Express, TypeScript, Prisma, PostgreSQL
/remember Architecture: 3-layer REST (API, Service, Data)

# === CONVENTIONS ===
/remember Style: ESLint Airbnb + Prettier
/remember Naming: camelCase functions, PascalCase classes
/remember Docs: JSDoc required for exports

# === BUSINESS ===
/remember Business: Premium ($9.99/mo) get 20% discount
/remember Business: Free shipping over $50

# === PREFERENCES ===
/remember Preference: Test-driven development
```

## Managing Memory

### View Memory:
```bash
# Ask Claude:
"What do you remember about this project?"
```

### Update Memory:
```bash
# If tech changes:
/remember Tech: Upgraded to Node.js 20 (from 18) for performance

# If business rules change:
/remember Business: Premium discount increased to 25% (was 20%)
```

### Organize Memory:
```bash
# Use prefixes for categories:
/remember [Tech] Express, TypeScript, PostgreSQL
/remember [Business] Premium users get 20% discount
/remember [Style] ESLint Airbnb + Prettier
```

## Common Mistakes

### ❌ Mistake 1: Over-Remembering
```bash
/remember File user-service.ts line 23 has getUserById
/remember Database connection in index.ts line 12
```
**Fix:** Remember patterns, not specifics
```bash
/remember Pattern: All database access through Prisma
/remember Pattern: Services use static methods
```

### ❌ Mistake 2: Under-Remembering
```bash
/remember We use a database
```
**Fix:** Be specific
```bash
/remember Database: PostgreSQL 14+ with Prisma ORM
```

### ❌ Mistake 3: Remembering Temporary State
```bash
/remember Currently working on authentication
/remember Bug on line 45 needs fixing
```
**Fix:** Remember outcomes, not process
```bash
/remember Auth: JWT tokens with 24-hour expiration
```

## Real Example

### Session 1: Setup
```bash
/remember Project: BlogHub - Blogging platform with markdown
/remember Tech: Next.js 14, React 18, TypeScript, MongoDB
/remember Architecture: App Router, Server Components default
/remember Style: Tailwind CSS, ESLint Next.js config
/remember Business: Free tier (5 posts), Pro tier ($5/mo, unlimited)
```

### Session 2 (Next Day): Add Feature
```
You: "Add comment system"
Claude: "I'll add comments to your BlogHub Next.js app with MongoDB,
        following your Server Components pattern..."
[Already knows everything!]
```

### Session 3 (Next Week): Refactor
```
You: "Optimize the post listing"
Claude: "I'll optimize post listing in your Next.js app, keeping
        the Free (5 posts) vs Pro (unlimited) tier logic..."
[Still remembers business rules!]
```

## Key Takeaways

1. **Memory Persists Forever**
   - Context disappears, memory stays
   - Set it once, use it forever

2. **Remember Facts, Not State**
   - ✅ Tech stack, architecture, rules
   - ❌ Current work, bugs, files

3. **Memory Saves Time**
   - No repetition across sessions
   - Consistent help every time

4. **Update as Needed**
   - Tech upgrades
   - Business rule changes
   - Pattern evolution

## Examples & Practice

**See it in action:**
→ [EXAMPLES.md](EXAMPLES.md) - Real conversations, exercises, templates

## Next Steps

1. Read [EXAMPLES.md](EXAMPLES.md) for hands-on practice
2. Then move to [Module 3: Session Context](../03-SESSION-CONTEXT/README.md)

---

**Remember: Memory = What Claude Remembers FOREVER** 🧠✨
