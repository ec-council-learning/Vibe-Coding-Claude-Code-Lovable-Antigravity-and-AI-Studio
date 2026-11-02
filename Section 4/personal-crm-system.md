# Personal CRM — System Instructions & Brand Data

---

## 1. App Overview

**App Name:** Nexus  
**Tagline:** *Your relationships, organized.*  
**Type:** Full-stack Personal CRM web application  
**Target Audience:** Anyone — professionals, freelancers, solopreneurs, students, and anyone who wants to manage their personal and professional network intentionally.

---

## 2. Core Purpose

Nexus helps users stay on top of the people who matter most in their lives — clients, leads, investors, collaborators, mentors, and friends. It eliminates the "I forgot to follow up" problem by giving users a single, clean place to log contacts, track interactions, and get reminded when a relationship needs attention.

---

## 3. Core Features

### 3.1 Contact Management
- Add contacts with: Name, Role/Title, Company, Email, Phone, LinkedIn, Tags, Category, Notes
- Categories: `Client`, `Lead`, `Investor`, `Partner`, `Mentor`, `Friend`, `Other`
- Tags: user-defined, free-form (e.g. `#warm`, `#follow-up`, `#VIP`)
- Contact strength indicator: `Strong`, `Warm`, `Cold`, `Dormant` — auto-calculated from last interaction date

### 3.2 Interaction Log
- Log every interaction per contact: Call, Email, Meeting, Coffee, Message, LinkedIn, Other
- Each log entry: Date, Type, Duration (optional), Notes, Sentiment (Positive / Neutral / Needs attention)
- Timeline view per contact showing full history

### 3.3 Follow-up Reminders
- Set manual follow-up dates per contact
- AI-suggested follow-up: if no interaction in X days → auto-flag as needing attention
- Dashboard widget: "Who to reach out to today"

### 3.4 Dashboard
- Total contacts count
- Contacts by category (donut chart)
- "Needs attention" list (no interaction in 30+ days)
- Recent activity feed
- Quick-add contact button
- Search bar (global search across all contacts)

### 3.5 Smart Search & Filter
- Search by name, company, tag, category
- Filter by: Category, Contact strength, Last interaction date, Has follow-up pending



---

## 4. Technical Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 14 (App Router) + TypeScript |
| Styling | Tailwind CSS |
| Auth | Google OAuth via Firebase Auth or Supabase Auth |
| Database | Firestore (Firebase) or Supabase PostgreSQL |
| AI | Anthropic Claude API (claude-sonnet-4-20250514) |
| Hosting | Vercel |
| Storage (avatars) | Firebase Storage or Supabase Storage |

---

## 5. Brand Identity

### 5.1 Brand Name & Personality
- **Name:** Nexus
- **Personality:** Calm, intelligent, trustworthy, quietly powerful. Like a very organized friend who never forgets a name.
- **Voice:** Clear, direct, human. Never corporate. Never noisy.

### 5.2 Color Palette

| Token | Value | Usage |
|---|---|---|
| `--color-bg` | `#FAFAF8` | App background (warm off-white) |
| `--color-surface` | `#FFFFFF` | Cards, panels |
| `--color-border` | `#E8E6E1` | Borders, dividers |
| `--color-text-primary` | `#1A1A18` | Headings, primary text |
| `--color-text-secondary` | `#6B6B63` | Labels, metadata |
| `--color-text-muted` | `#A8A89E` | Placeholder, disabled |
| `--color-accent` | `#2D6A4F` | Primary action (deep forest green) |
| `--color-accent-light` | `#EAF4EE` | Accent backgrounds, hover states |
| `--color-accent-hover` | `#245C43` | Button hover |
| `--color-warning` | `#C17B2A` | Needs attention, warnings |
| `--color-warning-light` | `#FDF3E7` | Warning badge background |
| `--color-danger` | `#B84040` | Destructive actions |
| `--color-success` | `#3A7D44` | Confirmations, success |

### 5.3 Typography

| Role | Font | Weight | Size |
|---|---|---|---|
| Display / Logo | `Fraunces` (Google Fonts) | 600 | 28–36px |
| Headings | `Fraunces` | 500 | 20–24px |
| Body | `DM Sans` | 400 | 14–16px |
| Labels / Meta | `DM Sans` | 500 | 12–13px |
| Monospace / IDs | `DM Mono` | 400 | 12–13px |

### 5.4 Spacing & Layout

