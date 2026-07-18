# UGC GULF – API Architecture & Specification

## Overview

RESTful API for UGC GULF Creator Operating System. Supports creator portfolios, campaign management, applications, escrow payments, and AI-powered features.

**Base URL**: `https://api.ugcgulf.com/v1`

**Authentication**: JWT Bearer Token (NextAuth.js)

---

## 1. Authentication Endpoints

### 1.1 User Registration

```
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123",
  "userType": "creator" | "brand" | "admin",
  "firstName": "John",
  "lastName": "Doe",
  "phoneNumber": "+971501234567"
}

Response: 201 Created
{
  "id": "uuid",
  "email": "user@example.com",
  "userType": "creator",
  "accessToken": "jwt_token",
  "refreshToken": "jwt_token",
  "createdAt": "2026-07-18T00:00:00Z"
}
```

### 1.2 User Login

```
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securePassword123"
}

Response: 200 OK
{
  "id": "uuid",
  "email": "user@example.com",
  "userType": "creator",
  "accessToken": "jwt_token",
  "refreshToken": "jwt_token",
  "expiresIn": 3600
}
```

### 1.3 Refresh Token

```
POST /auth/refresh
Content-Type: application/json

{
  "refreshToken": "jwt_token"
}

Response: 200 OK
{
  "accessToken": "new_jwt_token",
  "expiresIn": 3600
}
```

### 1.4 Logout

```
POST /auth/logout
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "message": "Logged out successfully"
}
```

---

## 2. Creator Profile Endpoints

### 2.1 Get Creator Profile

```
GET /creators/:creatorId
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "id": "uuid",
  "userId": "uuid",
  "displayName": "John Creator",
  "bio": "Professional UGC creator specializing in tech",
  "profileImage": "https://cdn.ugcgulf.com/image.jpg",
  "website": "https://johncreator.com",
  "country": "UAE",
  "city": "Dubai",
  "experienceLevel": "advanced",
  "isVerified": true,
  "totalFollowers": 150000,
  "totalEarnings": 25000,
  "responseRate": 0.95,
  "rating": 4.8,
  "totalReviews": 245,
  "socialAccounts": [
    {
      "platform": "instagram",
      "handle": "@johncreator",
      "url": "https://instagram.com/johncreator",
      "followers": 150000,
      "engagementRate": 5.2
    }
  ],
  "portfolio": [
    {
      "id": "uuid",
      "title": "Tech Product Review",
      "media": "https://cdn.ugcgulf.com/video.mp4",
      "type": "video",
      "category": "tech",
      "views": 5000
    }
  ],
  "createdAt": "2026-01-01T00:00:00Z",
  "updatedAt": "2026-07-18T00:00:00Z"
}
```

### 2.2 Update Creator Profile

```
PATCH /creators/:creatorId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "displayName": "John Creator",
  "bio": "Updated bio",
  "website": "https://newwebsite.com",
  "experienceLevel": "expert"
}

Response: 200 OK
{
  "id": "uuid",
  "displayName": "John Creator",
  "bio": "Updated bio",
  ...
}
```

### 2.3 Get Creator Portfolio

```
GET /creators/:creatorId/portfolio?page=1&limit=12
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "items": [
    {
      "id": "uuid",
      "title": "Product Review",
      "media": "https://cdn.ugcgulf.com/video.mp4",
      "type": "video",
      "category": "tech",
      "views": 5000,
      "likes": 250
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 12,
    "total": 45,
    "totalPages": 4
  }
}
```

### 2.4 Upload Portfolio Item

```
POST /creators/:creatorId/portfolio
Authorization: Bearer {accessToken}
Content-Type: multipart/form-data

{
  "title": "Product Review",
  "description": "Review of latest smartphone",
  "category": "tech",
  "media": <file>,
  "thumbnail": <file>
}

Response: 201 Created
{
  "id": "uuid",
  "title": "Product Review",
  "media": "https://cdn.ugcgulf.com/video.mp4",
  "status": "processing"
}
```

---

## 3. Brand Profile Endpoints

