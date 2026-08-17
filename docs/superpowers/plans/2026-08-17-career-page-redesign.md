# Career Page Redesign (Stripe Light Tech Style) Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Redesign the portfolio page to transition from an AI-like template design (neon purple gradients, glowing box shadows) to a premium, minimalist Stripe-style light tech layout.

**Architecture:** Refactor CSS variables to establish a high-contrast Slate/Zinc system with a single Tech Blue accent. Adjust the HTML layout from centered neon elements to asymmetric grid alignments, converting publication cards into a clean list format. Sync these aesthetic changes to the print-friendly resume sub-page.

**Tech Stack:** HTML5, Vanilla CSS, JavaScript (for theme toggle).

## Global Constraints
- Do not use Tailwind CSS. Modify local CSS files instead.
- Retain the current Light/Dark mode functionality but map it to the new design tokens.
- Do not use colored glowing shadows or text gradients.
- Do not use placeholders (TBD, TODO, etc.).

---

### Task 1: CSS Variables & Style Redesign System

**Files:**
- Modify: `css/style.css`

**Interfaces:**
- Consumes: Existing `:root` variables in `css/style.css`
- Produces: Stripe-style light/dark color variables, clean link hovers, non-glowing profile, and flat cards.

- [ ] **Step 1: Replace CSS Variables in `css/style.css`**

Replace lines 1 to 21 in `css/style.css` with the following:
```css
/* CSS Variables - Stripe Light Tech Aesthetic */
:root {
    --primary: #2563eb;         /* Tech Blue */
    --secondary: #1e40af;       /* Darker Blue for hover */
    --bg-dark: #09090b;         /* Zinc 950 (Neutral Dark) */
    --bg-dark-alt: #18181b;     /* Zinc 900 (Card Dark) */
    --bg-light: #f8fafc;        /* Slate 50 (Neutral Light) */
    --bg-light-alt: #ffffff;    /* Slate 100/White (Card Light) */
    --text-dark: #f4f4f5;       /* Zinc 100 */
    --text-light: #0f172a;      /* Slate 900 */
    --text-muted-dark: #a1a1aa;  /* Zinc 400 */
    --text-muted-light: #475569; /* Slate 600 */
    --card-dark: #18181b;       /* Zinc 900 */
    --card-light: #ffffff;      /* White */
    --border-dark: #27272a;     /* Zinc 800 */
    --border-light: #e2e8f0;    /* Slate 200 */
    --accent-subtle-light: #eff6ff; /* Blue 50 */
    --accent-subtle-dark: rgba(59, 130, 246, 0.1);
    --shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px -1px rgba(0, 0, 0, 0.1);
    --shadow-light: 0 1px 3px 0 rgba(0, 0, 0, 0.05);
    --transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}
```

- [ ] **Step 2: Update typography and heading fonts**

Add letter-spacing rules to `body`, `h1`, `h2` in `css/style.css`.
Modify:
```css
body {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background-color: var(--bg-dark);
    color: var(--text-dark);
    line-height: 1.6;
    transition: var(--transition);
}
```
Add:
```css
h1, h2, h3, h4 {
    letter-spacing: -0.02em;
}
.mono-label {
    font-family: SFMono-Regular, Consolas, Monaco, monospace;
    font-size: 0.75rem;
    letter-spacing: 0.05em;
    text-transform: uppercase;
}
```

- [ ] **Step 3: Refactor Navbar and Hero in `css/style.css`**

Search and replace classes for `.navbar`, `.nav-logo-img`, `.nav-menu a::after`, `.profile-avatar`, `.gradient-text`, `.social-links a` to strip neon glow, gradients, and purple accents.
Specifically replace:
```css
.profile-avatar {
    width: 220px;
    height: 220px;
    border-radius: 50%;
    object-fit: cover;
    margin: 0 auto;
    display: block;
    box-shadow: 0 0 60px rgba(102, 126, 234, 0.4);
    border: 4px solid rgba(102, 126, 234, 0.3);
}
```
with:
```css
.profile-avatar {
    width: 200px;
    height: 200px;
    border-radius: 8px; /* Square/rounded modern tech photo */
    object-fit: cover;
    margin: 0 auto;
    display: block;
    border: 1px solid var(--border-light);
    box-shadow: var(--shadow-light);
}
body.light-mode .profile-avatar {
    border-color: var(--border-light);
}
body:not(.light-mode) .profile-avatar {
    border-color: var(--border-dark);
}
```

