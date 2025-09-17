# Troubleshooting Guide: Common Issues & Solutions

## 🚨 CRITICAL ISSUES

### Issue 1: Claude-Flow Not Responding

**Symptoms:**
- Commands timeout
- No response to prompts
- "Command timed out after 2m" error

**Solutions:**
```bash
# Solution 1: Check if MCP is running
claude mcp list

# Solution 2: Restart Claude-Flow
claude mcp restart claude-flow

# Solution 3: Clear cache and restart
rm -rf ~/.claude/cache
claude mcp add claude-flow npx claude-flow@alpha mcp start
```

**Prevention:**
- Keep Claude-Flow updated: `npm update claude-flow@alpha`
- Monitor memory usage
- Clear cache weekly

---

### Issue 2: Memory Not Persisting

**Symptoms:**
- Patterns not remembered between sessions
- "Memory not found" errors
- Lost context after restart

**Diagnosis:**
```
You: "Check memory status and list all stored patterns"
```

**Solutions:**
```javascript
// Force memory persistence
You: "Store this in memory with namespace 'critical' and ttl 999999:
[your important data]"

// Verify storage
You: "Retrieve all entries from namespace 'critical'"
```

**Prevention:**
- Always use namespaces
- Set appropriate TTL values
- Backup critical patterns regularly

---

### Issue 3: Agents Not Coordinating

**Symptoms:**
- Agents working in isolation
- Duplicate work being done
- Conflicting implementations

**Solutions:**
```
You: "Initialize swarm with hierarchical topology for better coordination.
Ensure all agents use shared memory namespace 'project-coordination'"
```

**Prevention:**
- Always initialize swarm before multi-agent tasks
- Use consistent memory namespaces
- Define clear agent responsibilities

---

## 🐛 COMMON PROBLEMS

### Problem 1: Generated Code Doesn't Follow Project Style

**Issue:** Claude generates code that doesn't match your style guide

**Solution:**
```
You: "Learn our code style:
- Indentation: 2 spaces
- Quotes: single
- Semicolons: always
- Component files: PascalCase
- Utilities: camelCase
Store as 'code-style' pattern and apply to all future code"
```

---

### Problem 2: Tests Failing After Generation

**Issue:** Generated tests fail immediately

**Solution:**
```
You: "Debug the failing tests:
1. Run tests and show exact errors
2. Check test environment setup
3. Verify mock data matches schema
4. Fix import paths
5. Ensure test database is configured"
```

**Prevention Template:**
```
You: "Generate tests that:
- Use our existing test utilities
- Match our database schema exactly
- Include proper setup and teardown
- Run successfully before completion"
```

---

### Problem 3: Performance Degradation

**Issue:** Claude-Flow becoming slower over time

**Solutions:**
```bash
# Clear memory bloat
You: "List memory usage by namespace and clean unused entries"

# Optimize swarm topology
You: "Switch to mesh topology for current task"

# Reset neural patterns
You: "Clear learned patterns older than 30 days"
```

---

### Problem 4: Conflicting Dependencies

**Issue:** Generated code adds incompatible packages

**Solution:**
```
You: "Before adding any dependency:
1. Check current package.json
2. Verify version compatibility
3. Check for existing alternatives
4. Only add if absolutely necessary"
```

---

## 📝 ERROR MESSAGES DECODED

### "Tool claude-flow executed successfully" but nothing happens

**Meaning:** Command executed but produced no output
**Fix:** Add `--verbose` flag or check logs:
```bash
tail -f ~/.claude/logs/claude-flow.log
```

---

### "Context window full"

**Meaning:** Too much information in current session
**Fix:**
```
You: "Compact our conversation focusing on:
- Current task only
- Keep recent patterns
- Remove completed work
- Preserve critical decisions"
```

---

### "Pattern not found in memory"

**Meaning:** Requested pattern wasn't stored or expired
**Fix:**
```
You: "List all patterns in memory and recreate missing ones"
```

---

### "Agent spawn failed"

**Meaning:** Can't create new agent due to limits
**Fix:**
```
You: "Show current agent count and terminate idle agents"
```

---

## 🔧 DEBUGGING TECHNIQUES

### Technique 1: Verbose Mode

```
You: "Enable verbose mode and trace the execution of [task]"
```

### Technique 2: Step-by-Step Execution

```
You: "Break this task into atomic steps and execute one at a time:
1. [First step]
Let me verify before continuing..."
```

### Technique 3: Memory Inspection

```
You: "Debug memory issues:
1. List all namespaces
2. Show entries in each namespace
3. Check TTL values
4. Identify conflicts"
```

