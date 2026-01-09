# ACME Corp Monorepo

A high-performance monorepo containing all ACME Corp's web properties, shared libraries, and internal tools. Built with **Turborepo**, **pnpm workspaces**, and modern tooling for maximum developer productivity.

**🚀 Apps**: 3 production apps | **📦 Packages**: 8 shared libraries | **👥 Team**: 45 developers

## 🎯 What is This Monorepo?

This repository is the single source of truth for ACME Corp's web ecosystem. It contains:

- **Customer-Facing Apps**: Marketing site, product dashboard, mobile app API
- **Internal Tools**: Admin dashboard, analytics platform
- **Shared Libraries**: UI components, utilities, configs, API clients
- **Documentation**: Technical docs, API references, style guides

### Why a Monorepo?

✅ **Single Source of Truth**: One repo, one version, one deploy  
✅ **Code Sharing**: Share components, utils, and configs effortlessly  
✅ **Atomic Changes**: Update shared code and all consumers in one PR  
✅ **Unified Tooling**: One linting config, one testing setup  
✅ **Better Collaboration**: See the whole picture, review across apps  
✅ **Faster CI/CD**: Smart caching with Turborepo (up to 85% faster builds)

## 📊 Repository Statistics

- **Total Lines of Code**: ~850,000
- **Active Contributors**: 45 developers
- **Monthly Deploys**: ~280
- **Test Coverage**: 87%
- **Build Time** (with cache): 3.2 minutes
- **Build Time** (cold): 18 minutes

## 🏗 Monorepo Structure

```text
acme-monorepo/
│
├── apps/                        # Production applications
│   ├── web/                     # Next.js marketing website
│   │   ├── src/
│   │   ├── public/
│   │   ├── package.json
│   │   └── next.config.js
│   │
│   ├── dashboard/               # React SaaS dashboard
│   │   ├── src/
│   │   ├── package.json
│   │   └── vite.config.ts
│   │
│   ├── docs/                    # Documentation site (Docusaurus)
│   │   ├── docs/
│   │   ├── blog/
│   │   └── docusaurus.config.js
│   │
│   ├── mobile-api/              # Node.js API for mobile apps
│   │   ├── src/
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   └── admin/                   # Internal admin panel
│       ├── src/
│       └── package.json
│
├── packages/                    # Shared packages
│   ├── ui/                      # Shared React component library
│   │   ├── src/
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   └── index.ts
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   └── README.md
│   │
│   ├── utils/                   # Shared utility functions
│   │   ├── src/
│   │   │   ├── date.ts
│   │   │   ├── string.ts
│   │   │   └── validation.ts
│   │   └── package.json
│   │
│   ├── api-client/              # Shared API client
│   │   ├── src/
│   │   └── package.json
│   │
│   ├── eslint-config/           # Shared ESLint configuration
│   │   ├── index.js
│   │   ├── react.js
│   │   └── package.json
│   │
│   ├── tsconfig/                # Shared TypeScript configs
│   │   ├── base.json
│   │   ├── react.json
│   │   ├── node.json
│   │   └── package.json
│   │
│   ├── tailwind-config/         # Shared Tailwind config
│   │   ├── index.js
│   │   └── package.json
│   │
│   ├── database/                # Prisma database client
│   │   ├── prisma/
│   │   │   └── schema.prisma
│   │   ├── src/
│   │   └── package.json
│   │
│   └── auth/                    # Authentication library
│       ├── src/
│       └── package.json
│
├── tooling/                     # Development tools
│   ├── scripts/                 # Automation scripts
│   │   ├── setup.sh
│   │   └── deploy.sh
│   └── github/                  # GitHub actions
│       └── workflows/
│
├── .github/                     # GitHub configuration
│   ├── workflows/
│   │   ├── ci.yml
│   │   ├── deploy.yml
│   │   └── release.yml
│   └── CODEOWNERS
│
├── turbo.json                   # Turborepo configuration
├── package.json                 # Root package.json
├── pnpm-workspace.yaml          # pnpm workspaces config
├── .npmrc                       # npm configuration
├── tsconfig.json                # Base TypeScript config
├── .eslintrc.js                 # Root ESLint config
├── .prettierrc                  # Prettier config
└── README.md
```

