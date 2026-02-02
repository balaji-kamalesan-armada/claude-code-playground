# Session Context Examples

## What IS a Session?

```
Session = Open Claude → Chat → Close Claude

Everything in between = ONE session
```

---

## Example 1: Poor Session Management ❌

**One 7-hour session, context exhausted:**

```
9:00 AM - SESSION START
Token: 0 / 200,000

You: Build REST API
Claude: [Works perfectly]
Token: 15,000 / 200,000 ✅


10:00 AM - Still same session
You: Add auth
Claude: [Still good]
Token: 35,000 / 200,000 ✅


12:00 PM - Still same session
You: Add database
Claude: [Starting to ask questions]
Token: 95,000 / 200,000 ⚠️


2:00 PM - Still same session
You: Add payments
Claude: "What database are you using again?"
You: (frustrated) "We set up PostgreSQL 2 hours ago!"
Token: 158,000 / 200,000 🚨


4:00 PM - Still same session
You: Add emails
Claude: "What authentication system?"
You: (very frustrated) "JWT! We built it at 10 AM!"
Token: 195,000 / 200,000 🔥 CRITICAL


RESULT:
- Duration: 7 hours
- Quality: Excellent → Good → Declining → Poor
- Frustration: MAXIMUM
- Context: EXHAUSTED
```

---

## Example 2: Good Session Management ✅

**Multiple focused sessions, fresh context:**

```
9:00 AM - SESSION 1: API Setup (30 min)
Token: 0 / 200,000
/remember Tech: Express, TypeScript, Prisma
Build API
Token: 15,000 / 200,000 ✅
[CLOSE CLAUDE]


10:00 AM - SESSION 2: Auth (45 min)
Token: 0 / 200,000 (Fresh!)
Add JWT auth
Claude: "Using Express/TypeScript..." ← Remembered!
Token: 32,000 / 200,000 ✅
[CLOSE CLAUDE]


11:00 AM - SESSION 3: Database (30 min)
Token: 0 / 200,000 (Fresh!)
Setup Prisma with PostgreSQL
Token: 25,000 / 200,000 ✅
[CLOSE CLAUDE]


1:00 PM - SESSION 4: Payments (45 min)
Token: 0 / 200,000 (Fresh!)
Add Stripe integration
Token: 38,000 / 200,000 ✅
[CLOSE CLAUDE]


2:00 PM - SESSION 5: Emails (30 min)
Token: 0 / 200,000 (Fresh!)
Add email notifications
Token: 27,000 / 200,000 ✅
[CLOSE CLAUDE]


RESULT:
- Duration: 3 hours 50 min (45% faster!)
- Quality: Excellent throughout
- Frustration: ZERO
- Context: Always fresh
```

---

## What is `/compact`?

**Compact = Summarize conversation to save tokens**

### Example:

**BEFORE `/compact`:**
```
Token: 85,000 / 200,000

You: "Create user model with email, name"
Claude: [Full 500 lines of code]
You: "Add validation"
Claude: [Full 200 lines of code]
You: "Add tests"
Claude: [Full 300 lines of code]

All messages and code still in context: 85,000 tokens
```

**AFTER `/compact`:**
```
Summary: Created user model with email/name,
added validation, added tests. Current state
ready for next feature.

Token: 30,000 / 200,000 ✅ Saved 55,000 tokens!
```

### When to Use `/compact`:

```
✅ Use when:
- Token count > 100,000
- Want to continue same session
- Finished a sub-task

❌ Don't use when:
- Token count < 50,000 (no benefit)
- Debugging (need full context)
- About to restart anyway
```

---

## How Memory Helps Sessions

### Problem: Repeating Wastes Tokens

**WITHOUT Memory:**
```
Every session you repeat:
"Use Express, TypeScript, Prisma, PostgreSQL,
 3-layer architecture, ESLint Airbnb..."

Cost: 450 tokens EVERY SESSION
10 sessions: 4,500 tokens wasted! 🔥
```

**WITH Memory:**
```
Session 1: /remember Tech: Express, TypeScript...
           /remember Architecture: 3-layer...
           Cost: 150 tokens (once)

Sessions 2-100: Claude remembers automatically
                Cost: 0 tokens! ✨

10 sessions: 150 tokens total
Saved: 4,350 tokens!
```

---

## Token Budget Guide

```
0-50k tokens:       ✅ Fresh, optimal
50k-100k tokens:    ✅ Good, keep going
100k-130k tokens:   ⚠️  Use /compact if continuing
130k-150k tokens:   ⚠️  Finish task soon
150k-170k tokens:   🚨 Finish current subtask
170k+ tokens:       🔥 Close NOW
```

---

## When to Restart

### ✅ Start New Session When:

1. **Task complete**
   ```
   Auth done → Close → New session → Database
   ```

2. **Tokens > 150k**
   ```
   Token: 165,000 / 200,000 → Close → Fresh session
   ```

3. **Claude seems confused**
   ```
   Asks questions already answered → Close → Fresh session
   ```

4. **Switching features**
   ```
   Login done → Close → New session → Payment
   ```

### ❌ Don't Restart When:

1. **Mid-task**
   ```
   Building login → DON'T restart → Finish first
   ```

2. **Tokens still low**
   ```
   Token: 40,000 / 200,000 → Keep going
   ```

3. **Small related changes**
   ```
   Fix bug → Add test → Same session OK
   ```

---

## Practical Decision Guide

```
"Should I close or continue?"

Close if:                Continue if:
✅ Task complete         ✅ Mid-task
✅ Tokens > 150k         ✅ Tokens < 100k
✅ Quality dropping      ✅ Quality good
✅ Claude confused       ✅ Claude working well
✅ Switching features    ✅ Related subtasks
```

---

## Exercise: Monitor Your Session

Try this:

1. **Start Claude, check tokens**
   - Look for: "Token usage: X / 200,000"

2. **Ask a simple question**
   - Check new token count
   - See how much it grew

3. **Read a file**
   - Check token count
   - Files use more tokens!

4. **Continue for 5-10 exchanges**
   - Watch tokens grow
   - Note the pattern

5. **Ask yourself:**
   - At what point should I restart?
   - Could I use `/compact` instead?
   - Should I use memory to save tokens?

---

## Key Takeaways

1. **Session = Open to Close**
   - Everything in message window
   - Has 200k token limit
   - Clears when you close

2. **`/compact` = Summarize**
   - Saves tokens mid-session
   - Use at 100k+ tokens
   - Keeps session alive

3. **Memory = 0 Tokens**
   - Set once, use forever
   - Survives session restart
   - No repetition needed

4. **Fresh Sessions = Better Quality**
   - One task per session
   - Close when task done
   - Monitor tokens always

---

## Quick Reference

```
MEMORY              SESSION CONTEXT
(Permanent)         (Temporary)
─────────────────   ──────────────────
Tech stack          Current messages
Architecture        Files being read
Rules               Commands run
Preferences         This conversation

Lasts: Forever      Lasts: Until close
Cost: 0 tokens      Cost: Uses tokens
Limit: None         Limit: 200k tokens
```

**Monitor tokens, use memory, restart strategically!** 📊✨
