# UGC GULF – Creator Operating System

**UGC GULF** is a decentralized creator economy platform for the Gulf region, combining:
- **UGC GULF**: A professional UGC marketplace connecting creators with brands
- **Spotless Pay**: Secure escrow and payment infrastructure

## 🎯 Product Vision

From marketplace to **Creator Operating System** with:
- AI creator assistant & campaign builder
- Media kit generator & smart contracts
- Auto invoicing & brand/creator CRM
- Referral system, leaderboards, learning academy
- Mobile app, Chrome extension, public API

## 🚀 MVP Roadmap

### Phase 1: Core Marketplace (Weeks 1-8)
- [ ] Database schema & migrations
- [ ] API architecture & authentication
- [ ] Creator portal (profile, portfolio, analytics)
- [ ] Brand portal (campaign creation, creator search)
- [ ] Campaign marketplace & application system
- [ ] Escrow & payment integration (Stripe Connect)

### Phase 2: Enhanced Marketplace (Weeks 9-14)
- [ ] Admin dashboard & moderation
- [ ] AI campaign builder
- [ ] Media kit generator
- [ ] Advanced analytics & reporting
- [ ] Notification system

### Phase 3: Creator OS (Weeks 15-20)
- [ ] Creator CRM
- [ ] Auto invoicing
- [ ] Learning academy
- [ ] Community & leaderboards
- [ ] Referral system

### Phase 4: Scale & Mobile (Weeks 21+)
- [ ] Mobile app (React Native)
- [ ] Chrome extension
- [ ] Public API
- [ ] Regional expansion (UAE, KSA, etc.)

## 🛠 Tech Stack

```
Frontend:      Next.js 14, TypeScript, TailwindCSS, Shadcn/ui
Backend:       Node.js, Express.js (optional), Prisma ORM
Database:      PostgreSQL
Authentication: NextAuth.js, JWT
Payments:      Stripe Connect, Stripe Webhooks
AI:            Claude AI (Anthropic)
Storage:       AWS S3 / Cloudinary
Email:         SendGrid / Mailgun
Notifications: Firebase Cloud Messaging, WebSockets
Deployment:    Vercel (Frontend), Railway/Render (Backend)
CI/CD:         GitHub Actions
Monitoring:    Sentry, LogRocket
```

## 📁 Project Structure

```
ugc-gulf/
├── apps/
│   ├── web/                 # Next.js frontend
│   ├── api/                 # Backend (optional separate service)
│   └── mobile/              # React Native (future)
├── packages/
│   ├── database/            # Prisma schema & migrations
│   ├── types/               # Shared TypeScript types
│   ├── ui/                  # Shadcn/ui components
│   └── hooks/               # Custom React hooks
├── docs/
│   ├── DATABASE.md          # Schema documentation
│   ├── API.md               # API specification
│   ├── USER_FLOWS.md        # User journey documentation
│   ├── SETUP.md             # Local development setup
│   └── DEPLOYMENT.md        # Production deployment
├── .github/
│   ├── workflows/           # GitHub Actions
│   └── project-board/       # Project management
├── docker-compose.yml       # Local PostgreSQL + services
└── .env.example             # Environment variables template
```

## 🔧 Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL 15+
- Docker (optional, for local PostgreSQL)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/kerolosshenoda58-png/ugc-gulf.git
   cd ugc-gulf
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or yarn install
   ```

3. **Setup environment variables**
   ```bash
   cp .env.example .env.local
   # Edit .env.local with your credentials
   ```

4. **Setup database**
   ```bash
   npx prisma migrate dev
   npx prisma generate
   ```

5. **Start development server**
   ```bash
   npm run dev
   ```

The application will be available at `http://localhost:3000`

## 📚 Documentation

- **[Database Schema](./docs/DATABASE.md)** - Complete database design with relationships
- **[API Architecture](./docs/API.md)** - RESTful API specification
- **[User Flows](./docs/USER_FLOWS.md)** - Creator, Brand, and Admin journeys
- **[Setup Guide](./docs/SETUP.md)** - Detailed development setup
- **[Deployment](./docs/DEPLOYMENT.md)** - Production deployment guide

## 🎨 Design & Wireframes

[Figma Design System](https://figma.com/your-project) (to be created)

## 🔐 Core Features

### For Creators
- ✅ Portfolio & profile management
- ✅ Discover & apply for campaigns
- ✅ Track performance & earnings
- ✅ Media kit generation
- ✅ Messaging with brands
- ✅ Secure payments via escrow

### For Brands
- ✅ Create & manage campaigns
- ✅ Discover & filter creators
- ✅ Review submissions
- ✅ Manage budgets & payments
- ✅ Analytics & ROI tracking
- ✅ Team collaboration

### For Admins
- ✅ User management & moderation
- ✅ Campaign oversight
- ✅ Financial reporting
- ✅ Platform analytics
- ✅ Dispute resolution

## 📊 Database Overview

**~75 tables across 8 domains:**
- Authentication & Users (8 tables)
- Profiles & Portfolios (12 tables)
- Campaigns & Applications (15 tables)
- Payments & Escrow (10 tables)
- Analytics & Reporting (12 tables)
- Messaging & Notifications (8 tables)
- AI & Automation (6 tables)
- Admin & Moderation (6 tables)

## 🌍 Deployment

- **Frontend**: Vercel (auto-deploy from main)
- **Backend**: Railway/Render
- **Database**: Managed PostgreSQL
- **Storage**: AWS S3
- **CDN**: Cloudflare

## 📝 License

Proprietary - UGC GULF

## 👥 Contributors

- Keroloss Shenoda (Product & Engineering Lead)

## 📧 Contact

For questions or collaboration inquiries, reach out to the development team.

---

**Last Updated**: July 18, 2026  
**Status**: Foundation Phase - Ready for MVP Development