### Technique 4: Pattern Analysis

```
You: "Analyze why this pattern isn't working:
1. Show the stored pattern
2. Show how it's being applied
3. Identify mismatches
4. Correct and re-store"
```

---

## 🚑 EMERGENCY PROCEDURES

### Complete Reset
```bash
# WARNING: This removes all data
rm -rf ~/.claude
rm -rf .claude-flow
claude mcp remove claude-flow
claude mcp add claude-flow npx claude-flow@alpha mcp start
```

### Restore from Backup
```
You: "Restore memory from backup:
1. List available backups
2. Load backup from [date]
3. Verify critical patterns restored"
```

### Safe Mode Operation
```
You: "Enter safe mode:
- Disable auto-execution
- Manual review required
- No file system writes
- Log all operations"
```

---

## 💊 QUICK FIXES

### Quick Fix 1: Unresponsive Claude
```bash
# Restart Claude Code
pkill -f claude
claude
```

### Quick Fix 2: Clear Bad Patterns
```
You: "Remove corrupted pattern [name] and recreate from scratch"
```

### Quick Fix 3: Fix Import Errors
```
You: "Scan all imports and fix:
- Relative vs absolute paths
- Missing file extensions
- Circular dependencies
- Case sensitivity issues"
```

### Quick Fix 4: Database Connection Issues
```
You: "Debug database connection:
1. Check connection string
2. Verify credentials
3. Test connection
4. Check firewall rules
5. Verify database is running"
```

---

## 🎯 PREVENTION STRATEGIES

### Daily Health Check
```
You: "Perform daily health check:
- Memory usage status
- Active agent count
- Pattern integrity
- Performance metrics
- Error rate analysis"
```

### Weekly Maintenance
```
You: "Weekly maintenance tasks:
- Clear old cache
- Optimize memory storage
- Update patterns library
- Review error logs
- Backup critical data"
```

### Pattern Validation
```
You: "Validate all stored patterns:
- Check syntax
- Test applicability
- Remove outdated ones
- Update documentation"
```

---

## 📊 DIAGNOSTIC COMMANDS

### System Status
```
You: "Show complete system status including:
- Claude-Flow version
- Memory usage
- Active agents
- Recent errors
- Performance metrics"
```

### Performance Analysis
```
You: "Analyze performance bottlenecks:
- Token usage by operation
- Slowest operations
- Memory hot spots
- Agent efficiency"
```

### Error Analysis
```
You: "Analyze recent errors:
- Group by type
- Identify patterns
- Suggest fixes
- Prevention strategies"
```

---

## 🤝 GETTING HELP

### Self-Diagnosis
```
You: "Diagnose current issues and suggest solutions"
```

### Documentation Check
```
You: "Search documentation for [error message or issue]"
```

### Pattern Reset
```
You: "Reset to default patterns for [feature/component]"
```

### Community Resources
- GitHub Issues: https://github.com/ruvnet/claude-flow/issues
- Documentation: https://github.com/ruvnet/claude-flow
- Discord: [Community Discord Link]

---

## ⚡ OPTIMIZATION TIPS

### Tip 1: Batch Operations
```
You: "Batch these 10 similar operations for efficiency"
```

### Tip 2: Selective Memory
```
You: "Only store patterns that will be reused, with appropriate TTL"
```

### Tip 3: Agent Specialization
```
You: "Use specialized agents rather than general ones for better performance"
```

### Tip 4: Progressive Enhancement
```
You: "Start with basic implementation, then enhance incrementally"
```

---

## 🎨 TROUBLESHOOTING FLOWCHART

```
Problem Occurs
    ↓
Is it responding? → No → Restart Claude-Flow
    ↓ Yes
Is memory working? → No → Check memory namespace
    ↓ Yes
Are agents coordinating? → No → Reinitialize swarm
    ↓ Yes
Is output correct? → No → Review and correct patterns
    ↓ Yes
Problem Solved ✓
```

---

## 🔴 WHEN TO ESCALATE

Escalate to senior developer or CTO when:
- Data loss occurs
- Security breach suspected
- Production system affected
- Multiple team members blocked
- Systematic failures observed

**Escalation Template:**
```
Issue: [Brief description]
Impact: [Who/what is affected]
Tried: [Solutions attempted]
Need: [What help is needed]
Priority: [Critical/High/Medium/Low]
```

Remember: Most issues have simple solutions. Stay calm, follow the debugging steps, and remember that Claude-Flow is just a tool - you're in control!