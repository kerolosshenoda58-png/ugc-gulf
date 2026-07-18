# UGC GULF – Local Development Setup Guide

## Prerequisites

### Required Software
- **Node.js**: 18.x or higher
- **npm**: 9.x or higher (or yarn/pnpm)
- **PostgreSQL**: 15.x or higher
- **Git**: Latest version
- **Docker** (optional, for PostgreSQL)

### Recommended Tools
- **VS Code** with extensions:
  - ESLint
  - Prettier
  - TypeScript Vue Plugin
  - Tailwind CSS IntelliSense
  - REST Client (for API testing)
- **Postman** or **Insomnia** (API testing)
- **DBeaver** or **pgAdmin** (Database GUI)

---

## 1. Initial Setup

### 1.1 Clone the Repository

```bash
git clone https://github.com/kerolosshenoda58-png/ugc-gulf.git
cd ugc-gulf
```

### 1.2 Install Dependencies

```bash
# Using npm
npm install

# Or using yarn
yarn install

# Or using pnpm
pnpm install
```

### 1.3 Install Pre-commit Hooks

```bash
npm run prepare
# Installs husky hooks for linting on commit
```

---

## 2. Database Setup

### Option A: Using Docker (Recommended)

```bash
# Start PostgreSQL and Redis containers
docker-compose up -d

# Verify containers are running
docker-compose ps
```

Expected output:
```
NAME                COMMAND             STATUS
ugc_gulf_db         postgres            Up 2 minutes
ugc_gulf_cache      redis               Up 2 minutes
ugc_gulf_email      mailhog             Up 2 minutes
```

### Option B: Manual Installation

```bash
# macOS (using Homebrew)
brew install postgresql

# Ubuntu/Debian
sudo apt-get install postgresql postgresql-contrib

# Start PostgreSQL
sudo service postgresql start

# Or if using Homebrew on macOS
brew services start postgresql
```

### 2.1 Create Database

```bash
# Using docker-compose (skip if already running)
docker exec ugc_gulf_db psql -U ugcgulf -c "CREATE DATABASE ugc_gulf_dev;"

# Or manually
createdb -U postgres ugc_gulf_dev
```

### 2.2 Setup Environment Variables

```bash
# Copy example .env file
cp .env.example .env.local

# Edit .env.local with your local settings
nano .env.local
```

**Key configurations for local development:**
```env
# Database
DATABASE_URL="postgresql://ugcgulf:dev_password_change_me@localhost:5432/ugc_gulf_dev"
SHADOW_DATABASE_URL="postgresql://ugcgulf:dev_password_change_me@localhost:5432/ugc_gulf_shadow"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-local-dev-secret-key-min-32-chars"

# API
API_URL="http://localhost:3000/api"

# Development
NODE_ENV="development"
```

### 2.3 Run Database Migrations

```bash
# Generate Prisma Client
npx prisma generate

# Run migrations
npx prisma migrate dev --name init

# Seed database (optional - creates sample data)
npx prisma db seed
```

### 2.4 Open Prisma Studio (Optional)

```bash
# View and manage database in GUI
npx prisma studio
```

Browser will open at `http://localhost:5555`

---

## 3. Environment Configuration

### 3.1 Required Environment Variables

Create `.env.local` in the root directory:

```bash
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/ugc_gulf_dev"
SHADOW_DATABASE_URL="postgresql://user:password@localhost:5432/ugc_gulf_shadow"

# NextAuth
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="min-32-character-secret-key-for-dev"

# OAuth (Optional - for social login)
GITHUB_ID="your-github-id"
GITHUB_SECRET="your-github-secret"
GOOGLE_ID="your-google-id"
GOOGLE_SECRET="your-google-secret"

# Stripe (Testing)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY="pk_test_..."
STRIPE_SECRET_KEY="sk_test_..."
STRIPE_WEBHOOK_SECRET="whsec_test_..."

# AWS S3 (for file uploads)
AWS_REGION="us-east-1"
AWS_ACCESS_KEY_ID="your-access-key"
AWS_SECRET_ACCESS_KEY="your-secret-key"
AWS_S3_BUCKET="ugc-gulf-uploads-dev"

# Email Service (SendGrid)
SENDGRID_API_KEY="your-sendgrid-key"
SENDGRID_FROM_EMAIL="dev@ugcgulf.local"

# AI & Automation (Claude)
ANTHROPIC_API_KEY="your-anthropic-key"

# Firebase (Notifications)
NEXT_PUBLIC_FIREBASE_API_KEY="your-firebase-key"
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN="your-project.firebaseapp.com"
NEXT_PUBLIC_FIREBASE_PROJECT_ID="your-project-id"
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET="your-bucket.appspot.com"
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID="your-sender-id"
NEXT_PUBLIC_FIREBASE_APP_ID="your-app-id"

# Monitoring
SENTRY_DSN="your-sentry-dsn"
NEXT_PUBLIC_GA_ID="your-analytics-id"

# Application
APP_ENV="development"
APP_URL="http://localhost:3000"
LOG_LEVEL="debug"
```

---

## 4. Running the Development Server

### 4.1 Start Development Environment

```bash
# Start all services (frontend, backend, database)
npm run dev

# Or start specific services
npm run dev:web      # Next.js frontend only
npm run dev:db       # Database only
npm run dev:docker   # Docker containers only
```

### 4.2 Access the Application

- **Frontend**: http://localhost:3000
- **API**: http://localhost:3000/api
- **Database**: localhost:5432 (PostgreSQL)
- **Database GUI**: http://localhost:5555 (Prisma Studio)
- **Email Testing**: http://localhost:8025 (Mailhog)

---

## 5. Testing

### 5.1 Run Tests

