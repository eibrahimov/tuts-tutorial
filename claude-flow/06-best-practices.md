# Best Practices & Anti-Patterns

## ✅ BEST PRACTICES

### 1. Context is King

#### ✅ DO: Provide Complete Context
```
"In our Remix app using TypeScript and Prisma, update the User model
to include migration status field. We follow domain-driven design
and all models should have audit fields (createdAt, updatedAt)."
```

#### ❌ DON'T: Give Vague Instructions
```
"Add status to user"
```

---

### 2. Incremental Development

#### ✅ DO: Build Incrementally
```
Step 1: "Create the basic User model with essential fields"
Step 2: "Add validation to the User model"
Step 3: "Add relationships to other models"
Step 4: "Create comprehensive tests"
```

#### ❌ DON'T: Ask for Everything at Once
```
"Build complete user management system with all features,
validations, relationships, tests, documentation, and deployment"
```

---

### 3. Memory Management

#### ✅ DO: Store Important Decisions
```
"Remember: We use camelCase for JavaScript variables,
PascalCase for components, and kebab-case for file names.
Store this in memory as 'naming-conventions'"
```

#### ❌ DON'T: Forget to Document Patterns
```
[Makes architectural decision but doesn't store it]
[Next session, makes conflicting decision]
```

---

### 4. Testing Strategy

#### ✅ DO: Request Comprehensive Tests
```
"Create the login function with:
- Unit tests for all scenarios
- Integration tests with database
- E2E test for user flow
- Edge cases covered
- Error scenarios tested"
```

#### ❌ DON'T: Skip Testing
```
"Create login function" [without mentioning tests]
```

---

### 5. Error Handling

#### ✅ DO: Plan for Failure
```
"Implement user registration with:
- Try-catch blocks
- Specific error messages
- User-friendly error responses
- Logging for debugging
- Recovery suggestions"
```

#### ❌ DON'T: Ignore Error Cases
```
"Add user registration" [assuming happy path only]
```

---

## 🚫 ANTI-PATTERNS TO AVOID

### Anti-Pattern 1: The Monolithic Request

#### ❌ WRONG:
```
"Build entire e-commerce platform"
```

#### ✅ CORRECT:
```
"Let's build an e-commerce platform. Start with:
1. User authentication system
2. Product catalog
3. Shopping cart
[Address each separately]"
```

---

### Anti-Pattern 2: Context Switching

#### ❌ WRONG:
```
Message 1: "Working on authentication"
Message 2: "Actually, let's do payments"
Message 3: "Wait, go back to auth"
```

#### ✅ CORRECT:
```
"Complete authentication first, then we'll tackle payments"
```

---

### Anti-Pattern 3: Ignoring Existing Patterns

#### ❌ WRONG:
```
"Create a new way to handle forms"
[When project already has form patterns]
```

#### ✅ CORRECT:
```
"Following our existing form patterns, create a migration application form"
```

---

### Anti-Pattern 4: Premature Optimization

#### ❌ WRONG:
```
"Create a button component with every possible option,
micro-optimizations, and support for 50 variants"
```

#### ✅ CORRECT:
```
"Create a button component with primary and secondary variants.
We'll add more as needed."
```

---

### Anti-Pattern 5: Skipping Code Review

#### ❌ WRONG:
```
"Create feature and commit directly"
```

#### ✅ CORRECT:
```
"Create feature, then review the code for:
- Best practices
- Performance issues
- Security concerns
- Test coverage"
```

---

## 💡 GOLDEN RULES

### Rule 1: Start Small, Iterate Fast
```
Small request → Review → Refine → Next iteration
```

### Rule 2: Document As You Go
```
Build feature → Store pattern → Share with team
```

### Rule 3: Test Everything
```
No code without tests (minimum 80% coverage)
```

### Rule 4: Review Before Committing
```
Generate → Review → Refine → Commit
```

### Rule 5: Learn from Patterns
```
Identify pattern → Store → Reuse → Improve
```

---

## 🎯 PROMPT TEMPLATES

### Feature Development Template
```
"Build [feature name] with these requirements:
Context: [Current system state]
Requirements: [Functional requirements]
Constraints: [Technical constraints]
Testing: [Test requirements]
Documentation: [What needs documenting]
Success Criteria: [How we know it's complete]"
```

### Bug Fix Template
```
"Fix bug in [location]:
Symptoms: [What users see]
Expected: [Correct behavior]
Steps to reproduce: [How to trigger]
Affected areas: [What might be impacted]
Tests needed: [Regression prevention]"
```

