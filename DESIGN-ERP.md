# Design System — Twendee Work ERP

> Category: Enterprise / Admin Dashboard
> A data-dense, professional ERP interface built on a Cerulean blue theme. Prioritizes navigational efficiency, scannable data tables, and structured form workflows over expressiveness.

## 1. Visual Theme & Atmosphere

An enterprise-grade admin shell. The dark cerulean sidebar grounds every page; light surfaces in the main area ensure data legibility. Flyout menus, KPI cards, and modal workflows provide density without clutter.

- **Visual style:** professional, structured, data-first
- **Color stance:** dark gradient sidebar on a light-blue-tinted canvas
- **Design intent:** Surface operational data efficiently. Every chrome element should recede behind the content it frames.

## 2. Color

### Brand & Interactive
- **Primary:** `#007BA7` — Cerulean, main interactive color
- **Primary hover:** `#006490`
- **Primary active:** `#004f72` — Deep cerulean for pressed/active states
- **Primary-50:** `#e8f4f8` — Soft tinted background (hover areas, input bg, modal footer)
- **Primary-100:** `#c5e4ef` — Tinted border, flyout header bg
- **Accent:** `#00AADD` — Lighter cerulean, gradient endpoint
- **Accent-50 / Accent-100:** `#e8f4f8` / `#a0d8ef`

### Gradients / CTA
- **CTA (`--grad`):** `#007BA7` — Flat cerulean used for buttons, badges, pagination active, checkboxes, toggles
- **CTA hover (`--grad-hover`):** `#006490` — Button hover state
- **Sidebar (`--grad-sidebar`):** `#007BA7` — Rail sidebar background (flat cerulean)

### Semantic
- **Success:** `#10B981` · **Success-50:** `#ECFDF5`
- **Warning:** `#F59E0B` · **Warning-50:** `#FFFBEB`
- **Danger:** `#EF4444` · **Danger-50:** `#FEF2F2`

### Neutral
- **Surface:** `#FFFFFF` — Cards, table body, modals, panels
- **Background (bg):** `#e8f4f8` — App canvas (matches primary-50 for seamless integration)
- **Text:** `#111827`
- **Text secondary:** `#374151`
- **Text muted:** `#6B7280`
- **Text disabled:** `#9CA3AF`
- **Border:** `#E2E8F0` · **Border strong:** `#CBD5E1`
- **Divider:** `#F1F5F9`

### Sidebar-specific (on dark bg)
- **Sidebar text:** `rgba(255,255,255,0.85)`
- **Sidebar text muted:** `rgba(255,255,255,0.5)`
- **Sidebar active bg:** `rgba(255,255,255,0.15)`
- **Sidebar hover bg:** `rgba(255,255,255,0.08)`
- **Sidebar border:** `rgba(255,255,255,0.12)`

- Use `--grad` (`#007BA7` flat cerulean) for all primary CTAs and active/selected states.
- Use `--primary-50` as the "tinted hover" surface; never use pure white as a hover background.
- Table row hover uses `#F0FDFF` — a very light cyan wash — not a grey.

## 3. Typography

- **Scale:** 11 / 12 / 13 / 13.5 / 14 / 15 / 18 / 20
- **Families:**
  - Sans: `Inter` — All body copy, labels, table data, buttons, navigation
  - Display: `Be Vietnam Pro` — Page titles, modal titles, panel titles, profile names
  - Mono: `JetBrains Mono` — Currency/numeric cells, IDs, search keyboard shortcut, language code chip
- **Weights used:** 400, 500, 600, 700, 800
- **Base size:** 14px, 1.5 line-height
- **Letter-spacing:** `-0.01em` on display headings; `0.04–0.09em` on uppercase labels/headers

## 4. Spacing & Grid

Named spacing tokens on an **4pt base grid**:

| Token | Value |
|---|---|
| `--s1` | 4px |
| `--s2` | 8px |
| `--s3` | 12px |
| `--s4` | 16px |
| `--s5` | 24px |
| `--s6` | 32px |
| `--s7` | 48px |
| `--s8` | 64px |

- **App layout:** `grid-template-columns: 64px 1fr` (slim rail) / `240px 1fr` (expanded); `grid-template-rows: 60px 1fr`
- **KPI grid:** 4 columns → 2 columns at ≤1100px → 2 columns on mobile (always 2-up)
- **Form grids:** 2-column → 1-column on mobile
- **Gallery/component grid:** 2-column → 1-column at ≤1100px

## 5. Layout & Composition

