# Real-World Examples: MigrationPro Remix App

## 🎯 Your Actual Project Context

You're building **MigrationPro.io** - a Remix application for migration services. Here are real examples from YOUR codebase showing how to use Claude-Flow effectively.

---

## Example 1: API Client Singleton Issue

### The Real Problem You Had
```javascript
// File: app/api/apiClientSingleton.server.js
// Issue: Connection bridgg issue (typo and connection problem)
```

### How to Fix with Claude-Flow
```
You: "Fix the connection issue in apiClientSingleton.server.js:
- Fix the typo 'bridgg' → 'bridge'
- Ensure singleton pattern is correctly implemented
- Add connection retry logic
- Add comprehensive error handling
- Include tests for connection scenarios"
```

### What Claude-Flow Does
1. Analyzes the singleton pattern
2. Fixes typo and connection logic
3. Implements exponential backoff retry
4. Adds proper error boundaries
5. Creates test suite with mocked connections

---

## Example 2: E2E Testing for Migration Flow

### Your Requirement
Testing the complete user migration flow in your Remix app

### The Perfect Prompt
```
You: "Create E2E tests for our migration flow using Playwright:

User Journey:
1. User lands on homepage
2. Clicks 'Start Migration'
3. Fills migration assessment form
4. Views migration options
5. Selects migration package
6. Completes payment
7. Receives confirmation

Requirements:
- Test each step independently
- Test complete flow
- Handle API mocking for payment
- Test error scenarios
- Mobile and desktop viewports
- Store patterns for reuse"
```

### Generated Test Structure
```typescript
// Claude-Flow creates:

// tests/e2e/migration-flow.spec.ts
import { test, expect } from '@playwright/test';
import { MigrationPage } from './pages/MigrationPage';
import { mockPaymentAPI } from './mocks/payment';

test.describe('Migration Flow', () => {
  test('Complete migration journey', async ({ page }) => {
    const migrationPage = new MigrationPage(page);

    // Step 1: Homepage
    await migrationPage.goto();
    await expect(page).toHaveTitle(/MigrationPro/);

    // Step 2: Start migration
    await migrationPage.startMigration();

    // Step 3: Assessment form
    await migrationPage.fillAssessment({
      currentCountry: 'Brazil',
      destinationCountry: 'Portugal',
      familySize: 4,
      profession: 'Software Engineer'
    });

    // Continue through flow...
  });

  test('Handles payment failure gracefully', async ({ page }) => {
    // Test implementation
  });
});
```

---

## Example 3: Remix Route Organization

### Your Current Structure Problem
```
app/routes/
├── _index.tsx
├── settings.tsx
├── support.tsx
└── [messy organization]
```

### Reorganizing with Claude-Flow
```
You: "Reorganize our Remix routes following best practices:
- Group related routes
- Implement proper layouts
- Add error boundaries
- Optimize bundle splitting
- Maintain SEO meta tags
- Preserve existing functionality"
```

### What Claude-Flow Creates
```
app/routes/
├── _index.tsx                    // Homepage
├── _auth.tsx                     // Auth layout
├── _auth.login.tsx              // Login page
├── _auth.register.tsx           // Register page
├── _dashboard.tsx               // Dashboard layout
├── _dashboard._index.tsx        // Dashboard home
├── _dashboard.migration.$id.tsx // Migration details
├── _dashboard.settings.tsx      // Settings
├── api.v1.$.ts                 // API routes
└── $.tsx                        // 404 handler
```

---

## Example 4: Internationalization Setup

### Your Need
Supporting multiple languages for global users

### Complex Multi-Agent Prompt
```
You: "Implement complete i18n for our migration app:

Requirements:
- Languages: English, Portuguese, Spanish
- Remix-i18n integration
- Lazy load translations
- Cookie-based persistence
- RTL support preparation
- Type-safe translations

Spawn agents for:
- Backend i18n setup
- Frontend components update
- Translation file structure
- Testing strategy
- Documentation

Work in parallel and coordinate through memory"
```

