# Bestme Settings - Hierarchical Structure

This repository maintains the **source of truth** for the Bestme application's settings structure. The structure is documented as a visual hierarchy that can be edited and viewed in draw.io.

## File Overview

### `ProfileSettings.drawio.html`
- **Purpose**: Visual representation of the settings hierarchy
- **Format**: draw.io HTML (editable in draw.io)
- **Status**: Source of truth for the entire settings structure

## How to Work With This File

### Viewing the Structure

1. **In a Web Browser**:
   - Open `ProfileSettings.drawio.html` directly in any web browser
   - The diagram will render using the embedded draw.io viewer

2. **In draw.io**:
   - Go to https://app.diagrams.net/
   - File → Open From → Device
   - Select `ProfileSettings.drawio.html`
   - Edit and save back to the same file

### Editing the Structure

To make changes to the settings hierarchy:

1. Open the file in draw.io (https://app.diagrams.net/)
2. Make your modifications to the structure
3. Save the file (File → Save)
4. Download as HTML with embedded diagram
5. Replace `ProfileSettings.drawio.html` in this repository
6. Commit your changes with a descriptive message

### Important Notes

- ⚠️ **Always maintain draw.io compatibility** - Don't edit the raw HTML unless you know what you're doing
- 💾 **Always save as HTML with embedded diagram** to ensure the file remains editable
- 📝 **Document changes** in commit messages describing what was added/modified/removed
- 🔄 **Progressive updates** - This structure will evolve over time as requirements are added

## Current Structure

### Main Settings Categories

1. **Account & Profile**
   - Profile details (Name, Avatar, Cover, Bio, Birthday, Gender, Status)
   - Contact information (Phone, Email, Address, Location)
   - Personal links

2. **Interests & Goals**
   - Category selection
   - Goal setting

3. **Content & Activity**
   - Default audience for posts
   - Media settings
   - Saved content

4. **Visibility**
   - Profile details visibility
   - Contact information visibility
   - Personal links visibility
   - Interests & goals visibility
   - Network visibility
   - Content visibility
   - Activity & access visibility
   - Search & discovery
   - Followers & subscriptions
   - Profile discoverability
   - Active status
   - Blocking
   - Category discussions visibility

5. **Preferences**
   - Language & region
   - Accessibility
   - Dark mode

6. **Security & Login**
   - Email & password
   - Two-factor authentication
   - Active sessions
   - Devices
   - Login activity

7. **Data & Privacy**
   - Download your data
   - Data permissions/consents
   - Delete account
   - Deactivate profile

8. **Professional/Business**
   - Create Business Profile
   - Verify your business
   - Learn about business features
   - Switch between Personal and Business profiles

### Privacy Levels

The system supports three main privacy levels for profile fields:
- **Public**: Visible to everyone
- **Friends**: Only visible to friends
- **Private**: Only visible to you

Special privacy options exist for specific fields:
- **Birthday**: Full date or age only options for both Public and Friends
- **Location**: Can be set to Public, Friends, or Private

## Maintenance

This file should be updated whenever:
- New settings categories are added
- New settings options are introduced
- The hierarchy structure changes
- Privacy options are modified
- Business requirements evolve

## Contributing

When adding requirements or making changes:
1. Open an issue describing the change needed
2. Update the draw.io diagram
3. Submit changes with clear documentation
4. Ensure backward compatibility where possible

## Technical Details

- **Format**: HTML with embedded mxGraph JSON
- **Compatible with**: draw.io / diagrams.net
- **Embedded viewer**: Uses viewer-static.min.js from diagrams.net
- **Edit-friendly**: Can be opened and edited directly in draw.io