Replace `.gradient-text`:
```css
.gradient-text {
    font-size: 3.5rem;
    font-weight: 700;
    background: var(--gradient);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.5rem;
}
```
with:
```css
.gradient-text {
    font-size: 3.5rem;
    font-weight: 800;
    color: var(--text-dark);
    margin-bottom: 0.5rem;
}
body.light-mode .gradient-text {
    color: var(--text-light);
}
```

Remove glowing effects from `.social-links a:hover` and `.theme-toggle:hover`.

- [ ] **Step 4: Refactor Timeline and Project tag styling**

Replace target selectors in `css/style.css` for timeline elements.
Replace:
```css
.timeline-marker {
    position: absolute;
    top: 0;
    left: 15px;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: var(--gradient);
    border: 3px solid var(--bg-dark);
    transition: var(--transition);
}
```
with:
```css
.timeline-marker {
    position: absolute;
    top: 5px;
    left: 19px;
    width: 7px;
    height: 7px;
    background: var(--primary);
    border-radius: 1px; /* Square indicator */
    transition: var(--transition);
}
```

Update `.timeline-projects` tags:
```css
.project-tag, .impact-badge, .rank-badge, .timeline-projects .project-badge {
    font-family: SFMono-Regular, Consolas, monospace;
    font-size: 0.7rem;
    padding: 2px 8px;
    border-radius: 4px;
    font-weight: 600;
}
```

- [ ] **Step 5: Verify syntax of `css/style.css`**

Run a clean static lint check or visual reload verification.
Expected: CSS file has correct syntax, no unclosed brackets.

- [ ] **Step 6: Commit changes to Git**
```bash
git add css/style.css
git commit -m "style: refactor CSS variables and remove glowing AI gradients"
```

---

### Task 2: HTML Page Structure & Component Redesign

**Files:**
- Modify: `index.html`

**Interfaces:**
- Consumes: Variables and typography defined in Task 1.
- Produces: Asymmetric grid layout in Hero, updated list-based Publications page, and clean timeline elements.

- [ ] **Step 1: Modify Hero section in `index.html`**

Update the Hero markup (`index.html:52-80`) to use an asymmetric split layout:
```html
    <!-- Hero Section -->
    <section id="hero" class="hero">
        <div class="hero-container">
            <div class="hero-grid">
                <div class="hero-text-side">
                    <span class="mono-label" style="color: var(--primary);">SK Hynix NAND Process Engineer // KAIST Ph.D.</span>
                    <h1 class="gradient-text">Junhyeok Jeon</h1>
                    <p class="hero-subtitle">Domain-First AI Architect</p>
                    <p class="hero-tagline">I bring AI-native thinking from research to production — wherever hard science meets the real world.</p>
                    <div class="social-links">
                        <a href="https://github.com/jhjeonkaist" target="_blank" rel="noopener" aria-label="GitHub"><i class="fab fa-github"></i></a>
                        <a href="https://scholar.google.com/citations?user=nh47l44AAAAJ" target="_blank" rel="noopener" aria-label="Google Scholar"><i class="fas fa-graduation-cap"></i></a>
                        <a href="https://www.linkedin.com/in/junhyeok-jeon-5b823532a/" target="_blank" rel="noopener" aria-label="LinkedIn"><i class="fab fa-linkedin"></i></a>
                        <a href="mailto:hyeok797@gmail.com" aria-label="Email"><i class="fas fa-envelope"></i></a>
                    </div>
                </div>
                <div class="hero-image-side">
                    <img src="images/profile.jpg" alt="Junhyeok Jeon" class="profile-avatar">
                </div>
            </div>
        </div>
        <div class="scroll-indicator">
            <i class="fas fa-chevron-down"></i>
        </div>
    </section>
```

Add CSS for `.hero-container`, `.hero-grid`, `.hero-text-side`, and `.hero-image-side` to `css/style.css`:
```css
.hero-container {
    max-width: 1100px;
    width: 100%;
    margin: 0 auto;
    padding: 0 20px;
    text-align: left;
}
.hero-grid {
    display: grid;
    grid-template-columns: 1.5fr 1fr;
    gap: 3rem;
    align-items: center;
}
@media (max-width: 768px) {
    .hero-grid {
        grid-template-columns: 1fr;
        text-align: center;
        gap: 2rem;
    }
}
```

- [ ] **Step 2: Update Publications list formatting in `index.html`**

