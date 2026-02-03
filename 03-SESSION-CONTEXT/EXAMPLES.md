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

## Exercise 1: Monitor Your Session

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

## Exercise 2: Deliberately Exhaust Context 🔥

**Goal:** Experience hitting the context limit so you know what it feels like

### Scenario 1: Read Large Files Repeatedly

**What to do:**
```
1. Start new Claude session
2. Read a large file (>2000 lines): "Read src/large-file.ts"
3. Ask Claude to explain different parts of it
4. Read another large file
5. Ask Claude to compare them
6. Read 5-10 more large files
7. Keep asking questions about each file
8. Watch token count climb: 50k → 100k → 150k → 180k+
```

**What you'll experience:**
- Token count grows rapidly with each file read
- Around 150k tokens, Claude may start being less detailed
- Near 180k tokens, you'll notice degraded quality
- At ~200k tokens, you can't send more messages

**When this happens in real work:**
- Reading too many files without restarting
- Long debugging sessions with multiple file reads
- Code reviews of large PRs in one session

---

### Scenario 2: Generate Large Amounts of Code

**What to do:**
```
1. Start new session
2. Ask: "Create a complete Express REST API with 10 endpoints"
3. Claude generates ~1000 lines of code (15k tokens)
4. Ask: "Add validation for all endpoints"
5. Claude generates ~500 more lines (8k tokens)
6. Ask: "Add tests for everything"
7. Claude generates ~800 lines tests (12k tokens)
8. Ask: "Add authentication middleware"
9. Ask: "Add error handling"
10. Ask: "Add logging"
11. Ask: "Add documentation"
12. Keep going...
```

**What you'll experience:**
- Each large code generation uses 10-20k tokens
- After 8-10 generations, you're at 100k+ tokens
- Around 150k, Claude's responses get shorter
- Context window fills with all previous code
- Eventually can't send more messages

**When this happens in real work:**
- Building large features in one session
- Multiple refactoring iterations
- Generating extensive test suites

---

### Scenario 3: Long Conversation with Context Build-up

**What to do:**
```
1. Start debugging a complex issue
2. Ask Claude questions, get answers
3. Share error logs (paste large log files)
4. Ask follow-up questions
5. Try solutions, share results
6. More questions, more context
7. Keep conversation going for 2+ hours
8. Never close, never /compact
```

**What you'll experience:**
- Gradual token accumulation: +5k per exchange
- After 50+ exchanges: 100k+ tokens
- Claude starts asking "What was X again?"
- Quality degrades slowly, easy to miss
- Finally hits limit

**When this happens in real work:**
- Long debugging sessions
- Complex architecture discussions
- Pair programming sessions
- Code reviews with lots of back-and-forth

---

### Scenario 4: Forced Exhaustion Challenge 🎯

**Deliberate exercise to hit the wall:**

```bash
# Do this intentionally to feel the limit:

1. Start Claude session
2. Check token count: 0 / 200,000

3. Read 10 large files from your codebase:
   "Read src/file1.ts"
   "Read src/file2.ts"
   ... (repeat for all 10)

   Token: ~80,000 / 200,000

4. Ask Claude to analyze all files:
   "Compare the architecture across these files"
   "Identify code duplication"
   "Suggest refactoring opportunities"

   Token: ~120,000 / 200,000

5. Generate code based on analysis:
   "Create a new service that consolidates logic"
   "Add tests for the new service"
   "Add documentation"

   Token: ~160,000 / 200,000

6. Keep asking questions:
   "Explain how this integrates"
   "What are the edge cases"
   "Show me error handling"

   Token: ~185,000 / 200,000

7. Try to continue...
   Token: ~198,000 / 200,000

   ⚠️ WARNING: Context nearly full

8. One more message...
   🔥 ERROR: Cannot send message, context exhausted
```

**What you'll learn:**
- Exactly what "context exhaustion" feels like
- Warning signs before hitting the limit
- Why strategic session management matters
- When `/compact` could have helped
- When to restart sessions

---

### Recovery Strategies After Exhaustion

**When you hit the limit:**

**Option 1: Start Fresh Session** (Best)
```
1. Close Claude completely
2. Open new session
3. Use /remember for key facts
4. Continue with fresh context
```

**Option 2: Use /compact Earlier** (Prevention)
```
Before hitting limit:
- At 100k tokens: /compact
- Freed space: Continue working
- At 130k again: /compact or restart
```

**Option 3: Save Progress First**
```
1. Copy important context/decisions
2. Close session
3. Open new session
4. Paste key information back
5. Continue
```

---

### Signs You're Approaching Limit

**Watch for these warnings:**

1. **Token count visible:**
   ```
   150k+ = Start planning restart
   170k+ = Finish current task
   190k+ = Can't continue much longer
   ```

2. **Claude behavior changes:**
   - Shorter responses
   - Asks about things discussed earlier
   - Less detailed explanations
   - "Can you remind me about X?"

3. **Quality drops:**
   - More generic answers
   - Missing context from earlier
   - Inconsistent with previous work
   - Repetition of suggestions

---

### Best Practices to Avoid Exhaustion

1. **Monitor tokens constantly**
   - Check after every major operation
   - Plan restart before 150k

2. **Use memory strategically**
   - Store facts once
   - Never repeat tech stack
   - 0 tokens for persistent info

3. **Close sessions between tasks**
   - One feature = One session
   - Don't string together unrelated work
   - Fresh context = Better quality

4. **Use /compact wisely**
   - When continuing same feature
   - At 100k-130k token range
   - Not a substitute for restart

5. **Avoid reading unnecessary files**
   - Only read what you need
   - Don't read entire codebase
   - Read specific files for specific tasks

---

## Real-World Exhaustion Example

**What happened:**
```
Developer building payment integration:
  9 AM: Started session, read Stripe docs (20k)
 10 AM: Read existing payment code (15k)
 11 AM: Generated new integration (25k)
 12 PM: Fixed bugs, read more files (30k)
  1 PM: Added tests (20k)
  2 PM: Refactored code (25k)
  3 PM: Added error handling (20k)
  4 PM: Documentation (15k)

Total: 170k tokens
Quality: Excellent → Good → Degraded
Result: Had to restart, lost context
```

**Better approach:**
```
SESSION 1 (9-10 AM): Research
  - Read Stripe docs
  - Plan approach
  - Close at 30k tokens ✅

SESSION 2 (10-11 AM): Implementation
  - Build integration
  - Close at 40k tokens ✅

SESSION 3 (11 AM-12 PM): Testing
  - Add tests
  - Fix bugs
  - Close at 35k tokens ✅

SESSION 4 (1-2 PM): Polish
  - Error handling
  - Documentation
  - Close at 30k tokens ✅

Total: 135k tokens spread across 4 sessions
Quality: Excellent throughout ✨
```

---

## Try It Yourself: Context Exhaustion Lab

**Controlled experiment:**

1. **Week 1: Bad habits**
   - Work in single sessions all day
   - Never restart
   - Read lots of files
   - Track when you hit issues

2. **Week 2: Good habits**
   - Restart between tasks
   - Use memory for facts
   - Monitor tokens
   - Compare experience

3. **Document:**
   - When did quality drop?
   - What token count causes issues?
   - How does restart help?
   - What's your optimal session length?

**You'll discover your personal thresholds and develop intuition for session management!**

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
