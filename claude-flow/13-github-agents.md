# GitHub Agents & Modes in Claude-Flow

## 🤖 SPECIALIZED GITHUB AGENTS

Claude-Flow provides powerful GitHub-specific agents that automate complex repository operations. Here's how to use each one effectively.

---

## 📋 AVAILABLE GITHUB AGENTS

### Core GitHub Agents
- `github-modes` - Comprehensive GitHub integration
- `pr-manager` - Pull request management
- `code-review-swarm` - Multi-agent code review
- `issue-tracker` - Issue management & tracking
- `release-manager` - Release coordination
- `workflow-automation` - GitHub Actions automation
- `project-board-sync` - Project board synchronization
- `repo-architect` - Repository structure optimization
- `multi-repo-swarm` - Cross-repository coordination
- `sync-coordinator` - Multi-repo synchronization
- `release-swarm` - Complex release orchestration
- `swarm-pr` - PR swarm management
- `swarm-issue` - Issue-based swarm coordination

---

## 🎯 AGENT USAGE EXAMPLES

### 1. PR-MANAGER AGENT

**Purpose**: Comprehensive pull request management with automated reviews and merge workflows

```
You: "Use pr-manager agent to handle PR #123:
- Perform security review
- Check test coverage
- Validate against team patterns
- Suggest improvements
- Auto-merge if all checks pass"
```

What happens:
```javascript
Task("PR Manager", `
  Review PR #123:
  1. Clone and checkout PR branch
  2. Run security scanners
  3. Calculate test coverage delta
  4. Check pattern compliance
  5. Generate improvement suggestions
  6. Create detailed review comment
  7. Approve or request changes
  8. Merge if approved and CI passes
`, "pr-manager")
```

Real execution:
```bash
# Agent performs:
gh pr checkout 123
npm test -- --coverage
npx audit-ci --critical
npx claude-flow validate-patterns
gh pr review --approve --body "Auto-review complete"
gh pr merge --auto --squash
```

---

### 2. CODE-REVIEW-SWARM

**Purpose**: Deploy multiple specialized agents for comprehensive code review

```
You: "Deploy code-review-swarm for PR #456:
Spawn agents for:
- Security analysis
- Performance review
- Architecture compliance
- Test coverage
- Documentation check"
```

Swarm coordination:
```javascript
// Parallel agent deployment
Task("Security Reviewer", "Scan for OWASP Top 10 vulnerabilities", "reviewer")
Task("Performance Analyst", "Check for performance regressions", "perf-analyzer")
Task("Architecture Validator", "Verify design patterns compliance", "system-architect")
Task("Test Engineer", "Validate test coverage and quality", "tester")
Task("Docs Reviewer", "Check documentation completeness", "api-docs")

// Agents coordinate through shared memory
namespace: 'pr-456-review'
```

Consolidated report:
```markdown
## Code Review Summary for PR #456

### ✅ Security (Agent: security-reviewer)
- No vulnerabilities found
- All inputs validated
- Authentication properly implemented

### ⚠️ Performance (Agent: perf-analyzer)
- Minor regression: +50ms on dashboard load
- Suggestion: Add caching to user queries

### ✅ Architecture (Agent: architect)
- Follows established patterns
- Proper separation of concerns

### ✅ Tests (Agent: tester)
- Coverage: 89% (+2%)
- All scenarios covered

### ❌ Documentation (Agent: docs)
- Missing API documentation for 2 endpoints
- README needs updating
```

---

### 3. ISSUE-TRACKER AGENT

**Purpose**: Intelligent issue management with automated triage and assignment

```
You: "Use issue-tracker agent to:
- Triage all open issues
- Assign priority labels
- Suggest assignees based on expertise
- Create sprint milestone
- Generate sprint planning report"
```

Agent execution:
```javascript
Task("Issue Tracker", `
  Manage GitHub issues:
  1. Fetch all open issues
  2. Analyze issue content and classify
  3. Apply smart labels (bug/feature/enhancement)
  4. Calculate priority based on impact
  5. Match with developer expertise
  6. Create sprint-24 milestone
  7. Generate planning markdown
`, "issue-tracker")
```

