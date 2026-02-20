# Settings Structure Guide

This document provides a detailed breakdown of the settings hierarchy for the Bestme application.

## Structure Philosophy

The settings are organized into logical groups that reflect:
1. **User Type**: Personal vs Business profiles
2. **Information Type**: Profile data, Privacy, Security, etc.
3. **Privacy Granularity**: Field-level privacy controls where needed

## Detailed Hierarchy

### 🟣 Account & Profile
*Purpose: Manage personal profile information*

#### Profile Details
Fields that define your identity and appearance:
- **Edit Cover**: Profile cover image
- **Avatar**: Profile picture
- **Status**: Current status message (3 possible statuses)
- **Name**: First name
- **Last Name**: Last name
- **Bio/About**: Personal description
- **Birthday**: Date of birth with granular privacy:
  - Everyone — full date
  - Everyone — age only
  - Friends — full date
  - Friends — age only
  - Private ✅
- **Gender**: Gender identity with privacy options:
  - Public
  - Friends
  - Private ✅

*Note: Each field can have individual privacy settings or use global Visibility settings*

#### Contact Information
How people can reach you:
- **Phone Number**: With privacy options (Friends, Private ✅)
- **Email**: With privacy options (Friends, Private ✅)
- **Address**: With privacy options (Friends, Private ✅)
- **Location (City, Country)**: With privacy options:
  - Public
  - Friends ✅
  - Private

#### Personal Links
- Links to favorite platforms, blogs, or resources
- Shows what inspires you and where to find you
- Privacy controlled by lock icons

---

### 🟢 Interests & Goals
*Purpose: Help users connect with like-minded people*

#### Category
- Choose categories that describe your interests
- Helps connect with like-minded people
- Discover services that match your needs
- Privacy: Controlled through dedicated settings

#### Goal
- Pick a goal that matters to you
- Take steps toward a healthier, happier you
- Find people on the same journey
- Privacy: Controlled through dedicated settings

---

### 🟠 Content & Activity
*Purpose: Control how you interact and what you share*

- **Default Audience (for posts)**: Who can see your posts by default
- **Media Settings**: How media content is handled
- **Saved Content**: Access to saved posts and content

---

### 🟠 Visibility
*Purpose: Central control panel for all visibility settings*

This section provides a consolidated view of privacy settings across all categories:

1. **Profile Details**
2. **Contact Information**
3. **Personal Links**
4. **Interests & Goals**
5. **Content**
6. **Network**
7. **Activity & Access**
8. **Search & Discovery**
9. **Followers & Subscriptions**
10. **Profile Discoverability**
11. **Active Status**
12. **Blocking**
13. **Category Discussions Visibility**

*All changes take effect immediately*

---

### 🟠 Preferences
*Purpose: Personalize your app experience*

- **Language & Region**: Set preferred language and regional settings
- **Accessibility**: Enable accessibility features
- **Dark Mode**: Toggle dark/light theme

---

### 🟠 Security & Login
*Purpose: Protect your account*

- **Email & Password**: Manage login credentials
- **Two-Factor Authentication**: Enable additional security
- **Active Sessions**: View and manage active login sessions
- **Devices**: See which devices are logged in
- **Login Activity**: Review recent login attempts

---

### 🟠 Data & Privacy
*Purpose: Control your data*

- **Download Your Data**: Request a copy of your data
- **Data Permissions/Consents**: Manage what data you've shared
- **Delete Account**: Permanently remove your account
- **Deactivate Profile**: Temporarily disable your account

---

### 🟤 Professional/Business
*Purpose: Manage business profile features*

- **Create Business Profile**: Opens flow to create a business profile
- **Verify Your Business**: Submit verification for your business
- **Learn About Business Features**: Information about business tools
- **Switch to Business Profile**: Toggle between Personal and Business
  - Currently: Personal profile
  - Status shown at top of settings

---

## Privacy Control Patterns

### Three-Level Privacy
Most fields support:
- **Public**: Visible to everyone
- **Friends**: Only visible to friends
- **Private**: Only visible to you

### Complex Privacy (Birthday)
Five levels of granularity:
1. Everyone — full date
2. Everyone — age only
3. Friends — full date
4. Friends — age only
5. Private

### Default Privacy
Fields without explicit privacy controls inherit from:
- Visibility settings (centralized)
- Category-level defaults

---

## Special Indicators

- 🔒 **Lock Icons**: Indicate fields with privacy controls
- ✅ **Checkmark**: Shows currently selected privacy option
- 🟣 **Purple**: Account & Profile sections
- 🟢 **Green**: Interests & Goals
- 🟠 **Orange**: Content, Visibility, Preferences, Security, Data & Privacy
- 🟤 **Brown**: Business/Professional features
- 🟡 **Yellow**: Actions that open flows (e.g., Create Business Profile)

---

## Design Principles

1. **Progressive Disclosure**: Basic settings first, advanced later
2. **Privacy by Default**: Most sensitive settings default to private
3. **Consistency**: Similar controls work the same way
4. **Clarity**: Clear labels and descriptions
5. **Flexibility**: Field-level or category-level privacy options
6. **Reversibility**: Most actions can be undone

---

## Future Considerations

As the structure evolves, consider:
- Multi-level categorization (sub-settings)
- Conditional settings (based on profile type)
- Bulk privacy controls
- Privacy presets (e.g., "Lock Everything", "Public Profile")
- Export/import settings between profiles

---

## Notes from Original Design

From the draw.io diagram annotations:

1. **Status Field**: Should display one of 3 possible statuses
2. **Settings Header**: Consider showing avatar next to "Settings" text to indicate which profile's settings (Personal vs Business)
3. **Category Component**: Design shows category selection is needed as first component, followed by standard selection UI
4. **Goal Selection**: Uses same flow/screens as home page goal selection
5. **Personal Links**: Designed as already shown in the design mockups
6. **Switch Profile**: 
   - Yellow: "Create Business Profile" - Opens business profile creation flow
   - Brown: "Switch to Business Profile" - Toggles between existing profiles

---

*Last Updated: 2026-02-17*
