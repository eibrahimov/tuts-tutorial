# 🚀 Claude-Flow Ultimate Cheat Sheet

## 📌 ONE-PAGE EVERYTHING GUIDE

### 🎯 BASIC COMMANDS

```bash
# What You Say → What Happens
"Fix the bug" → Searches, fixes, tests
"Build feature X" → Creates complete implementation
"Review my code" → Analyzes and suggests improvements
"Create tests" → Generates comprehensive test suite
"Optimize performance" → Profiles and improves speed
```

---

## 🔥 GITHUB OPERATIONS

### Issues
```bash
"Create issue for bug X" → gh issue create
"Triage all open issues" → Analyze and label
"Start work on issue #45" → Create branch, link issue
```

### Pull Requests
```bash
"Create PR for current branch" → gh pr create with rich description
"Review PR #123" → Security, performance, quality check
"Merge approved PRs" → Auto-merge after checks
```

### Releases
```bash
"Prepare v2.0 release" → Changelog, version bump, tag
"Deploy to production" → Run CI/CD pipeline
"Rollback last release" → Revert and redeploy
```

---

## 💾 MEMORY OPERATIONS

### Store
```javascript
"Remember: We use PostgreSQL for database"
"Store pattern: Always validate input"
"Save decision: JWT for authentication"
```

### Retrieve
```javascript
"What did we decide about authentication?"
"Show all patterns for forms"
"Apply our API pattern"
```

---

## 🤖 AGENT SPAWNING

### Single Agent
```javascript
"Use backend-dev agent to build REST API"
"Deploy tester agent for comprehensive tests"
"Spawn security reviewer for audit"
```

### Multi-Agent (Parallel)
```javascript
"Build complete feature with:
- Backend API (backend-dev)
- Frontend UI (coder)
- Tests (tester)
- Docs (api-docs)"
```

---

## 📝 PROMPT TEMPLATES

### Feature Development
```
"Build [feature]:
- Requirements: [list]
- Tech stack: [current stack]
- Include tests
- Follow our patterns"
```

### Bug Fix
```
"Fix bug: [description]
- Symptoms: [what happens]
- Expected: [correct behavior]
- Add regression tests"
```

### Optimization
```
"Optimize [component]:
- Current: [metric]
- Target: [goal]
- Maintain: [constraints]"
```

---

## 🎨 SPARC MODES

```bash
# Quick Usage
"Use SPARC TDD for login feature"       → Full TDD cycle
"Use SPARC architect for database"      → Design only
"Use SPARC debug for memory leak"       → Debug mode
"Use SPARC security for audit"          → Security review
```

---

## ⚡ PERFORMANCE TIPS

### Fast Operations
```javascript
// Use patterns
"Apply crud pattern to User model"      // 30 seconds

// Batch operations
"Fix all ESLint errors"                 // Parallel fixes

// Reuse memory
"Use our authentication pattern"        // Instant recall
```

---

## 🔐 SECURITY ALWAYS

### Never Share
```
❌ Passwords: "password123"
❌ API Keys: "sk_live_abc123"
❌ Secrets: Any production credentials
```

### Always Use
```
✅ Environment vars: process.env.API_KEY
✅ Placeholders: "YOUR_KEY_HERE"
✅ Test data: "test@example.com"
```

---

## 📊 PROJECT PATTERNS

### Your Patterns (MigrationPro)
```javascript
// API Pattern
"All endpoints under /api/v1/"

// Component Pattern
"Compound components for complex UI"

// Test Pattern
"Page object model for E2E"

// Error Pattern
"User-friendly messages with recovery"
```

---

## 🚦 DECISION TREE

```
Simple edit? → Just ask
Need planning? → Use SPARC spec
Multiple parts? → Spawn agents
GitHub work? → Use GitHub agents
Team feature? → Coordinate with memory
```

---

## 📈 DAILY WORKFLOW

### Morning (5 min)
```
"What patterns do we have?"
"Show yesterday's work"
"What's in progress?"
```

### During Work
```
"Fix issue #45"
"Apply our patterns"
"Store successful approach"
```

### End of Day (2 min)
```
"Create PR for today's work"
"Update project board"
"Document new patterns"
```

---

## 🎯 QUICK WINS

### 1-Minute Tasks
```bash
"Format this file"
"Add missing types"
"Update imports"
"Fix this typo"
```

