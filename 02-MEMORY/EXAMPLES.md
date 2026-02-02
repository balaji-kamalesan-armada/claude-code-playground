# Memory Examples

## Example 1: Without Memory (Frustration) ❌

### Session 1 - Monday 9:00 AM
```
You: Build a REST API with Express and TypeScript

Claude: [Creates API]
```

### Session 2 - Monday 2:00 PM (NEW SESSION)
```
You: Add authentication

Claude: What's your tech stack?

You: (frustrated) Express and TypeScript

Claude: What database?

You: PostgreSQL with Prisma

Claude: [Finally creates auth after asking questions]
```

### Session 3 - Tuesday (NEW SESSION)
```
You: Add task endpoints

Claude: What's your tech stack?

You: (very frustrated) Express, TypeScript, PostgreSQL, Prisma...

Claude: What's your architecture?

You: 3-layer pattern...

[Repeat everything AGAIN]
```

**Result: 20+ minutes wasted repeating yourself across 3 sessions** 😫

---

## Example 2: With Memory (Smooth) ✅

### Session 1 - Monday 9:00 AM
```
You:
/remember Project: TaskAPI - Team task management
/remember Tech: Express, TypeScript, PostgreSQL, Prisma
/remember Architecture: 3-layer (API, Service, Data)
/remember Style: ESLint Airbnb + Prettier

You: Build a REST API

Claude: [Creates API using all remembered info]
```

### Session 2 - Monday 2:00 PM (NEW SESSION)
```
You: Add authentication

Claude: I'll add JWT authentication to your Express/TypeScript
        API using Prisma and PostgreSQL, following your
        3-layer architecture...

[No questions, immediate start!]
```

### Session 3 - Tuesday (NEW SESSION)
```
You: Add task endpoints

Claude: I'll create task endpoints in src/api/endpoints/
        following your 3-layer pattern with Express and Prisma...

[Still remembers everything!]
```

**Result: 0 minutes wasted, consistent code, zero frustration** ✨

---

## Real Conversation Examples

### WITHOUT Memory - 5 Sessions

**SESSION 1:**
```
You: Build API
Claude: [Works]
```

**SESSION 2:**
```
You: Add auth
Claude: "What's your tech stack?" ← Forgot!
You: "Express, TypeScript..." ← Repeat
```

**SESSION 3:**
```
You: Add database
Claude: "What database?" ← Forgot again!
You: "PostgreSQL with Prisma" ← Repeat again
```

**SESSION 4:**
```
You: Add validation
Claude: "What validation library?" ← Still asking
You: "Joi..." ← Still repeating
```

**SESSION 5:**
```
You: Add payments
Claude: "What's your architecture?" ← Lost track
You: "3-layer pattern..." ← Exhausted
```

**Total: 15+ questions, 20+ minutes wasted**

---

### WITH Memory - 6 Sessions

**SESSION 1:**
```
You: /remember Tech: Express, TypeScript, PostgreSQL, Prisma
     /remember Architecture: 3-layer pattern
     /remember Style: ESLint Airbnb
You: Build API
Claude: [Works]
```

**SESSION 2:**
```
You: Add auth
Claude: "Using Express/TypeScript..." ← Remembered!
```

**SESSION 3:**
```
You: Add database
Claude: "With Prisma and PostgreSQL..." ← Remembered!
```

**SESSION 4:**
```
You: Add validation
Claude: "Following your 3-layer pattern..." ← Remembered!
```

**SESSION 5:**
```
You: Add payments
Claude: "In your Express API..." ← Remembered!
```

**SESSION 6:**
```
You: Add emails
Claude: "Following ESLint Airbnb style..." ← Remembered!
```

**Total: 0 questions, 0 minutes wasted, 25+ minutes saved!**

---

## What to Remember

### ✅ DO Remember:

```bash
# Tech Stack
/remember Tech: Express, TypeScript, PostgreSQL, Prisma

# Architecture
/remember Architecture: 3-layer REST (API, Service, Data)
/remember Folders: src/api/, src/services/, src/models/

# Conventions
/remember Style: ESLint Airbnb + Prettier
/remember Naming: camelCase functions, PascalCase classes

# Business Rules
/remember Business: Premium users get 20% discount
/remember Business: Free shipping over $50
```

### ❌ DON'T Remember:

```bash
# Current work (temporary)
❌ /remember Working on authentication feature

# File contents (they change)
❌ /remember user.js has getUserById on line 23

# Bugs (temporary)
❌ /remember Bug in login function

# This conversation (already in context)
❌ /remember We discussed using JWT tokens
```

---

## The Memory Test

Before using `/remember`, ask:

1. **"Will this be true tomorrow?"**
   - ✅ "We use TypeScript" → Remember
   - ❌ "I'm debugging line 45" → Don't remember

2. **"Is this permanent or temporary?"**
   - ✅ "Premium users get 20% off" → Remember
   - ❌ "Working on auth" → Don't remember

3. **"Would I want Claude to know this next month?"**
   - ✅ "We use Prisma" → Remember
   - ❌ "Bug in user.js" → Don't remember

**If YES to all 3: Use `/remember`**

---

## Exercise: Set Up Memory

For a project with these details:
- Name: BlogAPI
- Tech: Next.js, TypeScript, MongoDB, Mongoose
- Pattern: App Router with Server Components
- Style: Tailwind CSS

**Your task:** Write `/remember` commands

<details>
<summary>Click to see solution</summary>

```bash
/remember Project: BlogAPI - Blogging platform with markdown support
/remember Tech: Next.js 14, React 18, TypeScript, MongoDB, Mongoose
/remember Architecture: App Router, Server Components default
/remember Style: Tailwind CSS, ESLint Next.js config
```

</details>

---

## Quick Start Template

Copy and customize for your project:

```bash
# === CORE ===
/remember Project: [Name] - [Description]
/remember Tech: [Runtime, Framework, Language, Database]
/remember Architecture: [Pattern]

# === CONVENTIONS ===
/remember Style: [Linter, formatter]
/remember Naming: [Conventions]
/remember Docs: [Requirements]

# === BUSINESS ===
/remember Business: [Key rule 1]
/remember Business: [Key rule 2]
```

---

## Key Takeaways

1. **Memory persists forever** (until you change it)
2. **Context disappears** (when session closes)
3. **Set memory once, use forever**
4. **Remember facts, not state**
5. **Memory saves 20+ minutes per project**

**Use `/remember` to never repeat yourself!** 🧠✨
