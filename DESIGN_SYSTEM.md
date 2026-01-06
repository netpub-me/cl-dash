# Design System Documentation - Claude Tutorial Dashboard

## 1. Design Philosophy

- **Terminal/Developer Aesthetic** - Monospace fonts, command-line inspired elements
- **Cyberpunk/Hacker Vibes** - Neon accent colors, dark backgrounds
- **Clean & Modern** - Card-based layout, generous spacing, smooth animations
- **Responsive First** - Mobile-friendly grid system

---

## 2. Color Palette

### Dark Theme (Default)

```css
--bg-primary: #0a0e14        /* Deep navy/black - main background */
--bg-secondary: #151a23      /* Slightly lighter - cards, header */
--bg-tertiary: #1f2430       /* Lighter still - demo boxes, buttons */
--text-primary: #e6e1dc      /* Off-white - main text */
--text-secondary: #95a3b3    /* Muted blue-gray - secondary text */
--accent-primary: #39ff14    /* Neon green - highlights, borders */
--accent-secondary: #00d9ff  /* Cyan blue - secondary accents */
--border: #2d3748            /* Dark gray - borders */
--hover: #2a3441             /* Subtle hover state */
```

### Light Theme

```css
--bg-primary: #f8f9fa        /* Light gray - main background */
--bg-secondary: #ffffff      /* Pure white - cards, header */
--bg-tertiary: #e9ecef       /* Slightly darker - demo boxes */
--text-primary: #1a202c      /* Dark navy - main text */
--text-secondary: #4a5568    /* Medium gray - secondary text */
--accent-primary: #00a86b    /* Forest green - highlights */
--accent-secondary: #0088cc  /* Professional blue - secondary */
--border: #cbd5e0            /* Light gray - borders */
--hover: #edf2f7             /* Subtle hover */
```

---

## 3. Typography

### Font Families

- **Body/UI**: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif`
- **Code/Terminal**: `'Courier New', monospace`

### Font Sizes

- **H1**: 1.8rem (header title)
- **H2**: 1.5rem (card titles)
- **H3**: 1.2rem (section headers, nav cards)
- **Body**: Default (1rem)
- **Small**: 0.95rem (descriptions)
- **Code**: 0.85rem (code blocks)
- **Labels**: 0.75rem (code block labels)
- **Buttons**: 0.9rem

### Special Typography Features

- **Terminal prompts**: Headers prefixed with `> `, `// `, `$ `
- **Text shadow**: Neon glow on main title
- **Letter spacing**: 0.5px on code block labels (uppercase)

---

## 4. Layout System

### Container

- Max-width: 1200px
- Centered with auto margins
- Padding: 20px

### Grid System

```css
nav {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}
```

- Auto-responsive cards
- Minimum card width: 250px
- Equal distribution

---

## 5. Component Styles

### Header (`index.html:53-62`)

- Sticky positioning (stays on scroll)
- 2px neon green bottom border
- Box shadow for depth
- Flexbox layout for title/controls
- z-index: 100

### Navigation Cards (`index.html:148-196`)

- Card background with border
- 3px gradient top border (appears on hover)
- Hover effects:
  - Transform: `translateY(-5px)`
  - Border color change to accent
  - Shadow: `0 10px 20px rgba(0,0,0,0.5)`
- Smooth transitions (0.3s)

### Content Cards (`index.html:219-225`)

- Secondary background
- 1px border
- 8px border-radius
- 25px padding
- 20px bottom margin

### Code Blocks (`index.html:292-315`)

**FIXED DESIGN:**

- Primary (darker) background
- 3px left border in accent green
- Padding: `30px 15px 15px 15px` (top padding for label)
- Labels positioned **inside** at top (8px from top, 15px from left)
- Label styling:
  - Uppercase
  - Bold
  - Cyan color
  - 0.5px letter spacing
  - 0.75rem font size
- Overflow-x: auto (horizontal scroll)

### Demo Boxes (`index.html:245-263`)

- Tertiary background
- 1px border
- 15px padding
- Interactive variant:
  - Cursor: pointer
  - Hover: accent border + glow shadow

### Buttons (`index.html:90-110`)

- Tertiary background
- 1px border
- 4px border-radius
- Padding: 8px 16px
- Hover effects:
  - Background change
  - Accent border
  - Glow shadow
- Active: `scale(0.98)` (press effect)

### Special Buttons

- **Reveal buttons**: Accent primary background, bold, dark text
- **Export buttons**: Same styling, used in export section