### 5-Minute Tasks
```bash
"Add loading state"
"Create error boundary"
"Add input validation"
"Write unit test"
```

### 30-Minute Tasks
```bash
"Add authentication"
"Create CRUD API"
"Build dashboard page"
"Set up CI/CD"
```

---

## 🔧 TROUBLESHOOTING

### Common Fixes
```bash
"Claude-Flow not responding" → Restart: claude mcp restart claude-flow
"Memory not persisting" → Check namespace
"Agents not coordinating" → Initialize swarm first
"Tests failing" → Check environment setup
```

---

## 📱 TEAM COLLABORATION

### Share Patterns
```
"Store team pattern: [pattern name]"
"Document our approach to [feature]"
"Create playbook for [task]"
```

### Code Review
```
"Review PR using team standards"
"Check pattern compliance"
"Suggest improvements"
```

---

## 🏆 PRODUCTIVITY HACKS

### Batch Everything
```javascript
// SLOW: Multiple messages
Message 1: "Create component"
Message 2: "Add tests"
Message 3: "Update docs"

// FAST: Single message
"Create component with tests and docs"
```

### Use Patterns
```javascript
// SLOW: Describe everything
"Create API with validation, error handling..."

// FAST: Use pattern
"Apply standard-api pattern"
```

### Parallel Agents
```javascript
// SLOW: Sequential
"First do X, then Y, then Z"

// FAST: Parallel
"Do X, Y, and Z simultaneously with agents"
```

---

## 📚 ADVANCED TECHNIQUES

### Meta-Prompting
```
"Generate the best prompt for building an auth system, then execute it"
```

### Self-Correction
```
"Build feature, then find and fix any issues"
```

### Progressive Enhancement
```
"Start with basic version, then add features incrementally"
```

---

## 🎮 KEYBOARD SHORTCUTS (Mental)

```
Ctrl+F = "Find pattern for X"
Ctrl+S = "Store this pattern"
Ctrl+R = "Apply stored pattern"
Ctrl+T = "Create tests"
Ctrl+P = "Create PR"
Ctrl+D = "Deploy"
```

---

## 📋 ESSENTIAL COMMANDS

### Must Know
```bash
# GitHub
gh issue create
gh pr create
gh pr review
gh pr merge

# Claude-Flow
npx claude-flow sparc tdd "feature"
npx claude-flow sparc run debug "issue"
npx claude-flow validate-patterns

# Memory
"Store in memory: X"
"Retrieve from memory: X"
"List all patterns"
```

---

## ⚠️ ANTI-PATTERNS (AVOID!)

```
❌ "Do everything"              → Too vague
❌ "Make it perfect"            → No clear criteria
❌ Skipping tests               → Always include tests
❌ Ignoring patterns            → Always check first
❌ Working alone                → Share with team
❌ No documentation             → Always document
```

---

## 🎯 SUCCESS METRICS

### You're Succeeding When:
- ✅ 50% less time on tasks
- ✅ 90%+ test coverage
- ✅ Zero critical bugs
- ✅ Reusing patterns daily
- ✅ Team adopting your patterns

---

## 💎 GOLDEN RULES

1. **Start small** - Don't try to do everything at once
2. **Use patterns** - Don't reinvent the wheel
3. **Test everything** - No code without tests
4. **Share knowledge** - Document and share patterns
5. **Stay secure** - Never expose secrets
6. **Be specific** - Clear requirements = better results
7. **Iterate quickly** - Small improvements > perfection
8. **Collaborate** - Use team patterns and memory
9. **Measure progress** - Track your improvements
10. **Keep learning** - Try new approaches

---

## 🚨 EMERGENCY CONTACTS

```
Problem: Claude-Flow issue
Solution: Check troubleshooting guide

Problem: Security concern
Solution: Contact security team immediately

Problem: Production issue
Solution: Follow incident response plan

Problem: Need help
Solution: Ask in #claude-flow-help
```

---

## 📞 ONE-LINE HELPERS

```bash
"Help"                          # Get assistance
"Status"                        # Check current state
"What can you do?"             # See capabilities
"Show examples"                # Get examples
"Explain this"                 # Understand code
"Fix this"                     # Solve problems
"Improve this"                 # Optimize code
"Test this"                    # Create tests
"Document this"                # Add documentation
"Deploy this"                  # Ship to production
```

---

**Remember: You talk, Claude-Flow works! 🚀**

*Keep this handy - it's all you need!*