## 🚀 Quick Start

### Prerequisites

Ensure you have the following installed:

- **Node.js**: v20.0.0 or higher ([Download](https://nodejs.org/))
- **pnpm**: v8.0.0 or higher (`npm install -g pnpm`)
- **Git**: Latest version

### Initial Setup

```bash
# 1. Clone the repository
git clone https://github.com/acme/monorepo.git
cd monorepo

# 2. Install all dependencies (for all apps and packages)
pnpm install

# 3. Build all packages
pnpm build

# 4. Run development servers for all apps
pnpm dev
```

That's it! All apps should now be running:

- 🌐 Marketing Site: http://localhost:3000
- 📊 Dashboard: http://localhost:3001
- 📖 Docs: http://localhost:3002
- 🔧 Admin: http://localhost:3003
- 🚀 API: http://localhost:4000

### Environment Setup

Copy environment files for each app:

```bash
# Marketing site
cp apps/web/.env.example apps/web/.env.local

# Dashboard
cp apps/dashboard/.env.example apps/dashboard/.env.local

# API
cp apps/mobile-api/.env.example apps/mobile-api/.env
```

Fill in your environment variables (see individual app READMEs for details).

## 📦 Applications

### 1. Marketing Website (`apps/web`)

**Tech Stack**: Next.js 14, React 18, Tailwind CSS  
**URL**: https://acme.com  
**Purpose**: Public-facing marketing and SEO-optimized content

**Key Features**:
- Static generation for landing pages (99 Lighthouse score)
- Blog with MDX support
- Multi-language support (English, Spanish, French)
- Contact forms with Resend integration
- Analytics with Vercel Analytics

**Local Development**:
```bash
cd apps/web
pnpm dev
```

[📖 Full README](./apps/web/README.md)

### 2. Dashboard (`apps/dashboard`)

**Tech Stack**: React 18, Vite, TanStack Query, Zustand  
**URL**: https://app.acme.com  
**Purpose**: Customer-facing SaaS dashboard

**Key Features**:
- Real-time data updates with WebSockets
- Complex data tables with virtualization
- Charts and analytics (Recharts)
- Multi-tenant architecture
- Role-based access control (RBAC)

**Local Development**:
```bash
cd apps/dashboard
pnpm dev
```

[📖 Full README](./apps/dashboard/README.md)

### 3. Documentation Site (`apps/docs`)

**Tech Stack**: Docusaurus 3, React, Algolia  
**URL**: https://docs.acme.com  
**Purpose**: Developer documentation and API references

**Key Features**:
- Interactive code examples
- API reference auto-generated from OpenAPI
- Versioned documentation
- Full-text search with Algolia
- Dark mode support

**Local Development**:
```bash
cd apps/docs
pnpm dev
```

[📖 Full README](./apps/docs/README.md)

### 4. Mobile API (`apps/mobile-api`)

**Tech Stack**: Node.js, Express, PostgreSQL, Redis  
**URL**: https://api.acme.com  
**Purpose**: REST API for mobile applications

**Key Features**:
- RESTful API with OpenAPI spec
- JWT authentication
- Rate limiting and caching
- Background jobs with Bull
- Monitoring with Sentry

**Local Development**:
```bash
cd apps/mobile-api
pnpm dev
```

[📖 Full README](./apps/mobile-api/README.md)

### 5. Admin Panel (`apps/admin`)

**Tech Stack**: React, Material-UI, React Admin  
**URL**: https://admin.acme.com (internal)  
**Purpose**: Internal admin tools for customer support and ops

**Key Features**:
- User management
- Analytics dashboards
- Feature flags management
- System health monitoring

**Local Development**:
```bash
cd apps/admin
pnpm dev
```

[📖 Full README](./apps/admin/README.md)

## 📦 Shared Packages

### UI Component Library (`packages/ui`)

Shared React components used across all applications.

**Components** (50+):
- Buttons, Cards, Modals, Tooltips
- Forms (Input, Select, Checkbox, Radio)
- Data Display (Tables, Lists, Badge)
- Feedback (Alert, Toast, Progress)
- Navigation (Tabs, Breadcrumb, Pagination)

**Usage**:
```typescript
import { Button, Card, Modal } from '@acme/ui';

export default function MyComponent() {
  return (
    <Card>
      <Button variant="primary" size="lg">
        Click Me
      </Button>
    </Card>
  );
}
```

**Storybook**: http://localhost:6006 (`pnpm storybook`)

[📖 Full Docs](./packages/ui/README.md) | [🎨 Storybook](https://storybook.acme.com)

### Utilities (`packages/utils`)

Shared utility functions and helpers.

**Categories**:
- **Date/Time**: `formatDate`, `parseDate`, `timeAgo`
- **String**: `truncate`, `slugify`, `capitalize`
- **Validation**: `isEmail`, `isURL`, `isPhoneNumber`
- **Array**: `groupBy`, `unique`, `sortBy`
- **Object**: `deepMerge`, `pick`, `omit`
- **Number**: `formatCurrency`, `formatNumber`, `clamp`

**Usage**:
```typescript
import { formatDate, truncate, isEmail } from '@acme/utils';

const date = formatDate(new Date(), 'MMM DD, YYYY');
const excerpt = truncate(longText, 100);
const valid = isEmail('user@example.com');
```

[📖 Full Docs](./packages/utils/README.md)

### API Client (`packages/api-client`)

Type-safe API client for communicating with backend services.

**Features**:
- Automatic TypeScript types from OpenAPI
- Built-in authentication
- Request/response interceptors
- Retry logic and error handling

**Usage**:
```typescript
import { createClient } from '@acme/api-client';

const client = createClient({
  baseURL: process.env.API_URL,
  token: session.accessToken
});

// Fully typed requests
const user = await client.users.get('123');
const posts = await client.posts.list({ page: 1, limit: 10 });
```

[📖 Full Docs](./packages/api-client/README.md)

### Database (`packages/database`)

Prisma database client shared across backend services.

**Schema**: PostgreSQL with Prisma ORM  
**Models**: Users, Organizations, Posts, Comments, etc.

**Usage**:
```typescript
import { prisma } from '@acme/database';

const users = await prisma.user.findMany({
  where: { active: true },
  include: { posts: true }
});
```

**Migrations**:
```bash
cd packages/database
pnpm prisma migrate dev
pnpm prisma generate
```

[📖 Full Docs](./packages/database/README.md)

### Configuration Packages

#### ESLint Config (`packages/eslint-config`)
```json
{
  "extends": ["@acme/eslint-config/react"]
}
```

#### TypeScript Config (`packages/tsconfig`)
```json
{
  "extends": "@acme/tsconfig/react.json"
}
```

#### Tailwind Config (`packages/tailwind-config`)
```javascript
module.exports = {
  presets: [require('@acme/tailwind-config')],
}
```

## 🛠 Development Workflows

### Working on a Single App

```bash
# Run only the dashboard
pnpm --filter dashboard dev

# Run dashboard with dependencies
pnpm --filter dashboard... dev

# Build only the marketing site
pnpm --filter web build
```

### Working on Multiple Apps

```bash
# Run specific apps
pnpm --filter "{web,dashboard}" dev

# Run all apps except docs
pnpm --filter "!docs" dev
```

### Working on Shared Packages

```bash
# Watch mode for UI package
cd packages/ui
pnpm dev  # Rebuilds on file changes

# Apps importing @acme/ui will auto-reload
```

### Adding Dependencies

```bash
# Add to a specific app
pnpm --filter web add lodash

# Add to a package
pnpm --filter @acme/utils add date-fns

# Add to root (dev dependencies)
pnpm add -D -w prettier
```

### Creating a New App

```bash
# Use the generator
pnpm generate:app

# Or manually
mkdir apps/new-app
cd apps/new-app
pnpm init
# Add to pnpm-workspace.yaml
```

### Creating a New Package

```bash
# Use the generator
pnpm generate:package

# Or manually
mkdir packages/new-package
cd packages/new-package
pnpm init
```

## 🏗 Build System (Turborepo)

### How Turborepo Works

Turborepo intelligently caches build outputs and only rebuilds what changed.

**Benefits**:
- ⚡ **85% faster** builds with caching
- 🎯 **Smart scheduling** of parallel tasks
- 🔄 **Remote caching** shared across team
- 📊 **Build visualization** to debug slowness

### Turbo Configuration

```json
// turbo.json
{
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", ".next/**"]
    },
    "dev": {
      "cache": false,
      "persistent": true
    },
    "lint": {
      "outputs": []
    },
    "test": {
      "outputs": ["coverage/**"]
    }
  }
}
```

### Common Turbo Commands

```bash
# Build everything
pnpm build

# Build with remote caching
pnpm build --remote-cache

# Force rebuild (ignore cache)
pnpm build --force

# Dry run (see what would run)
pnpm build --dry-run

# See dependency graph
pnpm turbo run build --graph

# Clear cache
pnpm turbo prune
```

### Pipeline Visualization

```bash
# Generate visual graph
pnpm turbo run build --graph=graph.html
```

Opens an interactive graph showing:
- Build dependencies
- Parallel vs sequential tasks
- Cache hits/misses
- Execution time per task

## 🧪 Testing

### Test Strategy

| Type | Tool | Coverage |
|:-----|:-----|:---------|
| Unit Tests | Vitest | 87% |
| Component Tests | React Testing Library | 82% |
| E2E Tests | Playwright | Critical paths |
| Visual Tests | Chromatic | UI components |
| API Tests | Supertest | 91% |

### Running Tests

```bash
# Run all tests
pnpm test

# Run tests for specific app
pnpm --filter dashboard test

# Run tests in watch mode
pnpm test:watch

# Run E2E tests
pnpm test:e2e

# Generate coverage report
pnpm test:coverage
```

### Writing Tests

```typescript
// packages/ui/src/Button.test.tsx
import { render, screen } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  it('renders with correct text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });
  
  it('handles click events', () => {
    const handleClick = vi.fn();
    render(<Button onClick={handleClick}>Click</Button>);
    screen.getByText('Click').click();
    expect(handleClick).toHaveBeenCalledOnce();
  });
});
```

## 🚀 Deployment

### CI/CD Pipeline

**GitHub Actions** workflow runs on every push:

1. ✅ **Lint** - ESLint, Prettier
2. ✅ **Type Check** - TypeScript compilation
3. ✅ **Test** - Unit, integration, E2E
4. ✅ **Build** - All apps and packages
5. ✅ **Deploy** - Vercel (preview) or Production

### Deployment Targets

| App | Platform | URL |
|:----|:---------|:----|
| Marketing | Vercel | https://acme.com |
| Dashboard | Vercel | https://app.acme.com |
| Docs | Vercel | https://docs.acme.com |
| API | Railway | https://api.acme.com |
| Admin | Vercel | https://admin.acme.com |

### Manual Deployment

```bash
# Deploy all apps
pnpm deploy

# Deploy specific app
pnpm --filter web deploy

# Deploy to staging
pnpm deploy:staging

# Deploy to production (requires approval)
pnpm deploy:production
```

### Environment Variables

Each app has its own environment variables:

```bash
# Marketing site
apps/web/.env.local

# Dashboard
apps/dashboard/.env.local

# API
apps/mobile-api/.env
```

**Never commit `.env` files!** Use Vercel/Railway secret management.

## 📊 Monitoring & Observability

### Tools Used

- **Error Tracking**: Sentry
- **Performance**: Vercel Analytics
- **Uptime**: Better Uptime
- **Logs**: Datadog
- **APM**: New Relic (API only)

### Health Checks

```bash
# Check all services
pnpm health:check

# Output:
# ✅ web: https://acme.com (200 OK)
# ✅ dashboard: https://app.acme.com (200 OK)
# ✅ api: https://api.acme.com/health (200 OK)
```

## 🔧 Troubleshooting

### Common Issues

**Problem**: "Cannot find module '@acme/ui'"
```bash
# Solution: Build packages first
pnpm build
# Or run in watch mode
cd packages/ui && pnpm dev
```

**Problem**: "Port 3000 already in use"
```bash
# Solution: Kill process or use different port
pnpm --filter web dev -- --port 3001
```

**Problem**: "Out of memory during build"
```bash
# Solution: Increase Node memory
export NODE_OPTIONS="--max-old-space-size=4096"
pnpm build
```

**Problem**: "Changes in package not reflecting in app"
```bash
# Solution: Clear Turborepo cache
pnpm turbo prune
pnpm build
```

### Getting Help

1. Check the [internal wiki](https://wiki.acme.com)
2. Ask in #eng-help Slack channel
3. Open an issue with `[HELP]` prefix
4. Ping @platform-team for urgent issues

## 📚 Documentation

- **Architecture**: [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md)
- **Contributing**: [CONTRIBUTING.md](./CONTRIBUTING.md)
- **Security**: [SECURITY.md](./SECURITY.md)
- **Code of Conduct**: [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)
- **Release Process**: [docs/RELEASES.md](./docs/RELEASES.md)

## 🤝 Contributing

### Development Process

1. **Create a branch**: `git checkout -b feature/amazing-feature`
2. **Make changes**: Follow our [coding standards](./docs/CODING_STANDARDS.md)
3. **Write tests**: Maintain or improve coverage
4. **Run checks**: `pnpm lint && pnpm test && pnpm build`
5. **Commit**: Use [conventional commits](https://conventionalcommits.org)
6. **Push**: `git push origin feature/amazing-feature`
7. **Open PR**: Fill out the PR template
8. **Get reviews**: At least 2 approvals required
9. **Merge**: Squash and merge to main

### Commit Convention

```bash
# Format: type(scope): message

feat(dashboard): add user analytics chart
fix(ui): resolve button hover state bug
docs(readme): update installation steps
chore(deps): upgrade react to v18.3
test(utils): add date formatting tests
```

### Code Review Guidelines

- ✅ Keep PRs small (<500 lines)
- ✅ Write descriptive PR titles
- ✅ Add screenshots for UI changes
- ✅ Update relevant documentation
- ✅ Ensure CI passes before requesting review

## 📊 Repository Metrics

### Code Quality

![Test Coverage](https://img.shields.io/badge/coverage-87%25-brightgreen)
![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Type Safety](https://img.shields.io/badge/typescript-100%25-blue)

### Dependencies

```bash
# Check for outdated packages
pnpm outdated

# Update all dependencies
pnpm update -r

# Check for vulnerabilities
pnpm audit
```

### Bundle Sizes

| App | Initial JS | Total Size | Lighthouse |
|:----|:-----------|:-----------|:-----------|
| Marketing | 85 KB | 320 KB | 99/100 |
| Dashboard | 210 KB | 890 KB | 94/100 |
| Docs | 120 KB | 450 KB | 98/100 |

## 🛡 Security

- **Dependency Scanning**: Dependabot (weekly)
- **Secret Scanning**: GitHub Advanced Security
- **SAST**: SonarCloud
- **Penetration Testing**: Quarterly audits
- **Security Policy**: [SECURITY.md](./SECURITY.md)

## 📄 License

This monorepo is proprietary and confidential.  
© 2024 ACME Corporation. All rights reserved.

Unauthorized copying, distribution, or use is strictly prohibited.

## 👥 Team & Ownership

### Platform Team (@platform-team)
- **Lead**: @alice (alice@acme.com)
- **Members**: @bob, @carol, @dave
- **Responsibilities**: Infrastructure, CI/CD, monorepo tooling

### Product Teams

**Marketing** (@marketing-team)
- Owner: @emily
- Apps: `web`, `docs`

**Product** (@product-team)
- Owner: @frank
- Apps: `dashboard`

**API** (@api-team)
- Owner: @grace
- Apps: `mobile-api`

**Internal Tools** (@tools-team)
- Owner: @henry
- Apps: `admin`

## 🔗 Useful Links

- **Internal Wiki**: https://wiki.acme.com
- **Design System**: https://design.acme.com
- **Component Storybook**: https://storybook.acme.com
- **Status Page**: https://status.acme.com
- **Metrics Dashboard**: https://metrics.acme.com
- **Slack**: #engineering channel

---

**Questions?** Ask in #eng-help or email platform@acme.com

**Last Updated**: December 2024  
**Maintainers**: @platform-team
