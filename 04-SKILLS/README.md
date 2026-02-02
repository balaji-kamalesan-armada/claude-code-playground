# Skills: Custom Workflows

## What Are Skills?

Skills are **custom slash commands** that automate repetitive workflows.

```
Skill = /command that runs a predefined workflow
```

## How It Works

```
1. Create skill file: .claude/skills/my-skill/skill.md
2. Use it: Type /my-skill in Claude
3. Claude executes the workflow automatically
```

## Why Use Skills?

**Without Skills:**
```
You: "Create a git commit with my changes"
Claude: [Asks questions, runs git status, git diff, git log,
         analyzes changes, writes message, runs git add, git commit]
Time: 5-10 minutes, 10+ steps
```

**With Skills:**
```
You: /commit
Claude: [Executes entire workflow automatically]
Time: 30 seconds, 1 command
```

## Built-in Skills

Claude Code includes:

### `/commit`
```bash
# Create intelligent git commit
/commit

# With custom message
/commit -m "Fix login bug"
```

### `/review-pr`
```bash
# Review pull request
/review-pr 123
/review-pr https://github.com/user/repo/pull/123
```

Check all skills: `/help`

## Creating Custom Skills

### Step 1: Create Skill File

```
.claude/skills/my-skill/skill.md
```

### Step 2: Define Workflow

```markdown
---
name: my-skill
description: What this skill does
---

# Instructions for Claude

When user types `/my-skill`:

1. First step of workflow
2. Second step
3. Third step

## Parameters
- `arg1`: Description

## Example
/my-skill arg1
```

### Step 3: Use It

```bash
/my-skill argument
```

## Skill Examples

### Example 1: API Endpoint Skill

```markdown
---
name: endpoint
description: Create new API endpoint with tests
---

When user types `/endpoint <name> <method>`:

1. Create endpoint file in src/api/endpoints/
2. Create service file in src/services/
3. Add Joi validation schema
4. Create test file with basic tests
5. Update API documentation
6. Run tests to verify

Parameters:
- name: Endpoint name (e.g., "users")
- method: HTTP method (GET, POST, PUT, DELETE)

Example: /endpoint users POST
```

### Example 2: Code Review Skill

```markdown
---
name: review
description: Comprehensive code review checklist
---

When user types `/review <file>`:

1. Read the specified file
2. Check for:
   - Code style issues
   - Security vulnerabilities
   - Performance problems
   - Missing tests
   - Documentation gaps
3. Provide feedback:
   - Issues (high/medium/low priority)
   - Suggestions
   - Praise for good practices

Parameters:
- file: Path to file to review

Example: /review src/services/user.ts
```

### Example 3: Deploy Skill

```markdown
---
name: deploy
description: Deploy to environment with safety checks
---

When user types `/deploy <env>`:

1. Verify environment (dev/staging/prod)
2. Run all tests
3. Build production bundle
4. If production: Ask for confirmation
5. Run deployment command
6. Verify deployment succeeded
7. Report status

Parameters:
- env: Target environment

Example: /deploy staging
```

## When to Create Skills

### ✅ Create Skills For:
- Repetitive multi-step workflows
- Team standard processes
- Complex operations you do often
- Ensuring consistency

### ❌ Don't Create Skills For:
- One-time tasks
- Simple single commands
- Processes that change frequently
- Things already in built-in skills

## Skill Best Practices

### DO:
- ✅ One skill, one purpose
- ✅ Clear step-by-step instructions
- ✅ Document all parameters
- ✅ Include examples
- ✅ Make team-friendly

### DON'T:
- ❌ Make overly complex skills
- ❌ Duplicate built-in functionality
- ❌ Leave parameters undocumented
- ❌ Make vague instructions

## Skill vs Memory vs Rules

```
SKILLS              MEMORY              RULES
(Workflows)         (Facts)             (Standards)
─────────────────   ─────────────────   ────────────────
/commit workflow    Tech stack          Code style guide
/review checklist   Architecture        Naming rules
/endpoint builder   Business rules      Documentation req
/deploy process     Preferences         File structure

Automate tasks      Remember facts      Define standards
```

## Key Takeaways

1. **Skills = Automation**
   - Turn workflows into commands
   - Save time on repetitive tasks

2. **Skills are reusable**
   - Write once, use everywhere
   - Share with team

3. **Skills ensure consistency**
   - Same process every time
   - No steps forgotten

4. **Skills are simple**
   - Create markdown file
   - Define workflow
   - Use with `/command`

## Examples & Practice

**See it in action:**
→ [EXAMPLES.md](EXAMPLES.md) - Skill templates, real examples, exercises

## Next Steps

1. Read [EXAMPLES.md](EXAMPLES.md) for hands-on practice
2. Then move to [Module 5: Rules](../05-RULES/README.md)

---

**Remember: Skills = Automate repetitive workflows!** ⚡