```bash
# Run all tests
npm run test

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm run test -- auth.test.ts
```

### 5.2 Linting & Formatting

```bash
# Check linting errors
npm run lint

# Fix linting errors automatically
npm run lint:fix

# Format code with Prettier
npm run format

# Check formatting
npm run format:check
```

### 5.3 Type Checking

```bash
# Check TypeScript types
npm run type-check

# Watch mode
npm run type-check:watch
```

---

## 6. Common Development Tasks

### 6.1 Database Operations

```bash
# Create a new migration
npx prisma migrate dev --name add_new_field

# View migration status
npx prisma migrate status

# Reset database (WARNING: deletes all data)
npx prisma migrate reset

# Seed database with sample data
npx prisma db seed

# View database in GUI
npx prisma studio
```

### 6.2 API Testing

```bash
# Using REST Client (VS Code extension)
# Create .http file and send requests

GET http://localhost:3000/api/campaigns

###

POST http://localhost:3000/api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

### 6.3 Debugging

```bash
# Start with debugger
node --inspect-brk node_modules/.bin/next dev

# Or use VS Code debugger with .vscode/launch.json
```

**.vscode/launch.json** configuration:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js",
      "type": "node",
      "request": "attach",
      "port": 9229,
      "skipFiles": ["<node_internals>/**"],
      "restart": true
    }
  ]
}
```

---

## 7. Git Workflow

### 7.1 Branch Naming Convention

```
feature/feature-name       # New features
bugfix/bug-name           # Bug fixes
hotfix/issue-name         # Production hotfixes
docs/documentation-name   # Documentation
refactor/refactor-name    # Refactoring
```

### 7.2 Commit Message Convention

```
feat: add campaign creation API
fix: resolve payment processing issue
docs: update API documentation
style: format code with prettier
refactor: simplify campaign logic
test: add campaign tests
chore: update dependencies
```

### 7.3 Pull Request Process

```bash
# 1. Create and switch to feature branch
git checkout -b feature/my-feature

# 2. Make changes and commit
git add .
git commit -m "feat: add my feature"

# 3. Push to remote
git push origin feature/my-feature

# 4. Create Pull Request on GitHub
# - Set base branch to `main`
# - Fill out PR template
# - Request reviews

# 5. Merge after approval
git checkout main
git pull origin main
git merge feature/my-feature
git push origin main
```

---

## 8. Troubleshooting

### Issue: Port 3000 Already in Use

```bash
# Find process using port 3000
lsof -i :3000

# Kill process
kill -9 <PID>

# Or use different port
PORT=3001 npm run dev
```

### Issue: PostgreSQL Connection Refused

```bash
# Check if PostgreSQL is running
psql -U postgres

# Or if using Docker
docker-compose logs ugc_gulf_db

# Restart Docker containers
docker-compose restart ugc_gulf_db
```

### Issue: Module Not Found Error

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Clear Next.js cache
rm -rf .next
npm run dev
```

### Issue: Prisma Migrations Failed

```bash
# Resolve migration conflicts
npx prisma migrate resolve --rolled-back

# Try migrating again
npx prisma migrate deploy
```

### Issue: Environment Variables Not Loading

```bash
# Ensure .env.local exists in root directory
ls -la .env.local

# Restart dev server
npm run dev
```

---

## 9. Performance Optimization

### 9.1 Enable Turbo Cache

```bash
# Use Turbo for faster builds
npm run build

# Force cache invalidation
npm run build -- --force
```

### 9.2 Database Query Optimization

```bash
# Enable query logging in .env.local
DATABASE_LOG_QUERIES="true"

# Monitor slow queries
npx prisma studio  # Check query performance
```

---

## 10. Security Best Practices

### 10.1 Local Development Security

```bash
# Never commit .env.local
echo ".env.local" >> .gitignore

# Use strong NEXTAUTH_SECRET
openssl rand -base64 32  # Generate secure secret

# Keep dependencies updated
npm audit
npm update
```

### 10.2 Database Security

```bash
# Use strong passwords
# Don't use default credentials in production

# Backup database
pg_dump -U ugcgulf -d ugc_gulf_dev > backup.sql

# Restore from backup
psql -U ugcgulf -d ugc_gulf_dev < backup.sql
```

---

## 11. Useful Commands Reference

```bash
# Development
npm run dev                  # Start all services
npm run dev:web            # Start Next.js only
npm run build              # Build for production
npm run start              # Start production server

# Database
npx prisma migrate dev     # Create and run migration
npx prisma studio         # Open database GUI
npx prisma generate       # Generate Prisma Client

# Testing & Quality
npm run test              # Run tests
npm run lint              # Check linting
npm run lint:fix          # Fix linting issues
npm run format            # Format code
npm run type-check        # Check TypeScript

# Clean
npm run clean             # Remove build artifacts
npm run clean:db          # Reset database
```

---

## 12. Resources & Documentation

- **Next.js**: https://nextjs.org/docs
- **Prisma**: https://www.prisma.io/docs
- **TypeScript**: https://www.typescriptlang.org/docs
- **Tailwind CSS**: https://tailwindcss.com/docs
- **PostgreSQL**: https://www.postgresql.org/docs
- **Jest**: https://jestjs.io/docs/getting-started
- **Stripe**: https://stripe.com/docs

---

## 13. Getting Help

### Support Channels
- **GitHub Issues**: Report bugs or feature requests
- **Discussions**: General questions and discussions
- **Slack/Discord**: Real-time team communication (if available)
- **Email**: dev@ugcgulf.com

### Before Creating an Issue
1. Check existing issues for duplicates
2. Search documentation
3. Try the troubleshooting section above
4. Provide detailed reproduction steps

---

**Last Updated**: July 18, 2026  
**Version**: 1.0  
**Status**: Complete
