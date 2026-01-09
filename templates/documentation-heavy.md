# MegaFramework Documentation

**The Modern Web Framework for Building Scalable Enterprise Applications**

Welcome to MegaFramework - a next-generation full-stack framework that combines the best of React, server-side rendering, and edge computing. Built for teams that need to ship fast without sacrificing performance, security, or developer experience.

**Version**: 3.0.0 | **License**: MIT | **Status**: Stable ✅

## 🚀 Quick Links

- 📖 [Full Documentation](https://docs.megaframework.com)
- 🎓 [Interactive Tutorial](https://megaframework.com/tutorial)
- 💬 [Community Discord](https://discord.gg/megaframework)
- 📺 [Video Courses](https://megaframework.com/learn)
- 🐛 [Issue Tracker](https://github.com/mega/framework/issues)

## 📑 Table of Contents

### Getting Started
- [What is MegaFramework?](#what-is-megaframework)
- [Why MegaFramework?](#why-megaframework)
- [Installation](#installation)
- [Your First App](#your-first-app)
- [Project Structure](#project-structure)

### Core Concepts
- [Routing](#routing)
- [Data Fetching](#data-fetching)
- [State Management](#state-management)
- [Styling](#styling)
- [API Routes](#api-routes)

### Advanced Topics
- [Server-Side Rendering (SSR)](#server-side-rendering)
- [Static Site Generation (SSG)](#static-site-generation)
- [Edge Functions](#edge-functions)
- [Authentication](#authentication)
- [Middleware](#middleware)
- [Caching Strategies](#caching-strategies)
- [Internationalization (i18n)](#internationalization)

### API Reference
- [CLI Commands](#cli-commands)
- [Configuration](#configuration)
- [Core APIs](#core-apis)
- [Plugins](#plugins)

### Deployment
- [Vercel](#deploy-to-vercel)
- [Netlify](#deploy-to-netlify)
- [AWS](#deploy-to-aws)
- [Docker](#deploy-with-docker)

### Additional Resources
- [FAQ](#faq)
- [Troubleshooting](#troubleshooting)
- [Migration Guides](#migration-guides)
- [Community Plugins](#community-plugins)

---

## What is MegaFramework?

MegaFramework is a **full-stack React framework** that provides everything you need to build production-ready web applications:

### Key Features

✅ **Hybrid Rendering**: Mix SSR, SSG, and CSR in one app  
✅ **File-Based Routing**: Routes from your file system  
✅ **API Routes**: Build your backend alongside your frontend  
✅ **Edge Functions**: Run code at the edge for lowest latency  
✅ **TypeScript First**: Full type safety from database to UI  
✅ **Zero Config**: Sensible defaults, configure only what you need  
✅ **Optimized Builds**: Automatic code splitting and lazy loading  
✅ **Developer Experience**: Hot reload, error overlay, time-travel debugging

### What Can You Build?

- 🛍️ **E-commerce Sites**: High-performance storefronts with SEO
- 📱 **SaaS Applications**: Full-stack apps with auth and payments
- 📰 **Content Sites**: Blogs, documentation, marketing pages
- 🎮 **Interactive Apps**: Dashboards, tools, games
- 🌐 **Multi-tenant Platforms**: Enterprise apps with customization

## Why MegaFramework?

### vs Next.js
- ✅ Simpler data fetching APIs
- ✅ Built-in state management
- ✅ Better edge function support
- ✅ Native TypeScript (no compilation needed)

### vs Remix
- ✅ More flexible rendering options
- ✅ Established ecosystem (5+ years)
- ✅ Better static site generation

### vs SvelteKit
- ✅ Larger React ecosystem
- ✅ More enterprise adoption
- ✅ Richer tooling and IDE support

### The Numbers

- **1.2M** weekly downloads
- **45K** GitHub stars
- **2,500+** companies in production
- **99.9%** uptime on framework CDN
- **<100ms** p50 response time

## Installation

### Requirements

- Node.js 18.17 or later
- macOS, Windows, or Linux

### Create a New App

The fastest way to get started:

\`\`\`bash
# Using npx (npm 5.2+)
npx create-mega-app my-app

# Using yarn
yarn create mega-app my-app

# Using pnpm
pnpm create mega-app my-app

# With TypeScript (recommended)
npx create-mega-app my-app --typescript

# With a template
npx create-mega-app my-app --template blog
# Available templates: blog, e-commerce, dashboard, docs, landing
\`\`\`

### Manual Installation

Add to an existing project:

\`\`\`bash
npm install megaframework react react-dom

# Peer dependencies
npm install --save-dev @types/react @types/react-dom typescript
\`\`\`

Create \`mega.config.ts\`:

\`\`\`typescript
import { defineConfig } from 'megaframework';

export default defineConfig({
  // Your config here
});
\`\`\`

Add scripts to \`package.json\`:

\`\`\`json
{
  "scripts": {
    "dev": "mega dev",
    "build": "mega build",
    "start": "mega start",
    "lint": "mega lint"
  }
}
\`\`\`

## Your First App

### 1. Create a Page

Create \`pages/index.tsx\`:

\`\`\`typescript
export default function Home() {
  return (
    <div>
      <h1>Welcome to MegaFramework!</h1>
      <p>Build something amazing.</p>
    </div>
  );
}
\`\`\`

### 2. Add Styling

MegaFramework supports CSS Modules, Tailwind, Styled Components, and more.

Using CSS Modules (\`index.module.css\`):

\`\`\`css
.container {
  min-height: 100vh;
  padding: 4rem;
  text-align: center;
}

.title {
  font-size: 3rem;
  color: #0070f3;
}
\`\`\`

\`\`\`typescript
import styles from './index.module.css';

export default function Home() {
  return (
    <div className={styles.container}>
      <h1 className={styles.title}>Welcome!</h1>
    </div>
  );
}
\`\`\`

### 3. Fetch Data

\`\`\`typescript
import { getServerData } from 'megaframework';

export default function Blog({ posts }) {
  return (
    <div>
      <h1>Blog Posts</h1>
      {posts.map(post => (
        <article key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.excerpt}</p>
        </article>
      ))}
    </div>
  );
}

// Runs on the server
export const getData = getServerData(async () => {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();
  
  return { props: { posts } };
});
\`\`\`

### 4. Add Dynamic Routes

Create \`pages/blog/[slug].tsx\`:

\`\`\`typescript
import { useRouter } from 'megaframework/router';
import { getServerData } from 'megaframework';

export default function BlogPost({ post }) {
  const router = useRouter();
  
  if (router.isFallback) {
    return <div>Loading...</div>;
  }
  
  return (
    <article>
      <h1>{post.title}</h1>
      <div dangerouslySetInnerHTML={{ __html: post.content }} />
    </article>
  );
}

export const getData = getServerData(async ({ params }) => {
  const post = await fetch('https://api.example.com/posts/${params.slug}');
  
  return {
    props: { post: await post.json() },
    revalidate: 60 // ISR: Revalidate every 60 seconds
  };
});

// Generate static paths at build time
export const getPaths = getServerData(async () => {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();
  
  return {
    paths: posts.map(post => ({ params: { slug: post.slug } })),
    fallback: true // Enable ISR for new paths
  };
});
\`\`\`

### 5. Create an API Route

Create \`pages/api/hello.ts\`:

\`\`\`typescript
import { NextApiRequest, NextApiResponse } from 'megaframework';

export default function handler(req: NextApiRequest, res: NextApiResponse) {
  res.status(200).json({ 
    message: 'Hello from MegaFramework!',
    timestamp: new Date().toISOString()
  });
}
\`\`\`

Advanced API route with database:

\`\`\`typescript
import { db } from '@/lib/database';
import { withAuth } from '@/middleware/auth';

async function handler(req, res) {
  if (req.method === 'GET') {
    const users = await db.user.findMany();
    return res.status(200).json(users);
  }
  
  if (req.method === 'POST') {
    const user = await db.user.create({
      data: req.body
    });
    return res.status(201).json(user);
  }
  
  res.status(405).json({ error: 'Method not allowed' });
}

export default withAuth(handler); // Protected route
\`\`\`

### 6. Run Development Server

\`\`\`bash
npm run dev
\`\`\`

Open http://localhost:3000 🎉

## Project Structure

Recommended structure for a MegaFramework app:

\`\`\`
my-mega-app/
├── pages/              # File-based routes
│   ├── index.tsx       # / route
│   ├── about.tsx       # /about route
│   ├── blog/
│   │   ├── index.tsx   # /blog route
│   │   └── [slug].tsx  # /blog/:slug route
│   ├── api/            # API routes
│   │   └── users.ts    # /api/users endpoint
│   ├── _app.tsx        # Custom App component
│   └── _document.tsx   # Custom Document
│
├── components/         # Reusable components
│   ├── Button.tsx
│   ├── Header.tsx
│   └── Layout.tsx
│
├── lib/                # Utility functions
│   ├── database.ts
│   ├── auth.ts
│   └── api.ts
│
├── styles/             # Global styles
│   ├── globals.css
│   └── variables.css
│
├── public/             # Static files
│   ├── images/
│   └── favicon.ico
│
├── middleware/         # Custom middleware
│   └── auth.ts
│
├── types/              # TypeScript types
│   └── index.ts
│
├── mega.config.ts      # Framework configuration
├── tsconfig.json       # TypeScript configuration
├── package.json
└── .env.local          # Environment variables
\`\`\`

## Routing

### File-Based Routing

MegaFramework uses your file system as the API for routes:

| File Path | URL |
|:----------|:----|
| \`pages/index.tsx\` | \`/\` |
| \`pages/about.tsx\` | \`/about\` |
| \`pages/blog/index.tsx\` | \`/blog\` |
| \`pages/blog/first-post.tsx\` | \`/blog/first-post\` |
| \`pages/blog/[slug].tsx\` | \`/blog/:slug\` |
| \`pages/posts/[...all].tsx\` | \`/posts/*\` (catch-all) |
| \`pages/[[...slug]].tsx\` | \`/*\` (optional catch-all) |

### Dynamic Routes

\`\`\`typescript
// pages/posts/[id].tsx
import { useRouter } from 'megaframework/router';

export default function Post() {
  const router = useRouter();
  const { id } = router.query;
  
  return <div>Post: {id}</div>;
}
\`\`\`

### Nested Dynamic Routes

\`\`\`typescript
// pages/shop/[category]/[product].tsx
export default function Product() {
  const router = useRouter();
  const { category, product } = router.query;
  
  return <div>{category} - {product}</div>;
}
// URL: /shop/electronics/laptop
\`\`\`

### Catch-All Routes

\`\`\`typescript
// pages/docs/[...slug].tsx
export default function Docs() {
  const router = useRouter();
  const { slug } = router.query; // slug is an array
  
  return <div>Docs: {slug?.join(' / ')}</div>;
}
// URL: /docs/getting-started/installation
// slug: ['getting-started', 'installation']
\`\`\`

### Programmatic Navigation

\`\`\`typescript
import { useRouter } from 'megaframework/router';
import Link from 'megaframework/link';

export default function Navigation() {
  const router = useRouter();
  
  const handleClick = () => {
    router.push('/about');
    // Or with query params
    router.push({
      pathname: '/blog',
      query: { page: '2' }
    });
  };
  
  return (
    <div>
      <Link href="/about">About</Link>
      <button onClick={handleClick}>Go to About</button>
    </div>
  );
}
\`\`\`

## Data Fetching

MegaFramework offers multiple data fetching strategies:

### Server-Side Rendering (SSR)

Fetch data on every request:

\`\`\`typescript
import { getServerData } from 'megaframework';

export const getData = getServerData(async (context) => {
  const { req, res, params, query } = context;
  
  // Access request headers
  const userAgent = req.headers['user-agent'];
  
  // Fetch data
  const data = await fetch('https://api.example.com/data');
  
  return {
    props: {
      data: await data.json(),
      userAgent
    }
  };
});

export default function Page({ data, userAgent }) {
  return <div>{data.title}</div>;
}
\`\`\`

### Static Site Generation (SSG)

Generate pages at build time:

\`\`\`typescript
import { getStaticData } from 'megaframework';

export const getData = getStaticData(async () => {
  const posts = await fetchPosts();
  
  return {
    props: { posts },
    revalidate: 3600 // ISR: Regenerate every hour
  };
});
\`\`\`

### Incremental Static Regeneration (ISR)

Update static pages after deployment:

\`\`\`typescript
export const getData = getStaticData(async () => {
  return {
    props: { data: await fetchData() },
    revalidate: 10 // Regenerate every 10 seconds
  };
});
\`\`\`

### Client-Side Fetching

For dynamic data that doesn't need SEO:

\`\`\`typescript
import { useState, useEffect } from 'react';
import { useSWR } from 'megaframework/data';

// With SWR (recommended)
export default function Profile() {
  const { data, error, isLoading } = useSWR('/api/user', fetcher);
  
  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error loading data</div>;
  
  return <div>Hello {data.name}!</div>;
}

// With useEffect
export default function Dashboard() {
  const [data, setData] = useState(null);
  
  useEffect(() => {
    fetch('/api/dashboard')
      .then(res => res.json())
      .then(setData);
  }, []);
  
  return data ? <div>{data.stats}</div> : <div>Loading...</div>;
}
\`\`\`

## State Management

MegaFramework includes built-in state management:

### Local Component State

\`\`\`typescript
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
\`\`\`

### Global State (Atoms)

\`\`\`typescript
// lib/store.ts
import { atom, useAtom } from 'megaframework/state';

export const userAtom = atom({
  key: 'user',
  default: null
});

export const themeAtom = atom({
  key: 'theme',
  default: 'light'
});

// components/Profile.tsx
import { useAtom } from 'megaframework/state';
import { userAtom } from '@/lib/store';

export default function Profile() {
  const [user, setUser] = useAtom(userAtom);
  
  return (
    <div>
      {user ? 'Welcome ${user.name}!' : 'Please log in'}
    </div>
  );
}
\`\`\`

### Derived State (Selectors)

\`\`\`typescript
import { selector, useValue } from 'megaframework/state';
import { userAtom } from '@/lib/store';

const userNameSelector = selector({
  key: 'userName',
  get: ({ get }) => {
    const user = get(userAtom);
    return user?.name ?? 'Guest';
  }
});

export default function Greeting() {
  const userName = useValue(userNameSelector);
  return <h1>Hello, {userName}!</h1>;
}
\`\`\`

## API Reference

### CLI Commands

\`\`\`bash
# Development
mega dev              # Start dev server (hot reload)
mega dev --port 4000  # Custom port
mega dev --turbo      # Enable turbopack (faster)

# Production
mega build            # Build for production
mega start            # Start production server
mega export           # Export static HTML

# Utilities
mega lint             # Run ESLint
mega lint --fix       # Auto-fix issues
mega analyze          # Analyze bundle size
mega info             # Show system info
\`\`\`

### Configuration API

\`\`\`typescript
// mega.config.ts
import { defineConfig } from 'megaframework';

export default defineConfig({
  // Server
  port: 3000,
  hostname: 'localhost',
  
  // Build
  outDir: 'dist',
  typescript: {
    strict: true,
    paths: {
      '@/*': ['./src/*']
    }
  },
  
  // Optimization
  experimental: {
    turbo: true,
    serverComponents: true
  },
  
  // SEO
  meta: {
    title: 'My App',
    description: 'My awesome app'
  },
  
  // Plugins
  plugins: [
    'mega-plugin-mdx',
    ['mega-plugin-sitemap', { domain: 'https://example.com' }]
  ]
});
\`\`\`

For the complete API reference, visit: https://docs.megaframework.com/api

## FAQ

### Q: How does MegaFramework compare to Next.js?

**A**: MegaFramework is similar to Next.js but focuses on simplicity and developer experience. Key differences:
- Simpler data fetching API
- Built-in state management
- Native TypeScript support (no build step)
- More flexible rendering options

### Q: Can I use MegaFramework with my existing React app?

**A**: Yes! MegaFramework can be adopted incrementally. Start by migrating one route at a time.

### Q: Does MegaFramework support TypeScript?

**A**: Yes, TypeScript is a first-class citizen. All APIs are fully typed, and \`.tsx\` files work out of the box.

### Q: How do I deploy a MegaFramework app?

**A**: Deploy anywhere Node.js runs: Vercel, Netlify, AWS, DigitalOcean, etc. See our [deployment guide](#deployment).

### Q: Is MegaFramework production-ready?

**A**: Absolutely. It's used by 2,500+ companies including Fortune 500 enterprises.

### Q: Can I use my preferred CSS solution?

**A**: Yes. MegaFramework supports CSS Modules, Tailwind, styled-components, Emotion, and vanilla CSS.

---

**Need more help?**
- 📖 [Full Documentation](https://docs.megaframework.com)
- 💬 [Discord Community](https://discord.gg/megaframework)
- 🐦 [Twitter Updates](https://twitter.com/megaframework)
- 📧 Email: support@megaframework.com
