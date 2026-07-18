# UGC GULF – User Flows & Workflows

## Overview

Complete user journey documentation for all three user types: Creators, Brands, and Admins.

---

## 1. Creator User Flow

### 1.1 Onboarding Flow

```
Start
  ↓
Sign Up (email/password)
  ↓
Complete Profile
  ├─ Display Name
  ├─ Bio
  ├─ Profile Picture
  ├─ Social Media Accounts
  ├─ Experience Level
  └─ Categories/Niches
  ↓
Add Bank Account
  ├─ Bank Name
  ├─ Account Number
  ├─ IBAN
  └─ Verification
  ↓
Upload Portfolio
  ├─ First 3-5 samples
  ├─ Title & Description
  └─ Category
  ↓
Complete Profile (100%)
  ↓
Access Creator Dashboard
```

### 1.2 Discovery & Application Flow

```
Creator Dashboard
  ↓
Browse Campaigns
  ├─ Filter by:
  │  ├─ Budget Range
  │  ├─ Campaign Type
  │  ├─ Brand Category
  │  └─ Deadline
  │
  └─ Search
  ↓
View Campaign Details
  ├─ Campaign Brief
  ├─ Requirements
  ├─ Budget
  ├─ Brand Info
  ├─ Brand Reviews
  └─ Deliverables
  ↓
Decision: Apply? / Save? / Ignore?
  │
  ├─ APPLY
  │  ├─ Write Proposal
  │  ├─ Bid Amount (or accept posted rate)
  │  ├─ Portfolio Samples
  │  ├─ Video Introduction (optional)
  │  └─ Submit
  │  ↓
  │  Application Status: "Pending"
  │
  ├─ SAVE
  │  └─ Added to Saved Campaigns
  │
  └─ IGNORE
     └─ Continue Browsing
```

### 1.3 Campaign Acceptance & Collaboration Flow

```
Application Status: "Pending"
  ↓
Brand Reviews Application
  ↓
Decision: Accept / Reject / Shortlist?
  │
  ├─ ACCEPTED
  │  ├─ Payment goes to Escrow
  │  ├─ Creator gets notification
  │  ├─ Status changes to "Accepted"
  │  └─ Creator Portal Updated
  │     ├─ Campaign Overview
  │     ├─ Deliverables List
  │     ├─ Deadline
  │     ├─ Brand Contact Info
  │     └─ Message Brand
  │  ↓
  │  Create Content
  │  ├─ Review Content Guidelines
  │  ├─ Create/Film UGC
  │  ├─ Edit & Polish
  │  ├─ Prepare Captions & Hashtags
  │  └─ Ready for Submission
  │  ↓
  │  Submit Content
  │  ├─ Upload Media File
  │  ├─ Add Caption
  │  ├─ Add Hashtags
  │  ├─ Add Notes (optional)
  │  └─ Submit
  │  ↓
  │  Brand Reviews Content
  │  ↓
  │  Decision: Approve / Request Revision / Reject?
  │  │
  │  ├─ APPROVED
  │  │  ├─ Creator notified
  │  │  ├─ Payment released from Escrow
  │  │  ├─ Creator receives notification
  │  │  ├─ Earnings added to Wallet
  │  │  └─ Campaign Status: "Completed"
  │  │
  │  ├─ REVISION REQUESTED
  │  │  ├─ Creator receives feedback
  │  │  ├─ Revision deadline set (e.g., 48 hours)
  │  │  ├─ Creator revises & resubmits
  │  │  └─ Loop back to Brand Reviews
  │  │
  │  └─ REJECTED
  │     ├─ Creator receives feedback
  │     ├─ Option to submit different content
  │     ├─ Payment remains in Escrow
  │     └─ Escalate to Support (optional)
  │
  ├─ SHORTLISTED
  │  └─ Status: "Shortlisted" (waiting for final decision)
  │
  └─ REJECTED
     ├─ Creator receives notification
     └─ Reason provided (optional)
```

### 1.4 Earnings & Withdrawal Flow

```
Creator Dashboard → Wallet
  ↓
View Earnings
├─ Available Balance
├─ Pending Balance
├─ Total Lifetime Earnings
└─ Recent Transactions
  ↓
Request Payout (Available Balance > 100 AED)
  ├─ Select Amount
  ├─ Choose Payout Method
  │  ├─ Bank Transfer
  │  └─ Digital Wallet
  ├─ Confirm Bank Account (if bank transfer)
  └─ Submit Request
  ↓
Payout Processing
├─ Status: "Pending" (1-2 days)
├─ Status: "Processing" (2-5 business days)
└─ Status: "Completed"
  ↓
Money Received
├─ Creator notified
└─ Transaction details provided
```

### 1.5 Media Kit Generation Flow

