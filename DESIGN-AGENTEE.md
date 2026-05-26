# Design System — Agentee Chat Interface

> Category: Conversational AI
> A chat-first interface with a blue-cyan gradient identity, optimized for agentic task delegation, real-time tool call visibility, and progressive disclosure of detail.

## 1. Visual Theme & Atmosphere

Conversational AI workspace with a clean two-panel layout — collapsible sidebar on the left, chat canvas on the right. The interface stays out of the user's way; the gradient signal draws attention only to CTAs and active agent states.

- **Visual style:** light, clean, gradient-accented
- **Color stance:** near-white surfaces with a blue-to-cyan gradient identity
- **Design intent:** Make agent activity readable at a glance while keeping the conversation in focus.

## 2. Color

- **Primary:** `#2563EB` — Blue, core brand and CTA color
- **Accent:** `#06B6D4` — Cyan, gradient endpoint and interactive highlights
- **Gradient primary:** `linear-gradient(135deg, #2563EB 0%, #06B6D4 100%)` — Buttons, avatar marks, active states
- **Gradient soft:** `linear-gradient(135deg, #EFF6FF 0%, #ECFEFF 100%)` — Hover backgrounds, stat cards
- **Gradient mark:** `linear-gradient(135deg, #3B82F6 0%, #0EA5E9 50%, #06B6D4 100%)` — Brand logomark
- **Primary soft:** `#EFF6FF` — Chip hover, code background, nav active bg
- **Primary soft-2:** `#DBEAFE` — Tool preview hover border
- **Primary deep:** `#1E40AF` — Inline code text color
- **Secondary (bg):** `#F8FAFC` — App background, sidebar-less areas
- **Success:** `#10B981` — Task step done, status dot, positive trends
- **Warning:** `#F59E0B` — At-risk indicators
- **Danger:** `#EF4444` — Error states, negative trends
- **Surface:** `#FFFFFF` — Cards, bubbles, sidebar, composer, detail panel
- **Text:** `#0F172A` — Body copy; also used as user-message bubble background
- **Text muted:** `#64748B` — Secondary labels, subtitles
- **Text subtle:** `#94A3B8` — Timestamps, placeholders, section labels
- **Border:** `#E2E8F0` — Visible dividers
- **Border soft:** `#F1F5F9` — Subtle separators between surface layers

- Use the gradient on any element that represents a primary action or live agent state.
- Keep `Surface (#FFFFFF)` for all message bubbles and panels.
- User message bubbles invert: `Text (#0F172A)` background, `Surface (#FFFFFF)` text.

## 3. Typography

- **Scale:** 11 / 12 / 13 / 14 / 18 / 20 / 22
- **Families:**
  - Display: `Playfair Display` — Chat title, panel titles, stat values
  - Body: `Inter` — All UI labels, messages, buttons
  - Mono: `JetBrains Mono` — Code blocks, timestamps, keyboard hints, tool call descriptions
- **Weights used:** 400, 500, 600, 700, 800, 900
- **Base size:** 14px body, 1.5 line-height
- **Letter-spacing:** `-0.02em` on brand name; `-0.01em` on chat/panel titles; `0.08–0.10em` on uppercase section labels

## 4. Spacing & Grid

- **Spacing base:** 8pt baseline grid
- **App layout:** `grid-template-columns: 260px 1fr` — fixed sidebar, fluid chat area
- **Tablet breakpoint (≤1024px):** sidebar narrows to 220px; content padding reduces
- **Mobile breakpoint (≤767px):** sidebar becomes a slide-in drawer (280px, `translateX(-100%)` → `translateX(0)`); chat takes full width
- **Message content max-width:** 760px, centered in the chat body
- **Composer max-width:** 760px, matching message content
- **Consistent padding rhythm:** 28px desktop → 20px tablet → 14px mobile for all primary content areas

## 5. Layout & Composition

- Two zones: `sidebar` (navigation + history) and `chat-main` (header + scrollable messages + composer).
- Sidebar divides into: brand header, nav list, recent chat list, user card footer.
- Chat area divides into: sticky header, scrollable message body, pinned composer.
- A slide-in **detail panel** (480px wide, fixed right) provides progressive disclosure for tool calls and analysis results without leaving the conversation.
- Message thread has a maximum reading width (760px) with generous vertical rhythm (24px gap between messages, 28px body padding).

## 6. Components

