# Context Exhaustion Challenge 🔥

**Goal:** Deliberately hit the context limit so you understand what it feels like and when to restart.

---

## Why Do This?

You need to **experience** context exhaustion to:
- Recognize warning signs in real work
- Know when to use `/compact` vs restart
- Develop intuition for token management
- Understand why session boundaries matter

**This is a safe learning environment. Break things. Hit limits. Learn!**

---

## Challenge 1: The File Reader 📁

**Objective:** Exhaust context by reading many large files

### Instructions:

```bash
1. Start new Claude session
   Token: 0 / 200,000 ✅

2. Find 10-15 large files in your codebase (500+ lines each)

3. Ask Claude to read them one by one:
   "Read src/components/Dashboard.tsx"
   "Read src/services/api.service.ts"
   "Read src/utils/helpers.ts"
   ... continue ...

4. After each file, ask Claude to explain it:
   "What does this file do?"
   "What are the main functions?"

5. Keep going until you reach 150k+ tokens

6. Try to ask one more complex question:
   "Compare all these files and identify code duplication"

7. Keep pushing until Claude can't respond
```

### What to Watch For:

- **50k tokens**: Everything works perfectly
- **100k tokens**: Still good, responses detailed
- **150k tokens**: Responses get shorter
- **170k tokens**: Claude starts asking "What was X?"
- **190k tokens**: Clear quality degradation
- **200k tokens**: ❌ Can't send messages

### Success Criteria:

- [ ] Hit 150k tokens
- [ ] Notice quality drop
- [ ] Experience "context full" message
- [ ] Understand why restart is needed

---

## Challenge 2: The Code Generator 💻

**Objective:** Fill context with generated code

### Instructions:

```bash
1. Start new Claude session

2. Ask Claude to generate a complete application:
   "Build a task management REST API with:
   - User authentication
   - Task CRUD operations
   - Task assignment
   - Comments on tasks
   - File attachments
   - Email notifications
   - Search functionality
   - Pagination
   - Rate limiting
   - Error handling"

3. Claude generates code (~20k tokens)

4. Ask for additions:
   "Add comprehensive tests for all endpoints"
   (+15k tokens)

5. Ask for more:
   "Add API documentation with examples"
   (+10k tokens)

6. Keep adding features:
   "Add WebSocket support for real-time updates"
   "Add caching layer"
   "Add logging and monitoring"
   "Add deployment configurations"
   "Add database migrations"

7. Continue until context is exhausted
```

### What You'll Experience:

- **Early responses**: Detailed, comprehensive code
- **Middle responses**: Still good but less explanation
- **Late responses**: Code only, minimal comments
- **Final responses**: Incomplete or errors
- **Can't continue**: Context full

### Success Criteria:

- [ ] Generated 5+ major features
- [ ] Accumulated 150k+ tokens
- [ ] Noticed decreasing response quality
- [ ] Hit the context limit

---

## Challenge 3: The Debugger 🐛

**Objective:** Exhaust context through debugging session

### Instructions:

```bash
1. Start new session

2. Share a complex error:
   "I'm getting this error: [paste 100 line stack trace]"

3. Claude suggests solutions

4. Try them, share results:
   "That didn't work, here's the new error: [paste logs]"

5. Ask follow-up questions:
   "Why would that happen?"
   "What about this approach?"
   "Can you explain X?"

6. Read multiple files:
   "Let me show you the code: [read 5 files]"

7. Keep the debugging session going for 2+ hours

8. Never use /compact, never restart

9. Continue until context is full
```

### What Happens:

- **Hour 1**: Excellent debugging help
- **Hour 1.5**: Still good but asking clarifying questions
- **Hour 2**: "Can you remind me what error you got?"
- **Hour 2.5**: Suggestions become repetitive
- **Hour 3**: Quality severely degraded
- **Can't continue**: Exhausted

### Success Criteria:

- [ ] Debug session lasted 2+ hours
- [ ] Shared 50+ messages
- [ ] Claude started forgetting context
- [ ] Hit token limit

---

## Challenge 4: The Marathon Session 🏃

