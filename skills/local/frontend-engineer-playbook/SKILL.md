---
name: "frontend-engineer-playbook"
description: "Frontend engineer specialty playbook — runbook scoped to the Packlinx Next.js 16 + React + TypeScript stack covering component patterns, data fetching, accessibility, and the Korean-text rendering rules that catch most production bugs."
slug: "frontend-engineer-playbook"
metadata:
  paperclip:
    slug: "frontend-engineer-playbook"
    skillKey: "local/6062702b72/frontend-engineer-playbook"
  paperclipSkillKey: "local/6062702b72/frontend-engineer-playbook"
  skillKey: "local/6062702b72/frontend-engineer-playbook"
key: "local/6062702b72/frontend-engineer-playbook"
---

# Frontend Engineer Playbook

Specialty bundle for the Packlinx Frontend Engineer role. Scoped to the
actual stack: Next.js 16 (App Router), React 19, TypeScript, Tailwind, and
Supabase as the data backend.

Common skills handle voice, decision protocol, and company context. Do not
duplicate that content here.

## When to invoke this skill

- Starting a new component or page
- Touching data-fetching behavior (server / client / streaming)
- Touching anything that renders Korean user-facing copy
- Reviewing a teammate's frontend PR
- Debugging a production issue on the web surface

## Architecture defaults

These are defaults, not laws — but defaults exist because deviations have
caused outages. Justify deviations explicitly.

### Server vs. client components

- **Default:** Server Component. Don't add `"use client"` until you need
  state, effects, browser APIs, or interactivity.
- **Move boundary down, not up.** Wrap the smallest interactive leaf in a
  client component; keep its parents server.
- **Never mark a page-level component `"use client"`** unless every child
  needs the client runtime. That defeats RSC bundle savings.

### Data fetching

- Server Components fetch directly via Supabase server client. No
  `useEffect` round-trip from a server component.
- Client Components that need data: pass it down from a server parent
  whenever possible. Reach for SWR / React Query only for genuinely
  client-driven state (search-as-you-type, optimistic mutations).
- Cache choice is intentional:
  - `cache: "force-cache"` only for content that mutates rarely (vendor
    profile, static catalog).
  - `cache: "no-store"` for personalized or rapidly mutating data.
  - `revalidate: <seconds>` for stable-with-drift (search index, lists).
- No fetch waterfalls. If A and B don't depend on each other, fetch in
  parallel with `Promise.all`.

### Routing and rendering

- App Router. No `pages/` directory work.
- Use `loading.tsx` and `error.tsx` per route segment when the data
  fetch can be slow or fail. Don't ship blank-screen loading.
- Streaming with `Suspense` for slow segments; keep the shell fast.
- Edge runtime only when geographic latency matters and the function
  has no Node-only deps. Default is Node runtime.

### State management

- Local state: `useState`.
- Cross-component on the same screen: lift to nearest common ancestor or
  use a server component that fetches once.
- Persistent client state: URL params first (shareable, indexable),
  then `localStorage` for per-user preferences.
- Avoid Redux / Zustand / global stores until a real shared-state
  problem exists. Don't pre-install them.

## Component patterns

- **One component per file** for non-trivial components. Pure helpers
  can co-locate.
- **Props are explicit.** No `...rest` on top-level components — that
  hides what the component expects.
- **Boolean props are named for the *true* state.** `isLoading`,
  `disabled`, not `notLoaded`.
- **Server-only utilities go under `lib/server/`** with a top-of-file
  comment: `// server-only`. Importing from a client component should
  fail loudly.
- **Composition over configuration.** Three boolean props is the limit
  before splitting into named variants.
- **No prop-drilling past 3 levels.** Compose, don't drill.

## Korean-text rendering rules

These catch ~80% of production "looks wrong on prod" bugs.

- All text storage and rendering: UTF-8 NFC. Verify per
  `encoding-discipline`.
- `lang="ko"` on the `<html>` root for Korean pages; `lang="en"` for
  English-only routes.
- Line-break behavior: use `word-break: keep-all` for Korean paragraphs.
  Default `word-break: break-word` chops mid-syllable in Korean and
  looks broken.
