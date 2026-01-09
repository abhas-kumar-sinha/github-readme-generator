# Backend API Service

A production-ready RESTful API service built with modern best practices. This service provides user authentication, data management, and integrates with third-party services. Designed for scalability, security, and maintainability.

## 🎯 Overview

This is a comprehensive backend API that handles:
- **User Management**: Registration, authentication, profile management
- **Data Operations**: CRUD operations with validation and authorization
- **File Uploads**: Secure file handling with S3 storage
- **Real-time Updates**: WebSocket support for live data
- **Background Jobs**: Queue-based task processing
- **Monitoring**: Health checks, metrics, and logging

**Live API**: https://api.example.com  
**Documentation**: https://api.example.com/docs  
**Status Page**: https://status.example.com

## 🏗 Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Client    │────▶│  API Server  │────▶│  Database   │
│  (React)    │     │  (Node.js)   │     │ (Postgres)  │
└─────────────┘     └──────────────┘     └─────────────┘
                            │
                            ├────▶ Redis Cache
                            ├────▶ S3 Storage
                            └────▶ Queue (Bull)
```

## 🛠 Tech Stack

### Core
- **Runtime**: Node.js 20 LTS
- **Framework**: Express.js 4.18 / NestJS 10
- **Language**: TypeScript 5.0

### Database & Caching
- **Primary Database**: PostgreSQL 15
- **ORM**: Prisma / TypeORM
- **Caching**: Redis 7
- **Search**: Elasticsearch (optional)

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **Process Manager**: PM2
- **Reverse Proxy**: Nginx
- **Cloud**: AWS / GCP / DigitalOcean

### Development
- **Testing**: Jest, Supertest
- **Linting**: ESLint, Prettier
- **CI/CD**: GitHub Actions
- **API Docs**: Swagger/OpenAPI

## 📋 Prerequisites

Before you begin, ensure you have:

- **Node.js**: v20.0.0 or higher ([Download](https://nodejs.org/))
- **Docker**: v24.0+ and Docker Compose v2.20+ ([Install](https://docs.docker.com/get-docker/))
- **PostgreSQL**: v15+ (or use Docker)
- **Redis**: v7+ (or use Docker)

Optional:
- **Make**: For convenience commands
- **AWS CLI**: If deploying to AWS

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/yourorg/api-service.git
cd api-service
```

### 2. Environment Configuration

Copy the example environment file and configure it:

```bash
cp .env.example .env
```