- Base unit: `4px`
- Card border radius: `12px`
- Button border radius: `8px`
- Input border radius: `8px`
- Avatar border radius: `50%` (circular)
- Max content width: `1200px`
- Sidebar width: `240px`
- Page padding: `24px`

### 5.5 Shadows

```css
--shadow-sm: 0 1px 2px rgba(0,0,0,0.04);
--shadow-md: 0 4px 12px rgba(0,0,0,0.06);
--shadow-lg: 0 8px 24px rgba(0,0,0,0.08);
```

### 5.6 Motion

- Transitions: `150ms ease` for hover, `200ms ease` for modals/drawers
- No heavy animations — subtle, purposeful micro-interactions only
- Page transitions: fade (opacity 0→1, 150ms)

---

## 6. UI Structure

### 6.1 Layout
```
┌─────────────────────────────────────────────┐
│  Sidebar (240px)  │  Main Content Area       │
│                   │                          │
│  Logo: Nexus      │  Page Header             │
│                   │  ─────────────────────   │
│  Navigation:      │  Content                 │
│  • Dashboard      │                          │
│  • Contacts       │                          │
│  • Follow-ups     │                          │
│  • Activity       │                          │
│                   │                          │
│  ─────────────    │                          │
│  User Avatar      │                          │
│  Settings         │                          │
└─────────────────────────────────────────────┘
```

### 6.2 Pages

| Route | Page | Description |
|---|---|---|
| `/` | Dashboard | Overview, needs attention, recent activity |
| `/contacts` | Contacts List | Grid/list of all contacts with search + filter |
| `/contacts/[id]` | Contact Detail | Full profile, interaction log, AI summary |
| `/contacts/new` | Add Contact | Form to create new contact |
| `/follow-ups` | Follow-ups | All pending follow-ups sorted by urgency |
| `/activity` | Activity Feed | All interactions logged, reverse chronological |
| `/settings` | Settings | Profile, preferences, data export |

---

## 7. AI System Prompt (for Claude API calls)

```
You are a relationship intelligence assistant inside Nexus, a personal CRM app. 
Your job is to help users manage their professional and personal relationships with clarity and warmth.

You have access to a user's contact data, interaction logs, and notes. 
Use this context to provide helpful, concise, and human insights.

Guidelines:
- Be concise. No fluff. Respect the user's time.
- Be warm but professional. This is about real human relationships.
- When drafting messages, match the tone of the relationship (formal for clients, casual for friends).
- Never fabricate information. Only use what's provided in the context.
- When summarizing a contact, highlight: who they are, last interaction, any open items, and relationship health.
- When the user asks "what should I say?", draft a short, natural message — not a template.
```

---

## 8. Contact Strength Logic

| Status | Condition | Badge Color |
|---|---|---|
| `Strong` | Interaction in last 14 days | Green |
| `Warm` | Interaction in last 30 days | Blue |
| `Cold` | Interaction in last 60 days | Yellow/Warning |
| `Dormant` | No interaction in 60+ days | Gray |

---

## 9. Data Models

### Contact
```typescript
interface Contact {
  id: string;
  userId: string;
  name: string;
  photoUrl?: string;
  role?: string;
  company?: string;
  email?: string;
  phone?: string;
  linkedin?: string;
  category: 'Client' | 'Lead' | 'Investor' | 'Partner' | 'Mentor' | 'Friend' | 'Other';
  tags: string[];
  notes?: string;
  followUpDate?: Date;
  createdAt: Date;
  updatedAt: Date;
}
```

### Interaction
```typescript
interface Interaction {
  id: string;
  contactId: string;
  userId: string;
  date: Date;
  type: 'Call' | 'Email' | 'Meeting' | 'Coffee' | 'Message' | 'LinkedIn' | 'Other';
  duration?: number; // minutes
  notes?: string;
  sentiment: 'Positive' | 'Neutral' | 'Needs attention';
  createdAt: Date;
}
```

---

## 10. Key UX Principles

1. **Speed first** — Adding a contact or logging an interaction should take under 30 seconds
2. **Zero clutter** — Only show what the user needs right now
3. **Proactive, not reactive** — The app should surface who needs attention before the user has to think about it
4. **Privacy by default** — All data is private, no social features, no public profiles
5. **Mobile-aware** — Responsive design, key actions accessible on mobile

---

## 11. Out of Scope (v1)

- Team/shared CRM features
- Email inbox integration
- Calendar sync
- Mobile native app
- Public contact pages
- Billing / paid tiers

---

*This document serves as the single source of truth for the Nexus Personal CRM app — system instructions, brand data, and technical specification.*
