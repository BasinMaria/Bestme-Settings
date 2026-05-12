# BestMe — Privacy Policy

**Version:** 1.0 · **Date:** March 2026  
**Language:** English (authoritative) · Russian translation: bestme.app/privacy/ru  
**Legal basis:** GDPR (EU) 2016/679 · DSA 2022/2065 · CCPA/CPRA (California) · PIPEDA (Canada) · Quebec Law 25 · Israel PPL · ePrivacy Directive

> This Privacy Policy explains what personal data BestMe collects, how we use it, who we share it with, and the controls you have over your data — with particular focus on **Privacy & Visibility** settings that directly affect your personal data.

---

## Table of Contents

1. [Who We Are and How to Contact Us](#1-who-we-are-and-how-to-contact-us)
2. [What Data We Collect](#2-what-data-we-collect)
3. [Why We Collect Your Data (Legal Bases)](#3-why-we-collect-your-data-legal-bases)
4. [Privacy & Visibility — How We Control What Others See](#4-privacy--visibility--how-we-control-what-others-see)
   - 4.1 [Account Privacy](#41-account-privacy)
   - 4.2 [Profile Visibility — Which Fields Are Personal Data](#42-profile-visibility--which-fields-are-personal-data)
   - 4.3 [Contact Info Privacy — Strict Protections](#43-contact-info-privacy--strict-protections)
   - 4.4 [Content Visibility](#44-content-visibility)
   - 4.5 [Interactions — Who Can Reach You](#45-interactions--who-can-reach-you)
   - 4.6 [Discoverability and Algorithmic Recommendations](#46-discoverability-and-algorithmic-recommendations)
   - 4.7 [Safety & Blocking — Data Processing in Blocking](#47-safety--blocking--data-processing-in-blocking)
5. [Login & Security — Data We Process for Account Protection](#5-login--security--data-we-process-for-account-protection)
   - 5.1 [Password Data](#51-password-data)
   - 5.2 [Two-Factor Authentication Data](#52-two-factor-authentication-data)
   - 5.3 [Linked Accounts (OAuth Tokens)](#53-linked-accounts-oauth-tokens)
   - 5.4 [Active Sessions Data](#54-active-sessions-data)
   - 5.5 [Login History Data](#55-login-history-data)
6. [Friends & Community — Data We Process for Social Features](#6-friends--community--data-we-process-for-social-features)
7. [Default Privacy Settings — Summary](#7-default-privacy-settings--summary)
8. [How Long We Keep Your Data](#8-how-long-we-keep-your-data)
9. [Who We Share Your Data With](#9-who-we-share-your-data-with)
10. [International Data Transfers](#10-international-data-transfers)
11. [Your Rights as a Data Subject](#11-your-rights-as-a-data-subject)
12. [Cookies and Tracking](#12-cookies-and-tracking)
13. [Children's Privacy (COPPA / GDPR Art.8)](#13-childrens-privacy-coppa--gdpr-art8)
14. [Security of Your Data](#14-security-of-your-data)
15. [Changes to This Policy](#15-changes-to-this-policy)
16. [Contact and Supervisory Authorities](#16-contact-and-supervisory-authorities)

---

## 1. Who We Are and How to Contact Us

**Data Controller:** BestMe  
**DPO (Data Protection Officer):** dpo@bestme.app  
**General support:** support@bestme.app  
**Privacy settings:** Settings → Privacy & Visibility (in-app)

---

## 2. What Data We Collect

### 2.1 Data You Provide Directly

| Data category | Examples | Mandatory? |
|---|---|---|
| **Account credentials** | Email, password (hashed with bcrypt), OAuth tokens | Yes (to create account) |
| **Identity data** | Full name, username, date of birth | Yes |
| **Profile data** | Avatar, cover photo, bio, status, gender, relationship status | Optional |
| **Contact data** | Phone number, location (city), home address, website links | Optional |
| **Health & wellness data** | Interests (wellness categories), personal goals | Optional |
| **Content** | Posts, photos, videos, comments, reactions, messages | Optional (user-generated) |

### 2.2 Data We Collect Automatically

| Data category | Examples | Purpose |
|---|---|---|
| **Usage data** | Pages visited, features used, session duration | Product improvement |
| **Device data** | Device model, OS version, app version | Bug fixing, security |
| **IP address** | Collected at login | Security (login history, geo-location for sessions) |
| **User-Agent string** | Browser/app identifier | Session management (Active Sessions screen) |
| **Login events** | Login/logout timestamp, method (email/Google/Apple), success/failure | Security audit (Login History screen) |

### 2.3 Data from Third Parties

When you log in via Google, Apple, or Facebook, we receive your name, email address, and profile photo from that provider, subject to their privacy policies.

---

## 3. Why We Collect Your Data (Legal Bases)

| Purpose | Legal basis (GDPR) |
|---|---|
| Providing the Service (account, features) | Art.6(1)(b) — contract performance |
| Security (login history, sessions, 2FA) | Art.6(1)(f) — legitimate interest in security |
| Legal compliance (GDPR, DSA, COPPA) | Art.6(1)(c) — legal obligation |
| Algorithmic recommendations (opt-out available) | Art.6(1)(f) — legitimate interest; Art.6(1)(a) — consent where required |
| Analytics and product improvement | Art.6(1)(f) — legitimate interest |
| Storing date of birth (age-gating) | Art.6(1)(c) — COPPA / GDPR Art.8 legal obligation |

---

## 4. Privacy & Visibility — How We Control What Others See

> This section is the core of our privacy promise. It explains, field by field and feature by feature, **exactly what data is collected, who can see it, what the default is, and what law requires it**.

All Privacy & Visibility settings are available in: **Settings → Privacy & Visibility**

### 4.1 Account Privacy

**Path:** Settings → Privacy & Visibility → Account Privacy

**What data is affected:** Account discoverability, search indexing, relationship status.

#### Private Account (`account_private`)

- **Default:** OFF (open profile — standard for 18+ social platforms, confirmed lawful by CNIL and ICO under GDPR Art.25)
- **When ON:** Your profile is only visible to approved followers. Your posts, bio, and profile fields are hidden from non-followers.
- **Who can change it:** You, at any time.
- **Legal basis:** GDPR Art.25 — an open default is permitted for adults; the user has full control.

#### Profile in Search Results (`profile_searchable`)

- **Default:** ON — your profile appears in BestMe's internal search
- **When OFF:** Your profile will not appear in search results within the app
- **Your right:** You may opt out at any time (GDPR Art.17 — right to erasure includes de-indexing)
- **Note:** Changing this setting does not affect your profile page URL — it only affects searchability within BestMe.

#### SEO Indexing (`seo_indexable`)

- **Default:** **OFF — permanently. Cannot be ON by default.**
- **What it means:** Your profile will **not** be indexed by Google, Bing, or other web search engines.
- **GDPR Art.25 requirement:** Setting this to ON by default would constitute a violation of Privacy by Default, carrying fines up to €10 million or 4% of annual global turnover.
- **If you want to opt in:** You may manually enable SEO indexing in Settings → Privacy & Visibility → Account Privacy.

#### Relationship Status Visibility (`relationship_visible`)

- **Default:** Friends only (not Everyone)
- **What it is:** Whether your displayed relationship status ("In a relationship", "Married", etc.) is visible.
- **Note:** Relationship status is optional. You may hide it from everyone (Only me) at any time.

---

### 4.2 Profile Visibility — Which Fields Are Personal Data

**Path:** Settings → Privacy & Visibility → Profile Visibility

Each profile field below is processed as personal data under GDPR and has a default visibility setting:

| Field | Data category | Default visibility | Notes |
|---|---|---|---|
| Full name | Personal data | Everyone | Standard for social apps |
| Avatar (profile photo) | Personal data (biometric if identifiable) | Everyone | Standard for social apps |
| Cover photo | Personal data | Everyone | Standard |
| Bio | Personal data | Everyone | Standard |
| Status | Personal data | Everyone | Short public status |
| **Birthday** | **Special category (GDPR Art.9)** | **Friends — age only** | Full date is sensitive data. **Never publicly visible by default.** |
| Gender | Personal data | Everyone | Standard |
| Interests (wellness) | Personal data | Friends only | User's chosen wellness categories |
| Goals | Personal data | Friends only | User's personal wellness goals |

#### Birthday — Special Protection (GDPR Art.9)

Your **full date of birth** is classified as sensitive personal data under GDPR Art.9 because it can be combined with other data to enable identity fraud or other harms.

- **By default:** Only the **age** (not the full date) is visible, and only to friends.
- **What others see:** "30 years old" — not "Born 15 March 1994"
- **Why:** Full birthdates combined with name and location can be used for identity theft (GDPR Art.9 protection principle).
- **You may:** Restrict birthday visibility further (e.g., "Only me") or display full date to friends if you choose — but the default is age-only.

---

### 4.3 Contact Info Privacy — Strict Protections

**Path:** Settings → Privacy & Visibility → Contact Info Privacy

**Legal basis:** GDPR Art.5 (data minimisation), GDPR Art.9 (sensitive data — address), TCPA (US — phone number)

| Field | Default | Can it ever be "Everyone" default? | Law |
|---|---|---|---|
| **Email address** | **Only me** | **NO — never** | GDPR Art.5 |
| **Phone number** | **Only me** | **NO — never** | GDPR Art.5 · TCPA |
| Location (city/region) | Friends | Only if you change it | GDPR |
| **Home/postal address** | **Only me** | **NO — never** | GDPR Art.9 |
| Personal website link | Everyone | Yes (non-sensitive) | — |
| Blog link | Everyone | Yes (non-sensitive) | — |
| Business link | Everyone | Yes (non-sensitive) | — |

#### Our Guarantee on Contact Information

BestMe **technically enforces** the following as hardcoded defaults that no platform update can change without your action:

1. **Email address** is **always private (Only me)** by default. No other user can ever see your email address unless you explicitly make it visible.
2. **Phone number** is **always private (Only me)** by default. Phone numbers are regulated under TCPA (US) and GDPR Art.5 — distribution without consent is prohibited.
3. **Home/postal address** is **always private (Only me)** by default. An address is classified as location-based sensitive data under GDPR Art.9. It must never be publicly visible.

These three defaults are **legal requirements**, not design choices.

---

### 4.4 Content Visibility

**Path:** Settings → Privacy & Visibility → Content Visibility

**Legal basis:** GDPR Art.25 (Privacy by Default), Quebec Law 25 Art.8

| Content type | Default audience | Legal requirement |
|---|---|---|
| **New posts** | **Friends** | GDPR Art.25 · Quebec L25 Art.8 — default must be restrictive |
| **Media gallery** | **Friends** | GDPR Art.25 |
| Friends list | Friends | Social graph protection |
| Interests / Categories | Everyone | Non-sensitive, public activity |
| Subscribed blogs | Everyone | Public activity |
| Subscribed communities | Everyone | Public activity |
| Discussions | Everyone | Public contributions |
| Activity feed (likes, challenges started) | Everyone | Public activity (social engagement) |
| Likes & reactions | Everyone | Public activity |
| Challenges | Everyone | Public activity |

#### About Activity Feed

Your **activity feed** (`activity_visibility`) shows a log of your public actions: which posts you liked, which challenges you started, which goals you set. This is:
- **Not** your personal reading feed (the content you see in the app) — that is private
- A public log of how you engage with the community
- Default **Everyone** — supports wellness community engagement and social transparency

You may change this to **Friends only** or **Only me** in Settings → Privacy & Visibility → Content Visibility.

#### Quebec Law 25 (Canada — Province of Quebec)

Quebec Law 25 (Art.8) requires that the default audience for user-generated content must be the **most privacy-protective** option, not the most open. BestMe sets new posts to **Friends** (not Everyone) by default, in compliance with this requirement.

---

### 4.5 Interactions — Who Can Reach You

**Path:** Settings → Privacy & Visibility → Interactions

**Legal basis:** DSA Art.14 (user controls over interactions), GDPR Art.25, ePrivacy Directive Art.5(3)

| Interaction type | Default | Law |
|---|---|---|
| **Messages** | Friends only | DSA Art.14 · Israel PPL §2 |
| **Tags** | Friends only + approval required | GDPR Art.25 |
| **Tag approval** | **ON (required)** | GDPR Art.25 — tag = data processing of your image/identity |
| **Comments on your posts** | Friends only | DSA Art.14 |
| Reactions to your posts | Everyone | — |
| **Sharing your posts** | **Friends only** | GDPR Art.25 — sharing = data distribution |
| Friend requests | Everyone | — |
| **Online / activity status** | **ON — Friends only** | ePrivacy Art.5(3) |
| **Last seen** | **Friends only** | GDPR Art.25 — activity metadata |
| Read receipts | ON (bilateral) | — |
| Comment moderation | OFF | — |

#### Tag Approval — Why It's ON by Default

When someone tags you in a post or photo, that tag creates a public association between your identity and that content. Under GDPR Art.25 (Privacy by Default), we require your approval before any tag appears. This means:
- You receive a notification: "User X tagged you in a post"
- You may approve or decline
- The tag is **not visible** until you approve

You may disable tag approval in Settings, but this means all tags appear immediately without your review.

#### Online Status — Legal Requirement

Your "online" status (green dot indicator) is visible only to **Friends**, even when the setting is ON. Making online presence visible to all users without their consent would violate **ePrivacy Directive Art.5(3)**.

#### Data We Process for Interactions

For messaging, tagging, and interactions, we process:
- Message content (stored for delivery; not read by BestMe employees)
- Metadata (timestamp, sender ID, recipient ID)
- Tag associations (approved tags are stored as profile data)

---

### 4.6 Discoverability and Algorithmic Recommendations

**Path:** Settings → Privacy & Visibility → Discoverability

**Legal basis:** GDPR Art.22 (automated decisions), DSA Art.27 (algorithmic transparency), DSA Art.29 (recommender systems), CCPA §1798.121

#### How the Recommendation Algorithm Works

BestMe uses an algorithm to suggest content and profiles to users based on:
- Wellness interests and goals
- Engagement patterns (what content you interact with)
- Community connections (friends of friends)
- Location (optional, if you enable it)

#### Data Used in Recommendations

The following data **may** be used for recommendations (when `recommendations_opt_out = false`):
- Your wellness interests and categories
- Your engagement activity (likes, challenges, goals)
- Your friend connections

The following data is **never** used for recommendations:
- Your email address
- Your phone number
- Your home address
- Your date of birth

#### Your Rights Regarding Recommendations

**1. Opt-out (`recommendations_opt_out`):**
- Default: OFF (you participate in recommendations — this is standard for social/wellness platforms)
- **You may opt out at any time** via Settings → Privacy & Visibility → Discoverability
- When opted out: your profile will not be recommended to other users; your activity will not feed the recommendation engine

**2. Transparency — "Why am I recommended this?" (`show_recommendation_info`):**
- Default: **ON**
- On any recommended content or profile, tap the "?" or "Why am I seeing this?" option
- You will receive a plain-language explanation of the factors used
- **DSA Art.27 requirement:** This transparency feature is mandatory for platforms operating in the EU

**3. No profiling for significant decisions:**
BestMe does not use algorithmic profiling for decisions that produce **legal or similarly significant effects** on users (GDPR Art.22). Recommendations are for content discovery only.

**CCPA / CPRA (California):**
Under CCPA §1798.121, California residents have the right to opt out of the **"sale" or "sharing" of personal information** for cross-context behavioral advertising. BestMe does **not** sell your personal data. The opt-out toggle in Discoverability settings also satisfies CCPA §1798.121 requirements.

---

### 4.7 Safety & Blocking — Data Processing in Blocking

**Path:** Settings → Privacy & Visibility → Safety & Blocked Accounts

#### What Data We Store When You Block a User

When you block a user, we store:
- A record of the block relationship (your user ID + blocked user's ID)
- This record is used to enforce the block across all features

The blocked user is **not notified** that they have been blocked. They see a neutral "profile not found" or "user unavailable" response — this is a privacy protection against harassment (GDPR principle of protection from harm).

#### What Data We Store When You Report a User or Content

When you report:
- Reporter's user ID
- Reported user ID or content ID
- Report category (selected by you)
- Timestamp

Report data is processed by our Trust & Safety team. We do not share report details with the reported user.

**DSA Art.16 obligation:** BestMe maintains a legally required notice-and-action mechanism. Reports involving illegal content are processed within the timeframes required by the DSA.

#### Restrict Feature

A "restricted" user can see your public posts but their comments appear only to themselves. Restriction records are stored similarly to blocks and are not visible to the restricted user.

---

## 5. Login & Security — Data We Process for Account Protection

> This section describes in detail what personal data BestMe processes for Login & Security features, the legal basis for each processing activity, and how long we keep this data.  
> Full technical specification: [GDPRArt5SecuritySpec.md](../03_settings/GDPRArt5SecuritySpec.md).

---

### 5.1 Password Data

| Data element | What we store | Legal basis | Retention |
|---|---|---|---|
| **Password hash** | bcrypt hash of your password — **never the plain-text password** | Art.6(1)(b) — contract / Art.32 — security | Until account deletion |
| **Password history hashes** | Last 5 bcrypt hashes (prevent reuse) | Art.6(1)(f) — legitimate interest (security) | Until account deletion |
| **Password change timestamp** | When the password was last changed | Art.6(1)(f) — legitimate interest (security audit) | Until account deletion |
| **Rate limit log** | Timestamp + IP of failed password-change attempts | Art.6(1)(f) — legitimate interest (brute-force prevention) | 24 hours |

**Why we collect this:** To authenticate you securely and prevent unauthorized account access.  
**Who has access:** Password hashes are stored in the database. Only the bcrypt verification function has access; no human can read your password.  
**Your rights:** You may change your password at any time (Settings → Login & Security → Password). You may not request deletion of the password hash while your account exists, as it is necessary to provide the Service (GDPR Art.17(3)(b)).

---

### 5.2 Two-Factor Authentication Data

**Applicable when 2FA is enabled by the user (optional feature)**

| Data element | What we store | Legal basis | Retention |
|---|---|---|---|
| **TOTP secret key** | Encrypted TOTP seed (used to generate/verify 6-digit codes) | Art.6(1)(b) — contract / Art.32 — security | Until 2FA disabled or account deleted |
| **Backup code hashes** | 10 bcrypt-hashed single-use backup codes | Art.6(1)(b) — contract · Art.15 — right to account recovery | Until regenerated or account deleted |
| **2FA method** | Which method is active: Email Code / Authenticator App | Art.6(1)(b) — contract | Until 2FA disabled or account deleted |
| **2FA attempt log** | Timestamp + IP of failed 2FA attempts (rate limiting) | Art.6(1)(f) — legitimate interest (brute-force prevention) | 24 hours |
| **2FA enabled/disabled timestamp** | Audit trail | Art.6(1)(f) — legitimate interest (security audit) | Until account deletion |

**Why we collect this:** To provide additional account security layers that you choose to enable.  
**Your rights:** You may enable, disable, or change your 2FA method at any time. If you disable 2FA, your TOTP secret and unused backup codes are deleted immediately (GDPR Art.17 — right to erasure).  
**Email OTP:** Email-based OTP codes are generated on demand and not stored after transmission. They expire within 10 minutes.

---

### 5.3 Linked Accounts (OAuth Tokens)

**Applicable when you use Google, Apple, or Facebook login**

| Data element | What we store | Legal basis | Retention |
|---|---|---|---|
| **OAuth provider name** | Which provider: google / apple / facebook | Art.6(1)(b) — contract | Until disconnected or account deleted |
| **OAuth provider user ID** | Unique identifier from the provider (not your email) | Art.6(1)(b) — contract performance | Until disconnected or account deleted |
| **Name from provider** | As provided at login | Art.6(1)(b) — contract (populate your profile) | Until you change it or account deleted |
| **Email from provider** | Used to match/create account | Art.6(1)(b) — contract | Until account deleted |
| **OAuth access token** | Short-lived token for API access (not stored long-term) | Art.6(1)(b) — contract | 1 hour or less |
| **OAuth refresh token** | Stored in OS secure storage (iOS Keychain / Android Keystore) | Art.6(1)(b) — contract | Until disconnected or account deleted |

> ⚠️ **Apple Private Relay email:** When using "Hide My Email" via Sign in with Apple, Apple provides a private relay email (e.g. abc123@privaterelay.appleid.com). We store this relay address as your account email. If you later disable the relay in your Apple account, we cannot contact you at that address. We will not attempt to unilaterally replace Apple relay emails.

**Disconnecting a provider:** You may disconnect any OAuth provider from Settings → Login & Security → Linked Accounts. After disconnection, we delete the OAuth provider's user ID and tokens. If your BestMe account has no password set, you must set a password before disconnecting your only OAuth provider (to prevent account lockout).

**Third-party privacy policies:**
- Google: [policies.google.com/privacy](https://policies.google.com/privacy)
- Apple: [apple.com/legal/privacy](https://www.apple.com/legal/privacy/)
- Facebook: [facebook.com/privacy/policy](https://www.facebook.com/privacy/policy/)

---

### 5.4 Active Sessions Data

| Data element | What we store | Legal basis | Retention |
|---|---|---|---|
| **Session ID (JWT identifier)** | Unique identifier for each active session | Art.6(1)(b) — contract (authentication) | Until session expired or terminated |
| **Refresh token** | Stored in OS secure storage (iOS Keychain / Android Keystore) | Art.6(1)(b) — contract | Until expired (configurable — default 30 days) or terminated |
| **IP address at login** | Used to display approximate location in Active Sessions | Art.6(1)(f) — legitimate interest (security) · Art.15 (right of access) | Until session terminated |
| **Device / User-Agent** | Parsed to display "iPhone, iOS 17" etc. in Active Sessions | Art.6(1)(f) — legitimate interest (security) · Art.15 | Until session terminated |
| **Session start time** | Displayed in Active Sessions list | Art.6(1)(f) | Until session terminated |

**Session termination:** When you terminate a session (remotely or by logging out), the refresh token is immediately invalidated server-side. Even if someone has a copy of the token, it cannot be used after invalidation.

**JWT access tokens:** Short-lived (15 minutes). They are not stored in our database; they are self-contained tokens validated cryptographically. After 15 minutes, a new access token must be obtained via the refresh token.

---

### 5.5 Login History Data

| Data element | What we store | Legal basis | Retention |
|---|---|---|---|
| **Login timestamp** | Exact date/time of login event | Art.6(1)(f) — legitimate interest (security) · Art.15 | **90 days** |
| **Login method** | email / google / apple / facebook | Art.6(1)(f) — security audit | **90 days** |
| **IP address** | Source IP of login | Art.6(1)(f) — security / Art.15 | **90 days** |
| **Geo-location (city/region)** | Derived from IP via geo-lookup service (country/city only — no precise coordinates) | Art.6(1)(f) — security | **90 days** |
| **Device / User-Agent** | Device identification | Art.6(1)(f) — security | **90 days** |
| **Login result** | success / failed / blocked | Art.6(1)(f) — brute-force detection | **90 days** |
| **2FA result** | passed / failed / bypassed-with-backup | Art.6(1)(f) — security audit | **90 days** |

**Automatic deletion:** Login history records older than 90 days are automatically deleted by a scheduled database job (GDPR Art.5(1)(e) — storage limitation). This deletion is automatic and does not require user action.

**Your right of access (GDPR Art.15):** You may view your full login history at any time via Settings → Login & Security → Login History. You may request a data export including login history via Settings → Your Data → Download My Data.

**Geo-IP processing note:** IP-to-location conversion uses a geo-lookup service. The result is approximate (city/region level). The raw IP address is stored for 90 days; no precise GPS coordinates are ever derived from login events.

**Breach notification:** If we detect unauthorized access to your account (e.g., successful login from an unrecognized location), we will notify you via push notification and email. You may also trigger the **Protect Account** flow manually from Login History → "This wasn't me".

---

## 6. Friends & Community — Data We Process for Social Features

When you use Friends, Subscriptions, or Communities features, we process the following personal data.

### 6.1 Friends Data

| Data | Legal Basis | Retention |
|---|---|---|
| Friend connections (user ID pairs) | GDPR Art.6(1)(b) — Contract performance | Until friendship is removed |
| Friend request history (sent / received / declined) | GDPR Art.6(1)(b) | 90 days after resolution |
| Friend recommendations (computed graph) | GDPR Art.6(1)(f) — Legitimate interest | Not stored — computed on-demand |

**Privacy by Design (GDPR Art.25):** Friend request declines are never disclosed to the requester.
Removed friends are not notified. Recommendations can be turned off at any time
(Settings → Privacy & Visibility → Discoverability → Recommendations).

### 6.2 Subscriptions Data

| Data | Legal Basis | Retention |
|---|---|---|
| Blog subscription records | GDPR Art.6(1)(b) | Until unsubscribed |
| Business profile subscription records | GDPR Art.6(1)(b) | Until unsubscribed |
| Ratings and reviews on business profiles | GDPR Art.6(1)(b) | Until deleted by user or removed by moderation |

**DSA Art.16:** Ratings and reviews are user-generated content. We maintain a moderation and reporting mechanism.

### 6.3 Communities Data

| Data | Legal Basis | Retention |
|---|---|---|
| Community membership records | GDPR Art.6(1)(b) | Until user leaves community |
| Community administration records | GDPR Art.6(1)(b) | Until community is deleted |
| Community posts and comments | GDPR Art.6(1)(b) | Until deleted by user or community admin |
| Audit log of community actions | GDPR Art.6(1)(c) — Legal obligation | 90 days |

**Right to Erasure (GDPR Art.17):** You may leave any community at any time. Community administrators may
delete communities. Upon deletion, all content is removed from our servers within **30 days**.

**DSA Compliance (Art.14 / Art.16):** We maintain a notice-and-action mechanism for illegal or harmful content
in communities and blogs. All reports are logged and actioned within our moderation process.

**Algorithmic Recommendations (DSA Art.27):** Friend and community recommendations are generated based on
mutual connections, shared communities, and similar interests. You may opt out at any time
(Settings → Privacy & Visibility → Discoverability → Recommendations).

> **See also:** Terms of Service §5 for your rights regarding Friends & Community features.

## 7. Default Privacy Settings — Summary

This table summarises all default privacy values that BestMe applies at account creation, as required by GDPR Art.25 (Privacy by Default):

| Setting | Variable | Default | Legal requirement |
|---|---|---|---|
| SEO indexing | `seo_indexable` | **OFF** | 🔴 GDPR Art.25 — must be OFF |
| Email visibility | `email_visibility` | **Only me** | 🔴 GDPR Art.5 — must not be public |
| Phone visibility | `phone_visibility` | **Only me** | 🔴 GDPR Art.5 · TCPA — must not be public |
| Address visibility | `address_visibility` | **Only me** | 🔴 GDPR Art.9 — must not be public |
| Birthday display | `birthday_visibility` | **Friends — age only** | 🔴 GDPR Art.9 — full date is sensitive |
| Tag approval | `tag_approval_required` | **ON** | 🔴 GDPR Art.25 |
| Online status audience | `online_status_visible` | **Friends only** | 🔴 ePrivacy Art.5(3) |
| Algorithmic transparency | `show_recommendation_info` | **ON** | 🔴 DSA Art.27 |
| New post audience | `default_post_audience` | **Friends** | ⚖️ GDPR Art.25 · Quebec L25 |
| Media gallery | `gallery_visibility` | **Friends** | ⚖️ GDPR Art.25 |
| Messages | `who_can_message` | **Friends** | ⚖️ DSA Art.14 |
| Comments | `who_can_comment` | **Friends** | ⚖️ DSA Art.14 |
| Tags | `who_can_tag` | **Friends** | ⚖️ GDPR Art.25 |
| Share permission | `share_permission` | **Friends** | ⚖️ GDPR Art.25 |
| Last seen | `last_seen_visible` | **Friends** | ⚖️ GDPR Art.25 |
| Account private | `account_private` | OFF (open) | ✅ GDPR Art.25 — open is lawful for 18+ |
| Recommendations opt-out | `recommendations_opt_out` | OFF (participating) | ✅ GDPR Art.22 opt-out available |

---

## 8. How Long We Keep Your Data

| Data type | Retention period | Legal basis |
|---|---|---|
| Account data | Until account deletion + 30 days (recovery window) | Contract |
| Login history (Login History screen) | **90 days**, then auto-deleted by scheduled job | GDPR Art.5(1)(e) — storage limitation |
| Security audit logs | 1 year | GDPR Art.32 — security obligation |
| Active session records | Until session ends or is terminated | Contract / Security |
| Messages | Until deleted by either party | Contract |
| Reports (Trust & Safety) | Up to 3 years (legal obligation to maintain records) | DSA / Legal obligation |
| Blocked user records | Until you unblock + account deletion | Contract |
| Posts and content | Until you delete them or your account | Contract |

> **Login History auto-deletion:** Login history records are automatically deleted after **90 days** using a scheduled database job (`pg_cron`), in compliance with GDPR Art.5(1)(e) (data should not be kept longer than necessary). You can view your login history for the last 90 days in Settings → Login & Security → Login History.

---

## 9. Who We Share Your Data With

| Recipient | What we share | Why |
|---|---|---|
| **Other BestMe users** | Only what your privacy settings allow (see §4) | Providing the social platform |
| **Supabase** (database/auth infrastructure) | Account data, session data | Service infrastructure |
| **IP geolocation service** (e.g., ip-api.com / MaxMind) | IP address at login | To display location in Login History and Active Sessions |
| **Apple / Google / Facebook** | Authentication tokens (OAuth) | When you choose to log in via these providers |
| **Legal authorities** | As required by court order or law | Legal obligation |

**We do not:**
- Sell your personal data to third parties (CCPA §1798.100)
- Share your personal data with advertisers
- Use your data for cross-context behavioral advertising

---

## 10. International Data Transfers

If you are located in the EU/EEA, your data may be transferred to servers outside the EU. Such transfers are protected by:
- **Standard Contractual Clauses (SCCs)** approved by the European Commission (GDPR Art.46)
- **Adequacy decisions** where applicable

---

## 11. Your Rights as a Data Subject

### GDPR Rights (EU/EEA residents)

| Right | Description | How to exercise |
|---|---|---|
| **Art.15 — Access** | Obtain a copy of your personal data | Settings → Your Data → Download My Data |
| **Art.16 — Rectification** | Correct inaccurate data | Settings → Account |
| **Art.17 — Erasure** | Delete your account and data | Settings → Your Data → Delete Account |
| **Art.18 — Restriction** | Restrict processing while a dispute is resolved | Email dpo@bestme.app |
| **Art.20 — Portability** | Export data in machine-readable format | Settings → Your Data → Export Data |
| **Art.21 — Objection** | Object to processing based on legitimate interests | Email dpo@bestme.app |
| **Art.22 — Automated decisions** | Opt out of algorithmic recommendations | Settings → Privacy & Visibility → Discoverability |

### CCPA Rights (California residents)

| Right | Description |
|---|---|
| Right to know | What personal information we collect and how we use it |
| Right to delete | Request deletion of your personal information |
| Right to opt out | Opt out of "sale" or "sharing" of personal information (we do not sell data) |
| Right to non-discrimination | You will not be discriminated against for exercising CCPA rights |

### PIPEDA Rights (Canadian residents)

You have the right to access your personal information, correct inaccuracies, and withdraw consent for non-essential processing. Contact: dpo@bestme.app

### Israel PPL Rights (Israeli residents)

Under the Protection of Privacy Law 5741-1981, you have the right to access and correct information about you held in our database. Contact: dpo@bestme.app

---

## 12. Cookies and Tracking

BestMe's mobile application does not use browser cookies. We use:
- **Secure token storage:** Refresh tokens are stored in the OS secure storage (iOS Keychain, Android Keystore/EncryptedSharedPreferences) — not in cookies
- **Analytics:** We may use privacy-preserving analytics (no cross-app tracking)

If you access BestMe via a web browser, standard browser cookies may be used for session management. See our Cookie Policy at bestme.app/cookies.

---

## 13. Children's Privacy (COPPA / GDPR Art.8)

BestMe is not directed at children under 13. We do not knowingly collect personal data from children under 13.

- **Age verification:** Date of birth is required at registration and is **immutable** after creation (COPPA / GDPR Art.8 age-gating)
- **If you believe a child under 13 has created an account:** Contact childsafety@bestme.app immediately
- **For users aged 13–17:** Parental consent is required; certain features may be restricted

---

## 14. Security of Your Data

BestMe implements security measures consistent with GDPR Art.32 and NIST SP 800-63B:

- **Passwords:** Hashed with bcrypt (industry standard — see [GDPRArt5SecuritySpec.md](../03_settings/GDPRArt5SecuritySpec.md))
- **Sessions:** Active session management with remote logout capability (Settings → Login & Security → Active Sessions)
- **Login History:** 90-day log of all login events with geo-location (Settings → Login & Security → Login History)
- **Two-Factor Authentication (2FA):** Available via Email Code or Authenticator App (Settings → Login & Security → Two-Factor Authentication)
- **Access tokens:** Short-lived JWT (15 minutes); Refresh tokens stored in OS secure storage
- **Data in transit:** TLS encryption for all API communications

In the event of a security breach affecting your data, we will notify you and relevant supervisory authorities within the timeframes required by GDPR Art.33 (72 hours for supervisory authority notification).

---

## 15. Changes to This Policy

We will notify you of material changes to this Privacy Policy:
- Via email (to the address associated with your account)
- Via in-app notification
- At least **30 days** before the changes take effect

The updated policy will be available at bestme.app/privacy and via Settings → About → Privacy Policy.

---

## 16. Contact and Supervisory Authorities

| Contact | Details |
|---|---|
| **Data Protection Officer (DPO)** | dpo@bestme.app |
| **General support** | support@bestme.app |
| **Child Safety** | childsafety@bestme.app |
| **Legal** | legal@bestme.app |

### Supervisory Authorities

If you believe we have not adequately addressed a privacy concern:

- **EU residents:** Contact your national Data Protection Authority (DPA). A list of EU DPAs is available at: edpb.europa.eu
- **UK residents:** Information Commissioner's Office (ICO) — ico.org.uk
- **California residents:** California Privacy Protection Agency (CPPA) — cppa.ca.gov
- **Canadian residents:** Office of the Privacy Commissioner of Canada — priv.gc.ca
- **Israeli residents:** Privacy Protection Authority (PPA) — gov.il/en/departments/the_privacy_protection_authority

---

*PrivacyPolicy.md v1.1 · BestMe · March 2026*  
*Related documents: [TermsOfService.md](TermsOfService.md) · [PrivacyVisibilitySpec.md](../03_settings/PrivacyVisibilitySpec.md) · [GDPRArt5SecuritySpec.md](../03_settings/GDPRArt5SecuritySpec.md) · [AccountDeletionSpec.md](../03_settings/AccountDeletionSpec.md)*