---

## 6. Interactive Elements

### Breadcrumbs (`index.html:113-138`)

- Secondary background
- 3px left border (cyan)
- Flexbox layout with gap
- Horizontal scroll on overflow
- Active item: bold + accent green color

### Progress Bar (`index.html:345-357`)

- Tertiary background
- 4px height
- Gradient fill (green to cyan)
- Smooth width transition (0.3s)
- Tracks visited sections

### Toast Notifications (`index.html:386-407`)

- Fixed position (bottom right)
- Accent primary background
- Transform/opacity animation
- Auto-dismiss after 2s
- z-index: 1000

### Hidden/Revealed Content (`index.html:265-274`)

- Max-height: 0 → 500px transition
- Overflow hidden
- Smooth ease-out animation (0.4s)
- Activated via `.revealed` class

---

## 7. Animations & Transitions

### Fade In (page sections)

```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
```

Duration: 0.4s

### Highlight (pulsing effect)

```css
@keyframes highlight {
  0%, 100% { background-position: 100% 0; }
  50% { background-position: 0 0; }
}
```

- Gradient sweep animation
- Duration: 2s infinite

### Standard Transitions

- Most interactive elements: 0.3s
- Hover effects: 0.2s
- Theme changes: 0.3s
- Hidden content: 0.4s ease-out

---

## 8. Responsive Breakpoints

### Mobile (@media max-width: 768px)

- H1: 1.8rem → 1.3rem
- Header: column layout
- Controls: full width with space-between
- Nav: single column grid
- Breadcrumbs: 0.8rem font
- Export buttons: column layout
- Button padding/font size reduced

---

## 9. JavaScript-Driven Features

### Theme Switching

- Toggles `data-theme` attribute on `<html>`
- Stores preference in localStorage
- Shows toast notification
- All colors transition smoothly via CSS variables

### Navigation

- SPA-style (no page reload)
- Shows/hides sections via `.active` class
- Updates breadcrumbs dynamically
- Smooth scroll to top
- Tracks progress

### Progress Tracking

- Uses `Set` to track visited sections
- Calculates percentage: visited/total × 100
- Updates progress bar width

---

## 10. Accessibility Features

- **Semantic HTML**: Proper heading hierarchy
- **Keyboard**: All interactive elements focusable
- **Transitions**: Smooth, not too fast
- **Color contrast**: Meets WCAG standards in both themes
- **Responsive**: Works on all screen sizes
- **No motion**: Could add `prefers-reduced-motion` support

---

## 11. Design Patterns Used

1. **CSS Custom Properties** - Complete theme system
2. **BEM-ish naming** - Clear, descriptive class names
3. **Mobile-first responsive** - Grid auto-fit pattern
4. **Progressive enhancement** - Works without JS for content
5. **Component isolation** - Self-contained styled components
6. **State management** - CSS classes for show/hide
7. **Smooth UX** - Transitions on all state changes

---

## 12. Key Fixes & Improvements

### Code Block Label Fix (2026-01-06)

**Problem**: Labels were positioned absolutely outside code blocks (`top: -10px`) and getting clipped by parent containers.

**Solution**: Moved labels inside code blocks:
- Changed padding to `30px 15px 15px 15px` (extra top padding)
- Positioned label at `top: 8px, left: 15px` (inside the block)
- Simplified styling: removed border/background, added uppercase + letter spacing
- Result: Labels always visible, no clipping issues

---

## 13. Future Enhancement Opportunities

- Add `prefers-reduced-motion` media query
- ARIA labels for better screen reader support
- Keyboard navigation (arrow keys between cards)
- Focus indicators
- Print stylesheet
- Service worker for offline use
- More color themes (add purple/orange variants)
- Search functionality
- Section anchors for direct linking

---

## File Structure

```
cl-dash/
├── index.html           # Single-file dashboard (HTML + CSS + JS)
└── DESIGN_SYSTEM.md     # This file
```

---

## Usage Notes

This is a **single-file artifact** - all HTML, CSS, and JavaScript are contained in `index.html`. No external dependencies, no build process, no server required.

To modify:
1. Edit `index.html` directly
2. All CSS is in the `<style>` tag (lines 7-454)
3. All JavaScript is in the `<script>` tag (lines 820-1071)
4. Use CSS custom properties for theme changes
5. Follow existing component patterns for new additions

---

**Last Updated**: 2026-01-06
**Version**: 1.1 (Fixed code block labels)