### Refactoring Template
```
"Refactor [component/module]:
Current issues: [Problems to solve]
Goals: [Desired improvements]
Constraints: [What must not break]
Patterns to apply: [Design patterns]
Metrics: [How to measure success]"
```

### Code Review Template
```
"Review [component/PR]:
Check for:
- Best practices adherence
- Performance implications
- Security vulnerabilities
- Test coverage
- Documentation completeness
- Accessibility compliance
Suggest improvements with explanations"
```

---

## 🔄 WORKFLOW BEST PRACTICES

### Morning Routine
1. **Restore Context**: "What were we working on yesterday?"
2. **Check Patterns**: "Show stored patterns for this feature"
3. **Plan Day**: "Help prioritize these tasks for today"

### During Development
1. **Small Chunks**: Work in 30-60 minute focused sessions
2. **Frequent Saves**: Store patterns immediately when found
3. **Regular Reviews**: Review generated code every few iterations
4. **Test Often**: Run tests after each significant change

### End of Day
1. **Document Patterns**: "Store today's learnings"
2. **Update TODOs**: "What's left for tomorrow?"
3. **Generate Summary**: "Summarize today's progress"

---

## 📊 QUALITY CHECKLIST

### Before Starting a Task
- [ ] Clear requirements defined
- [ ] Success criteria established
- [ ] Existing patterns reviewed
- [ ] Test strategy planned

### During Development
- [ ] Following project conventions
- [ ] Writing tests alongside code
- [ ] Handling errors properly
- [ ] Adding appropriate logging
- [ ] Documenting complex logic

### Before Completing
- [ ] All tests passing
- [ ] Code reviewed for quality
- [ ] Performance acceptable
- [ ] Security considered
- [ ] Documentation updated
- [ ] Patterns stored

---

## 🚀 ADVANCED PATTERNS

### Pattern 1: Progressive Enhancement
```
"Build form with progressive enhancement:
1. HTML form that works without JavaScript
2. Add JavaScript validation
3. Enhance with real-time feedback
4. Add optimistic UI updates"
```

### Pattern 2: Defensive Programming
```
"Implement API client with:
- Input validation
- Type checking
- Null safety
- Boundary checking
- Rate limiting
- Circuit breaker pattern"
```

### Pattern 3: Performance-First
```
"Build component with performance focus:
- Lazy loading
- Code splitting
- Memoization where appropriate
- Virtual scrolling for lists
- Image optimization
- Bundle size monitoring"
```

---

## 🎨 CODE STYLE BEST PRACTICES

### Consistency
```
"Apply these style rules consistently:
- 2 spaces for indentation
- Single quotes for strings
- Semicolons always
- Trailing commas in multi-line
- Destructuring when possible"
```

### Readability
```
"Prioritize readability:
- Descriptive variable names
- Functions do one thing
- Comments explain why, not what
- Consistent file organization
- Clear module boundaries"
```

### Maintainability
```
"Ensure maintainability:
- No magic numbers
- Configuration extracted
- Dependencies injected
- Side effects isolated
- Pure functions preferred"
```

---

## 🏆 TEAM BEST PRACTICES

### Knowledge Sharing
1. **Pattern Library**: Document and share successful patterns
2. **Code Reviews**: Learn from each other's approaches
3. **Pair Programming**: Work together on complex features
4. **Weekly Demos**: Show what you built with Claude-Flow

### Standardization
1. **Naming Conventions**: Agree and document
2. **File Structure**: Consistent organization
3. **Testing Approach**: Unified strategy
4. **Error Handling**: Standard patterns
5. **Documentation Style**: Common format

### Continuous Improvement
1. **Retrospectives**: What worked, what didn't
2. **Pattern Evolution**: Refine patterns based on experience
3. **Metric Tracking**: Measure productivity improvements
4. **Training Sessions**: Share advanced techniques

---

## ⚠️ WHEN NOT TO USE CLAUDE-FLOW

### Human-Only Decisions
- Business strategy
- User experience design
- Pricing decisions
- Legal compliance interpretation
- Sensitive data handling

### Better Done Manually
- Simple find-replace across files
- One-line fixes you already know
- Git operations you're comfortable with
- Environment-specific configurations

---

## 📈 SUCCESS METRICS

Track these to ensure best practices adoption:

1. **Code Quality**
   - Test coverage > 80%
   - Zero critical bugs in generated code
   - Code review approval rate > 95%

2. **Productivity**
   - Features delivered per sprint
   - Time to market reduction
   - Bug resolution time

3. **Team Health**
   - Pattern reuse rate
   - Knowledge sharing frequency
   - Developer satisfaction score

Remember: Best practices evolve. What works today might be an anti-pattern tomorrow. Stay flexible and keep learning!