# GitHub Integration with Claude-Flow

## 🚀 COMPLETE GITHUB WORKFLOW GUIDE

### How Claude-Flow Works with Your GitHub Repository

Claude-Flow seamlessly integrates with GitHub for a complete development workflow. This guide shows you exactly how to use Claude-Flow for every GitHub operation.

---

## 📋 ISSUE-DRIVEN DEVELOPMENT

### Creating Issues from Claude-Flow

```
You: "Create a GitHub issue for the login bug:
Title: Users with + in email cannot login
Labels: bug, high-priority
Assign to: me
Description: Include steps to reproduce and error logs"
```

Claude-Flow executes:
```bash
gh issue create \
  --title "Users with + in email cannot login" \
  --label "bug,high-priority" \
  --assignee "@me" \
  --body "## Description\n..."
```

### Working on Issues

```
You: "Start working on issue #45:
1. Create feature branch
2. Link to issue
3. Set up tracking
4. Begin implementation"
```

Claude-Flow executes:
```bash
# Create branch from issue
gh issue develop #45 --checkout

# Or manually
git checkout -b fix-45-email-validation
git push -u origin fix-45-email-validation
```

### Auto-Closing Issues

```
You: "Fix issue #45 and prepare commit message that will auto-close it"
```

Claude-Flow creates commit:
```
Fix email validation for special characters

- Updated regex to support RFC 5322
- Added test cases for + and other special chars
- Improved error messages

Fixes #45
```

---

## 🔄 PULL REQUEST WORKFLOW

### Creating Perfect PRs

```
You: "Create a pull request for my current branch:
- Analyze all changes
- Generate comprehensive description
- Link related issues
- Add reviewers
- Set up CI checks"
```

Claude-Flow workflow:
```bash
# 1. Analyze changes
git diff main...HEAD
git log main..HEAD

# 2. Create PR with rich description
gh pr create \
  --title "Fix email validation for RFC 5322 compliance" \
  --body "## Summary
  - Fixed email validation regex
  - Added comprehensive tests
  - Updated documentation

  ## Changes
  - `src/validators/email.ts`: Updated regex pattern
  - `tests/email.test.ts`: Added 50+ test cases

  ## Testing
  - [x] Unit tests pass
  - [x] Integration tests pass
  - [x] Manual testing completed

  Fixes #45

  ## Screenshots
  [If applicable]

  ## Checklist
  - [x] Tests added
  - [x] Documentation updated
  - [x] No console.logs
  - [x] Follows code style" \
  --reviewer senior-dev,tech-lead \
  --label enhancement,tested
```

### PR Review with Claude-Flow

```
You: "Review PR #123:
- Check code quality
- Security vulnerabilities
- Performance implications
- Test coverage
- Suggest improvements"
```

Claude-Flow performs:
```bash
# Fetch PR
gh pr checkout 123

# Review checklist
- Code style compliance ✓
- Test coverage > 80% ✓
- No secrets exposed ✓
- Performance benchmarks ✓
- Documentation updated ✓

# Add review comment
gh pr review 123 --comment -b "LGTM with suggestions:
1. Consider memoizing the validation function
2. Add edge case for international domains
3. Update changelog"
```

### Automated PR Checks

```yaml
# .github/workflows/claude-flow-pr-check.yml
name: Claude-Flow PR Validation

on:
  pull_request:
    types: [opened, synchronize]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Claude-Flow Analysis
        run: |
          npx claude-flow analyze \
            --check-patterns \
            --security-scan \
            --test-coverage \
            --performance-impact

      - name: Comment Results
        uses: actions/github-script@v6
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              body: `Claude-Flow Analysis Complete:
              ✅ Pattern compliance
              ✅ Security scan passed
              ✅ Coverage: 92%
              ⚠️ Performance: +50ms load time`
            })
```

---

## 🎬 GITHUB ACTIONS INTEGRATION

### Claude-Flow in CI/CD

```yaml
# .github/workflows/claude-flow-ci.yml
name: Claude-Flow CI/CD

on:
  push:
    branches: [main, develop]
  pull_request:

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Claude-Flow
        run: npm install -g claude-flow@alpha

      - name: Pattern Validation
        run: |
          npx claude-flow validate \
            --patterns .claude/patterns \
            --strict

      - name: Generate Tests
        if: github.event_name == 'pull_request'
        run: |
          npx claude-flow generate-tests \
            --coverage-target 90 \
            --changed-files-only

      - name: Security Scan
        run: |
          npx claude-flow security-scan \
            --owasp \
            --secrets-detection \
            --dependency-check

      - name: Performance Analysis
        run: |
          npx claude-flow perf-analyze \
            --baseline main \
            --fail-on-regression
```

