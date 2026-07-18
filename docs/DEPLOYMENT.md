name: Deployment Guide

on: []

---

# UGC GULF – Production Deployment Guide

## Overview

Complete guide for deploying UGC GULF to production environments.

---

## 1. Pre-Deployment Checklist

### Code Quality
- [ ] All tests passing
- [ ] No linting errors
- [ ] TypeScript compilation successful
- [ ] Code review completed
- [ ] Changelog updated

### Security
- [ ] Environment variables configured
- [ ] SSL/TLS certificates valid
- [ ] Security headers configured
- [ ] CORS settings correct
- [ ] Database credentials secured
- [ ] API keys rotated (if necessary)

### Performance
- [ ] Build optimization verified
- [ ] Database indexes optimized
- [ ] CDN configured
- [ ] Caching strategy implemented
- [ ] Load testing completed

### Infrastructure
- [ ] Database backups configured
- [ ] Monitoring/logging setup
- [ ] Error tracking enabled (Sentry)
- [ ] Analytics configured
- [ ] Health checks configured

---

## 2. Environment Configuration

### 2.1 Production Environment Variables

Create `.env.production` with all required variables:

```bash
# Database
DATABASE_URL="postgresql://prod_user:prod_password@db-prod.internal:5432/ugc_gulf_prod"
SHADOW_DATABASE_URL="postgresql://prod_user:prod_password@db-prod.internal:5432/ugc_gulf_shadow"

# NextAuth
NEXTAUTH_URL="https://ugcgulf.com"
NEXTAUTH_SECRET="your-production-secret-key-min-32-chars"

# Stripe (Production)
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY="pk_live_..."
STRIPE_SECRET_KEY="sk_live_..."
STRIPE_WEBHOOK_SECRET="whsec_live_..."

# AWS S3
AWS_REGION="us-east-1"
AWS_ACCESS_KEY_ID="prod-access-key"
AWS_SECRET_ACCESS_KEY="prod-secret-key"
AWS_S3_BUCKET="ugc-gulf-uploads-prod"

# SendGrid
SENDGRID_API_KEY="prod-sendgrid-key"
SENDGRID_FROM_EMAIL="noreply@ugcgulf.com"

# Claude AI
ANTHROPIC_API_KEY="prod-anthropic-key"

# Firebase
NEXT_PUBLIC_FIREBASE_API_KEY="prod-firebase-key"
NEXT_PUBLIC_FIREBASE_PROJECT_ID="ugc-gulf-prod"

# Monitoring
SENTRY_DSN="https://your-sentry-dsn"
NEXT_PUBLIC_GA_ID="prod-ga-id"

# Application
NODE_ENV="production"
APP_ENV="production"
APP_URL="https://ugcgulf.com"
LOG_LEVEL="info"
```

---

## 3. Database Deployment

### 3.1 Pre-Migration Backup

```bash
# Backup production database
pg_dump -h db-prod.internal -U prod_user -d ugc_gulf_prod > backup-$(date +%Y%m%d-%H%M%S).sql

# Verify backup
file backup-*.sql
```

### 3.2 Run Migrations

```bash
# From deployment environment
npx prisma migrate deploy

# Verify migrations ran successfully
npx prisma migrate status
```

### 3.3 Seed Data (if needed)

```bash
# Only for initial deployment
npx prisma db seed
```

---

## 4. Deployment to Vercel

### 4.1 Setup Vercel Project

```bash
# Connect GitHub repository
vercel link

# Set production domain
vercel domains add ugcgulf.com

# Configure environment variables
vercel env add DATABASE_URL
vercel env add NEXTAUTH_SECRET
# ... add all required env vars
```

### 4.2 Deploy to Production

```bash
# Automatic deployment (via GitHub)
# Push to main branch triggers automatic production deployment

# Or manual deployment
vercel --prod

# Verify deployment
vercel inspect --prod
```

### 4.3 Verify Deployment

```bash
# Check application is running
curl https://ugcgulf.com/api/health

# Expected response
{ "status": "ok", "environment": "production" }
```

---

## 5. Database Deployment (Alternative: Railway/Render)

### 5.1 Railway Deployment

```bash
# Login to Railway
railway login

# Create new project
railway init

# Link project
railway link

# Deploy database
railway up

# Check logs
railway logs
```

### 5.2 Render Deployment

```bash
# Create new PostgreSQL database on Render
# Copy connection string to Vercel env vars

# Connect application
vercel env add DATABASE_URL
# Paste Render PostgreSQL connection string
```

---

## 6. Backend API Deployment (if using separate backend)

### 6.1 Deploy to Railway/Render

```bash
# Railway
railway link --service api
railway up

# Render
git push render main
```

### 6.2 Configure API Endpoints

```bash
# Update Vercel environment variable
vercel env add API_URL="https://api-prod.ugcgulf.com"

# Redeploy frontend
vercel --prod
```

---

## 7. SSL/TLS Configuration

### 7.1 Vercel SSL (Automatic)

Vercel automatically configures SSL for production domains.

```bash
# Verify SSL certificate
openssl s_client -connect ugcgulf.com:443 -showcerts
```

### 7.2 Custom Domain SSL

```bash
# If using custom DNS
# Add DNS records
# Vercel will auto-provision SSL certificate
# Typically takes 5-10 minutes
```

---

## 8. Monitoring & Observability

### 8.1 Enable Sentry

```bash
# Configure Sentry project
# Set SENTRY_DSN in environment variables

# Verify Sentry integration
# Send test error:
curl https://ugcgulf.com/api/test-error
```