### Buttons
| Variant | Background | Text | Notes |
|---|---|---|---|
| Primary | Gradient primary | Surface | `box-shadow: --shadow-glow`; lifts 1px on hover |
| Secondary | Surface | Text | 1px border `--border`; on hover: border + text switch to primary |
| Send | Gradient primary | Surface | 34×34px square, `border-radius: 10px` |
| Ghost pill | Surface | Primary | `border-radius: 999px`; used for "Show detail", chips |

### Inputs
- Composer: `border: 1.5px solid --border`; on `:focus-within` → border turns primary + 4px ring `rgba(37, 99, 235, 0.1)`
- Prevent iOS auto-zoom: composer input is `font-size: 16px` on mobile
- Padding-bottom uses `env(safe-area-inset-bottom)` for iOS home bar safety

### Message Bubbles
- Agent: Surface background, `--border-soft` border, `--radius-md` corners
- User: `#0F172A` background, white text, matching border — inverted dark treatment
- Inline code: `background: --primary-soft; color: --primary-deep` (agent); `rgba(255,255,255,0.15)` (user)

### Tool Preview
- Collapsed card with icon, title, mono description, and success indicator
- Hover: border changes to `--primary-soft-2`, background switches to gradient-soft

### Task Progress
- Header accent: 2px gradient top-border
- Steps: done (green filled circle), active (gradient circle with ring glow), pending (secondary bg outline)

### Suggestion Chips & Badges
- Pill shape (`border-radius: 999px`); 12px font
- Nav badge: gradient background; 10px font; 2–6px padding

### Detail Panel
- Slides in from right: `transform: translateX(100%)` → `0` over 320ms `cubic-bezier(0.32, 0.72, 0, 1)`
- Overlay: `rgba(15, 23, 42, 0.3)` + `backdrop-filter: blur(4px)`
- Header has 3px gradient top-accent bar
- Stat cards use gradient-soft background
- Code blocks: dark surface (`#0F172A`), monospace, syntax-colored (keywords `#60A5FA`, strings `#FCD34D`, numbers `#34D399`, comments `#64748B`)

### Citations
- Left 2px primary border accent
- Hover: shifts 2px right, background becomes gradient-soft

### Scrollbar
- Width: 6px; thumb: `--border` color, `border-radius: 999px`; track: transparent

## 7. Motion & Interaction

| Interaction | Duration | Easing |
|---|---|---|
| Button hover (lift) | 180ms | ease |
| Nav/chip hover | 150ms | ease |
| Detail panel slide | 320ms | `cubic-bezier(0.32, 0.72, 0, 1)` |
| Overlay fade | 280ms | ease |
| Message entrance | 360ms | ease (`fadeUp` — opacity 0→1, translateY 8px→0) |
| Sidebar drawer (mobile) | 300ms | `cubic-bezier(0.32, 0.72, 0, 1)` |

- **Status dot pulse:** 2s ease-in-out infinite — ring expands from 3px to 5px
- **Typing indicator:** 3 dots, staggered 0.2s, bounce + opacity (1.4s cycle)
- **Glow shadow:** `0 8px 24px rgba(37, 99, 235, 0.25)` — always on primary buttons; intensifies to `0 12px 28px rgba(37, 99, 235, 0.35)` on hover

All interactive states must be defined: hover, focus-visible, active, disabled. Focus rings use `0 0 0 4px rgba(37, 99, 235, 0.1)`.

## 8. Voice & Brand

- Brand name rendered as `Agent` + `<em>ic</em>` — the italic suffix in gradient text creates a subtle product personality.
- Chat title uses Playfair Display; all labels and messages use Inter — keeps hierarchy readable without competing.
- Microcopy is action-oriented: "New conversation", "Ask Atlas anything, or delegate a task…", "Show detail", "Use in chat".
- Section labels are uppercase + spaced (`0.08em`): `WORKSPACE`, `RECENT`.

## 9. Anti-patterns

- Do not use any color outside the palette for interactive states — always map to an existing token.
- Do not show the detail panel content inline; it must live in the side panel to preserve message readability.
- Do not apply the gradient to background surfaces — reserve it for interactive elements and agent identity marks.
- Do not flatten the user/agent bubble distinction; the inverted dark user bubble is a critical affordance.
- Do not remove the 760px max-width constraint on message content — unconstrained line length harms readability.
- Do not use `font-size < 16px` on the composer input on mobile (triggers iOS zoom).