### Auto-Generate Release Notes

```yaml
# .github/workflows/release.yml
name: Auto-Release with Claude-Flow

on:
  push:
    tags:
      - 'v*'

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Generate Release Notes
        id: notes
        run: |
          NOTES=$(npx claude-flow release-notes \
            --from-tag $(git describe --tags --abbrev=0 HEAD^) \
            --to-tag ${{ github.ref_name }} \
            --categorize \
            --include-contributors)
          echo "::set-output name=notes::$NOTES"

      - name: Create Release
        uses: actions/create-release@v1
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          body: ${{ steps.notes.outputs.notes }}
```

---

## 🏷️ BRANCH MANAGEMENT

### Smart Branch Creation

```
You: "Create a branch for new feature: user dashboard
Following our git-flow convention"
```

Claude-Flow:
```bash
# Analyzes your branch naming convention
# Creates: feature/user-dashboard
git checkout -b feature/user-dashboard
git push -u origin feature/user-dashboard

# Sets up branch protection
gh api repos/:owner/:repo/branches/feature/user-dashboard/protection \
  --method PUT \
  --field required_status_checks='{"strict":true,"contexts":["continuous-integration"]}' \
  --field enforce_admins=false \
  --field required_pull_request_reviews='{"required_approving_review_count":1}'
```

### Branch Cleanup

```
You: "Clean up merged branches"
```

Claude-Flow:
```bash
# List merged branches
git branch --merged main | grep -v main

# Delete locally and remotely
git branch -d feature/old-feature
git push origin --delete feature/old-feature

# Or use gh
gh pr list --state merged --json headRefName --jq '.[].headRefName' | \
  xargs -I {} git push origin --delete {}
```

---

## 📊 GITHUB PROJECT BOARDS

### Managing Project Board

```
You: "Move issue #45 to 'In Progress' column on our project board"
```

Claude-Flow:
```bash
# Using gh project commands
gh project item-edit --id ITEM_ID --field Status="In Progress"

# Or using API
gh api graphql -f query='
mutation {
  updateProjectV2ItemFieldValue(input: {
    projectId: "PROJECT_ID"
    itemId: "ITEM_ID"
    fieldId: "FIELD_ID"
    value: {text: "In Progress"}
  }) {
    projectV2Item {
      id
    }
  }
}'
```

### Creating Project Automation

```
You: "Set up automation: When PR is merged, move issue to Done"
```

Claude-Flow creates:
```yaml
# .github/workflows/project-automation.yml
name: Project Board Automation

on:
  pull_request:
    types: [closed]

jobs:
  update-project:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - name: Move to Done
        uses: actions/github-script@v6
        with:
          script: |
            const issueNumber = context.payload.pull_request.body.match(/#(\d+)/)[1];
            // Move issue to Done column
            await github.rest.projects.moveCard({
              card_id: cardId,
              position: 'top',
              column_id: doneColumnId
            });
```

---

## 🔍 GITHUB SEARCH & ANALYSIS

### Code Search Across Repos

```
You: "Search all our repos for deprecated functions"
```

Claude-Flow:
```bash
# Search organization repos
gh search code "deprecated" --owner=our-org --limit 100

# With more context
gh search code "// @deprecated" --lang=typescript --owner=our-org
```

### Repository Analytics

```
You: "Analyze our GitHub repo activity for the sprint report"
```

Claude-Flow generates:
```bash
# Get commit activity
gh api repos/:owner/:repo/stats/commit_activity

# PR metrics
gh pr list --state all --created "2024-01-01..2024-01-14" --json number,title,author,mergedAt | \
  jq 'length as $total | map(select(.mergedAt != null)) | length as $merged |
  {total: $total, merged: $merged, merge_rate: (($merged / $total) * 100)}'

# Issue velocity
gh issue list --state all --json number,closedAt,createdAt | \
  jq '[.[] | select(.closedAt != null) | {time_to_close: (.closedAt - .createdAt)}] |
  {average_close_time: (map(.time_to_close) | add / length)}'
```

---

## 🤖 GITHUB BOTS & WEBHOOKS

### Creating Claude-Flow Bot

```javascript
// github-bot/index.js
const { Octokit } = require("@octokit/rest");
const claudeFlow = require("claude-flow");

module.exports = async (req, res) => {
  const webhook = req.body;

  if (webhook.action === "opened" && webhook.pull_request) {
    // Auto-review with Claude-Flow
    const analysis = await claudeFlow.analyzePR({
      repo: webhook.repository.full_name,
      pr: webhook.number
    });

    await octokit.pulls.createReview({
      owner: webhook.repository.owner.login,
      repo: webhook.repository.name,
      pull_number: webhook.number,
      body: analysis.summary,
      event: analysis.approved ? 'APPROVE' : 'REQUEST_CHANGES',
      comments: analysis.suggestions
    });
  }
};
```

