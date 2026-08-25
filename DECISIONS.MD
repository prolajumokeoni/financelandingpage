# DECISIONS.md

**Live URL:** https://financelanding-ivory.vercel.app/ 

---

## How I built the sliding indicator

The indicator is a single absolutely-positioned `<span>` that lives inside the outer nav container, spanning everything from the logo to the Start Free button. By default it fills the full container width — creating the frosted-glass backdrop the whole bar sits on. When the user hovers a tab, I measure that tab's position with `getBoundingClientRect()` and write the result into three reactive refs (`pillX`, `pillW`, `pillH`) that drive inline `transform: translateX()`, `width`, and `height` styles. The pill contracts to wrap just that tab, then expands back to full width on mouse-leave or after a click. The animation runs as a pure CSS transition with `cubic-bezier(0.34, 1.4, 0.64, 1)` — a spring-approximating curve that overshoots slightly and settles, matching the feel of the Framer Motion original without any JS animation library. Because every measurement comes from the DOM at runtime, adding a tab or changing a label requires no code change.

---

## Mobile navigation decision

Below 991 px the animated tab bar is hidden and replaced by a hamburger button. Tapping it opens a full-viewport overlay containing the logo, a close button, and all nav items stacked vertically with generous tap targets (48 px minimum height). Above 991 px the full floating nav is shown with the sliding pill animation intact.

**Why a full-screen overlay instead of keeping the tab bar:** a row of five tabs with a pill indicator needs roughly 500 px of horizontal space to breathe. On a 360 px phone it would either overflow off-screen or compress tabs to illegible widths — both are wrong answers per the brief. A full-screen drawer is a familiar mobile pattern, gives every item equal space, and keeps the tap targets accessible without squinting.

**Responsive behaviour across the page:** every section uses CSS Grid and Tailwind's responsive prefixes (`max-[991px]:grid-cols-1`, `max-[640px]:flex-col`, etc.) so layouts reflow to single-column on narrow viewports. Font sizes and spacing are set in `rem`/`px` values that stay readable at 360 px without a horizontal scroll.

---

## What I could not match exactly

| Original | What I did instead |
|---|---|
| Dropdown menus on Home and Pages | Skipped — marked optional in the brief |
| Framer Motion spring physics (exact stiffness/damping) | Approximated with `cubic-bezier(0.34, 1.4, 0.64, 1)` — visually close, not mathematically identical |
| Blog posts section | Omitted per brief |
| Stats / key metrics block | Omitted per brief |
| Key features / benefits block | Omitted per brief |
| Some exact font weights from the React template | Rebuilt from visual inspection using DM Sans; minor weight differences possible |

---

## Reduced motion

When `prefers-reduced-motion: reduce` is set, the `.nav-slide` CSS transition is disabled via a `@media` query. The indicator still moves to the correct position instantly — no animation, no stuck state.

```css
@media (prefers-reduced-motion: reduce) {
  .nav-slide { transition: none; }
}
```

---

## Keyboard access

- Every tab has `tabindex="0"` — **Tab** moves through Home → Pages → Services → Blogs → Contact Us.
- **Arrow keys** (Left / Right / Home / End) also navigate between tabs and contract the pill to the focused item.
- **Enter or Space** activates the focused tab.
- **Tab past the last item** collapses the pill back to its expanded state.
- Focus ring: `box-shadow: 0 0 0 2px #44C486` via `:focus-visible`.

---

## Lighthouse scores (mobile)

<img width="1440" height="900" alt="Image" src="https://github.com/user-attachments/assets/d14b33ef-46cd-4e0d-b8a7-df744c858070" />

---

## Where I used AI

I used Claude (Anthropic) throughout this build as a coding assistant — for component scaffolding, debugging layout issues, and iterating on the pill animation logic. All design decisions, visual judgement calls, and architecture choices were made by me.