Output:
```markdown
## Sprint 24 Planning

### High Priority (P0)
- #102: Production login failure [@senior-dev]
- #98: Payment processing timeout [@backend-lead]

### Medium Priority (P1)
- #95: Dashboard performance [@frontend-dev]
- #91: Add dark mode [@ui-designer]

### Low Priority (P2)
- #87: Update documentation [@junior-dev]
- #83: Refactor utils module [@any]

### Velocity Metrics
- Capacity: 45 points
- Committed: 42 points
- Stretch goals: 8 points
```

---

### 4. RELEASE-MANAGER AGENT

**Purpose**: Automated release coordination across packages with version management

```
You: "Use release-manager to prepare v2.0.0 release:
- Generate changelog from commits
- Update version numbers
- Create release branch
- Run final tests
- Tag release
- Deploy to staging
- Create GitHub release"
```

Agent workflow:
```javascript
Task("Release Manager", `
  Coordinate v2.0.0 release:
  1. Create release/v2.0.0 branch
  2. Generate CHANGELOG.md from commits
  3. Bump versions in all packages
  4. Update documentation
  5. Run complete test suite
  6. Create release PR
  7. After approval: tag and release
  8. Trigger deployment pipeline
`, "release-manager")
```

Generated files:
```markdown
# CHANGELOG.md

## [2.0.0] - 2024-01-15

### 🎉 Major Features
- OAuth2 authentication (#89)
- Real-time collaboration (#92)
- API v2 with GraphQL (#94)

### 🚀 Enhancements
- 50% performance improvement
- Enhanced security measures
- Improved error handling

### 💔 Breaking Changes
- API v1 deprecated
- Config format changed (see migration guide)

### 🐛 Bug Fixes
- Fixed memory leak in websocket handler
- Resolved race condition in auth flow
```

---

### 5. WORKFLOW-AUTOMATION AGENT

**Purpose**: Create intelligent, self-organizing CI/CD pipelines

```
You: "Use workflow-automation agent to:
- Analyze our codebase
- Design optimal CI/CD pipeline
- Create GitHub Actions workflows
- Set up deployment stages
- Implement rollback procedures"
```

Generated workflow:
```yaml
# .github/workflows/intelligent-pipeline.yml
name: AI-Optimized Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:

jobs:
  # Agent determines optimal job parallelization
  quick-checks:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        check: [lint, typecheck, security]
    steps:
      - uses: actions/checkout@v3
      - run: npm run ${{ matrix.check }}

  test-suite:
    needs: quick-checks
    strategy:
      matrix:
        suite: [unit, integration, e2e]
    steps:
      - run: npm run test:${{ matrix.suite }}

  smart-deploy:
    if: github.ref == 'refs/heads/main'
    needs: test-suite
    steps:
      - name: Claude-Flow Deployment Decision
        run: |
          npx claude-flow deploy-decision \
            --analyze-risk \
            --check-dependencies \
            --verify-migrations \
            --canary-deploy
```

---

### 6. MULTI-REPO-SWARM

**Purpose**: Coordinate changes across multiple repositories

```
You: "Use multi-repo-swarm to:
Update API across all microservices:
- api-gateway repo
- user-service repo
- payment-service repo
- notification-service repo"
```

Swarm coordination:
```javascript
Task("Multi-Repo Coordinator", `
  Orchestrate cross-repo API update:
  1. Clone all repositories
  2. Create feature branches
  3. Update API contracts
  4. Modify implementations
  5. Update tests
  6. Create synchronized PRs
  7. Coordinate reviews
  8. Orchestrate deployment
`, "multi-repo-swarm")
```

Execution across repos:
```bash
# Repo 1: api-gateway
git checkout -b feat/api-v2-update
# Update gateway routes
gh pr create --title "API v2 Gateway Updates"

# Repo 2: user-service
git checkout -b feat/api-v2-update
# Update user endpoints
gh pr create --title "API v2 User Service"

# Coordinated through shared memory namespace
namespace: "api-v2-migration"
```

---

## 🔧 GITHUB MODES IN SPARC

### Using GitHub-Specific SPARC Modes

```
You: "Use SPARC github-pr mode to create perfect PR"
```

```bash
npx claude-flow sparc run github-pr "Create PR for user dashboard feature"
```

This runs specialized workflow:
1. **Analyze changes** - Understand what changed
2. **Generate description** - Create comprehensive PR text
3. **Link issues** - Find and link related issues
4. **Add metadata** - Labels, reviewers, projects
5. **Create PR** - Submit to GitHub
6. **Monitor checks** - Watch CI/CD status

