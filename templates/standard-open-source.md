# Project Name

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Coverage](https://img.shields.io/badge/coverage-95%25-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Version](https://img.shields.io/badge/version-1.0.0-orange)
![Downloads](https://img.shields.io/npm/dm/package-name)

A comprehensive description of the library that clearly explains what problem it solves. For example: "A type-safe HTTP client for TypeScript that provides automatic request/response validation, intelligent caching, and seamless error handling. Built for modern web applications that need reliability and developer experience."

## Why Use This?

Explain the key value propositions:

- **Problem it solves**: Traditional HTTP clients require extensive boilerplate for type safety
- **How it's different**: Automatic TypeScript inference and runtime validation
- **Who it's for**: Teams building production TypeScript applications

## Features

- 🚀 **Fast**: Optimized for performance with intelligent request batching
- 📦 **Lightweight**: Zero dependencies, only 4KB gzipped
- 🔧 **Fully Typed**: Written in TypeScript with comprehensive type definitions
- 🛡️ **Safe**: Runtime validation using Zod schemas
- 🔄 **Smart Caching**: Automatic response caching with configurable TTL
- 🎯 **Intuitive API**: Fluent interface design for better DX
- 📱 **Universal**: Works in Node.js, browsers, and edge environments

## Installation

\`\`\`bash
# npm
npm install my-cool-package

# yarn
yarn add my-cool-package

# pnpm
pnpm add my-cool-package
\`\`\`

## Quick Start

Here's a 30-second introduction to get you up and running:

\`\`\`typescript
import { createClient } from 'my-cool-package';

// Create a client instance
const client = createClient({
  baseURL: 'https://api.example.com',
  timeout: 5000
});

// Make a request
const data = await client.get('/users/123');
console.log(data);
\`\`\`

## Detailed Usage

### Basic Requests

\`\`\`typescript
// GET request
const user = await client.get('/users/123');

// POST request
const newUser = await client.post('/users', {
  body: { name: 'John Doe', email: 'john@example.com' }
});

// PUT request
const updated = await client.put('/users/123', {
  body: { name: 'Jane Doe' }
});

// DELETE request
await client.delete('/users/123');
\`\`\`

### Advanced Configuration

\`\`\`typescript
const client = createClient({
  baseURL: 'https://api.example.com',
  timeout: 10000,
  headers: {
    'Authorization': 'Bearer token',
    'Custom-Header': 'value'
  },
  retry: {
    attempts: 3,
    delay: 1000
  },
  cache: {
    enabled: true,
    ttl: 60000 // 1 minute
  }
});
\`\`\`

### Type-Safe Requests with Validation

\`\`\`typescript
import { z } from 'zod';

// Define your schema
const UserSchema = z.object({
  id: z.number(),
  name: z.string(),
  email: z.string().email()
});

// Type-safe request
const user = await client.get('/users/123', {
  schema: UserSchema
});
// user is now typed as { id: number; name: string; email: string }
\`\`\`

### Error Handling

\`\`\`typescript
try {
  const data = await client.get('/users/123');
} catch (error) {
  if (error.isNetworkError) {
    console.error('Network failed:', error.message);
  } else if (error.isValidationError) {
    console.error('Response validation failed:', error.details);
  } else {
    console.error('Request failed:', error.status, error.message);
  }
}
\`\`\`

## API Reference

### \`createClient(config: ClientConfig): Client\`

Creates a new HTTP client instance.

**Parameters:**
- \`config.baseURL\` (string): Base URL for all requests
- \`config.timeout\` (number, optional): Request timeout in milliseconds (default: 30000)
- \`config.headers\` (object, optional): Default headers for all requests
- \`config.retry\` (object, optional): Retry configuration
- \`config.cache\` (object, optional): Cache configuration

**Returns:** Client instance

### \`client.get(path: string, options?: RequestOptions)\`

Performs a GET request.

**Parameters:**
- \`path\` (string): Request path (relative to baseURL)
- \`options.schema\` (Schema, optional): Validation schema
- \`options.headers\` (object, optional): Request-specific headers
- \`options.params\` (object, optional): Query parameters

**Returns:** Promise resolving to the response data

### \`client.post(path: string, options?: RequestOptions)\`

Performs a POST request with the same options as GET, plus:
- \`options.body\` (any): Request body (automatically serialized)

## Examples

### Real-World Example: User Management API

\`\`\`typescript
import { createClient } from 'my-cool-package';
import { z } from 'zod';

// Define schemas
const UserSchema = z.object({
  id: z.number(),
  name: z.string(),
  email: z.string().email(),
  role: z.enum(['admin', 'user'])
});

const UsersListSchema = z.array(UserSchema);

// Create client
const api = createClient({
  baseURL: 'https://api.myapp.com',
  headers: {
    'Authorization': \`Bearer \${process.env.API_TOKEN}\`
  }
});

// Fetch all users
async function getUsers() {
  return await api.get('/users', {
    schema: UsersListSchema,
    params: { limit: 100, sort: 'name' }
  });
}

// Create a new user
async function createUser(name: string, email: string) {
  return await api.post('/users', {
    schema: UserSchema,
    body: { name, email, role: 'user' }
  });
}

// Update user
async function updateUser(id: number, updates: Partial<User>) {
  return await api.put(\`/users/\${id}\`, {
    schema: UserSchema,
    body: updates
  });
}
\`\`\`

## Comparison with Alternatives

| Feature | my-cool-package | axios | fetch | ky |
|---------|----------------|-------|-------|-----|
| TypeScript Support | ✅ Built-in | ⚠️ Via types | ⚠️ Via types | ✅ Built-in |
| Runtime Validation | ✅ Yes | ❌ No | ❌ No | ❌ No |
| Auto Retry | ✅ Yes | ⚠️ Via plugin | ❌ No | ✅ Yes |
| Bundle Size | 4KB | 14KB | 0KB (native) | 3KB |
| Browser Support | ✅ Modern | ✅ All | ✅ Modern | ✅ Modern |

## Performance

Benchmarks on M1 Mac, Node.js 20:
- Simple GET: ~2ms
- With validation: ~3ms
- Cached request: ~0.1ms

## Browser Compatibility

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Node.js 14+

## Migration Guide

### From Axios

\`\`\`typescript
// Before (axios)
const response = await axios.get('https://api.example.com/users');
const data = response.data;

// After (my-cool-package)
const client = createClient({ baseURL: 'https://api.example.com' });
const data = await client.get('/users');
\`\`\`

### From Fetch

\`\`\`typescript
// Before (fetch)
const response = await fetch('https://api.example.com/users');
const data = await response.json();

// After (my-cool-package)
const client = createClient({ baseURL: 'https://api.example.com' });
const data = await client.get('/users');
\`\`\`

## Contributing

We welcome contributions! Here's how to get started:

### Development Setup

1. Fork and clone the repository
   \`\`\`bash
   git clone https://github.com/yourusername/my-cool-package.git
   cd my-cool-package
   \`\`\`

2. Install dependencies
   \`\`\`bash
   npm install
   \`\`\`

3. Run tests
   \`\`\`bash
   npm test
   \`\`\`

4. Start development mode
   \`\`\`bash
   npm run dev
   \`\`\`

### Pull Request Process

1. Create a feature branch (\`git checkout -b feature/amazing-feature\`)
2. Make your changes and add tests
3. Ensure all tests pass (\`npm test\`)
4. Update documentation if needed
5. Commit your changes (\`git commit -m 'Add amazing feature'\`)
6. Push to your fork (\`git push origin feature/amazing-feature\`)
7. Open a Pull Request

### Code Style

We use ESLint and Prettier. Run \`npm run lint\` to check your code.

## FAQ

**Q: Can I use this in a browser?**
A: Yes! It works in all modern browsers.

**Q: Does it support authentication?**
A: Yes, through headers and interceptors.

**Q: Is it production-ready?**
A: Yes, used by 500+ companies in production.

## Changelog

See [CHANGELOG.md](./CHANGELOG.md) for version history.

## License

Distributed under the MIT License. See [LICENSE](./LICENSE) for more information.

## Support

- 📧 Email: support@example.com
- 💬 Discord: [Join our community](https://discord.gg/example)
- 🐛 Issues: [GitHub Issues](https://github.com/user/repo/issues)
- 📖 Docs: [Full Documentation](https://docs.example.com)

## Acknowledgments

- Inspired by [axios](https://github.com/axios/axios) and [ky](https://github.com/sindresorhus/ky)
- Built with [Zod](https://github.com/colinhacks/zod)
- Thanks to all our [contributors](https://github.com/user/repo/graphs/contributors)!
