# FriendsAndCommunitySpec.md — 5️⃣ 👥 Friends & Community

**Version:** 1.0 · **Date:** March 2026  
**Section:** Settings → Friends & Community  
**Status:** Draft — ready for review  
**Spec type:** Combined (UX + Legal Compliance + Publication Requirements)

---

## Table of Contents

1. [Overview — What is Friends & Community?](#1-overview--what-is-friends--community)
2. [Legal & Publication Requirements](#2-legal--publication-requirements)
3. [5.1 Friends](#31-friends)
4. [5.2 Friend Requests](#32-friend-requests)
5. [5.3 Blog](#33-blog)
6. [5.4 Communities](#34-communities)
7. [5.5 Business Profiles](#35-business-profiles)
8. [Database Schema](#6-database-schema)
9. [Settings Structure (UI Tree)](#7-settings-structure-ui-tree)
10. [Audit Log Events](#8-audit-log-events)
11. [Publication Blockers](#9-publication-blockers)
12. [Changelog](#10-changelog)

---

## 1. Overview — What is Friends & Community?

**Friends & Community** is section 5 of BestMe Settings. It controls how users connect with others, manage their social graph, create and join communities, maintain a personal blog, and interact with business profiles.

### What belongs here (Single Source of Truth)

| Feature | Scope |
|---|---|
| **Friends list** | View friends, remove friends |
| **Friend requests** | Send, accept, decline, cancel, block from request |
| **Blog** | 1 personal blog per user — create, manage settings |
| **Communities** | Create, join, manage, leave communities (unlimited) |
| **Business Profiles** | Follow, interact (comment, rate) business profiles |
| **Subscriptions** | Blogs and communities a user subscribes to |

### What does NOT belong here

| Feature | Where it belongs |
|---|---|
| Who can send friend requests | Privacy & Visibility → Interactions |
| Who can see your friends list | Privacy & Visibility → Content Visibility |
| Block a user | Privacy & Visibility → Safety & Blocked Accounts |
| Notification settings for friend requests | Notifications settings |

---

## 2. Legal & Publication Requirements

### Applicable Laws

| Law | Article | Relevance |
|---|---|---|
| **GDPR** | Art.6(1)(b) | Lawful basis: contract performance (social features user signed up for) |
| **GDPR** | Art.17 | Right to erasure: user can remove blog, leave communities, delete connections |
| **GDPR** | Art.25 | Privacy by Design: community membership lists may be sensitive |
| **DSA** | Art.14 | Illegal content in blogs / communities — notice-and-action required |
| **DSA** | Art.16 | Easy-access reporting mechanism for blog posts and community content |
| **DSA** | Art.27 | Algorithmic recommendations for communities must be explainable |
| **CCPA** | §1798.100 | Users can request deletion of their community posts and blog content |
| **App Store** | §5.1.1 | Disclosure: community membership, blog authorship = user data collection |
| **App Store** | §1.2 | Prohibition of user-generated content (UGC) without moderation capability |
| **Google Play** | User Data Policy | Blog posts, community messages = user-generated content — moderation required |

### Publication Blockers (🔴 = blocks App Store / Google Play release)

| # | Blocker | Law / Policy | Status |
|---|---|---|---|
| 1 | 🔴 **No reporting mechanism for blog posts** | DSA Art.16 · App Store §1.2 | Must be implemented before release |
| 2 | 🔴 **No reporting mechanism for community posts** | DSA Art.16 · App Store §1.2 | Must be implemented before release |
| 3 | 🔴 **No way to leave a community** | GDPR Art.17 (right to erasure / withdrawal) | Must be implemented before release |
| 4 | 🔴 **No way to delete a blog post** | GDPR Art.17 | Must be implemented before release |
| 5 | 🔴 **Community content visible without disclosure** | App Store §5.1.1 | Data collection disclosure required |
| 6 | ⚠️ **Business profile ratings — no moderation** | DSA Art.14 | Implement or disable ratings before release |

---

## 3. §5.1 Friends

### 3.1 What is the Friends list?

The **Friends list** is a mutual connection between two BestMe users. A friendship is established when a friend request is sent and accepted by both parties.

**Privacy note:** Who can see your friends list is controlled in **Privacy & Visibility → Content Visibility → Friends list visibility** (default: Friends).

### 3.2 Friends List — Settings & Actions

**Settings → Friends & Community → Friends**

| Action | Description | Confirmation required? |
|---|---|---|
| **View friends list** | See all current friends | No |
| **Remove friend** | Removes mutual friendship; the other user is not notified | No confirmation modal needed — reversible via re-add |
| **View mutual friends** | Tap a friend → see mutual connections | No |
| **Search in friends** | Filter friends list by name | No |

### 3.3 Database Fields

```sql
-- Table: friendships
CREATE TABLE friendships (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id_1       UUID REFERENCES auth.users(id) ON DELETE CASCADE,  -- alphabetically first user_id
  user_id_2       UUID REFERENCES auth.users(id) ON DELETE CASCADE,  -- alphabetically second user_id
  created_at      TIMESTAMPTZ DEFAULT now(),
  UNIQUE(user_id_1, user_id_2),
  CHECK (user_id_1 < user_id_2)  -- enforce canonical ordering to prevent duplicates
);
```

**Design note:** Friendships are stored as a single row with canonical ordering (user_id_1 < user_id_2) to prevent duplicate entries.

### 3.4 Laws & Compliance

| Aspect | Rule | Law |
|---|---|---|
| Deletion on account deletion | All friendship rows deleted when either user deletes account | GDPR Art.17 |
| Right to remove friend | User can always remove a friend without the other's consent | GDPR Art.7 (withdrawal) |
| Visibility of friends list | Controlled by Privacy & Visibility spec (SSoT: PrivacyVisibilitySpec.md §2.4) | GDPR Art.25 |

---

## 4. §5.2 Friend Requests

### 4.1 Friend Request Flow

```
[User A] → [Send Request] → [Pending] → [User B notified]
                                           ↓
                              [Accept] → Friendship created
                              [Decline] → Request deleted (A not notified)
                              [Block] → A is blocked + request deleted
```

### 4.2 Database Fields

```sql
-- Table: friend_requests
CREATE TABLE friend_requests (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  sender_id       UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  receiver_id     UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  status          TEXT CHECK (status IN ('pending', 'accepted', 'declined', 'cancelled')) DEFAULT 'pending',
  created_at      TIMESTAMPTZ DEFAULT now(),
  updated_at      TIMESTAMPTZ DEFAULT now(),
  UNIQUE(sender_id, receiver_id)
);
```

### 4.3 Rules

| Rule | Detail |
|---|---|
| Only one pending request per pair | UNIQUE constraint on (sender_id, receiver_id) |
| Who can send friend requests | Controlled by Privacy & Visibility spec (default: Everyone) |
| Private account | If User B has private account, the request goes to "pending" (same flow) |
| Decline is silent | User A is not notified when their request is declined |
| Cancel request | Sender may cancel a pending request at any time |
| Re-request after decline | Allowed after 24 hours cooldown |

### 4.4 UX Wireframe

```
┌────────────────────────────────────────┐
│   Friend Requests                      │
│   [Received (3)]  [Sent (1)]           │
│                                        │
│  ┌────────────────────────────────┐    │
│  │ 👤 Anna Koval                  │    │
│  │ 3 mutual friends               │    │
│  │ [Accept]        [Decline]      │    │
│  └────────────────────────────────┘    │
│                                        │
│  ┌────────────────────────────────┐    │
│  │ 👤 Dmitri Petrov               │    │
│  │ 1 mutual friend                │    │
│  │ [Accept]        [Decline]      │    │
│  └────────────────────────────────┘    │
│                                        │
└────────────────────────────────────────┘
```

---

## 5. §5.3 Blog

### 5.1 Blog — Overview

Each BestMe user may create **exactly one personal blog**. A blog is a dedicated space for longer-form posts, articles, and reflections.

| Rule | Value |
|---|---|
| **Maximum blogs per user** | **1** |
| **Subscriptions (other blogs)** | Unlimited |
| **Blog post length** | TBD (design decision) |
| **Media in blog posts** | Photos, videos (storage limits TBD) |
| **Blog visibility default** | Public (everyone can subscribe) |

### 5.2 Blog Settings

**Settings → Friends & Community → Blog**

| Setting | Options | Default | Law |
|---|---|---|---|
| **Blog visibility** | Public / Friends only / Private (only me) | Public | GDPR Art.25 |
| **Who can comment** | Everyone / Subscribers / Friends / No one | Subscribers | DSA Art.14 |
| **Comment moderation** | OFF / Auto-filter / Approve all | OFF | DSA Art.14 |
| **Allow sharing of posts** | ON / OFF | ON | GDPR Art.25 |
| **Show subscriber count** | ON / OFF | ON | — |

### 5.3 Blog — Reporting (DSA Art.16 — 🔴 required)

Every blog post must have a **Report** mechanism:
- **Three-dot menu on blog post → Report**
- Categories: Spam, Harassment, Hate speech, Misinformation, Illegal content, Other
- Reports are processed by BestMe moderation team
- This mechanism is **mandatory for App Store (EU) and Google Play** — absence = rejection

### 5.4 Blog Database Fields

```sql
-- Table: user_blogs
CREATE TABLE user_blogs (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID UNIQUE REFERENCES auth.users(id) ON DELETE CASCADE,  -- UNIQUE = 1 blog per user
  title           TEXT NOT NULL,
  description     TEXT,
  cover_image_url TEXT,
  visibility      TEXT CHECK (visibility IN ('public', 'friends', 'private')) DEFAULT 'public',
  who_can_comment TEXT CHECK (who_can_comment IN ('everyone', 'subscribers', 'friends', 'nobody')) DEFAULT 'subscribers',
  created_at      TIMESTAMPTZ DEFAULT now(),
  updated_at      TIMESTAMPTZ DEFAULT now()
);

-- Table: blog_posts
CREATE TABLE blog_posts (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  blog_id         UUID REFERENCES user_blogs(id) ON DELETE CASCADE,
  author_id       UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  title           TEXT,
  content         TEXT NOT NULL,
  media_urls      JSONB DEFAULT '[]',
  visibility      TEXT CHECK (visibility IN ('public', 'friends', 'private')) DEFAULT 'public',
  published_at    TIMESTAMPTZ,
  created_at      TIMESTAMPTZ DEFAULT now(),
  updated_at      TIMESTAMPTZ DEFAULT now()
);

-- Table: blog_subscriptions
CREATE TABLE blog_subscriptions (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  subscriber_id   UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  blog_id         UUID REFERENCES user_blogs(id) ON DELETE CASCADE,
  created_at      TIMESTAMPTZ DEFAULT now(),
  UNIQUE(subscriber_id, blog_id)
);
```

---

## 6. §5.4 Communities

### 6.1 Communities — Overview

Users may create and join communities on BestMe. Communities are group spaces for shared interests.

| Rule | Value |
|---|---|
| **Communities a user can create** | **Unlimited** |
| **Communities a user can join** | **Unlimited** |
| **Community types** | Public / Private |
| **Community admin roles** | Owner, Admin, Moderator, Member |

### 6.2 Community Settings (for Community Owners/Admins)

**Settings → Friends & Community → Communities → [Community Name] → Settings**

| Setting | Options | Default | Law |
|---|---|---|---|
| **Community visibility** | Public / Private | Public | GDPR Art.25 |
| **Who can join** | Anyone / Invite only | Anyone | — |
| **Who can post** | All members / Admins only | All members | — |
| **Comment moderation** | OFF / Auto-filter / Approve all | OFF | DSA Art.14 |
| **Allow member list visibility** | Everyone / Members only | Members only | GDPR Art.25 |

### 6.3 Community — Reporting (DSA Art.16 — 🔴 required)

Every community post must have a **Report** mechanism. Same categories as blog reporting.

### 6.4 Leave Community

**Settings → Friends & Community → Communities → [Community] → Leave Community**

- User can leave any community at any time
- Their posts may remain (depends on community settings) or be deleted
- Owner cannot leave without transferring ownership first

> 🔴 **GDPR Art.17 obligation:** Users must be able to leave communities and request deletion of their content within communities.

### 6.5 Community Database Fields

```sql
-- Table: communities
CREATE TABLE communities (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  owner_id        UUID REFERENCES auth.users(id),
  name            TEXT NOT NULL,
  description     TEXT,
  cover_image_url TEXT,
  visibility      TEXT CHECK (visibility IN ('public', 'private')) DEFAULT 'public',
  join_policy     TEXT CHECK (join_policy IN ('open', 'invite_only')) DEFAULT 'open',
  who_can_post    TEXT CHECK (who_can_post IN ('all', 'admins')) DEFAULT 'all',
  member_count    INT DEFAULT 0,
  created_at      TIMESTAMPTZ DEFAULT now()
);

-- Table: community_memberships
CREATE TABLE community_memberships (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  community_id    UUID REFERENCES communities(id) ON DELETE CASCADE,
  user_id         UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  role            TEXT CHECK (role IN ('owner', 'admin', 'moderator', 'member')) DEFAULT 'member',
  joined_at       TIMESTAMPTZ DEFAULT now(),
  UNIQUE(community_id, user_id)
);
```

---

## 7. §5.5 Business Profiles

### 7.1 Business Profiles — Overview

Business Profiles are a special profile type on BestMe for brands, organizations, and creators. Regular users can follow business profiles, comment on their content, and leave ratings.

| Rule | Value |
|---|---|
| **User actions on business profiles** | Follow / Unfollow, Comment, Rate |
| **Rating system** | 1–5 stars |
| **Business profile management** | Not in Settings (separate business dashboard) |

### 7.2 User Settings for Business Profiles

**Settings → Friends & Community → Business Profiles**

| Setting | Description |
|---|---|
| **Following list** | View all business profiles the user follows |
| **Unfollow** | Unfollow a business profile |
| **Rating history** | View ratings the user has given (if implemented) |

### 7.3 Ratings — Moderation requirement (⚠️ DSA consideration)

Ratings are a form of user-generated content. If ratings are publicly displayed on business profiles:
- A moderation / reporting mechanism for abusive ratings is required (DSA Art.14)
- Fake rating manipulation must be technically mitigated

> ⚠️ **Decide before release:** Either implement rating moderation OR disable public ratings for MVP. Ratings without moderation capability can be grounds for App Store / Google Play rejection.

---

## 8. Database Schema — Summary Table

| Table | Key field | Notes |
|---|---|---|
| `friendships` | user_id_1, user_id_2 | Canonical ordering: user_id_1 < user_id_2 |
| `friend_requests` | sender_id, receiver_id | Status: pending/accepted/declined/cancelled |
| `user_blogs` | user_id (UNIQUE) | Max 1 blog per user |
| `blog_posts` | blog_id, author_id | Visibility per post |
| `blog_subscriptions` | subscriber_id, blog_id | |
| `communities` | owner_id | Visibility: public/private |
| `community_memberships` | community_id, user_id | Role: owner/admin/moderator/member |

---

## 9. Settings Structure (UI Tree)

```
Settings
└── 5️⃣ Friends & Community
    ├── Friends
    │   ├── [Friends list with search]
    │   └── [each friend] → View profile / Remove friend
    ├── Friend Requests
    │   ├── Received
    │   │   └── [each request] → Accept / Decline / Block
    │   └── Sent
    │       └── [each request] → Cancel
    ├── Blog
    │   ├── My Blog
    │   │   ├── Edit blog (title, description, cover)
    │   │   ├── Blog visibility (Public / Friends / Private)
    │   │   ├── Who can comment
    │   │   ├── Comment moderation
    │   │   └── Allow sharing
    │   └── Subscriptions
    │       └── [list of subscribed blogs] → Unsubscribe
    ├── Communities
    │   ├── My Communities
    │   │   └── [each community] → Settings / Leave
    │   └── Joined Communities
    │       └── [each community] → Leave
    └── Business Profiles
        ├── Following
        │   └── [each business] → Unfollow
        └── [Rating history — if implemented]
```

---

## 10. Audit Log Events

Events to record in the security audit log (existing `user_audit_log` table):

| Event key | Description | Data logged |
|---|---|---|
| `friend_request_sent` | User sent a friend request | sender_id, receiver_id |
| `friend_request_accepted` | Friend request accepted | user_id, friend_id |
| `friend_request_declined` | Friend request declined | — (not logged for privacy) |
| `friendship_removed` | User removed a friend | user_id, removed_friend_id |
| `blog_created` | User created a blog | user_id, blog_id |
| `blog_deleted` | User deleted their blog | user_id, blog_id |
| `blog_post_published` | Blog post published | user_id, post_id |
| `blog_post_deleted` | Blog post deleted | user_id, post_id |
| `community_created` | Community created | user_id, community_id |
| `community_joined` | User joined community | user_id, community_id |
| `community_left` | User left community | user_id, community_id |
| `community_post_reported` | Report submitted on community post | reporter_id, post_id, category |
| `blog_post_reported` | Report submitted on blog post | reporter_id, post_id, category |
| `business_profile_followed` | User followed a business profile | user_id, business_id |
| `business_profile_unfollowed` | User unfollowed a business profile | user_id, business_id |

---

## 11. Publication Blockers

### 🔴 Must fix before release (App Store / Google Play blockers)

| # | Blocker | Law / Policy | Fix |
|---|---|---|---|
| 1 | No reporting mechanism for blog posts | DSA Art.16 · App Store §1.2 | Add Report button to blog posts |
| 2 | No reporting mechanism for community posts | DSA Art.16 · App Store §1.2 | Add Report button to community posts |
| 3 | No "Leave Community" button | GDPR Art.17 | Implement leave flow |
| 4 | No "Delete blog post" button | GDPR Art.17 | Implement delete post flow |
| 5 | No data collection disclosure for community membership | App Store §5.1.1 | Add to Privacy Policy §5 disclosures (already done) |

### ⚠️ Address before release (recommended)

| # | Issue | Recommendation |
|---|---|---|
| 6 | Business profile ratings without moderation | Disable ratings for MVP or implement moderation |
| 7 | Community member list visible to everyone by default | Default to "Members only" |
| 8 | No community content search for moderation | Low priority for MVP |

---

## 12. Changelog

| Version | Date | Changes |
|---|---|---|
| 1.0 | March 2026 | Initial version — Friends, Friend Requests, Blog, Communities, Business Profiles. Laws: GDPR Art.6/17/25, DSA Art.14/16, CCPA, App Store §1.2/5.1.1. |

---

*FriendsAndCommunitySpec.md v1.0 · BestMe · March 2026*  
*Related documents: [SettingsOverview.md](SettingsOverview.md) · [PrivacyVisibilitySpec.md](PrivacyVisibilitySpec.md) · [GDPRArt5SecuritySpec.md](GDPRArt5SecuritySpec.md) · [TermsOfService.md](TermsOfService.md) · [PrivacyPolicy.md](PrivacyPolicy.md)*