---

## 📝 COMMIT MESSAGE CONVENTIONS

### Semantic Commits with Claude-Flow

```
You: "Commit my changes with proper conventional commit format"
```

Claude-Flow analyzes changes and creates:
```
feat(auth): implement OAuth2 integration

- Added Google OAuth provider
- Implemented token refresh logic
- Added user profile sync

BREAKING CHANGE: Auth config structure changed

Fixes #45, Closes #46
```

### Auto-Generate Changelog

```
You: "Generate changelog from commits since last release"
```

Claude-Flow:
```markdown
## [2.0.0] - 2024-01-15

### 🚀 Features
- **auth**: Implement OAuth2 integration (#45)
- **dashboard**: Add real-time analytics widget (#52)

### 🐛 Bug Fixes
- **email**: Fix validation for special characters (#48)
- **api**: Resolve timeout on large datasets (#51)

### 💔 Breaking Changes
- Auth configuration structure has changed. See migration guide.

### 👥 Contributors
- @developer1
- @developer2
```

---

## 🔐 GITHUB SECRETS MANAGEMENT

### Safe Secret Handling

```
You: "Set up GitHub secrets for our deployment"
```

Claude-Flow never stores actual secrets but guides:
```bash
# Set secrets (you provide actual values)
gh secret set DATABASE_URL
gh secret set API_KEY
gh secret set SENTRY_DSN

# List secrets (safe - doesn't show values)
gh secret list

# Use in workflow
echo "Secrets are available as ${{ secrets.DATABASE_URL }} in workflows"
```

---

## 🎯 GITHUB WORKFLOW EXAMPLES

### Complete Feature Workflow

```
You: "Guide me through complete GitHub feature workflow"
```

Claude-Flow:
```bash
# 1. Create issue
gh issue create --title "Add user dashboard"

# 2. Create branch
gh issue develop #100 --checkout

# 3. Make changes (Claude-Flow helps with code)
[Implementation happens here]

# 4. Commit with issue reference
git commit -m "feat: implement user dashboard

- Added dashboard route
- Created widget components
- Integrated analytics API

Refs #100"

# 5. Push and create PR
git push -u origin feature/user-dashboard
gh pr create --fill --assignee @me --reviewer tech-lead

# 6. After approval, merge
gh pr merge --squash --delete-branch

# 7. Issue auto-closes from PR
```

---

## 📈 GITHUB METRICS & REPORTING

### Sprint Metrics Dashboard

```
You: "Generate sprint metrics for our GitHub activity"
```

Claude-Flow creates report:
```markdown
## Sprint 23 Metrics (Jan 1-14, 2024)

### Velocity
- **Issues Created**: 45
- **Issues Closed**: 38 (84% completion)
- **PRs Merged**: 42
- **Average PR Review Time**: 2.3 hours

### Code Metrics
- **Commits**: 234
- **Lines Added**: 5,432
- **Lines Removed**: 2,123
- **Test Coverage**: 87% (+3%)

### Contributors
- 8 active contributors
- 142 total contributions

### Highlights
- ✅ Authentication system completed
- ✅ Dashboard MVP launched
- ⚠️ Payment integration delayed
```

---

## 🚀 GITHUB ADVANCED FEATURES

### GitHub Copilot + Claude-Flow

```
You: "Configure my environment to use both GitHub Copilot and Claude-Flow effectively"
```

Best practices:
1. Use Copilot for line-by-line completion
2. Use Claude-Flow for architecture and complex features
3. Let Claude-Flow review Copilot's suggestions
4. Store patterns from both in memory

### GitHub Codespaces Integration

```
# .devcontainer/devcontainer.json
{
  "name": "Claude-Flow Dev Environment",
  "image": "mcr.microsoft.com/devcontainers/typescript-node:20",
  "postCreateCommand": "npm install -g claude-flow@alpha",
  "customizations": {
    "vscode": {
      "extensions": [
        "github.copilot",
        "claude.code"
      ]
    }
  }
}
```

---

## ✅ GITHUB INTEGRATION CHECKLIST

- [ ] Issue templates configured
- [ ] PR templates set up
- [ ] Branch protection rules
- [ ] GitHub Actions workflows
- [ ] Project board automation
- [ ] Webhook integration
- [ ] Secret management
- [ ] Team permissions
- [ ] Code review process
- [ ] Release automation

Remember: Claude-Flow enhances your GitHub workflow but never replaces human review and decision-making!