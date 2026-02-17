# Changelog

All notable changes to the settings structure will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to semantic versioning for structure updates.

## [Unreleased]

### Planned
- TBD based on requirements

---

## [1.0.0] - 2026-02-17

### Added - Initial Structure
This is the initial settings structure exported from draw.io, establishing the foundation for progressive development.

#### Main Categories
1. **Account & Profile** (Purple - #e1d5e7)
   - Profile details section
   - Contact information section
   - Personal links section

2. **Interests & Goals** (Green - #d5e8d4)
   - Category selection
   - Goal setting

3. **Content & Activity** (Orange - #fa6800)
   - Default audience for posts
   - Media settings
   - Saved content

4. **Visibility** (Orange - #fa6800)
   - 13 granular visibility controls
   - Centralized privacy management

5. **Preferences** (Orange - #fa6800)
   - Language & region
   - Accessibility
   - Dark mode

6. **Security & Login** (Orange - #fa6800)
   - Email & password management
   - Two-factor authentication
   - Session management
   - Device management
   - Login activity tracking

7. **Data & Privacy** (Orange - #fa6800)
   - Data export
   - Data permissions/consents
   - Account deletion
   - Profile deactivation

8. **Professional/Business** (Brown - #a0522d / Yellow - #e3c800)
   - Business profile creation
   - Business verification
   - Profile switching

#### Privacy Controls
- **Birthday**: 5-level granular privacy (Everyone full/age, Friends full/age, Private)
- **Gender**: 3-level privacy (Public, Friends, Private)
- **Phone Number**: 2-level privacy (Friends, Private)
- **Email**: 2-level privacy (Friends, Private)
- **Address**: 2-level privacy (Friends, Private)
- **Location**: 3-level privacy (Public, Friends, Private)
- **Personal Links**: Privacy indicators with lock icons

#### Visual Elements
- Lock icons (cisco19.lock) for privacy controls
- Checkmarks (✅) for selected options
- Callout shapes for design notes and annotations
- Orthogonal connections between related elements
- Consistent color coding by category type
- Status indicator (3 possible states)

### Documentation Added
- README.md - Overview and usage instructions
- STRUCTURE_GUIDE.md - Detailed hierarchy documentation
- UPDATE_GUIDE.md - Step-by-step maintenance guide
- QUICK_REFERENCE.md - Quick reference card
- VALIDATION.md - Validation checklist
- CHANGELOG.md - This file
- .gitignore - Repository cleanliness

### Technical Details
- Format: draw.io HTML with embedded mxGraph
- Compatibility: draw.io / diagrams.net
- Viewer: Embedded viewer-static.min.js
- File size: ~90KB
- Fully editable in draw.io
- Viewable in any modern browser

---

## Template for Future Entries

Use this template when documenting changes:

```markdown
## [Version] - YYYY-MM-DD

### Added
- New settings categories
- New fields
- New privacy controls
- New features

### Changed
- Modified field names
- Restructured categories
- Updated privacy options
- Layout improvements

### Deprecated
- Fields marked for future removal
- Old patterns to be replaced

### Removed
- Deleted fields
- Removed categories
- Eliminated redundant controls

### Fixed
- Corrected inconsistencies
- Fixed layout issues
- Resolved conflicts

### Security
- Privacy enhancements
- Security improvements
```

---

## Version Numbering Guide

- **Major version (X.0.0)**: Major restructuring, new main categories, breaking changes
- **Minor version (0.X.0)**: New sections, new fields, significant additions
- **Patch version (0.0.X)**: Small changes, fixes, clarifications, documentation updates

Examples:
- `1.0.0` → `2.0.0`: Added entire new top-level category structure
- `1.0.0` → `1.1.0`: Added "Notification Settings" category
- `1.0.0` → `1.0.1`: Fixed typo in "Preferences" section, updated privacy icon

---

## How to Update This Changelog

When making changes:

1. **Add entry under [Unreleased]** first:
   ```markdown
   ## [Unreleased]
   
   ### Added
   - New "Notification Preferences" section under Preferences
   ```

2. **When ready to release**, move to new version:
   ```markdown
   ## [1.1.0] - 2026-02-20
   
   ### Added
   - New "Notification Preferences" section under Preferences
   ```

3. **Update version in git tag**:
   ```bash
   git tag -a v1.1.0 -m "Add notification preferences"
   git push origin v1.1.0
   ```

4. **Keep entries in chronological order** (newest first)

5. **Link to issues/PRs** when applicable:
   ```markdown
   ### Added
   - New "Two-Step Verification" option in Security ([#123](link-to-issue))
   ```

---

## Change Categories Explained

- **Added**: New features, settings, categories, or capabilities
- **Changed**: Changes to existing functionality, names, or structure
- **Deprecated**: Features that will be removed in future versions
- **Removed**: Features that have been deleted
- **Fixed**: Bug fixes, corrections, layout improvements
- **Security**: Security enhancements, vulnerability fixes, privacy improvements

---

*Keep this file updated with every structural change to maintain a clear history of the settings evolution.*