```
Creator Dashboard → Tools
  ↓
Generate Media Kit
  ├─ Title
  ├─ Include Stats (followers, engagement rate)
  ├─ Include Demographics
  ├─ Include Rate Card
  └─ Generate
  ↓
AI Generates Media Kit
├─ Fetches latest stats
├─ Calculates demographics
├─ Formats into PDF
└─ AI enhances presentation
  ↓
Media Kit Generated
├─ Download PDF
├─ Share Link
└─ Set Expiration Date (optional)
```

---

## 2. Brand User Flow

### 2.1 Onboarding Flow

```
Start
  ↓
Sign Up (email/password)
  ↓
Company Profile
  ├─ Company Name
  ├─ Company Logo
  ├─ Website
  ├─ Description
  ├─ Industry
  ├─ Country & City
  └─ Company Size
  ↓
Billing & Payment Information
  ├─ Payment Method
  │  ├─ Credit Card
  │  └─ Bank Account
  ├─ Billing Address
  └─ VAT/Tax ID (if applicable)
  ↓
Add Team Members (optional)
  ├─ Email
  ├─ Role (Admin / Member)
  └─ Permissions
  ↓
Complete Profile
  ↓
Access Brand Dashboard
```

### 2.2 Campaign Creation Flow

```
Brand Dashboard
  ↓
Create New Campaign
  ↓
Campaign Setup (Step 1: Basic Info)
├─ Campaign Title
├─ Campaign Description
├─ Campaign Type (UGC Video / Image / Mixed)
├─ Campaign Category
└─ Next
  ↓
Deliverables Setup (Step 2)
├─ Number of Deliverables
├─ Deliverable Type (Video / Image / Carousel)
├─ Specifications (duration, resolution, etc.)
├─ Content Guidelines
├─ Revision Count (allowed revisions)
└─ Next
  ↓
Budget & Timeline (Step 3)
├─ Total Budget
├─ Per-Creator Budget / Rate
├─ Number of Creators Needed
├─ Applications Deadline
├─ Content Delivery Deadline
├─ Posting Date (optional)
└─ Next
  ↓
Creator Targeting (Step 4)
├─ Min Followers
├─ Max Followers (optional)
├─ Categories/Niches
├─ Countries
├─ Minimum Rating
├─ Verification Required? (Yes/No)
└─ Next
  ↓
Additional Settings (Step 5)
├─ Usage Rights
│  ├─ Single Use
│  ├─ Limited Time
│  └─ Perpetual
├─ Required Hashtags
├─ Banned Hashtags
├─ Languages Required
└─ Review & Save
  ↓
Save as Draft / Publish Campaign
  │
  ├─ DRAFT
  │  └─ Can edit later
  │
  └─ PUBLISH
     ├─ Campaign goes live
     ├─ Creators can apply
     ├─ Email sent to matched creators
     └─ Status: "Active"
```

### 2.3 Creator Discovery & Outreach Flow

```
Brand Dashboard
  ↓
Discover Creators
  ├─ Search
  ├─ Filter by:
  │  ├─ Followers
  │  ├─ Rating
  │  ├─ Category
  │  ├─ Country
  │  └─ Verification
  │
  └─ View Creator Profiles
     ├─ Portfolio
     ├─ Social Stats
     ├─ Reviews
     ├─ Rating
     └─ Contact Options
  ↓
Decision: Invite / Favorite / Skip?
  │
  ├─ INVITE
  │  ├─ Set Offer Price
  │  ├─ Add Personal Message
  │  └─ Send Invitation
  │  ↓
  │  Creator receives invitation
  │  ├─ Creator accepts / declines
  │  └─ Loop to Campaign Acceptance
  │
  ├─ FAVORITE
  │  └─ Add to Saved Creators
  │
  └─ SKIP
     └─ Continue searching
```

### 2.4 Application Review Flow

```
Campaign Active
  ↓
Applications Come In
  ├─ Notification: "New Application"
  └─ Brand Dashboard Updated
  ↓
View Applications
├─ Filter by:
│  ├─ Status (New / Reviewed / Accepted / Rejected)
│  ├─ Creator Rating
│  └─ Bid Price
│
└─ View Each Application
   ├─ Creator Profile
   ├─ Portfolio
   ├─ Proposal Text
   ├─ Video Introduction
   ├─ Bid Price
   ├─ Creator Reviews
   └─ Contact Information
  ↓
Decision: Accept / Reject / Shortlist?
  │
  ├─ ACCEPT
  │  ├─ Escrow funding triggered
  │  ├─ Creator notified
  │  └─ Application Status: "Accepted"
  │
  ├─ SHORTLIST
  │  └─ Application Status: "Shortlisted"
  │
  └─ REJECT
     ├─ Creator notified (optional feedback)
     └─ Application Status: "Rejected"
```