**Objective:** Work all day in one session (DON'T DO THIS IN REAL WORK!)

### Instructions:

```bash
1. Start session at 9 AM

2. Work through multiple unrelated tasks:
   - 9 AM: Build login feature
   - 10 AM: Create dashboard
   - 11 AM: Add data visualization
   - 12 PM: Build admin panel
   - 1 PM: Add email system
   - 2 PM: Create reports
   - 3 PM: Add analytics
   - 4 PM: Build settings page

3. NEVER close Claude
4. NEVER use /compact
5. Read files, generate code, debug issues
6. Track token count every hour
7. Note when quality drops
8. Continue until you can't
```

### Token Progression (Typical):

```
 9 AM: 15,000 tokens   ✅ Perfect
10 AM: 35,000 tokens   ✅ Excellent
11 AM: 60,000 tokens   ✅ Very good
12 PM: 90,000 tokens   ⚠️  Good, but watch it
 1 PM: 125,000 tokens  ⚠️  Declining quality
 2 PM: 155,000 tokens  🚨 Noticeable issues
 3 PM: 180,000 tokens  🔥 Poor quality
 4 PM: 198,000 tokens  💀 Can't continue
```

### Success Criteria:

- [ ] Worked 4+ hours in one session
- [ ] Built multiple unrelated features
- [ ] Documented token growth
- [ ] Experienced severe degradation
- [ ] Understood why this is bad

---

## Challenge 5: The Recovery Test 🔄

**Objective:** Learn to recover from exhaustion

### Part A: Exhaust It

```bash
1. Deliberately exhaust context using any method above
2. Get to 190k+ tokens
3. Try to continue working
4. Experience the pain
```

### Part B: Try /compact

```bash
1. When you hit 120k tokens, type: /compact
2. Check new token count
3. Continue working
4. See how much longer you can go
5. Hit limit again
```

### Part C: Restart Strategy

```bash
1. Hit the limit completely
2. Close Claude
3. Open new session
4. Use /remember for key facts:
   /remember Project: [your project]
   /remember Tech: [your stack]
   /remember Current: Working on [feature]
5. Continue work in fresh session
6. Notice the difference
```

### Success Criteria:

- [ ] Exhausted context completely
- [ ] Tried `/compact` mid-session
- [ ] Restarted with clean session
- [ ] Compared experiences
- [ ] Understood best practices

---

## Challenge 6: The Comparison Lab 🔬

**Objective:** Compare bad vs good session management

### Week 1: Bad Habits (Intentional)

```bash
Rules:
- Single session per day (no matter what)
- Never use /compact
- Never restart
- Read as many files as needed
- Track when problems start

Document:
- Token count when quality drops
- Types of issues encountered
- Frustration level
- Time wasted on repeated explanations
```

### Week 2: Good Habits

```bash
Rules:
- New session for each major task
- Use /compact at 100k tokens
- Monitor tokens constantly
- Use memory for persistent facts
- Close between features

Document:
- Token count per session
- Quality consistency
- Frustration level
- Time saved
```

### Compare Results:

| Metric | Bad Habits | Good Habits |
|--------|-----------|-------------|
| Avg token per session | 180k+ | 30-60k |
| Sessions per day | 1 | 5-8 |
| Quality drop incidents | Many | Zero |
| Time wasted | High | Low |
| Frustration | High | Low |

### Success Criteria:

- [ ] Completed both weeks
- [ ] Documented differences
- [ ] Measured quality impact
- [ ] Developed personal strategy

---

## Warning Signs Checklist ⚠️

**When you see these, you're approaching the limit:**

### Claude's Behavior:
- [ ] Responses getting shorter
- [ ] Asking about things already discussed
- [ ] Less detailed explanations
- [ ] Forgetting earlier context
- [ ] More generic suggestions
- [ ] Repetitive answers

### Token Count:
- [ ] 100k tokens → Plan ahead
- [ ] 130k tokens → Use `/compact` or prepare to restart
- [ ] 150k tokens → Finish current subtask
- [ ] 170k tokens → Stop and restart NOW
- [ ] 190k tokens → Too late, quality terrible

### Your Experience:
- [ ] Re-explaining things
- [ ] Copy-pasting context repeatedly
- [ ] Getting frustrated
- [ ] Claude seems "confused"
- [ ] Answers don't match earlier work

---

## Post-Challenge Reflection 🤔

After completing challenges, answer:

1. **At what token count did you notice quality drop?**
   - Your threshold: _______k tokens

2. **What were the first warning signs?**
   - Specific behaviors: _______________

3. **When should YOU personally restart?**
   - Your rule: At _______k tokens or when ___________

4. **When is `/compact` useful vs restart?**
   - Use /compact when: _______________
   - Restart when: _______________

5. **How will you change your workflow?**
   - New habit 1: _______________
   - New habit 2: _______________
   - New habit 3: _______________

---

## Real-World Application 🎯

**Now that you've experienced exhaustion, apply these lessons:**

### Daily Workflow:

```bash
Morning:
- Start fresh session for each feature
- Use memory for project facts
- Monitor tokens

Midday:
- Check token count before lunch
- Restart if > 100k tokens
- Fresh afternoon session

Afternoon:
- Close between major tasks
- Don't carry morning context
- End day with clean slate

Never:
- Work all day in one session
- Ignore token warnings
- Push past 150k tokens
```

### Team Guidelines:

```markdown
## Session Management Standards

1. **Restart between features**
   - One feature = One session
   - Maximum: 100k tokens per session

2. **Use memory for facts**
   - Tech stack
   - Architecture decisions
   - Team conventions

3. **Monitor constantly**
   - Check tokens after major operations
   - Plan restarts proactively

4. **Use /compact wisely**
   - When continuing same feature
   - Not as primary strategy
   - Restart is usually better
```

---

## Challenge Completed? 🏆

You've successfully learned context management if you can:

- [x] Deliberately exhaust context
- [x] Recognize warning signs
- [x] Use `/compact` effectively
- [x] Restart strategically
- [x] Develop personal thresholds
- [x] Explain to teammates why session management matters

**Congratulations! You now understand session context at a deep level.**

**Next:** Apply these lessons to real work and never hit unexpected context limits again! 🚀

---

## Quick Reference Card

```
PERSONAL SESSION STRATEGY
(Fill this out after challenges)

My token warning threshold: _______ k

I restart when:
1. _________________________
2. _________________________
3. _________________________

I use /compact when:
1. _________________________
2. _________________________

I avoid exhaustion by:
1. _________________________
2. _________________________
3. _________________________

Red flags I watch for:
1. _________________________
2. _________________________
3. _________________________
```

**Print this, fill it out, keep it visible while working with Claude!**
