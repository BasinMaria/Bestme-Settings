# How to Update the Settings Structure

This guide explains how to maintain and update `ProfileSettings.drawio.html` as requirements evolve.

## Before You Start

### Prerequisites
- Access to draw.io (https://app.diagrams.net/) - free, no account needed
- Understanding of the current structure (see `STRUCTURE_GUIDE.md`)
- Clear requirements for what needs to be added/changed

### Important Principles
1. ✅ **Maintain draw.io compatibility** - Always edit in draw.io, not raw HTML
2. ✅ **Keep it importable** - Save as HTML with embedded diagram
3. ✅ **Document changes** - Update this guide and commit messages
4. ✅ **Progressive updates** - Small, incremental changes are better
5. ✅ **Consistency** - Follow existing patterns and color schemes

---

## Step-by-Step Update Process

### 1. Open the File in draw.io

**Option A: Web Browser**
1. Go to https://app.diagrams.net/
2. Click "Open Existing Diagram"
3. Select "Device" tab
4. Choose `ProfileSettings.drawio.html`
5. Click "Open"

**Option B: Desktop App**
1. Download draw.io desktop from https://www.diagrams.net/
2. Install and open
3. File → Open → Select `ProfileSettings.drawio.html`

### 2. Understand the Current Layout

The diagram uses:
- **Swimlanes**: For main setting categories (the boxes with headers)
- **Text cells**: For individual settings within categories
- **Shapes**: For icons (like lock icons)
- **Connectors**: For relationships between settings and privacy controls
- **Colors**: To distinguish different categories

**Color Scheme:**
- Purple (`#e1d5e7`): Account & Profile
- Green (`#d5e8d4`): Interests & Goals
- Orange (`#fa6800`): Content, Visibility, Preferences, Security, Data
- Brown (`#a0522d`): Business/Professional features
- Yellow (`#e3c800`): Actions that open flows

### 3. Make Your Changes

#### Adding a New Setting Field

1. **Find the parent category** in the diagram
2. **Click on the category swimlane** to select it
3. **Right-click** → "Edit Style"
4. Find the `height` parameter and increase it (e.g., from `230` to `256` for one new field)
5. **Click inside the swimlane** where you want to add the field
6. **Insert** → "Text" (or just double-click)
7. **Type the field name**
8. **Format the text cell**:
   - Right-click → "Edit Style"
   - Copy style from similar cells: `text;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;rounded=0;shadow=0;html=0;`
9. **Adjust cell size**: Drag corners to fit content

#### Adding a New Category

1. **Click on an existing similar category** to select it
2. **Edit** → "Duplicate" (or Ctrl+D / Cmd+D)
3. **Drag it to desired position**
4. **Edit the swimlane title**:
   - Click on the header text
   - Type new category name
5. **Edit internal cells**:
   - Delete unwanted cells (select and press Delete)
   - Add new cells (see "Adding a New Setting Field")
6. **Adjust colors if needed**:
   - Right-click swimlane → "Edit Style"
   - Change `fillColor` value

#### Adding Privacy Controls

Privacy controls appear as small lock icons with connections to privacy option boxes.

1. **Add a lock icon**:
   - Search for "lock" in the shape library
   - Drag "cisco19.lock" onto the canvas
   - Position it near the field that needs privacy control
2. **Create privacy options box**:
   - Duplicate an existing privacy box (easier than creating new)
   - Adjust content for your field
3. **Connect them**:
   - Click the lock icon
   - Drag from connection point to the privacy box
   - Choose "Orthogonal Edge Style" for clean, right-angled connections

#### Adding Descriptions/Notes

1. **For field descriptions**:
   - Add a text cell within the swimlane
   - Style it with centered text and smaller font
   - Use strokeColor=default to add a border if needed

2. **For callout notes**:
   - Insert → Shape → Callout
   - Type your note
   - Position near relevant element

### 4. Review Your Changes

Before saving, check:
- ✅ All text is readable
- ✅ Colors are consistent with category types
- ✅ Connections are clean (use orthogonal routing)
- ✅ Layout is organized and not cluttered
- ✅ New elements match existing style
- ✅ No overlapping elements (unless intentional)

### 5. Save the File

**Critical: Save as HTML with embedded diagram**

1. **File** → "Save As"
2. Choose "HTML" format
3. **Important Options**:
   - ✅ Enable "Embed diagram"
   - ✅ Enable "Links" (if you want clickable elements)
   - ✅ Enable "Toolbar" (for zoom, layers, etc.)
   - ✅ Enable "Lightbox" (for better viewing)
4. Save to replace `ProfileSettings.drawio.html`

### 6. Update Documentation

After making changes:

1. **Update `STRUCTURE_GUIDE.md`**:
   - Add new sections/fields to the hierarchy
   - Update field counts
   - Document any new patterns or concepts

2. **Update `README.md`** if structure changed significantly:
   - Update the "Current Structure" section
   - Note any breaking changes

3. **Create clear commit message**:
   ```
   Add [feature/section]: [Brief description]
   
   - Added [field name] to [category]
   - Updated privacy controls for [feature]
   - Adjusted layout to accommodate [change]
   
   Related to: [requirement/issue number if applicable]
   ```

### 7. Test the File

1. **Open in browser**: Verify the diagram renders correctly
2. **Import back to draw.io**: Confirm it's still editable
3. **Check all interactions**: Test zoom, pan, collapsible sections

---

## Common Tasks

### Changing a Field Name
1. Open in draw.io
2. Double-click the field text
3. Edit the name
4. Save

### Removing a Field
1. Select the field cell
2. Press Delete
3. Adjust parent swimlane height if needed
4. Save

### Reordering Fields
1. Click and drag the field cell to new position
2. Other cells will shift automatically
3. Verify layout looks good
4. Save

### Changing Privacy Options
1. Find the privacy options box for the field
2. Edit the text within each option
3. Update checkmark (✅) position if default changed
4. Save

### Adding Comments/Annotations
Use the callout shape:
1. Insert → Shape → Callout
2. Type your annotation
3. Position near relevant element
4. Style: `shape=callout;whiteSpace=wrap;html=1;perimeter=calloutPerimeter;`

---

## Best Practices

### Layout
- ⭐ Keep related items close together
- ⭐ Use consistent spacing (multiples of 10px)
- ⭐ Align elements using guides (View → Guides)
- ⭐ Use the main canvas area (don't spread too wide)

### Styling
- ⭐ Copy styles from existing elements (Format Painter)
- ⭐ Use the color scheme consistently
- ⭐ Keep font sizes readable (12-14pt for body, 14-16pt for headers)
- ⭐ Use the same icon style (cisco19 for lock icons)

### Connections
- ⭐ Use orthogonal edge style for clean connections
- ⭐ Avoid crossing lines when possible
- ⭐ Route connections through waypoints if needed

### Documentation
- ⭐ Add callout notes for complex interactions
- ⭐ Use descriptive names (not "Field1", "Setting2")
- ⭐ Document non-obvious behaviors
- ⭐ Keep notes in the language of the team

---

## Troubleshooting

### File Won't Open in draw.io
- Ensure you saved as HTML with embedded diagram
- Check file isn't corrupted (should be ~90KB)
- Try opening in browser first, then "Edit in draw.io"

### Diagram Looks Different After Save
- Make sure you're using the same zoom level
- Check that "Embed diagram" was enabled when saving
- Verify the viewer.js script is loading (check browser console)

### Changes Not Appearing
- Clear browser cache
- Hard refresh (Ctrl+F5 / Cmd+Shift+R)
- Confirm file was saved to correct location

### Lost Edit History
- draw.io HTML doesn't preserve edit history
- Use git commits for version history
- Make frequent commits when making complex changes

---

## Advanced Tips

### Using Layers
- Separate different types of information into layers
- Example: Base structure, Privacy controls, Annotations
- Toggle visibility for cleaner editing

### Creating Templates
- Save common patterns as separate files
- Copy/paste into main diagram when needed
- Examples: Privacy option boxes, Category swimlanes

### Keyboard Shortcuts
- `Ctrl/Cmd + D`: Duplicate
- `Ctrl/Cmd + G`: Group elements
- `Ctrl/Cmd + Shift + G`: Ungroup
- `Ctrl/Cmd + Z`: Undo
- `Ctrl/Cmd + Y`: Redo
- `Ctrl/Cmd + A`: Select all
- Arrow keys: Move selected elements
- `Shift + Arrow`: Move in larger increments

---

## Getting Help

If you're stuck:
1. Check draw.io documentation: https://www.diagrams.net/doc/
2. Review this guide and `STRUCTURE_GUIDE.md`
3. Look at git history to see how previous changes were made
4. Ask the team for help

---

*Last Updated: 2026-02-17*