Edit `.env` with your settings (see [Environment Variables](#environment-variables) section).

### 3. Start Dependencies with Docker

```bash
# Start PostgreSQL and Redis
docker-compose up -d postgres redis

# Verify services are running
docker-compose ps
```

### 4. Install Dependencies

```bash
npm install
```

### 5. Database Setup

```bash
# Run migrations
npm run migrate

# Seed database with sample data
npm run seed
```

### 6. Start Development Server

```bash
npm run dev
```

API should now be running at http://localhost:3000

Visit http://localhost:3000/docs for interactive API documentation.

## 🔐 Environment Variables

Create a `.env` file in the root directory:

### Server Configuration
```bash
# Server
NODE_ENV=development
PORT=3000
API_VERSION=v1

# Logging
LOG_LEVEL=info
LOG_FORMAT=json
```

### Database
```bash
# PostgreSQL
DATABASE_URL=postgresql://user:password@localhost:5432/mydb?schema=public
DB_HOST=localhost
DB_PORT=5432
DB_NAME=mydb
DB_USER=myuser
DB_PASSWORD=supersecretpassword

# Connection Pool
DB_POOL_MIN=2
DB_POOL_MAX=10
```

### Authentication
```bash
# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRY=7d
REFRESH_TOKEN_EXPIRY=30d

# OAuth (Optional)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GITHUB_CLIENT_ID=your-github-client-id
GITHUB_CLIENT_SECRET=your-github-client-secret
```

### Redis
```bash
REDIS_URL=redis://localhost:6379
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=
REDIS_TLS=false
```

### External Services
```bash
# AWS (for file uploads)
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_S3_BUCKET=your-bucket-name

# Email Service (SendGrid)
SENDGRID_API_KEY=your-sendgrid-key
FROM_EMAIL=noreply@example.com

# Stripe (for payments)
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

### Security
```bash
# Rate Limiting
RATE_LIMIT_WINDOW=15m
RATE_LIMIT_MAX_REQUESTS=100

# CORS
CORS_ORIGIN=http://localhost:3001,https://app.example.com
```

## 📁 Project Structure

```
api-service/
├── src/
│   ├── controllers/       # Request handlers
│   ├── services/          # Business logic
│   ├── models/            # Database models
│   ├── routes/            # API routes
│   ├── middleware/        # Custom middleware
│   ├── utils/             # Utility functions
│   ├── config/            # Configuration files
│   ├── types/             # TypeScript types
│   └── app.ts             # Express app setup
├── tests/
│   ├── unit/              # Unit tests
│   ├── integration/       # Integration tests
│   └── e2e/               # End-to-end tests
├── prisma/
│   ├── schema.prisma      # Database schema
│   ├── migrations/        # Migration files
│   └── seeds/             # Seed data
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── docs/                  # Additional documentation
├── scripts/               # Utility scripts
├── .env.example
├── package.json
└── tsconfig.json
```

## 🌐 API Endpoints

### Authentication

| Method | Endpoint              | Description                    | Auth Required |
|:-------|:---------------------|:-------------------------------|:--------------|
| POST   | `/api/v1/auth/register` | Register new user            | No            |
| POST   | `/api/v1/auth/login`    | User login                   | No            |
| POST   | `/api/v1/auth/logout`   | User logout                  | Yes           |
| POST   | `/api/v1/auth/refresh`  | Refresh access token         | No            |
| POST   | `/api/v1/auth/forgot-password` | Request password reset | No    |
| POST   | `/api/v1/auth/reset-password` | Reset password       | No            |

### Users

| Method | Endpoint              | Description                    | Auth Required |
|:-------|:---------------------|:-------------------------------|:--------------|
| GET    | `/api/v1/users`        | List all users (paginated)   | Yes (Admin)   |
| GET    | `/api/v1/users/:id`    | Get user by ID               | Yes           |
| PUT    | `/api/v1/users/:id`    | Update user profile          | Yes (Owner)   |
| DELETE | `/api/v1/users/:id`    | Delete user account          | Yes (Owner)   |
| GET    | `/api/v1/users/me`     | Get current user profile     | Yes           |

### Posts

| Method | Endpoint              | Description                    | Auth Required |
|:-------|:---------------------|:-------------------------------|:--------------|
| GET    | `/api/v1/posts`        | List all posts               | No            |
| GET    | `/api/v1/posts/:id`    | Get post by ID               | No            |
| POST   | `/api/v1/posts`        | Create new post              | Yes           |
| PUT    | `/api/v1/posts/:id`    | Update post                  | Yes (Owner)   |
| DELETE | `/api/v1/posts/:id`    | Delete post                  | Yes (Owner)   |
| POST   | `/api/v1/posts/:id/like` | Like a post                | Yes           |

### Files

| Method | Endpoint              | Description                    | Auth Required |
|:-------|:---------------------|:-------------------------------|:--------------|
| POST   | `/api/v1/files/upload` | Upload file to S3            | Yes           |
| GET    | `/api/v1/files/:id`    | Get file metadata            | Yes           |
| DELETE | `/api/v1/files/:id`    | Delete file                  | Yes (Owner)   |

### Health & Monitoring

| Method | Endpoint          | Description                    | Auth Required |
|:-------|:-----------------|:-------------------------------|:--------------|
| GET    | `/health`         | Basic health check           | No            |
| GET    | `/health/ready`   | Readiness probe              | No            |
| GET    | `/health/live`    | Liveness probe               | No            |
| GET    | `/metrics`        | Prometheus metrics           | No            |

## 🔍 Example Requests

### Register a New User

```bash
curl -X POST http://localhost:3000/api/v1/auth/register \\
  -H "Content-Type: application/json" \\
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "name": "John Doe"
  }'
```

Response:
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "user_abc123",
      "email": "user@example.com",
      "name": "John Doe"
    },
    "tokens": {
      "accessToken": "eyJhbGciOiJIUzI1NiIs...",
      "refreshToken": "eyJhbGciOiJIUzI1NiIs..."
    }
  }
}
```

### Login

```bash
curl -X POST http://localhost:3000/api/v1/auth/login \\
  -H "Content-Type: application/json" \\
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!"
  }'
```

### Create a Post (Authenticated)

```bash
curl -X POST http://localhost:3000/api/v1/posts \\
  -H "Content-Type: application/json" \\
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \\
  -d '{
    "title": "My First Post",
    "content": "This is the content of my post",
    "tags": ["tutorial", "api"]
  }'
```

### Get Posts with Pagination

```bash
curl -X GET "http://localhost:3000/api/v1/posts?page=1&limit=10&sort=createdAt:desc"
```

## 🧪 Testing

### Run All Tests

```bash
npm test
```

### Run Specific Test Suites

```bash
# Unit tests only
npm run test:unit

# Integration tests only
npm run test:integration

# E2E tests only
npm run test:e2e

# With coverage
npm run test:coverage
```

### Watch Mode (Development)

```bash
npm run test:watch
```

### Test Example

```typescript
describe('POST /api/v1/auth/register', () => {
  it('should create a new user successfully', async () => {
    const response = await request(app)
      .post('/api/v1/auth/register')
      .send({
        email: 'test@example.com',
        password: 'SecurePass123!',
        name: 'Test User'
      });

    expect(response.status).toBe(201);
    expect(response.body.data.user.email).toBe('test@example.com');
    expect(response.body.data.tokens).toHaveProperty('accessToken');
  });
});
```

## 🐳 Docker Deployment

### Build and Run with Docker Compose

```bash
# Build and start all services
docker-compose up -d

# View logs
docker-compose logs -f api

# Stop all services
docker-compose down

# Rebuild after changes
docker-compose up -d --build
```

### Production Docker Build

```bash
# Build production image
docker build -t myapi:latest -f docker/Dockerfile .

# Run production container
docker run -d \\
  --name myapi \\
  -p 3000:3000 \\
  --env-file .env.production \\
  myapi:latest
```

## 🚀 Deployment

### AWS Elastic Beanstalk

```bash
# Initialize EB
eb init -p node.js-20 my-api

# Create environment
eb create production

# Deploy
eb deploy
```

### DigitalOcean App Platform

1. Connect your GitHub repository
2. Configure environment variables
3. Set build command: `npm run build`
4. Set run command: `npm start`

### Heroku

```bash
# Create app
heroku create myapi

# Add PostgreSQL addon
heroku addons:create heroku-postgresql:hobby-dev

# Deploy
git push heroku main

# Run migrations
heroku run npm run migrate
```

### VPS (Ubuntu 22.04)

```bash
# Install dependencies
sudo apt update
sudo apt install -y nodejs npm postgresql redis nginx

# Setup app
cd /var/www/myapi
npm install
npm run build

# Setup PM2
pm2 start dist/index.js --name myapi
pm2 startup
pm2 save

# Configure Nginx reverse proxy
sudo nano /etc/nginx/sites-available/myapi
```

## 📊 Monitoring & Logging

### Health Checks

```bash
# Basic health
curl http://localhost:3000/health

# Database connectivity
curl http://localhost:3000/health/ready

# Liveness probe
curl http://localhost:3000/health/live
```

### Logs

```bash
# Development logs
npm run dev

# Production logs with PM2
pm2 logs myapi

# Docker logs
docker-compose logs -f api
```

### Metrics

Access Prometheus metrics at: http://localhost:3000/metrics

## 🔒 Security

### Implemented Security Measures

- ✅ JWT-based authentication
- ✅ Password hashing with bcrypt
- ✅ Rate limiting (100 requests per 15 minutes)
- ✅ Helmet.js for security headers
- ✅ CORS configuration
- ✅ SQL injection prevention (ORM)
- ✅ XSS protection
- ✅ CSRF tokens
- ✅ Input validation with Joi/Zod
- ✅ File upload restrictions

### Security Best Practices

1. **Never commit `.env` files**
2. **Rotate secrets regularly**
3. **Use HTTPS in production**
4. **Enable 2FA for admin accounts**
5. **Regular dependency audits**: `npm audit`

## 🛠 Development Commands

```bash
# Development
npm run dev              # Start dev server with hot reload
npm run dev:debug        # Start with Node debugger

# Building
npm run build            # Compile TypeScript to JavaScript
npm run build:watch      # Watch mode

# Database
npm run migrate          # Run migrations
npm run migrate:rollback # Rollback last migration
npm run seed             # Seed database

# Code Quality
npm run lint             # Run ESLint
npm run lint:fix         # Fix linting issues
npm run format           # Format code with Prettier
npm run type-check       # TypeScript type checking

# Testing
npm test                 # Run all tests
npm run test:watch       # Watch mode
npm run test:coverage    # Generate coverage report

# Production
npm start                # Start production server
```

## 📚 Additional Documentation

- [API Documentation](./docs/API.md)
- [Database Schema](./docs/DATABASE.md)
- [Authentication Flow](./docs/AUTH.md)
- [Deployment Guide](./docs/DEPLOYMENT.md)
- [Troubleshooting](./docs/TROUBLESHOOTING.md)

## 🤝 Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md)

## 📄 License

MIT License - see [LICENSE](./LICENSE)

## 👥 Team

- **Tech Lead**: @username
- **Backend**: @developer1, @developer2
- **DevOps**: @devops1

## 📞 Support

- 📧 Email: dev-support@example.com
- 💬 Slack: #api-support
- 🐛 Issues: [GitHub Issues](https://github.com/org/repo/issues)