### 3.1 Get Brand Profile

```
GET /brands/:brandId
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "id": "uuid",
  "userId": "uuid",
  "companyName": "Tech Corp",
  "logo": "https://cdn.ugcgulf.com/logo.png",
  "website": "https://techcorp.com",
  "description": "Leading tech company",
  "industry": "technology",
  "country": "UAE",
  "companySize": "201-1000",
  "isVerified": true,
  "totalCampaigns": 25,
  "totalSpent": 150000,
  "rating": 4.9,
  "totalReviews": 89,
  "teamMembers": [
    {
      "id": "uuid",
      "email": "member@techcorp.com",
      "role": "admin",
      "joinedAt": "2026-01-01T00:00:00Z"
    }
  ],
  "createdAt": "2026-01-01T00:00:00Z"
}
```

### 3.2 Update Brand Profile

```
PATCH /brands/:brandId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "companyName": "Tech Corp",
  "description": "Updated description",
  "website": "https://newwebsite.com"
}

Response: 200 OK
{ ... }
```

### 3.3 Add Team Member

```
POST /brands/:brandId/team-members
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "email": "newmember@techcorp.com",
  "role": "member"
}

Response: 201 Created
{
  "id": "uuid",
  "email": "newmember@techcorp.com",
  "role": "member",
  "status": "pending_invite"
}
```

---

## 4. Campaign Endpoints

### 4.1 Create Campaign

```
POST /campaigns
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "title": "Summer Product Launch Campaign",
  "description": "We're launching our new summer collection...",
  "campaignType": "ugc_video",
  "budget": 5000,
  "minCreatorFollowers": 10000,
  "targetDemographics": {
    "ageRange": "18-35",
    "interests": ["tech", "lifestyle"]
  },
  "deliverables": {
    "count": 5,
    "description": "5 high-quality UGC videos"
  },
  "usageRights": "perpetual",
  "applicationsDeadline": "2026-08-31T23:59:59Z",
  "deliveryDeadline": "2026-09-15T23:59:59Z",
  "contentGuidelines": "Keep it authentic and engaging",
  "requiredHashtags": ["#SummerLaunch", "#NewCollection"]
}

Response: 201 Created
{
  "id": "uuid",
  "title": "Summer Product Launch Campaign",
  "status": "draft",
  "budget": 5000,
  "createdBy": "uuid",
  "createdAt": "2026-07-18T00:00:00Z"
}
```

### 4.2 Get Campaign Details

```
GET /campaigns/:campaignId
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "id": "uuid",
  "title": "Summer Product Launch Campaign",
  "description": "We're launching our new summer collection...",
  "campaignType": "ugc_video",
  "budget": 5000,
  "status": "active",
  "brandId": "uuid",
  "applications": {
    "total": 45,
    "accepted": 5,
    "rejected": 20,
    "pending": 20
  },
  "analytics": {
    "totalViews": 125000,
    "totalEngagement": 8500,
    "avgEngagementRate": 0.068,
    "roiPercentage": 250
  },
  "deliverables": [
    {
      "id": "uuid",
      "title": "Video 1",
      "type": "video",
      "status": "approved",
      "submittedBy": "uuid",
      "submittedAt": "2026-08-01T00:00:00Z"
    }
  ],
  "createdAt": "2026-07-18T00:00:00Z"
}
```

### 4.3 Search & Filter Campaigns

```
GET /campaigns?status=active&budget_min=1000&budget_max=10000&page=1&limit=20
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "items": [
    {
      "id": "uuid",
      "title": "Summer Product Launch Campaign",
      "budget": 5000,
      "status": "active",
      "brandName": "Tech Corp",
      "applicationsCount": 45,
      "createdAt": "2026-07-18T00:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 156,
    "totalPages": 8
  }
}
```

### 4.4 Apply for Campaign