### Result Structure
```typescript
// Claude-Flow creates complete i18n setup:

// app/i18n.server.ts
export const i18n = new RemixI18n({
  supportedLanguages: ['en', 'pt', 'es'],
  fallbackLng: 'en',
  cookie: i18nCookie
});

// app/hooks/useTranslation.ts
export function useTranslation() {
  const { t, i18n } = useTranslation();
  // Type-safe translation hook
}

// public/locales/en/common.json
{
  "welcome": "Welcome to MigrationPro",
  "migration": {
    "start": "Start Your Journey",
    "assessment": "Free Assessment"
  }
}
```

---

## Example 5: Performance Optimization

### Your Performance Issue
Slow initial page load on migration assessment

### Optimization Prompt
```
You: "Optimize the migration assessment page performance:

Current issues:
- 3.2s initial load time
- Large bundle size
- Blocking API calls
- No caching strategy

Implement:
- Route prefetching
- Progressive enhancement
- Image optimization
- API response caching
- Code splitting
- Lighthouse score > 90

Measure and report improvements"
```

### Optimization Results
```typescript
// Before: 3.2s load time
// After: 0.8s load time

// Implementations by Claude-Flow:

// 1. Route prefetching
<Link prefetch="intent" to="/assessment">
  Start Assessment
</Link>

// 2. Progressive enhancement
export function AssessmentForm() {
  return (
    <Form method="post" className="enhancement-friendly">
      {/* Works without JS */}
    </Form>
  );
}

// 3. Image optimization
import { cloudinaryLoader } from '~/utils/cloudinary';
<Image loader={cloudinaryLoader} src="hero.jpg" />

// 4. API caching
export const loader: LoaderFunction = async ({ request }) => {
  return json(data, {
    headers: {
      "Cache-Control": "max-age=300, stale-while-revalidate=86400"
    }
  });
};
```

---

## Example 6: Database Migration Scripts

### Your Database Evolution Need
```
You: "Create a database migration system for our Remix app:
- Current: Scattered SQL files
- Need: Versioned migrations
- Support rollbacks
- Seed data for development
- Type-safe queries with Prisma"
```

### Generated Migration System
```typescript
// migrations/001_initial_schema.sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

// migrations/002_add_migrations_table.sql
CREATE TABLE migration_applications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id),
  status VARCHAR(50),
  country_from VARCHAR(100),
  country_to VARCHAR(100)
);

// package.json scripts
{
  "db:migrate": "prisma migrate dev",
  "db:seed": "tsx prisma/seed.ts",
  "db:reset": "prisma migrate reset"
}
```

---

## Example 7: Authentication Flow

### Your Auth Requirements
```
You: "Implement complete authentication for MigrationPro:
- Email/password login
- Google OAuth
- Remember me feature
- Session management with Remix
- Secure password reset
- Rate limiting
- CSRF protection"
```

### Complete Implementation
```typescript
// app/services/auth.server.ts
import { Authenticator } from "remix-auth";
import { GoogleStrategy } from "remix-auth-google";
import { FormStrategy } from "remix-auth-form";

export const authenticator = new Authenticator<User>(sessionStorage);

// Email/Password strategy
authenticator.use(
  new FormStrategy(async ({ form }) => {
    const email = form.get("email");
    const password = form.get("password");
    const remember = form.get("remember");

    const user = await verifyLogin(email, password);
    if (!user) throw new AuthError("Invalid credentials");

    if (remember) {
      // Extended session logic
    }

    return user;
  }),
  "user-pass"
);

// Google OAuth
authenticator.use(
  new GoogleStrategy({
    clientID: process.env.GOOGLE_CLIENT_ID,
    clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    callbackURL: "/auth/google/callback"
  }, async ({ profile }) => {
    return findOrCreateUser(profile);
  }),
  "google"
);
```

---

## Example 8: Real-time Features

### Adding Real-time Updates
```
You: "Add real-time migration status updates:
- WebSocket connection for live status
- Show other users viewing same migration
- Real-time chat with migration consultant
- Notification system
- Offline support with sync"
```

