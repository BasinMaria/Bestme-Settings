# Quick Reference Card

## 🚀 Quick Start

### View the Structure
- **Browser**: Open `ProfileSettings.drawio.html` in any browser
- **draw.io**: https://app.diagrams.net/ → Open → Device → Select file

### Edit the Structure
1. Open in draw.io (https://app.diagrams.net/)
2. Make changes
3. File → Save As → HTML (with "Embed diagram" ✅)
4. Replace the file in the repository
5. Commit with clear message

---

## 📋 Common Operations

### Add a Setting Field
1. Select parent category swimlane
2. Increase height in style (add ~26 for each field)
3. Double-click inside swimlane → Type field name
4. Copy style from similar field
5. Adjust position

### Add a Category
1. Duplicate existing category (Ctrl+D)
2. Edit title and fields
3. Change color if needed (Right-click → Edit Style → fillColor)
4. Position and connect as needed

### Add Privacy Control
1. Add lock icon (Search "cisco19.lock")
2. Duplicate existing privacy options box
3. Connect with orthogonal line

### Reorder Fields
- Just drag and drop!

---

## 🎨 Color Scheme

```
Purple (#e1d5e7):  Account & Profile
Green (#d5e8d4):   Interests & Goals  
Orange (#fa6800):  Content, Visibility, Preferences, Security, Data
Brown (#a0522d):   Business/Professional
Yellow (#e3c800):  Action flows
```

---

## ⌨️ Keyboard Shortcuts

```
Ctrl/Cmd + D:       Duplicate
Ctrl/Cmd + G:       Group
Ctrl/Cmd + Z/Y:     Undo/Redo
Arrow keys:         Move (Shift = larger steps)
Delete:             Remove element
Double-click:       Edit text
```

---

## ✅ Save Checklist

Before saving:
- [ ] All text is readable
- [ ] Colors are consistent
- [ ] No overlapping elements
- [ ] Connections are clean
- [ ] New elements match existing style

When saving:
- [ ] File → Save As → HTML
- [ ] "Embed diagram" is CHECKED ✅
- [ ] Replace ProfileSettings.drawio.html
- [ ] Update STRUCTURE_GUIDE.md if needed
- [ ] Commit with clear message

---

## 📚 Documentation Files

- `README.md` - Overview and how to work with the file
- `STRUCTURE_GUIDE.md` - Detailed hierarchy breakdown
- `UPDATE_GUIDE.md` - Step-by-step update instructions
- `QUICK_REFERENCE.md` - This file!

---

## 🔒 Privacy Level Syntax

```
Public         → Visible to everyone
Friends        → Only visible to friends
Private ✅     → Only visible to you
```

For birthday:
```
Everyone — full date
Everyone — age only
Friends — full date
Friends — age only
Private ✅
```

---

## 🎯 Style Patterns

### Swimlane (Category)
```css
swimlane;fontStyle=0;align=center;verticalAlign=top;
childLayout=stackLayout;horizontal=1;startSize=26;
horizontalStack=0;resizeParent=1;resizeLast=0;
collapsible=1;marginBottom=0;rounded=0;shadow=0;
strokeWidth=1;fillColor=#e1d5e7;strokeColor=#9673a6;
```

### Text Cell (Field)
```css
text;align=left;verticalAlign=top;spacingLeft=4;
spacingRight=4;overflow=hidden;rotatable=0;
points=[[0,0.5],[1,0.5]];portConstraint=eastwest;
rounded=0;shadow=0;html=0;
```

### Lock Icon
```css
sketch=0;points=[[0.5,0,0],[1,0.5,0],[0.5,1,0],[0,0.5,0],
[0.145,0.145,0],[0.8555,0.145,0],[0.855,0.8555,0],[0.145,0.855,0]];
verticalLabelPosition=bottom;html=1;verticalAlign=top;
aspect=fixed;align=center;pointerEvents=1;
shape=mxgraph.cisco19.lock;fillColor=#005073;strokeColor=none;
```

---

## ⚠️ Important Warnings

- ❌ Don't edit raw HTML (unless you really know what you're doing)
- ❌ Don't forget to check "Embed diagram" when saving
- ❌ Don't use non-standard fonts (stick to system fonts)
- ✅ Always test that file can be reimported to draw.io
- ✅ Commit frequently with clear messages
- ✅ Keep the file under 1MB for easy loading

---

## 🆘 Emergency Recovery

If something breaks:
1. Check git history: `git log --oneline`
2. Revert to working version: `git checkout <commit> -- ProfileSettings.drawio.html`
3. Or restore from GitHub web interface

---

## 💡 Pro Tips

- Use Format Painter to copy styles quickly
- Hold Shift while dragging to constrain movement
- Use guides (View → Guides) for alignment
- Group related elements (Ctrl+G) before moving
- Keep a backup before major restructuring
- Test in browser after each major change

---

*Keep this file open while editing!*
*Last Updated: 2026-02-17*