```
POST /campaigns/:campaignId/applications
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "proposalText": "I'm a tech enthusiast with 150k followers...",
  "bidRate": 500,
  "portfolioSamples": ["uuid1", "uuid2"],
  "videoUrl": "https://youtube.com/watch?v=..."
}

Response: 201 Created
{
  "id": "uuid",
  "campaignId": "uuid",
  "creatorId": "uuid",
  "status": "applied",
  "bidRate": 500,
  "appliedAt": "2026-07-18T12:30:00Z"
}
```

### 4.5 Accept Application

```
PATCH /campaigns/:campaignId/applications/:applicationId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "status": "accepted",
  "agreedRate": 500
}

Response: 200 OK
{
  "id": "uuid",
  "status": "accepted",
  "agreedRate": 500,
  "acceptedAt": "2026-07-18T14:00:00Z"
}
```

---

## 5. Submissions Endpoints

### 5.1 Submit Content

```
POST /campaigns/:campaignId/submissions
Authorization: Bearer {accessToken}
Content-Type: multipart/form-data

{
  "deliverableId": "uuid",
  "submissionType": "video",
  "media": <file>,
  "caption": "Check out our amazing product!",
  "hashtags": ["#SummerLaunch", "#NewCollection"],
  "notes": "Authentic and engaging content"
}

Response: 201 Created
{
  "id": "uuid",
  "campaignId": "uuid",
  "deliverableId": "uuid",
  "status": "submitted",
  "mediaUrl": "https://cdn.ugcgulf.com/submission.mp4",
  "submittedAt": "2026-08-05T10:30:00Z"
}
```

### 5.2 Review Submission

```
PATCH /campaigns/:campaignId/submissions/:submissionId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "status": "approved",
  "brandNotes": "Excellent work! Very authentic.",
  "revisionCount": 0
}

Response: 200 OK
{
  "id": "uuid",
  "status": "approved",
  "approvedAt": "2026-08-06T09:00:00Z"
}
```

### 5.3 Request Revision

```
PATCH /campaigns/:campaignId/submissions/:submissionId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "status": "revision_requested",
  "feedback": "Please add more energy to the delivery",
  "revisionDeadline": "2026-08-07T23:59:59Z"
}

Response: 200 OK
{
  "id": "uuid",
  "status": "revision_requested",
  "feedback": "Please add more energy to the delivery"
}
```

---

## 6. Payments & Escrow Endpoints

### 6.1 Fund Campaign Escrow

```
POST /escrow/fund
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "campaignId": "uuid",
  "amount": 5000,
  "paymentMethod": "stripe",
  "stripePaymentMethodId": "pm_1234567890"
}

Response: 201 Created
{
  "id": "uuid",
  "campaignId": "uuid",
  "amount": 5000,
  "status": "pending",
  "createdAt": "2026-07-18T00:00:00Z"
}
```

### 6.2 Get Escrow Status

```
GET /escrow/:escrowId
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "id": "uuid",
  "campaignId": "uuid",
  "totalAmount": 5000,
  "heldAmount": 5000,
  "releasedAmount": 0,
  "status": "held",
  "releaseCondition": "approval",
  "createdAt": "2026-07-18T00:00:00Z"
}
```

### 6.3 Release Payment to Creator

```
POST /escrow/:escrowId/release
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "amount": 1000,
  "reason": "delivery_approved",
  "submissionIds": ["uuid1", "uuid2"]
}

Response: 200 OK
{
  "id": "uuid",
  "amount": 1000,
  "status": "released",
  "releasedAt": "2026-08-06T10:00:00Z",
  "transaction": {
    "id": "uuid",
    "stripeTransferId": "tr_1234567890",
    "status": "completed"
  }
}
```

### 6.4 Get Creator Wallet

```
GET /wallet/creator/:creatorId
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "creatorId": "uuid",
  "availableBalance": 15000,
  "pendingBalance": 5000,
  "totalEarned": 250000,
  "currency": "AED",
  "lastWithdrawal": "2026-07-10T00:00:00Z"
}
```

### 6.5 Request Payout

```
POST /wallet/payouts
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "amount": 5000,
  "payoutMethod": "bank_transfer",
  "bankAccountId": "uuid"
}

Response: 201 Created
{
  "id": "uuid",
  "amount": 5000,
  "status": "pending",
  "payoutMethod": "bank_transfer",
  "requestedAt": "2026-07-18T10:00:00Z"
}
```

