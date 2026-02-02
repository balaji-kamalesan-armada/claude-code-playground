# Context: What Claude Sees

## What is Context?

Context is everything Claude sees in **this conversation**. It's temporary and disappears when you close the session.

```
CONTEXT = What Claude sees RIGHT NOW
```

## The 3 Core Types

### 1. **Code Context** (in your files)
```javascript
// ❌ BAD - No context
function calc(x) { return x * 2; }

// ✅ GOOD - Rich context
/**
 * Calculate expedited shipping (2x base price)
 * @param {number} basePrice - Base shipping in USD
 */
function calculateExpeditedShipping(basePrice) {
  return basePrice * 2;
}
```

**Code context includes:**
- Descriptive function/variable names
- Comments explaining "why"
- JSDoc documentation
- File structure and organization

### 2. **Project Context** (project files)
- `README.md` - Project overview
- `package.json` - Dependencies and scripts
- `.claude/rules.md` - Coding standards
- `CONTRIBUTING.md` - How to contribute

### 3. **Conversation Context** (this chat)
- Your messages
- Claude's responses
- Files Claude has read
- Commands you've run

## Quick Test

**Ask yourself: "Will Claude see this in our conversation?"**
- ✅ YES = It's context
- ❌ NO = It's not context

## Examples

### Example 1: Function Names
```javascript
// Low context
function p(x, y) { return x + y - x * 0.2; }

// High context
function calculateFinalPrice(basePrice, shippingCost) {
  const discount = basePrice * 0.2; // 20% premium discount
  return basePrice + shippingCost - discount;
}
```

### Example 2: Project Files
```
Low Context Project:
my-app/
├── index.js
└── utils.js

High Context Project:
my-app/
├── README.md              ← Explains what this is
├── .claude/rules.md       ← Coding standards
├── src/
│   ├── api/endpoints/     ← Clear structure
│   ├── services/          ← Business logic
│   └── models/            ← Data models
└── docs/
    └── API.md             ← API documentation
```

### Example 3: Comments
```javascript
// ❌ No context
if (u.t === 'p') { d = d * 0.8; }

// ✅ Full context
// Premium users get 20% discount on all purchases
if (user.tier === 'premium') {
  discount = discount * 0.8;
}
```

## Why Context Matters

**Without Context:**
```
You: "Fix the bug in the user function"
Claude: "Which file? Which function? What's the bug?"
[You spend 5 minutes explaining]
```

**With Context:**
```
You: "Fix the bug in getUserById in src/services/user-service.ts"
Claude: [Reads file, sees JSDoc, understands immediately]
[Starts fixing in 10 seconds]
```

## How to Add Context

### 1. Use Descriptive Names
```javascript
// ❌ Bad
const x = u.p * 2;

// ✅ Good
const expeditedPrice = user.basePrice * 2;
```

### 2. Add "Why" Comments
```javascript
// ❌ Bad
price = price * 0.8;

// ✅ Good
// Premium members get 20% discount
price = price * 0.8;
```

### 3. Create Project Files
```bash
# Minimum context files
README.md              # What is this project?
.claude/rules.md       # How should code be written?
```

### 4. Organize Code Logically
```
src/
├── api/endpoints/     # HTTP endpoints
├── services/          # Business logic
├── models/            # Data structures
└── utils/             # Helper functions
```

## Context Checklist

Before asking Claude for help:

- [ ] Are my variable names descriptive?
- [ ] Do I have comments explaining business logic?
- [ ] Does my project have a README.md?
- [ ] Is my code organized in clear folders?
- [ ] Have I provided Claude with relevant file paths?

## Common Mistakes

### ❌ Mistake 1: Cryptic Names
```javascript
function h(u, p) {
  return p > 50 ? 0 : 10;
}
```

### ✅ Fix: Descriptive Names
```javascript
function calculateShippingCost(user, purchaseTotal) {
  // Free shipping over $50
  return purchaseTotal > 50 ? 0 : 10;
}
```

### ❌ Mistake 2: No Project Documentation
```
my-project/
└── index.js    ← What does this project do?
```

### ✅ Fix: Add README
```
my-project/
├── README.md   ← Explains the project
└── index.js
```

## Key Takeaways

1. **Context = What Claude Sees**
   - Code, comments, project files, conversation

2. **Context is Temporary**
   - Only exists in this session
   - Disappears when you close Claude

3. **Good Context Saves Time**
   - Less explaining, more doing
   - Claude understands faster

4. **3 Ways to Add Context**
   - Better code (names, comments)
   - Project files (README, rules)
   - Clear conversation (specific questions)

## Examples & Practice

**See it in action:**
→ [EXAMPLES.md](EXAMPLES.md) - Code examples, exercises, solutions

## Next Steps

1. Read [EXAMPLES.md](EXAMPLES.md) for hands-on practice
2. Then move to [Module 2: Memory](../02-MEMORY/README.md)

---

**Remember: Context = What Claude Sees RIGHT NOW** 👀
