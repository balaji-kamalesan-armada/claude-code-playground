# Session Context: Managing Conversations

**→ Confused about sessions, tokens, or `/compact`? Read [EXAMPLES.md](EXAMPLES.md) - everything explained! ←**

## What is Session Context?

Session context is your **current conversation history**. It includes everything in THIS session, but has limits.

```
SESSION CONTEXT = Messages + Files read + Commands run (THIS SESSION ONLY)
```

## Key Concept: Token Budget

Every session has a **token budget**:
- Claude Code: ~200,000 tokens
- 1 token ≈ 4 characters
- ~50,000 words per session

**When full:** Context gets summarized or you need to restart.

## The Three Layers

```
1. MEMORY (Permanent)
   ↓ Tech stack, Architecture, Rules
   ↓ Lasts: Forever

2. SESSION CONTEXT (Temporary)
   ↓ This conversation, files read
   ↓ Lasts: Until you close Claude
   ↓ Limit: ~200k tokens

3. CURRENT MESSAGE (Right now)
   ↓ Your question, Claude's answer
   ↓ Lasts: This exchange
```

## The Problem: Context Exhaustion

**Early in session:**
```
Token usage: 5,000 / 200,000
You: "Add login button"
Claude: [Perfect, reads all files, understands everything]
```

**Late in session:**
```
Token usage: 180,000 / 200,000
You: "Add logout button"
Claude: [Struggles, can't read many files, inconsistent]
```

**Signs context is full:**
- ⚠️ Claude asks questions you already answered
- ⚠️ Quality decreases
- ⚠️ Inconsistent with earlier code
- ⚠️ Token usage > 150,000

## When to Start New Session

### ✅ Start New Session:

1. **Finished a major task**
   ```
   ✅ Auth complete → Close → New session → Database
   ```

2. **Token count high**
   ```
   ✅ > 150,000 tokens → Close → Fresh session
   ```

3. **Claude seems confused**
   ```
   ✅ Asks repeated questions → Close → Fresh session
   ```

4. **Switching to different feature**
   ```
   ✅ Login done → Close → New session → Payment
   ```

### ❌ Don't Start New Session:

1. **Mid-task**
   ```
   ❌ Building login → DON'T restart → Finish first
   ```

2. **Small related changes**
   ```
   ❌ Fix bug → Add test → Same session OK
   ```

3. **Low token count**
   ```
   ❌ < 100,000 tokens → Keep going
   ```

## Managing Sessions

### Strategy 1: One Session, One Task

**Bad:**
```
SESSION 1 (7 hours):
- Build auth
- Create database
- Add validation
- Setup deployment
- Write docs
[Context exhausted, quality drops]
```

**Good:**
```
SESSION 1 (30 min): Auth [Complete, close]
SESSION 2 (45 min): Database [Complete, close]
SESSION 3 (30 min): Validation [Complete, close]
[Fresh context every time, high quality]
```

### Strategy 2: Use Memory, Not Context

**Without memory (wastes tokens):**
```
Every session:
You: "Use Express, TypeScript, PostgreSQL, Prisma..."
[Uses 500 tokens every session]
```

**With memory (no tokens):**
```
Session 1: /remember Tech: Express, TypeScript, PostgreSQL, Prisma
All future sessions: [Claude remembers, 0 tokens]
```

### Strategy 3: Read Only What You Need

**Bad (uses lots of tokens):**
```
You: "Read all 20 files in src/"
[Loads 50,000 tokens]
```

**Good (efficient):**
```
You: "Read src/auth/login.ts only"
[Loads 2,000 tokens]
```

## Real Example

**Poor Session Management:**
```
9 AM: Build REST API
10 AM: Add auth (same session)
12 PM: Create database (same session)
2 PM: Add payments (same session)
4 PM: Add emails (same session)

Token usage: 195,000 / 200,000
Quality: Degraded after 12 PM
Consistency: Poor
```

**Good Session Management:**
```
9 AM: SESSION 1 - REST API basics [Close]
10 AM: SESSION 2 - Auth [Close]
11 AM: SESSION 3 - Database [Close]
1 PM: SESSION 4 - Payments [Close]
2 PM: SESSION 5 - Emails [Close]

Token usage: 30,000-50,000 per session
Quality: High throughout
Consistency: Excellent
```

## Monitoring Tokens

Look for this in Claude's responses:
```
Token usage: 45,000 / 200,000; 155,000 remaining
```

**Guidelines:**
- **0-50k:** Fresh, optimal ✅
- **50k-100k:** Good, keep going ✅
- **100k-150k:** Monitor, finish task soon ⚠️
- **150k+:** Close after current task ⚠️

## Quick Reference

```
MEMORY          SESSION CONTEXT         CURRENT MESSAGE
(Permanent)     (Temporary)            (Right now)
├─ Tech stack   ├─ Messages           ├─ Your question
├─ Architecture ├─ Files read         └─ Claude's answer
├─ Rules        ├─ Commands run
└─ Preferences  └─ This conversation

Lasts: Forever  Lasts: Until close    Lasts: One exchange
Limit: None     Limit: 200k tokens    Limit: Per message
```

## Best Practices

**DO:**
- ✅ One major task per session
- ✅ Close when task complete
- ✅ Monitor token usage
- ✅ Use memory for permanent facts
- ✅ Restart if quality drops

**DON'T:**
- ❌ 8-hour sessions
- ❌ Mix unrelated tasks
- ❌ Restart mid-task
- ❌ Ignore high token count
- ❌ Repeat info (use memory)

## Key Takeaways

1. **Session context is temporary** (cleared when closed)
2. **Memory is permanent** (survives restarts)
3. **Fresh sessions = Better quality**
4. **One session, one task**
5. **Monitor token usage**

## Examples & Practice

**See it in action:**
→ [EXAMPLES.md](EXAMPLES.md) - Everything you need:
  - What IS a session?
  - What is `/compact`?
  - How memory saves tokens
  - When to restart
  - Real examples & exercises
  - Practical context exhaustion scenarios

**Want to experience hitting the limit?**
→ [CONTEXT-EXHAUSTION-CHALLENGE.md](CONTEXT-EXHAUSTION-CHALLENGE.md) - Deliberately exhaust context:
  - 6 practical challenges to hit the 200k token limit
  - Learn warning signs before it happens
  - Compare bad vs good session management
  - Develop your personal strategy
  - Safe environment to break things and learn!

## Next Steps

1. Read [EXAMPLES.md](EXAMPLES.md) for complete guide
2. Try [CONTEXT-EXHAUSTION-CHALLENGE.md](CONTEXT-EXHAUSTION-CHALLENGE.md) to feel the limits
3. Then move to [Module 4: Skills](../04-SKILLS/README.md)

---

**Remember: Fresh sessions = Better results!** 🔄✨
