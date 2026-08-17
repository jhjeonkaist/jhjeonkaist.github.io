# Design Spec: Career Page Redesign (Stripe Light Tech Style)

- **Date**: 2026-08-17
- **Author**: Antigravity AI
- **Status**: Approved by User

## 1. Goal & Context
The current career website ([index.html](file:///Users/jhjeon/jhjeonkaist.github.io/index.html)) uses standard AI-generated template styling (neon purple/blue gradients, glowing shadows, bloated floating cards). This spec outlines the redesign to a premium **Stripe-style Light Tech** aesthetic, aligning with the user's background as a KAIST PhD and NAND Process Engineer at SK Hynix. The goal is to convey deep technical credibility, clean layout structure, and avoid typical AI developer tropes.

---

## 2. Design Tokens & Styling System

### A. Color Palette
We will implement a clean Slate/Zinc palette with a single Tech Blue accent. Gradients and neon glows are completely removed.

| CSS Variable | Light Mode (Default) | Dark Mode | Usage |
| :--- | :--- | :--- | :--- |
| `--primary` | `#2563eb` (Tech Blue) | `#3b82f6` | Brand accent, active buttons, links |
| `--secondary` | `#1e40af` (Dark Blue) | `#60a5fa` | Secondary accent, focus rings |
| `--bg-dark` | `#09090b` (Zinc 950) | `#09090b` | Dark mode body background |
| `--bg-dark-alt` | `#18181b` (Zinc 900) | `#18181b` | Dark mode surface (cards, navbar) |
| `--bg-light` | `#f8fafc` (Slate 50) | `#f8fafc` | Light mode body background |
| `--bg-light-alt` | `#ffffff` (White) | `#ffffff` | Light mode surface (cards, navbar) |
| `--text-dark` | `#f4f4f5` (Zinc 100) | `#f4f4f5` | Dark mode primary text |
| `--text-light` | `#0f172a` (Slate 900) | `#0f172a` | Light mode primary text |
| `--text-muted-dark` | `#a1a1aa` (Zinc 400) | `#a1a1aa` | Dark mode secondary text |
| `--text-muted-light` | `#475569` (Slate 600) | `#475569` | Light mode secondary text |
| `--border-dark` | `#27272a` (Zinc 800) | `#27272a` | Dark mode hairline borders |
| `--border-light` | `#e2e8f0` (Slate 200) | `#e2e8f0` | Light mode hairline borders |
| `--accent-subtle` | `#eff6ff` (Blue 50) | `rgba(59, 130, 246, 0.1)` | Subtle badge backgrounds |

### B. Typography
- **Primary Font**: `Inter`, sans-serif (remains as is).
- **Secondary/Technical Font**: Monospace (`SFMono-Regular`, `Consolas`, `Menlo`, `monospace`) for tags, dates, publication indices, and sub-labels.
- **Letter Spacing**:
  - Headings (`h1`, `h2`): `letter-spacing: -0.02em` (tighter, solid feel).
  - Monospace tags/labels: `letter-spacing: 0.05em` (wider readability).

---

## 3. Structural Redesigns

### A. Navigation Bar
- Remove purple gradient bottom border and replace with a clean hairline border using `--border-light` / `--border-dark`.
- Remove profile photo hover box shadow (glow). Replace with a subtle border color shift.
- Change hover indicators of menu items to use Tech Blue (`var(--primary)`) instead of the custom background gradient.

### B. Hero Section
- Remove the massive blue/purple radial-glow background.
- Change layout from centered to left-aligned columns or a split grid.
  - Left column: Large bold title (`h1`), clean description paragraph, social links styled as clean bordered buttons.
  - Right column: Clean profile avatar without glowing shadows, bounded by a simple, thin border.
- Remove all text gradient clip styles. Use high-contrast solid text colors.

### C. Experience & Timeline
- Style the vertical timeline line using a thin, solid, light-slate color.
- Remove the round gradient timeline markers and replace them with a simple solid slate block or point.
- Rework project badge tags to use `--accent-subtle` background and `--primary` text color.

### D. Publications (Journals & Conferences)
- Transition publication listings from floating cards to a structured, bordered list (tabular layout).
- Each publication will be separated by a thin horizontal border (`border-bottom: 1px solid var(--border)`).
- Journal and Conference badges (e.g. IF factor, Rank) will be formatted as clean tech-tags.

---

## 4. Files to Update
1. [`css/style.css`](file:///Users/jhjeon/jhjeonkaist.github.io/css/style.css): Main stylesheet refactoring.
2. [`index.html`](file:///Users/jhjeon/jhjeonkaist.github.io/index.html): HTML class adjustments and timeline structure refinements.
3. [`resume/resume.html`](file:///Users/jhjeon/jhjeonkaist.github.io/resume/resume.html): Ensure print-version and sub-page alignment.
4. [`resume/resume.css`](file:///Users/jhjeon/jhjeonkaist.github.io/resume/resume.css): Update colors and fonts to match the new Stripe aesthetic.

---

## 5. Verification Plan
- **Aesthetic check**: Verify in a browser that all glows, gradients, and purple-on-dark styles are gone.
- **Dark Mode toggle check**: Ensure the theme toggle switch transitions smoothly and both modes look excellent with the new colors.
- **Console errors**: Check that no JS errors are introduced.
