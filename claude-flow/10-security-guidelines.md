# Security Guidelines for Claude-Flow

## 🔒 CRITICAL SECURITY RULES

### NEVER Share These with Claude-Flow

#### 🚫 FORBIDDEN ITEMS
```
❌ Production database passwords
❌ API keys and secrets
❌ SSH private keys
❌ Customer personal data (PII)
❌ Credit card information
❌ Internal network details
❌ Security audit reports
❌ Penetration test results
```

#### ✅ SAFE ALTERNATIVES
```
✅ Use environment variable names: process.env.API_KEY
✅ Use placeholder values: "YOUR_API_KEY_HERE"
✅ Use test data: "test@example.com"
✅ Use mock credentials: "demo_user" / "demo_pass"
```

---

## 🛡️ SECURE DEVELOPMENT PRACTICES

### Environment Variables

#### ❌ WRONG: Hardcoding Secrets
```javascript
// NEVER DO THIS
const apiKey = "sk_live_abcd1234...";
const dbPassword = "actualPassword123";
```

#### ✅ CORRECT: Environment Variables
```javascript
// Always do this
const apiKey = process.env.API_KEY;
const dbPassword = process.env.DATABASE_PASSWORD;

// With validation
if (!process.env.API_KEY) {
  throw new Error("API_KEY environment variable is required");
}
```

### Secure Prompting

#### Example: Database Work
```
You: "Create a database connection using these environment variables:
- DATABASE_URL (PostgreSQL connection string)
- DB_SSL_CERT (SSL certificate path)
Don't include actual values, just the structure"
```

---

## 🔐 AUTHENTICATION & AUTHORIZATION

### Secure Authentication Patterns

```
You: "Implement secure authentication with:
- Bcrypt for password hashing (min 10 rounds)
- JWT with short expiration (15 min)
- Refresh tokens with rotation
- Rate limiting on login attempts
- Account lockout after 5 failed attempts
- CSRF protection
- Secure session configuration"
```

### Authorization Best Practices

```
You: "Implement RBAC (Role-Based Access Control):
- Principle of least privilege
- Role hierarchy: Admin > Manager > User
- Resource-based permissions
- Audit logging for all access
- Token validation on every request"
```

---

## 🛡️ INPUT VALIDATION & SANITIZATION

### Always Validate Input

```
You: "Create API endpoint with security validations:
- Input type checking
- Length restrictions
- SQL injection prevention
- XSS prevention
- Command injection prevention
- Path traversal prevention
- Rate limiting"
```

### Example Implementation
```javascript
// Claude-Flow generates:
import { z } from 'zod';
import validator from 'validator';
import DOMPurify from 'isomorphic-dompurify';

const userSchema = z.object({
  email: z.string().email().refine(
    (email) => validator.isEmail(email, { allow_utf8_local_part: false }),
    "Invalid email format"
  ),
  username: z.string()
    .min(3)
    .max(20)
    .regex(/^[a-zA-Z0-9_-]+$/, "Invalid username format"),
  bio: z.string().transform((val) => DOMPurify.sanitize(val))
});
```

---

## 🔒 DATA PROTECTION

### Encryption Requirements

```
You: "Implement data encryption:
- At rest: AES-256 for sensitive data
- In transit: TLS 1.3 minimum
- Key rotation every 90 days
- Separate encryption keys from data
- Use AWS KMS / Azure Key Vault for key management"
```

### PII Handling

```
You: "Handle personal data with:
- Data minimization (only collect what's needed)
- Encryption for PII fields
- Audit trail for access
- GDPR compliance (right to deletion)
- Data retention policies
- Anonymization for analytics"
```

---

## 🚨 SECURITY SCANNING

### Automated Security Checks

```
You: "Add security scanning to our CI/CD:
- Dependency vulnerability scanning (npm audit)
- SAST (Static Application Security Testing)
- Container scanning
- Secret detection
- License compliance
- OWASP Top 10 checks"
```

### Pre-Commit Security

```yaml
# .pre-commit-config.yaml
repos:
  - repo: https://github.com/Yelp/detect-secrets
    hooks:
      - id: detect-secrets
  - repo: https://github.com/hadolint/hadolint
    hooks:
      - id: hadolint
  - repo: https://github.com/sqlfluff/sqlfluff
    hooks:
      - id: sqlfluff-lint
```

---

## 🔍 SECURE CODE REVIEW

### Security Review Checklist

```
You: "Review code for security issues:
□ No hardcoded secrets
□ Input validation present
□ Output encoding for XSS prevention
□ SQL parameterized queries
□ Authentication checks
□ Authorization checks
□ Error messages don't leak info
□ Logging doesn't include sensitive data
□ Dependencies up to date
□ Security headers configured"
```

---

## 🛑 COMMON VULNERABILITIES TO PREVENT

### SQL Injection Prevention

#### ❌ VULNERABLE
```javascript
const query = `SELECT * FROM users WHERE id = ${userId}`;
```

#### ✅ SECURE
```javascript
const query = "SELECT * FROM users WHERE id = $1";
const result = await db.query(query, [userId]);
```

### XSS Prevention