### 2.5 Content Review & Approval Flow

```
Creators Submit Content
  ↓
Brand Dashboard → Submissions
  ├─ Status: "Submitted"
  ├─ Creator Name
  ├─ Content Preview
  ├─ Submission Date
  └─ Deadline
  ↓
Review Content
├─ Watch/View Full Content
├─ Check Against Guidelines
├─ Read Creator Notes
└─ Assess Quality
  ↓
Decision: Approve / Request Revision / Reject?
  │
  ├─ APPROVE
  │  ├─ Add Brand Notes (optional)
  │  ├─ Submission Status: "Approved"
  │  ├─ Payment released (if all approved)
  │  ├─ Creator notified
  │  └─ Can now use content
  │
  ├─ REQUEST REVISION
  │  ├─ Provide Feedback
  │  ├─ Set Revision Deadline (e.g., 48 hours)
  │  ├─ Creator resubmits
  │  └─ Loop back to Review
  │
  └─ REJECT
     ├─ Provide Reason
     ├─ Option to resubmit different content
     ├─ Submission Status: "Rejected"
     └─ Payment held (unless campaign ends)
```

### 2.6 Analytics & Reporting Flow

```
Brand Dashboard → Analytics
  ↓
Campaign Performance
├─ Overview
│  ├─ Total Views
│  ├─ Total Engagement
│  ├─ Avg Engagement Rate
│  ├─ Total Reach
│  └─ ROI %
│
├─ By Submission
│  ├─ Views per Video
│  ├─ Engagement per Video
│  ├─ Top Performer
│  └─ Lowest Performer
│
├─ By Creator
│  ├─ Creator Name
│  ├─ Views Generated
│  ├─ Engagement
│  └─ Earnings Paid
│
└─ Financial Summary
   ├─ Total Budget
   ├─ Total Spent
   ├─ Cost per Submission
   ├─ Cost per View
   └─ ROI Calculation

Download Report (PDF/CSV)
```

### 2.7 Payment & Escrow Flow

```
Campaign Active → Creator Accepted
  ↓
Fund Escrow
├─ Calculate Total Cost (creators × rate)
├─ Add Platform Fees
├─ Select Payment Method
└─ Fund Escrow
  ↓
Escrow Funded
├─ Status: "Held"
├─ Amount locked for campaign
└─ Creator notified
  ↓
Creators Submit & Get Approved
  ↓
Release Payment to Creator
├─ Amount to Release
├─ Submission IDs
└─ Release
  ↓
Payment Released
├─ Transfer to Creator Account
├─ Creator notified
├─ Transaction recorded
└─ Remaining Balance shown
```

---

## 3. Admin User Flow

### 3.1 Dashboard Overview

```
Admin Dashboard
├─ Key Metrics
│  ├─ Total Users (Creators + Brands)
│  ├─ Active Campaigns
│  ├─ Total Revenue
│  ├─ Platform Health Score
│  └─ Disputes Count
│
├─ Recent Activity
│  ├─ New Campaigns
│  ├─ New Users
│  ├─ Flagged Content
│  └─ Payment Issues
│
└─ Quick Actions
   ├─ Review Flagged Content
   ├─ Handle Disputes
   ├─ View Reports
   └─ Manage Users
```

### 3.2 User Management Flow

```
Admin Panel → Users
  ↓
View All Users
├─ Filter by:
│  ├─ User Type (Creator / Brand / Admin)
│  ├─ Status (Active / Suspended / Deleted)
│  ├─ Verification (Verified / Not Verified)
│  ├─ Registration Date
│  └─ Search
│
└─ View User Details
   ├─ Profile Info
   ├─ Account Status
   ├─ Verification Status
   ├─ Disputes / Flags
   ├─ Revenue / Spending
   └─ Actions Available
  ↓
User Management Actions
├─ Verify Account
├─ Suspend Account (with reason)
├─ Ban Account (permanent)
├─ Reset Password
├─ View Activity
└─ Send Message
```

### 3.3 Content Moderation Flow

```
Admin Panel → Moderation
  ↓
Review Flagged Content
├─ Community Flags
├─ Automated Flags (AI detection)
└─ System Reports
  ↓
View Flagged Item
├─ Content Type (Portfolio / Campaign / Submission / Message)
├─ Reason Flagged
├─ Number of Flags
├─ Content Preview
├─ Flagged By (user info)
└─ Timestamp
  ↓
Moderation Decision
├─ APPROVE (remove flag)
├─ REMOVE CONTENT (delete)
├─ WARN USER (send message)
├─ SUSPEND USER (temporary)
└─ BAN USER (permanent)
  ↓
Action Taken
├─ User notified (if applicable)
├─ Content updated
├─ Flag resolved
└─ Logged for records
```