- Numbers and Korean: use `tabular-nums` for tabular data so digits align.
- Form inputs:
  - Korean composition (한글 IME) emits `compositionstart` /
    `compositionend`. Don't run on-change validation while
    `isComposing` — you'll fight the IME.
  - Min length for Korean fields counts characters, not bytes.
- Truncation: use CSS `text-overflow: ellipsis` with `overflow: hidden`
  and a fixed line height. Don't slice strings in JS — slicing UTF-16
  surrogate pairs corrupts emoji and rare Hanja.
- Currency: `Intl.NumberFormat("ko-KR", { style: "currency", currency:
  "KRW" })`. Don't hand-format.
- Dates: `Intl.DateTimeFormat("ko-KR", ...)`. Don't render UTC strings
  to users.

## Accessibility

- Every interactive element is reachable by keyboard. `Tab` visits every
  focusable element in reading order.
- Visible focus ring on every focusable element. Don't kill default
  outlines without a replacement.
- Every form field has a `<label>` with `htmlFor`. Placeholder is not a
  label.
- `alt` text on every image. Decorative images get `alt=""` (intentional
  empty), not omitted.
- Color contrast WCAG AA at minimum. Brand colors don't override
  contrast — design system enforces.
- ARIA only when semantic HTML is insufficient. Most "ARIA-heavy"
  components can be plain semantic HTML.
- Screen-reader-only utility class (`.sr-only`) for context that's
  visual-only.

## Performance

- Targets: LCP < 2.5s on 4G, INP < 200ms, CLS < 0.1.
- Images:
  - `next/image` always. No raw `<img>` for content images.
  - Korean character file names: rename to ASCII slug at import. Some
    CDN paths break with non-ASCII URLs.
  - Hero images: explicit `priority` on the LCP image, lazy on others.
- Fonts:
  - Korean web fonts are large. Subset to the needed glyph range or use
    `font-display: swap` and load asynchronously.
  - System font fallback for body text on slow connections.
- Bundle:
  - No moment.js, no lodash full import. Use `date-fns` or `Intl`,
    cherry-pick lodash modules.
  - Dynamic-import heavy components used below the fold.
- Third-party scripts:
  - `next/script` with `strategy="lazyOnload"` for analytics.
  - No inline scripts that block rendering.

## Forms and validation

- Form library: react-hook-form + Zod schema.
- Server-side validation is the source of truth. Client-side validation
  is UX, not security.
- Error copy in Korean for user-facing forms; in English for admin
  surfaces.
- Submit-disabled state during pending mutation, with a visible spinner.
- Empty / error / success states: all designed and copy-reviewed before
  ship. No "Error: undefined" reaching users.

## Testing

- Component tests with React Testing Library + Vitest.
- Test from the user's perspective: query by role, label, text — not
  by class or test-id (test-ids only when no semantic query works).
- Test the Korean composition flow on form components that take Korean
  input.
- Snapshot tests: only for stable structural output. Don't snapshot
  rapidly-changing copy.
- E2E tests with Playwright: the 3 most-trafficked user flows
  (search → vendor profile → contact) at minimum.

## PR checklist (before requesting review)

- [ ] Server vs. client component boundary is intentional and minimal.
- [ ] Korean text rendering verified (composition, line-break, truncation).
- [ ] All images use `next/image`.
- [ ] Accessibility: keyboard nav works, visible focus, labels present.
- [ ] Empty / error / loading states designed and implemented.
- [ ] Tests added for the new behavior; existing tests still pass.
- [ ] No unintended `"use client"` added.
- [ ] LCP image is the right image (not a logo or an icon).

## Refusals

- Refuse to render user-supplied HTML without sanitization
  (`dangerouslySetInnerHTML` requires a sanitizer in the same change).
- Refuse to ship a form without server-side validation.
- Refuse to add a global state library without a written reason.
- Refuse to copy a third-party UI library wholesale without auditing
  its bundle and accessibility.

## Self-check

- [ ] Does this component do one thing?
- [ ] Could a teammate understand it in 30 seconds?
- [ ] Have I checked the Korean rendering edge cases (composition,
      line-break, character-count limits)?
- [ ] Have I justified any deviation from the architecture defaults
      above?