#### ❌ VULNERABLE
```javascript
return `<div>${userInput}</div>`;
```

#### ✅ SECURE
```javascript
import DOMPurify from 'dompurify';
return `<div>${DOMPurify.sanitize(userInput)}</div>`;
```

### CSRF Prevention

```javascript
// Claude-Flow implements:
import csrf from 'csrf';

const tokens = new csrf();
const secret = tokens.secretSync();
const token = tokens.create(secret);

// Verify on requests
if (!tokens.verify(secret, requestToken)) {
  throw new Error("Invalid CSRF token");
}
```

---

## 🔐 API SECURITY

### Secure API Design

```
You: "Design secure API with:
- API key authentication
- Rate limiting (100 req/min)
- Request signing (HMAC)
- Versioning (/api/v1/)
- CORS properly configured
- Input validation
- Output filtering
- Audit logging
- Error handling (no stack traces)"
```

### API Security Headers

```javascript
// Security headers to implement
app.use((req, res, next) => {
  res.setHeader("X-Content-Type-Options", "nosniff");
  res.setHeader("X-Frame-Options", "DENY");
  res.setHeader("X-XSS-Protection", "1; mode=block");
  res.setHeader("Strict-Transport-Security", "max-age=31536000");
  res.setHeader("Content-Security-Policy", "default-src 'self'");
  next();
});
```

---

## 🚫 SECURITY ANTI-PATTERNS

### Anti-Pattern 1: Security by Obscurity
❌ Hiding endpoints
✅ Proper authentication and authorization

### Anti-Pattern 2: Rolling Your Own Crypto
❌ Custom encryption algorithms
✅ Use established libraries (bcrypt, argon2)

### Anti-Pattern 3: Trusting Client Input
❌ Client-side only validation
✅ Always validate server-side

### Anti-Pattern 4: Verbose Error Messages
❌ Detailed error: "User admin@example.com not found"
✅ Generic error: "Invalid credentials"

---

## 📋 SECURITY INCIDENT RESPONSE

### If Secrets Are Exposed

```
IMMEDIATE ACTIONS:
1. Rotate compromised credentials immediately
2. Check audit logs for unauthorized access
3. Notify security team
4. Document incident
5. Review how exposure occurred
6. Implement prevention measures
```

### Incident Response Template

```
You: "Create incident response plan:
- Detection mechanisms
- Escalation procedures
- Communication templates
- Recovery steps
- Post-mortem process
- Prevention improvements"
```

---

## 🔒 COMPLIANCE & REGULATIONS

### GDPR Compliance

```
You: "Implement GDPR requirements:
- Privacy by design
- Data portability
- Right to erasure
- Consent management
- Data breach notification (72 hours)
- Privacy policy
- Data processing agreements"
```

### Security Standards

```
You: "Ensure compliance with:
- OWASP Top 10
- PCI DSS (if handling payments)
- SOC 2 (if B2B SaaS)
- ISO 27001 principles
- NIST Cybersecurity Framework"
```

---

## 🛡️ SECURE DEPLOYMENT

### Production Security

```
You: "Secure production deployment:
- Secrets in secret manager (not in code)
- Minimum privilege IAM roles
- Private subnets for databases
- WAF for web applications
- DDoS protection
- Regular security updates
- Automated backups
- Disaster recovery plan"
```

---

## 📊 SECURITY METRICS

### Track These Metrics

```
Security Metrics Dashboard:
- Vulnerability scan results
- Dependency update lag
- Failed authentication attempts
- API abuse attempts
- Time to patch critical vulnerabilities
- Security training completion
- Code review coverage
- Incident response time
```

---

## 🎓 SECURITY TRAINING

### Team Security Awareness

```
You: "Create security training module:
1. Common vulnerabilities
2. Secure coding practices
3. Social engineering awareness
4. Incident response procedures
5. Compliance requirements
6. Tool usage (security scanners)
7. Case studies from breaches"
```

---

## 🔍 SECURITY AUDIT CHECKLIST

### Regular Security Audits

```
Monthly Security Audit:
□ Review access logs
□ Check for unused accounts
□ Verify API key rotation
□ Update dependencies
□ Review security alerts
□ Test backup restoration
□ Verify encryption status
□ Check compliance status
```

---

## 🚨 EMERGENCY CONTACTS

### Security Team Contacts
```
Store these in your incident response plan (not in Claude-Flow):
- Security Lead: [Contact]
- CTO: [Contact]
- DevOps On-Call: [Contact]
- Legal Team: [Contact]
- PR Team: [Contact]
```

---

## ✅ SECURITY BEST PRACTICES SUMMARY

1. **Never share real credentials** - Always use environment variables
2. **Validate all input** - Never trust user input
3. **Encrypt sensitive data** - Both at rest and in transit
4. **Use established libraries** - Don't roll your own security
5. **Keep dependencies updated** - Regular security patches
6. **Implement defense in depth** - Multiple layers of security
7. **Log security events** - But not sensitive data
8. **Regular security training** - Keep team aware
9. **Incident response plan** - Be prepared
10. **Regular audits** - Trust but verify

Remember: Security is everyone's responsibility. When in doubt, ask the security team!