### 8.2 Setup Logging

```bash
# Configure CloudWatch (AWS)
# Or use Railway/Render built-in logging

# View logs
vercel logs
# or
railway logs
```

### 8.3 Configure Health Checks

```bash
# Setup monitoring service
# Configure endpoint: https://ugcgulf.com/api/health
# Check interval: 5 minutes
# Alert threshold: 2 consecutive failures
```

---

## 9. Performance Optimization

### 9.1 CDN Configuration

```bash
# Cloudflare
# Add DNS records
# Enable caching rules
# Setup WAF rules

# or

# AWS CloudFront
# Create distribution
# Link to Vercel deployment
# Configure cache behaviors
```

### 9.2 Database Optimization

```bash
# Create essential indexes
CREATE INDEX idx_campaigns_brand_id ON campaigns(brand_id);
CREATE INDEX idx_campaigns_status ON campaigns(status);
CREATE INDEX idx_creator_profiles_verified ON creator_profiles(is_verified);
CREATE INDEX idx_transactions_user_ids ON transactions(from_user_id, to_user_id);

# Analyze query performance
EXPLAIN ANALYZE SELECT * FROM campaigns WHERE status = 'active';
```

### 9.3 Image Optimization

```bash
# Configure Cloudinary or AWS S3 for image optimization
# Set up image resizing rules
# Enable WebP format
# Setup CDN distribution
```

---

## 10. Security Hardening

### 10.1 CORS Configuration

```javascript
// In API routes
const corsOptions = {
  origin: ['https://ugcgulf.com', 'https://www.ugcgulf.com'],
  credentials: true,
  methods: ['GET', 'POST', 'PATCH', 'DELETE'],
  allowedHeaders: ['Content-Type', 'Authorization'],
};
```

### 10.2 Security Headers

```bash
# Configure in Vercel next.config.js
async headers() {
  return [
    {
      source: '/:path*',
      headers: [
        { key: 'X-Content-Type-Options', value: 'nosniff' },
        { key: 'X-Frame-Options', value: 'DENY' },
        { key: 'X-XSS-Protection', value: '1; mode=block' },
        { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
        { key: 'Permissions-Policy', value: 'geolocation=(), microphone=(), camera=()' },
      ],
    },
  ];
}
```

### 10.3 Rate Limiting

```bash
# Configure rate limiting
# Max 100 requests per minute per IP
# Max 5 requests per second per user
# Implement in API middleware
```

---

## 11. Backup & Disaster Recovery

### 11.1 Database Backups

```bash
# Automated daily backups (configure in Railway/Render)

# Manual backup
pg_dump -h db-prod.internal -U prod_user -d ugc_gulf_prod | gzip > backup-$(date +%Y%m%d).sql.gz

# Verify backup
gunzip -t backup-*.sql.gz

# Upload to S3
aws s3 cp backup-*.sql.gz s3://ugc-gulf-backups/
```

### 11.2 Recovery Plan

```bash
# If database corruption occurs:
# 1. Restore from latest backup
psql -h db-prod.internal -U prod_user -d ugc_gulf_prod < backup-latest.sql

# 2. Verify data integrity
# 3. Notify users if necessary
# 4. Run health checks
```

---

## 12. Deployment Checklist

Before going live:

- [ ] Database migrations tested in staging
- [ ] All environment variables configured
- [ ] SSL certificate valid
- [ ] Monitoring/logging active
- [ ] Backup system operational
- [ ] Performance baseline established
- [ ] Security audit completed
- [ ] Team notified of deployment
- [ ] Rollback plan prepared
- [ ] Post-deployment tests scheduled

---

## 13. Post-Deployment Verification

### 13.1 Immediate Checks (0-5 minutes)

```bash
# Health check
curl https://ugcgulf.com/api/health

# Database connection
curl https://ugcgulf.com/api/creators/test

# Frontend load
open https://ugcgulf.com

# Error tracking
# Check Sentry for any new errors

# Logs
# Review deployment logs for warnings
```

### 13.2 Smoke Tests (5-30 minutes)

```bash
# Creator registration
# Brand campaign creation
# Application submission
# Payment processing (test transaction)
# Notification sending
# Email delivery
```

### 13.3 Monitoring (30+ minutes)

```bash
# CPU usage
# Memory usage
# Database connections
# API response times
# Error rates
# User activity
```

---

## 14. Rollback Procedure

If issues arise:

```bash
# Option 1: Revert to previous Vercel deployment
vercel rollback

# Option 2: Redeploy previous commit
git revert <commit-hash>
git push origin main

# Option 3: Restore database from backup
pg_restore -h db-prod.internal -U prod_user -d ugc_gulf_prod backup-*.sql

# Notify users
# Post-incident review
```

---

## 15. Communication Template

### Deployment Announcement

```
🚀 UGC GULF Production Deployment

Date: [Date] at [Time] UTC
Environment: Production
Version: [Version]
Changes: [Summary of changes]

Expected Impact: Minimal (< 5 minutes downtime)

Status: [In Progress / Completed]

For issues, contact: support@ugcgulf.com
```

---

## Resources

- **Vercel Docs**: https://vercel.com/docs
- **Prisma Deployment**: https://www.prisma.io/docs/concepts/components/prisma-client/deployment
- **PostgreSQL Backups**: https://www.postgresql.org/docs/current/backup.html
- **Security Best Practices**: https://owasp.org/www-project-top-ten

---

**Last Updated**: July 18, 2026  
**Version**: 1.0  
**Status**: Ready for Production