### Implementation
```typescript
// app/services/websocket.server.ts
import { Server } from "socket.io";

export const io = new Server(server, {
  cors: { origin: process.env.CLIENT_URL }
});

io.on("connection", (socket) => {
  socket.on("join-migration", (migrationId) => {
    socket.join(`migration:${migrationId}`);

    // Notify others
    socket.to(`migration:${migrationId}`).emit("user-joined", {
      userId: socket.data.userId,
      timestamp: Date.now()
    });
  });

  socket.on("status-update", (data) => {
    io.to(`migration:${data.migrationId}`).emit("status-changed", data);
  });
});

// app/routes/migration.$id.tsx
import { useSocket } from "~/hooks/useSocket";

export default function MigrationDetails() {
  const socket = useSocket();
  const [viewers, setViewers] = useState([]);

  useEffect(() => {
    socket.on("user-joined", (data) => {
      setViewers(prev => [...prev, data]);
    });
  }, []);

  // Real-time UI updates
}
```

---

## Example 9: CI/CD Pipeline

### Setting Up Deployment
```
You: "Create GitHub Actions CI/CD pipeline:
- Run tests on PR
- Type checking
- Linting
- Build verification
- Deploy to staging on merge
- Production deploy on tag
- Rollback capability"
```

### Generated Workflow
```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  pull_request:
  push:
    branches: [main]
    tags: ['v*']

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
      - run: npm ci
      - run: npm run typecheck
      - run: npm run lint
      - run: npm test
      - run: npx playwright test

  deploy-staging:
    if: github.ref == 'refs/heads/main'
    needs: test
    runs-on: ubuntu-latest
    steps:
      - run: npm run deploy:staging

  deploy-production:
    if: startsWith(github.ref, 'refs/tags/v')
    needs: test
    runs-on: ubuntu-latest
    steps:
      - run: npm run deploy:production
```

---

## Example 10: Monitoring & Analytics

### Adding Observability
```
You: "Implement monitoring for our migration app:
- Error tracking with Sentry
- Analytics with Plausible
- Performance monitoring
- Custom business metrics
- Real user monitoring (RUM)
- Alerting system"
```

### Complete Setup
```typescript
// app/entry.client.tsx
import * as Sentry from "@sentry/remix";
import { Plausible } from "~/services/analytics";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  integrations: [
    new Sentry.BrowserTracing(),
    new Sentry.Replay()
  ]
});

// Custom metrics
export function trackMigrationStart(country: string) {
  Plausible.track("Migration Started", {
    country,
    timestamp: Date.now()
  });

  // Business metric
  incrementMetric("migrations.started");
}

// app/services/monitoring.server.ts
import { StatsD } from "@datadog/statsd";

const metrics = new StatsD({
  host: process.env.METRICS_HOST
});

export function recordResponseTime(route: string, time: number) {
  metrics.histogram("response_time", time, [`route:${route}`]);
}
```

---

## 🎯 Pattern Library for Your Project

### Store These Patterns
```
You: "Store these patterns for our MigrationPro project:

1. API Pattern: All endpoints under /api/v1 with consistent error responses
2. Component Pattern: Use compound components for complex UI
3. Testing Pattern: Page object model for E2E tests
4. State Pattern: Use Remix loader/action for server state, Zustand for client
5. Error Pattern: User-friendly messages with recovery actions
6. Security Pattern: OWASP Top 10 compliance checks
7. Performance Pattern: Core Web Vitals optimization
8. Deployment Pattern: Blue-green deployment with health checks"
```

---

## 💡 Project-Specific Tips

### For Your Migration App
1. **Use route prefetching** for multi-step forms
2. **Implement progress persistence** for long applications
3. **Add offline support** for areas with poor connectivity
4. **Create reusable form components** for repeated fields
5. **Use optimistic UI** for better perceived performance
6. **Implement proper error boundaries** for each route
7. **Add comprehensive logging** for debugging user issues
8. **Create admin dashboard** for migration consultants

---

## 🚀 Next Complex Feature to Build

```
You: "Build a complete migration assessment wizard:
- Multi-step form with progress indicator
- Smart field validation
- Conditional fields based on answers
- Save progress to database
- Calculate migration complexity score
- Generate personalized report
- Email PDF report
- Track analytics events
- A/B test different flows
- Full test coverage

Use SPARC TDD mode and create reusable patterns"
```

This would demonstrate the full power of Claude-Flow with your actual project!