---

## 7. AI Endpoints

### 7.1 Generate Campaign Brief

```
POST /ai/generateBrief
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "campaignTitle": "Summer Collection Launch",
  "productDescription": "New eco-friendly clothing line",
  "targetAudience": "18-35 year olds interested in sustainability",
  "brand": "Tech Corp"
}

Response: 200 OK
{
  "brief": "Create authentic UGC content showcasing our new sustainable clothing...",
  "keyPoints": [
    "Emphasize eco-friendly materials",
    "Show genuine lifestyle integration",
    "Target sustainability-conscious audience"
  ],
  "contentIdeas": [
    "Day-in-the-life with sustainable fashion",
    "Product comparison with traditional clothing",
    "Lifestyle integration showcase"
  ]
}
```

### 7.2 Generate Media Kit

```
POST /creators/:creatorId/media-kit/generate
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "title": "Media Kit 2026",
  "includeStats": true,
  "includeDemographics": true,
  "includeRateCard": true
}

Response: 201 Created
{
  "id": "uuid",
  "title": "Media Kit 2026",
  "status": "generating",
  "pdfUrl": "https://cdn.ugcgulf.com/mediakit.pdf",
  "generatedAt": "2026-07-18T12:00:00Z"
}
```

### 7.3 AI Campaign Builder (Conversational)

```
POST /ai/campaignBuilder
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "conversationId": "uuid",
  "message": "I want to launch a campaign for our new tech product",
  "step": "initial_brief"
}

Response: 200 OK
{
  "conversationId": "uuid",
  "response": "Great! Let's build your campaign. Tell me more about your product...",
  "nextQuestions": [
    "What's the product category?",
    "What's your budget?",
    "Who's your target audience?"
  ],
  "progress": 25
}
```

---

## 8. Matching & Discovery Endpoints

### 8.1 Find Creators

```
GET /creators/discover?
  minFollowers=10000&
  maxFollowers=500000&
  categories=tech,lifestyle&
  country=UAE&
  rating_min=4.0&
  verified=true&
  page=1&
  limit=20

Authorization: Bearer {accessToken}

Response: 200 OK
{
  "items": [
    {
      "id": "uuid",
      "displayName": "John Creator",
      "followers": 150000,
      "rating": 4.8,
      "categories": ["tech", "lifestyle"],
      "profileImage": "https://cdn.ugcgulf.com/image.jpg",
      "isVerified": true,
      "responseRate": 0.95
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 567,
    "totalPages": 29
  }
}
```

### 8.2 Invite Creator to Campaign

```
POST /campaigns/:campaignId/invitations
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "creatorIds": ["uuid1", "uuid2", "uuid3"],
  "invitedRate": 500,
  "message": "We'd love to have you collaborate on our campaign!"
}

Response: 201 Created
{
  "invitations": [
    {
      "id": "uuid",
      "creatorId": "uuid",
      "status": "pending",
      "invitedAt": "2026-07-18T10:00:00Z"
    }
  ]
}
```

---

## 9. Analytics Endpoints

### 9.1 Creator Dashboard Analytics

```
GET /creators/:creatorId/analytics?period=month&startDate=2026-06-18&endDate=2026-07-18
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "period": "2026-06-18 to 2026-07-18",
  "profileMetrics": {
    "profileViews": 5000,
    "impressions": 125000
  },
  "engagementMetrics": {
    "campaignApplications": 45,
    "acceptedApplications": 5,
    "totalEarnings": 5000
  },
  "topPerformingContent": [
    {
      "id": "uuid",
      "title": "Product Review",
      "views": 25000,
      "engagement": 2500,
      "engagementRate": 0.10
    }
  ],
  "chartData": {
    "dailyViews": [...],
    "dailyEarnings": [...]
  }
}
```

### 9.2 Campaign Analytics