Refactor the publications cards into horizontal table-like list rows. Add a new `.pub-row` styling to `css/style.css`:
```css
.publications-list {
    display: flex;
    flex-direction: column;
    gap: 0px; /* Border collapse feel */
}
.publication-card {
    background: transparent !important;
    border: none !important;
    border-bottom: 1px solid var(--border-dark) !important;
    padding: 1.5rem 0 !important;
    border-radius: 0 !important;
    box-shadow: none !important;
    margin-bottom: 0 !important;
    display: grid;
    grid-template-columns: 80px 1fr;
    gap: 1.5rem;
}
body.light-mode .publication-card {
    border-bottom-color: var(--border-light) !important;
}
.publication-year {
    font-family: monospace;
    font-size: 1rem;
    font-weight: 700;
    color: var(--primary) !important;
    text-align: left;
}
.publication-content h4 {
    font-size: 1.1rem;
    color: var(--text-dark);
    margin-bottom: 0.3rem;
}
body.light-mode .publication-content h4 {
    color: var(--text-light);
}
```

Update each publication item inside `index.html` to map to this structure.

- [ ] **Step 3: Update badges to use Slate / Accent Blue backgrounds**

Replace neon badge classes in `css/style.css`:
```css
.impact-badge {
    background: var(--accent-subtle-dark);
    color: var(--primary);
    border: 1px solid rgba(59, 130, 246, 0.2);
}
body.light-mode .impact-badge {
    background: var(--accent-subtle-light);
}
.rank-badge {
    background: rgba(16, 185, 129, 0.1);
    color: #10b981;
    border: 1px solid rgba(16, 185, 129, 0.2);
}
```

- [ ] **Step 4: Verify html changes render correctly**

Inspect index.html locally in the browser to ensure layouts adapt to desktop and mobile viewports.
Expected: Neat left-aligned grid, list-based publications, and solid-colored tags.

- [ ] **Step 5: Commit HTML and CSS tweaks to Git**
```bash
git add index.html css/style.css
git commit -m "feat: restructure homepage HTML layout and publication lists"
```

---

### Task 3: Resume Page Alignment

**Files:**
- Modify: `resume/resume.html`
- Modify: `resume/resume.css`

**Interfaces:**
- Consumes: Shared design system tokens.
- Produces: Re-styled print-first Resume page sharing the non-cliché tech identity.

- [ ] **Step 1: Replace CSS Variables in `resume/resume.css`**

Replace `:root` variables in `resume/resume.css` (lines 4-14) with:
```css
:root {
    --primary: #2563eb;         /* Tech Blue */
    --secondary: #1e40af;
    --text-primary: #0f172a;
    --text-secondary: #475569;
    --text-muted: #64748b;
    --border: #e2e8f0;
    --bg-subtle: #f8fafc;
    --bg-white: #ffffff;
    --accent-subtle: #eff6ff;
}
```

- [ ] **Step 2: Clean Header details and profile layout**

Modify `.header` in `resume/resume.css` to remove `border-image: var(--gradient) 1` and replace with:
```css
.header {
    display: flex;
    align-items: center;
    gap: 1.5rem;
    padding-bottom: 1rem;
    border-bottom: 2px solid var(--primary);
    margin-bottom: 1.2rem;
}
.profile-photo {
    width: 80px;
    height: 80px;
    border-radius: 6px; /* Square/rounded */
    object-fit: cover;
    border: 1px solid var(--border);
    flex-shrink: 0;
}
.name {
    font-size: 22pt;
    font-weight: 800;
    color: var(--text-primary);
    line-height: 1.2;
    margin-bottom: 0.15rem;
}
```

- [ ] **Step 3: Align Publication List styles in Resume CSS**

Change publication badges to use Tech Blue and green accents.
Replace:
```css
.pub-badge {
    display: inline-block;
    padding: 0.1rem 0.5rem;
    background: rgba(102, 126, 234, 0.12);
    color: var(--primary);
    border-radius: 10px;
    font-size: 7.5pt;
    font-weight: 600;
    margin-top: 0.2rem;
    margin-right: 0.3rem;
}
```
with:
```css
.pub-badge {
    display: inline-block;
    padding: 2px 6px;
    background: var(--accent-subtle);
    color: var(--primary);
    border: 1px solid rgba(37, 99, 235, 0.2);
    border-radius: 4px;
    font-size: 7.5pt;
    font-weight: 600;
    margin-top: 0.2rem;
    margin-right: 0.3rem;
}
```

- [ ] **Step 4: Verify print preview rendering**

Inspect the resume page (`resume/resume.html`) in a browser and check its print layout.
Expected: Clear monochrome typography, crisp Blue accents, and correct page breaks.

- [ ] **Step 5: Commit changes to Git**
```bash
git add resume/resume.html resume/resume.css
git commit -m "style: align print resume subpage with the new design identity"
```
