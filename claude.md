# ChSami Blog Style Guide

> **Design System: Swiss Minimalist**
> Follow these guidelines for all blog-related design work to maintain visual consistency.

---

## Design Philosophy

The ChSami blog follows a **Swiss Minimalist** aesthetic inspired by the International Typographic Style. Core principles:

- **Precision over decoration** — Every element serves a purpose
- **Grid-based layouts** — Clean alignment and mathematical spacing
- **Strong typography hierarchy** — Type does the heavy lifting
- **Generous whitespace** — Let content breathe
- **Monochromatic with purpose** — Black, cream, and subtle grays

---

## Color Palette

```css
--bg-primary: #F8F6F1;      /* Warm cream background */
--bg-card: #FFFFFF;          /* Pure white for cards */
--text-primary: #1A1A1A;     /* Near-black for headings */
--text-secondary: #6B6B6B;   /* Dark gray for body text */
--text-muted: #888888;       /* Medium gray for metadata */
--text-light: #A8A4A0;       /* Light gray for timestamps */
--border-color: #E8E4DC;     /* Warm gray borders */
--accent: #1A1A1A;           /* Black for buttons/active states */
```

**Rules:**
- Never use saturated colors except for syntax highlighting in code blocks
- Borders should be subtle (`1px solid #E8E4DC`)
- Active/hover states use solid black (`#1A1A1A`)

---

## Typography

### Font Stack

| Purpose | Font | Fallback |
|---------|------|----------|
| Headings & Body | Satoshi | Helvetica Neue, sans-serif |
| Metadata, Code, Dates | JetBrains Mono | monospace |

### Font Import
```html
<link href="https://api.fontshare.com/v2/css?f[]=satoshi@400,500,700,900&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Type Scale

| Element | Font | Size | Weight | Letter-spacing |
|---------|------|------|--------|----------------|
| Logo | Satoshi | 24px | 900 (CH) / 400 (SAMI) | -0.02em |
| Hero Title | Satoshi | 42px | 700 | -0.03em |
| Card Title | Satoshi | 22px | 600 | -0.02em |
| Body Text | Satoshi | 17px | 400 | normal |
| Sidebar Title | Satoshi | 14px | 500 | normal |
| Metadata | JetBrains Mono | 10-12px | 400-500 | 0.05em-0.15em |
| Category Labels | JetBrains Mono | 10px | 400 | 0.15em (uppercase) |

### Rules:
- Headings use negative letter-spacing for tighter feel
- Metadata uses positive letter-spacing and UPPERCASE
- Line height: 1.15-1.3 for headings, 1.6-1.7 for body
- Never use bold for body text; reserve for headings only

---

## Layout & Spacing

### Page Structure
```
┌─────────────────────────────────────────────────────────┐
│ HEADER (32px 60px padding)                              │
├──────────────┬──────────────────────────────────────────┤
│   SIDEBAR    │              MAIN CONTENT                │
│   340px      │              flex: 1                     │
│   sticky     │              48px 60px padding           │
│              │                                          │
└──────────────┴──────────────────────────────────────────┘
```

### Spacing System
Use multiples of 8px:
- `8px` — tight spacing (between related items)
- `16px` — standard gap
- `24px` — section padding
- `32px` — component separation
- `48px` — major section breaks
- `64px` — hero/section margins

### Grid
- Featured cards: `grid-template-columns: repeat(2, 1fr); gap: 32px`
- Sidebar posts: Single column, `20px` vertical padding per item

---

## Components

### Navigation Links
```css
.nav-item {
  font-size: 13px;
  font-weight: 500;
  letter-spacing: 0.02em;
  padding: 8px 0;
}
.nav-item::before {
  /* Underline animation on hover */
  height: 2px;
  background: #1A1A1A;
  transform: scaleX(0);
  transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}
```

### Category Pills
```css
.category-pill {
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  padding: 10px 20px;
  border: 1.5px solid transparent;
  background: transparent;
}
.category-pill.active {
  background: #1A1A1A;
  color: #F8F6F1;
}
```

### Cards
- No border-radius (sharp corners)
- White background
- Subtle hover: `transform: scale(1.02)` on images
- Number overlay: 72px JetBrains Mono in `#E8E4DC`

### Sidebar Posts
```css
.sidebar-post {
  padding: 20px 0;
  border-bottom: 1px solid #E8E4DC;
  display: flex;
  gap: 16px;
}
.post-index {
  font-family: 'JetBrains Mono';
  font-size: 11px;
  color: #A8A4A0;
  min-width: 28px;
}
```

### Buttons
- Primary: Black background, cream text
- Appear on hover (e.g., "READ →" on hero)
- Uppercase, 12px, letter-spacing 0.1em

---

## Imagery

### Hero Images
- Dimensions: Full width, 520px height
- Object-fit: cover
- Hover effect: `transform: scale(1.02)` with 0.6s ease

### Card Images
- Dimensions: Full width, 280px height
- Object-fit: cover
- Hover effect: `transform: scale(1.05)` with 0.5s ease

### Rules:
- Use high-quality, developer-relevant imagery
- Prefer abstract tech visuals, code screenshots, or workspace photos
- Avoid stock photo clichés (handshakes, generic office scenes)

---

## Animations & Transitions

### Timing Function
Always use: `cubic-bezier(0.4, 0, 0.2, 1)` for smooth, natural motion.

### Standard Transitions
```css
/* Hover states */
transition: all 0.2s ease;

/* Image transforms */
transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);

/* Page load animations */
@keyframes slideUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
animation: slideUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards;
```

### Stagger Delays
```css
.delay-100 { animation-delay: 0.1s; }
.delay-200 { animation-delay: 0.2s; }
.delay-300 { animation-delay: 0.3s; }
```

---

## Code Blocks & Syntax

When displaying code in blog posts:

```css
pre, code {
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  background: #1A1A1A;
  color: #F8F6F1;
  border-radius: 0; /* Sharp corners */
  padding: 24px;
}
```

---

## Responsive Breakpoints

```css
/* Tablet */
@media (max-width: 1100px) {
  .featured-grid { grid-template-columns: 1fr; }
}

/* Mobile */
@media (max-width: 900px) {
  .layout { flex-direction: column-reverse; }
  .sidebar { width: 100%; position: static; }
  .hero-title { font-size: 28px; }
  .hero-img { height: 300px; }
}
```

---

## Do's and Don'ts

### ✅ Do
- Use generous whitespace
- Keep typography hierarchy clear
- Use JetBrains Mono for all metadata
- Maintain sharp corners on all elements
- Use subtle, purposeful animations
- Keep the color palette monochromatic

### ❌ Don't
- Add decorative elements or icons
- Use border-radius on cards
- Use colored backgrounds (except code blocks)
- Add shadows to cards
- Use more than 2 font families
- Overuse bold or italic text

---

## Quick Reference

```
Logo:           CH (900) + SAMI (400) at 24px
Hero:           42px / 700 / -0.03em / #1A1A1A
Card Title:     22px / 600 / -0.02em / #1A1A1A
Body:           17px / 400 / normal / #5A5A5A
Metadata:       10-12px / JetBrains Mono / uppercase / #888
Background:     #F8F6F1
Cards:          #FFFFFF
Borders:        #E8E4DC
Active:         #1A1A1A bg, #F8F6F1 text
```

---

*This style guide ensures all ChSami blog content maintains the Swiss Minimalist aesthetic. Reference this document when creating new pages, components, or blog post templates.*