---

## 💡 COMBINING GITHUB AGENTS

### Complex Workflow Example

```
You: "Coordinate complete feature release:
1. Use issue-tracker to identify completed features
2. Deploy code-review-swarm for final review
3. Use release-manager to prepare release
4. Use workflow-automation for deployment
5. Use project-board-sync to update status"
```

Orchestrated execution:
```javascript
// Sequential coordination
await Task("Issue Tracker", "Identify completed features", "issue-tracker")
await Task("Review Swarm", "Final security review", "code-review-swarm")
await Task("Release Manager", "Prepare v2.0 release", "release-manager")
await Task("Workflow Automation", "Deploy to production", "workflow-automation")
await Task("Project Sync", "Update project board", "project-board-sync")
```

---

## 📊 GITHUB AGENT METRICS

### Measuring Agent Effectiveness

```
You: "Show metrics for GitHub agents performance this sprint"
```

```javascript
{
  "pr-manager": {
    "prs_processed": 42,
    "auto_merged": 38,
    "average_review_time": "5 min",
    "issues_caught": 12
  },
  "code-review-swarm": {
    "reviews_completed": 156,
    "vulnerabilities_found": 3,
    "patterns_enforced": 89,
    "coverage_improvement": "+8%"
  },
  "issue-tracker": {
    "issues_triaged": 234,
    "auto_assigned": 198,
    "priority_accuracy": "94%",
    "sprint_planning_time": "10 min vs 2 hours manual"
  },
  "release-manager": {
    "releases_coordinated": 8,
    "rollbacks_prevented": 2,
    "deployment_time": "-65%",
    "changelog_accuracy": "100%"
  }
}
```

---

## 🎯 BEST PRACTICES

### When to Use Each Agent

| Scenario | Best Agent | Why |
|----------|------------|-----|
| Daily PR reviews | `pr-manager` | Single-PR focused |
| Major feature review | `code-review-swarm` | Multiple perspectives |
| Sprint planning | `issue-tracker` | Issue organization |
| Hotfix deployment | `release-manager` | Quick coordination |
| New CI/CD setup | `workflow-automation` | Pipeline design |
| Monorepo changes | `multi-repo-swarm` | Cross-repo sync |

### Agent Coordination Patterns

```javascript
// Pattern 1: Sequential for dependent tasks
await Task("Issue analysis", ..., "issue-tracker")
then → Task("Sprint planning", ..., "project-board-sync")

// Pattern 2: Parallel for independent reviews
Task("Security review", ..., "reviewer") +
Task("Performance check", ..., "perf-analyzer") +
Task("Docs review", ..., "api-docs")

// Pattern 3: Hierarchical for complex flows
Task("Coordinator", ..., "github-modes")
  ├── Task("PR team", ..., "swarm-pr")
  ├── Task("Test team", ..., "tester")
  └── Task("Deploy team", ..., "release-manager")
```

---

## 🚀 ADVANCED GITHUB INTEGRATION

### Custom GitHub Bots with Claude-Flow

```javascript
// github-bot/claude-flow-bot.js
const claudeFlow = require('claude-flow');

// Auto-assign reviewers based on expertise
async function assignReviewers(pr) {
  const analysis = await claudeFlow.spawnAgent({
    type: 'pr-manager',
    task: `Analyze PR ${pr.number} and suggest reviewers based on:
      - File changes
      - Code expertise
      - Availability
      - Past review history`
  });

  return analysis.suggestedReviewers;
}

// Auto-label issues
async function labelIssue(issue) {
  const classification = await claudeFlow.spawnAgent({
    type: 'issue-tracker',
    task: `Classify issue: ${issue.title}`
  });

  return classification.labels;
}
```

---

## ✅ GITHUB AGENTS CHECKLIST

Before using GitHub agents:
- [ ] GitHub CLI (`gh`) installed and authenticated
- [ ] Proper repository permissions
- [ ] Claude-Flow connected to GitHub
- [ ] Memory namespaces set up
- [ ] Team patterns documented
- [ ] CI/CD pipelines ready
- [ ] Project boards configured

Remember: GitHub agents amplify your workflow but always require human oversight for critical decisions!