- **Three-zone shell:** slim rail sidebar (64px, expands to 240px) → top bar (60px) → main scrollable area.
- **Sidebar rail:** icon-only by default; on hover or toggle, expands to show labels + sub-menus. Uses CSS `transition: width 260ms` on the sidebar and a matching `grid-template-columns` transition on `.app`.
- **Flyout panel:** absolute-positioned panel that appears to the right of the rail on hover/click of a nav item. Slides in (`translateX(-10px)` → `0`, 180ms). Has a 3px left cerulean border accent.
- **Right panel / drawer:** slides in from the right (`translateX(100%)` → `0`, 320ms). 520px wide on desktop, full-width on mobile. Has a gradient header (`primary-50` → `accent-50`).
- **Page structure:** page header (title + subtitle + actions) → KPI row → toolbar + table → pagination.
- Use `border-bottom: 2px solid var(--primary-100)` on the topbar to subtly anchor the top of the main area.

## 6. Components

### Sidebar Rail
- 64px collapsed, 240px expanded; transition: `260ms cubic-bezier(0.4, 0, 0.2, 1)`
- Active item: white left-edge accent bar (3px, 30px tall, rounded right, glows white)
- Icons: 20px, inherit color; labels hidden until expanded
- Sub-menu items: 40px left indent, 12.5px font, muted white text

### Flyout Panel
- `min-width: 224px`; rounded on right (`--r-lg`); `border-left: 3px solid --cta`
- Header: uppercase, tight tracking, cerulean gradient background
- Active item: left-to-right gradient `primary-50 → accent-50`, deep cerulean text
- Badge: pill, `primary-100` bg → gradient when active

### Top Bar
- Height: 60px; white surface; `border-bottom: 2px solid --primary-100`; subtle cerulean box-shadow `0 1px 8px rgba(0,123,167,0.08)`
- Search: max-width 420px; `primary-50` background; focuses to white + cerulean border + 3px ring; `kbd` shortcut hint right-aligned (font-mono)
- Actions: `icon-btn` (36×36px, `--r-md`); notification dot uses `--danger` with white `border`
- User chip: avatar (28px, cerulean) + name; hover uses `--divider`
- **Language toggle:** flag emoji + language code chip (`font-mono`, 11px, 0.05em tracking); 34px tall, `--r-md` border; hover → `primary-50` bg + cerulean border + `primary-active` text; active → `primary-100` bg

### KPI Cards
- White surface, 1px border, cerulean-tinted shadow `0 2px 14px rgba(0, 123, 167, 0.12)`
- Label: 12px, muted; Value: 18px bold; Delta badge: pill with semantic color + bg
- Hover: lifts 2px, shadow intensifies to `0 6px 24px var(--cta-shadow)`

### Tabs
- Pill container with `primary-50` background and `1px border`
- Active tab: gradient bg, white text, `shadow-cta`
- Count badge: semi-transparent on active, muted on inactive

### Data Table
- Header: `linear-gradient(90deg, primary-50 0%, accent-50 100%)`; uppercase, tracked, muted text
- Row hover: `#F0FDFF` (cyan wash, not grey)
- `border-collapse: collapse`; cell borders use `--divider`
- Numeric cells: `font-family: --font-mono`, right-aligned
- Sortable headers: cursor pointer, hover to full text color

### Checkbox & Toggle
- Checkbox: 16×16px, `border-radius: 4px`; on `:checked` → gradient background, white checkmark
- Toggle: 36×20px pill; on `:checked` → gradient track, thumb slides 16px right
- Both use `box-shadow: 0 0 0 3px var(--cta-50)` on `:focus-visible`

### Buttons
| Variant | Treatment |
|---|---|
| `btn-primary` | Gradient bg, shadow-cta; `::before` shine overlay on hover; lifts 1px |
| `btn-secondary` | White bg, `primary-100` border; hover → `primary-50` bg, cerulean text |
| `btn-ghost` | Transparent, `--border` border; hover → `--divider` bg |
| `btn-danger` | Danger red, lifts on hover with red shadow |
| `btn-sm` | h:30px, 13px font |
| `btn-lg` | h:42px, 15px font |

Focus ring: `0 0 0 3px var(--cta-50), 0 0 0 1px var(--cta)`

### Forms
- Label: 13px, 500 weight, `--text`; required marker in `--danger`
- Input/Select/Textarea: `border: 1px solid --border-strong`; hover → text-muted border; focus → cerulean border + 3px ring
- Error state: danger border, danger-50 focus ring, error message with icon
- Radio cards: selected state uses double ring (`box-shadow: 0 0 0 1px --cta`) + gradient soft bg