```
GET /campaigns/:campaignId/analytics
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "campaignId": "uuid",
  "totalViews": 500000,
  "totalEngagement": 35000,
  "avgEngagementRate": 0.070,
  "conversions": 2500,
  "conversionRate": 0.005,
  "revenueGenerated": 25000,
  "roiPercentage": 400,
  "topPerformingSubmissions": [
    {
      "id": "uuid",
      "creatorName": "John Creator",
      "views": 125000,
      "engagement": 12000
    }
  ],
  "submissions": {
    "total": 25,
    "approved": 23,
    "rejected": 2,
    "pending": 0
  }
}
```

---

## 10. Messaging Endpoints

### 10.1 Send Message

```
POST /messages
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "recipientId": "uuid",
  "content": "Hi! I'm interested in your campaign",
  "messageType": "text",
  "campaignId": "uuid"
}

Response: 201 Created
{
  "id": "uuid",
  "conversationId": "uuid",
  "content": "Hi! I'm interested in your campaign",
  "sender": "uuid",
  "recipient": "uuid",
  "createdAt": "2026-07-18T12:30:00Z"
}
```

### 10.2 Get Conversations

```
GET /conversations?page=1&limit=20
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "items": [
    {
      "id": "uuid",
      "participant": {
        "id": "uuid",
        "name": "John Creator",
        "avatar": "https://cdn.ugcgulf.com/avatar.jpg"
      },
      "lastMessage": "Sounds great! When do you need the content?",
      "lastMessageAt": "2026-07-18T15:30:00Z",
      "unreadCount": 2,
      "campaignId": "uuid"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 15
  }
}
```

---

## 11. Notifications Endpoints

### 11.1 Get Notifications

```
GET /notifications?page=1&limit=20&unreadOnly=false
Authorization: Bearer {accessToken}

Response: 200 OK
{
  "items": [
    {
      "id": "uuid",
      "type": "campaign_invitation",
      "title": "New Campaign Invitation",
      "message": "You've been invited to 'Summer Collection Launch'",
      "isRead": false,
      "actionUrl": "/campaigns/uuid",
      "createdAt": "2026-07-18T14:00:00Z"
    }
  ],
  "unreadCount": 5
}
```

### 11.2 Mark as Read

```
PATCH /notifications/:notificationId
Authorization: Bearer {accessToken}
Content-Type: application/json

{
  "isRead": true
}

Response: 200 OK
{
  "id": "uuid",
  "isRead": true
}
```

---

## Error Handling

### Standard Error Response

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ],
    "timestamp": "2026-07-18T12:00:00Z"
  }
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| INVALID_CREDENTIALS | 401 | Email or password incorrect |
| UNAUTHORIZED | 401 | Missing or invalid token |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| VALIDATION_ERROR | 400 | Input validation failed |
| CONFLICT | 409 | Resource already exists |
| RATE_LIMITED | 429 | Too many requests |
| SERVER_ERROR | 500 | Internal server error |

---

## Rate Limiting

- **Requests**: 1000 per hour per user
- **Headers**:
  - `X-RateLimit-Limit`: Total requests allowed
  - `X-RateLimit-Remaining`: Requests remaining
  - `X-RateLimit-Reset`: Timestamp when limit resets

---

## Pagination

All list endpoints support:
- `page`: Page number (default: 1)
- `limit`: Items per page (default: 20, max: 100)
- `sort`: Sort field (e.g., `createdAt`, `-createdAt` for desc)
- `search`: Search query

Response includes:
```json
{
  "items": [...],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 156,
    "totalPages": 8
  }
}
```

---

## Webhooks (Future Implementation)

### Supported Events
- `campaign.created`
- `campaign.completed`
- `application.accepted`
- `submission.approved`
- `payment.released`
- `escrow.released`

### Webhook Payload
```json
{
  "event": "submission.approved",
  "timestamp": "2026-07-18T12:00:00Z",
  "data": {
    "submissionId": "uuid",
    "campaignId": "uuid",
    "creatorId": "uuid",
    "amount": 500
  }
}
```

---

**Last Updated**: July 18, 2026  
**API Version**: 1.0  
**Status**: Production Ready