### 3.4 Dispute Resolution Flow

```
Admin Panel → Disputes
  ↓
View Open Disputes
├─ Dispute Type
│  ├─ Payment Dispute
│  ├─ Quality Dispute
│  ├─ Communication Issue
│  └─ Other
│
├─ Status (Open / Under Review / Resolved)
├─ Party 1 (Creator/Brand)
├─ Party 2 (Brand/Creator)
└─ Date Filed
  ↓
Review Dispute Details
├─ Dispute Description
├─ Evidence Provided
│  ├─ Screenshots
│  ├─ Messages
│  ├─ Content
│  └─ Invoices
├─ Previous Communications
└─ Requested Resolution
  ↓
Investigation
├─ Review Campaign Details
├─ Review Submissions
├─ Check Payments
├─ Review Messages
└─ Make Assessment
  ↓
Resolution Decision
├─ FAVOUR CREATOR
│  └─ Issue refund / release payment
├─ FAVOUR BRAND
│  └─ Hold payment / remove content
├─ MEDIATE
│  └─ Suggest compromise
└─ ESCALATE
   └─ Manual review needed
  ↓
Notify Both Parties
├─ Decision
├─ Reasoning
├─ Next Steps
└─ Appeal Process (if applicable)
```

### 3.5 Financial Reporting Flow

```
Admin Panel → Reports
  ↓
Financial Reports
├─ Period Selection (Daily / Weekly / Monthly)
├─ Revenue Breakdown
│  ├─ Commission Revenue
│  ├─ Payment Processing Fees
│  └─ Total Revenue
│
├─ User Activity
│  ├─ New Creators
│  ├─ New Brands
│  ├─ Active Campaigns
│  └─ Total Transactions
│
└─ Export Options
   ├─ Download PDF
   ├─ Download CSV
   └─ Email Report
```

### 3.6 Platform Settings Flow

```
Admin Panel → Settings
  ↓
General Settings
├─ Platform Name
├─ Logo & Branding
├─ Support Email
└─ Support Phone
  ↓
Commission & Fees
├─ Platform Commission %
├─ Payment Processing Fee
├─ Withdrawal Fee (if any)
└─ Minimum Withdrawal Amount
  ↓
Campaign Settings
├─ Min Budget (campaign)
├─ Max Budget (campaign)
├─ Min Deliverables
├─ Max Deliverables
└─ Application Deadline Window
  ↓
Creator Settings
├─ Min Followers
├─ Rating Threshold for Featured
├─ Verification Requirements
└─ Portfolio Requirements
  ↓
Security Settings
├─ 2FA Requirement (Admin)
├─ Password Policy
├─ Rate Limiting
└─ IP Whitelisting (optional)
  ↓
Save Changes
```

---

## State Diagrams

### Campaign State Machine

```
┌─────────────────────────────────────────────────┐
│                  CAMPAIGN STATES                 │
└─────────────────────────────────────────────────┘

Draft → Active → In Review → Completed
  ↓       ↓         ↓           ↓
  └─ Cancelled    Paused    Archived
     (anytime)    (anytime)  (after 30 days)

```

### Application State Machine

```
Applied → Shortlisted → Accepted → Completed
  ↓           ↓            ↓          ↓
  │           │            │       Paid
  │           │            └─────────┘
  │           │
  └───────────┴─────→ Rejected
                        ↓
                    Declined
```

### Submission State Machine

```
Submitted → Under Review → Approved → Completed
              ↓                ↓           ↓
           Revision        Rejected    Paid
           Requested           ↓
              ↓            Declined
           Resubmitted
```

---

## Key User Interactions

### 1. Messaging System

**Creator → Brand**
- Ask questions about campaign
- Negotiate rate
- Provide updates

**Brand → Creator**
- Request clarifications
- Provide feedback
- Share additional resources

### 2. Notifications

**For Creators**
- Campaign invitations
- Application status updates
- Content approval/rejection
- Payment received
- New messages
- Review posted

**For Brands**
- New applications
- Content submissions
- Payment confirmations
- Team member actions
- Support tickets

**For Admins**
- Dispute filed
- User flagged content
- Payment issues
- System alerts
- Report ready

### 3. Search & Discovery

**Creators Search For**
- Campaigns by budget range
- Campaigns by category
- Recent campaigns
- High-paying campaigns
- Brands they trust

**Brands Search For**
- Creators by followers
- Creators by engagement rate
- Creators by category
- High-rated creators
- New creators

**Admins Search For**
- Users by activity
- Content by type
- Transactions by date
- Disputes by status
- Reports by period

---

**Last Updated**: July 18, 2026  
**Version**: 1.0  
**Status**: Complete