### Modal
- Backdrop: `rgba(17, 24, 39, 0.5)` + `blur(4px)`; `--shadow-xl`; entrance: `translateY(8px) scale(0.98)` → `0 / 1`
- `--r-xl` corners; modal footer uses `primary-50` background
- Mobile: anchors to bottom with `--r-xl` top corners, `max-height: 90vh`
- Confirm variant: icon badge (circle, semantic color) + body text layout

### Badges & Tags
- `.badge`: pill with dot indicator (`::before`); semantic color pairs (bg + text)
- `.badge-primary`: gradient bg, white text
- `.tag`: square-ish (`--r-sm`), muted grey bg

### Toasts
- Slides in from right: `translateX(110%)` → `0`, 280ms; slides out same direction, 220ms
- Icon: 20px circle, semantic color bg, white icon inside
- `info` variant uses the cerulean gradient
- Mobile: stretches full width (left + right inset `--s3`)

### Progress Bar
- 8px height, `--r-full`; bar uses `--grad`; semantic variants: success (green), warning (amber)

### Skeleton Loader
- `linear-gradient(90deg, divider → bg → divider)` shimmer animation at 200% width, 1.4s cycle

### Pagination
- Page button: 30×30px, `--r-sm`; active uses gradient + shadow-cta
- Page info: 13px muted with `<strong>` emphasis
- Jump input: 48px wide, centered, mono-ish; hides on mobile

### Right Panel / Drawer
- 520px desktop, 100vw mobile; slides with `cubic-bezier(0.32, 0.72, 0, 1)` over 320ms
- Header: gradient (`primary-50 → accent-50`), display font title, `border-bottom: 2px solid primary-100`
- Footer: `primary-50` bg, right-aligned actions

### Scrollbar
- Width: 10px; thumb: `--border-strong`, `2px solid --bg` offset border; hover → text-muted

## 7. Motion & Interaction

| Interaction | Duration | Easing |
|---|---|---|
| Button hover/lift | 180ms | `--ease` (cubic-bezier 0.4,0,0.2,1) |
| Nav/icon hover | 150ms (`--t-fast`) | `--ease` |
| Base transitions | 200ms (`--t-base`) | `--ease` |
| Sidebar expand/collapse | 260ms | `cubic-bezier(0.4, 0, 0.2, 1)` |
| Flyout appear | 180ms | `--ease` |
| Modal entrance | 200ms | `--ease` |
| Right panel slide | 320ms | `cubic-bezier(0.32, 0.72, 0, 1)` |
| Overlay fade in/out | 280ms | ease |
| Mobile sidebar drawer | 300ms | `cubic-bezier(0.32, 0.72, 0, 1)` |
| Toast slide in | 280ms | `--ease` |
| Toast slide out | 220ms | `--ease` |
| Shimmer skeleton | 1.4s | infinite |

- All interactive elements must define: hover, focus-visible, active, disabled states.
- CTA shadow: `rgba(0, 123, 167, 0.28)` — always present on primary buttons; intensifies to `rgba(0, 123, 167, 0.28+)` on hover.
- Button primary uses a `::before` shine overlay (`rgba(255,255,255,0.18)`) that fades in at opacity 1 on hover.

## 8. Voice & Brand

- Product name: **Twendee Work** — shown in topbar breadcrumb and mobile sidebar drawer header.
- Brand mark: white text on `rgba(255,255,255,0.2)` background, 800 weight, `-0.02em` letter-spacing. Scales up slightly on hover (`scale(1.05)`).
- Page titles use Be Vietnam Pro at 20px; all operational labels use Inter.
- Action labels are direct and operational: "Add Employee", "Export CSV", "Save Changes", "Confirm Delete".
- Section labels are uppercase + tracked: `EMPLOYEES`, `PAYROLL`, `REPORTS`.

## 9. Anti-patterns

- Do not use grey hover backgrounds on table rows — use `#F0FDFF` (cyan wash) to stay on-palette.
- Do not use the sidebar gradient on content surfaces — it belongs only to the rail sidebar.
- Do not flatten button variants — primary, secondary, ghost, and danger serve distinct interaction weights.
- Do not use arbitrary border radii — stick to `--r-sm` (6px), `--r-md` (8px), `--r-lg` (12px), `--r-xl` (16px), `--r-full` (9999px).
- Do not skip the focus-visible ring on form inputs — it is the only accessible keyboard indicator.
- Do not show flyout panels on mobile — they rely on hover, which doesn't exist on touch; use the drawer instead.
- Do not use `font-size` outside the defined scale for data in tables — consistency in numeric presentation is critical for scanning.
