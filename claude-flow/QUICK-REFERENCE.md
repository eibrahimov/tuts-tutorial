# Claude-Flow Quick Reference Guide

## 🚀 ONE-MINUTE UNDERSTANDING

**Claude-Flow = Smart helper system inside Claude chat**
- ✅ Works HERE in chat (no separate terminal)
- ✅ Already installed and configured
- ✅ I (Claude) use it automatically when needed
- ✅ You just ask, I handle the orchestration

## 🎯 HOW TO ASK FOR THINGS

### Simple Tasks (Direct execution)
```
"Add validation to my form"
"Fix the login bug"
"Update the database schema"
```

### Medium Tasks (SPARC mode auto-triggered)
```
"Build user authentication with tests"
"Create a REST API for products"
"Implement data migration feature"
```

### Complex Tasks (Hive-mind multi-agent)
```
"Build complete e-commerce system"
"Create full-stack application with auth, payments, and admin"
"Migrate entire codebase to TypeScript with tests"
```

## 📋 AVAILABLE MODES (I choose automatically)

| Mode | When Used | Example Task |
|------|-----------|--------------|
| **Direct** | Simple edits | "Fix typo" |
| **SPARC Spec** | Planning | "Design system architecture" |
| **SPARC TDD** | Feature building | "Build login with tests" |
| **Debug** | Bug fixing | "Find memory leak" |
| **Hive-Mind** | Complex multi-part | "Build full app" |
| **Security** | Security review | "Audit authentication" |

## 🧠 ADVANCED FEATURES

### Memory (Persistent Knowledge)
```
"Remember this API pattern for future use"
"What did we decide about authentication?"
"Apply the patterns we learned yesterday"
```

### Learning (Pattern Recognition)
```
"Learn this testing framework: [docs]"
"Train on these code examples"
"Remember this pattern worked well"
```

### DAA (Smart Agent Assignment)
```
Automatic - happens when you say:
"Build feature X" → DAA picks right agents
```

## 💡 POWER USER TIPS

### Request Specific Mode
```
"Use TDD to build calculator"
"Use SPARC architect mode to design database"
"Spawn multiple agents for this complex task"
```

### Teach New Skills
```
"Learn [framework]: [documentation]
Store patterns in memory namespace '[name]'
Train neural patterns on examples"
```

### Use Memory
```
"Store this decision: [detail]"
"Recall what we decided about [topic]"
"Apply learned [framework] patterns"
```

## 🚦 DECISION FLOWCHART

```
Your Request
    ↓
Simple? → I do it directly
    ↓
Medium? → I use SPARC mode
    ↓
Complex? → I spawn multiple agents
    ↓
Learning? → I store in memory + train patterns
```

## ⚡ MOST COMMON COMMANDS (I run these)

```bash
# Planning & Design
npx claude-flow sparc run spec-pseudocode "task"

# Build with Tests
npx claude-flow sparc tdd "feature"

# Quick Code
npx claude-flow sparc run code "implementation"

# Debug
npx claude-flow sparc run debug "issue"

# Full Pipeline
npx claude-flow sparc pipeline "complete task"
```

## 🎯 JUST REMEMBER

1. **You DON'T run commands** - I do
2. **You DON'T manage agents** - I do
3. **You DON'T configure memory** - I do
4. **You JUST ask** - I handle everything

## 📝 EXAMPLE CONVERSATIONS

### Basic
```
You: "Fix the login error"
Me: [Analyzes, fixes bug, tests]
```

### Advanced
```
You: "Build user dashboard with real-time updates"
Me: [Spawns frontend, backend, websocket agents]
```

### Teaching
```
You: "Learn Cypress E2E framework and apply to my app"
Me: [Studies docs, stores patterns, creates tests]
```

## 🔥 THE GOLDEN RULE

**Just tell me what you want to achieve.**
**I'll figure out how to use Claude-Flow to make it happen.**

---

*Remember: Claude-Flow is a tool I use, not something you need to operate!*