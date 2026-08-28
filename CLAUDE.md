# Van Field Group — website

Single-page static marketing site for Van Field Group, Inc.

## This repository is public

**Everything in this repository, including this file, is readable by anyone on the internet.** Treat this file as a published document, not as private working notes.

This applies to every file you create or edit here, and to this file itself:

- **Never write anything here that should not be public.** No email addresses beyond what is already published on the site, no phone numbers, no client names, no internal rationale, no notes about the owner's preferences, habits, schedule, or skill level, no commercial details, no credentials or tokens of any kind.
- **Never record why something was removed** if the reason is commercially sensitive or would read badly out of context. State the rule going forward instead of the history behind it.
- **Git history is permanent.** A sensitive value committed once and deleted later remains readable in the repository forever. There is no undo. Do not commit first and clean up after.
- **If context is genuinely useful but should not be public, put it in `CLAUDE.local.md`**, which is listed in `.gitignore` and never leaves the machine. Ask before writing anything sensitive rather than deciding on your own.
- **If you are unsure whether something belongs in a public file, leave it out and ask.**

## Stack and deployment

- One file: `index.html` at the repo root. Plain HTML and CSS, all inline in that file.
- No build step, no framework, no package manager, no dependencies to install.
- Deploys automatically to GitHub Pages on every push to `main`. Live in about a minute.
- Live at https://vanfieldgroup.com

## Hard rules

- **Never delete, rename, or modify `CNAME`.** It contains only `vanfieldgroup.com` and it is what binds the custom domain to GitHub Pages. If it disappears, the site stops resolving. GitHub requires the filename in all caps, one domain, nothing else.
- **Keep everything in `index.html`.** Do not split CSS or JS into separate files. Single file is the convention here, deliberately.
- **Do not add a build system.** No npm, no bundler, no static site generator, no Tailwind. If a change seems to need one, say so and stop rather than introducing it.
- **Do not add analytics, tracking, cookie banners, or third-party scripts** unless explicitly asked. First-party inline JS is fine; the theme toggle is an example.
- **Never add an email address, phone number, or personal contact detail** that is not already present in the file. Contact details are chosen deliberately. See the public repository notice above.
- **Read `index.html` before editing it.**
- One change at a time. Commit and push each one. Say what changed.

## Theming

The site ships **dark by default**. Every first-time visitor gets dark regardless of what their OS reports. Light is opt-in through a header toggle and remembered in `localStorage`.

How it works:

- Base `:root` holds the **dark** palette and sets `color-scheme:dark`.
- `:root[data-theme="light"]` overrides with the **light** palette and sets `color-scheme:light`.
- A small inline script in `<head>`, before any stylesheet, reads `localStorage['vfg-theme']` and sets `data-theme="light"` when appropriate. It runs early on purpose, to prevent a flash of the wrong theme. Do not move it later in the document or defer it.
- The toggle button lives in `.bar-end` in the header alongside the nav. A script at the end of `<body>` handles clicks, writes to `localStorage`, and swaps the button's icon, label, and `aria-label`.
- A `<noscript>` block hides the toggle when JS is off, leaving dark as a working default.
- `localStorage` access is wrapped in try/catch. Keep it that way; it throws in some privacy modes.

**When adding or changing any color, define it in both `:root` and `:root[data-theme="light"]`.** A token defined in only one place will break the other theme. Never hardcode a hex value in a rule; that is why the statement band's colors live in `--band-*` tokens.

## Design system

Do not introduce new fonts or spacing scales. Use the tokens in `:root`.

| Token | Dark (default) | Light |
|---|---|---|
| `--ink` | `#EDEFEA` | `#111312` |
| `--ink-2` | `#A6ABA4` | `#555956` |
| `--ink-3` | `#7E837C` | `#8A8E8A` |
| `--paper` | `#0E100F` | `#ffffff` |
| `--field` | `#161917` | `#F1F1EC` |
| `--rule` | `#2A2E2B` | `#DEDED7` |
| `--signal` | `#8AA0FF` | `#1B34C8` |
| `--signal-soft` | `rgba(138,160,255,.32)` | `rgba(27,52,200,.3)` |
| `--band-bg` | `#1A1E1B` | `#111312` |
| `--band-fg` | `#EDEFEA` | `#ffffff` |
| `--band-eyebrow` | `#868B84` | `#7E837F` |
| `--band-note` | `#AFB4AD` | `#A9ADA9` |

`--signal` is ultramarine in light and a lighter periwinkle in dark, for contrast against the dark background. Use it sparingly: links and hover states only.

Typography, all from Google Fonts:

- **Archivo** — headings and display, weight 600, tight negative tracking
- **IBM Plex Sans** — body copy
- **IBM Plex Mono** — eyebrows, labels, the toggle, and the record block. Uppercase, wide letter-spacing, small.

Layout is a max-width container with a fluid `clamp()` gutter. Sections separate with generous vertical padding and single hairline rules rather than boxes or shadows. No drop shadows, no rounded corners, no gradients.

## Favicon

Five files at the repo root, referenced from `<head>`: `favicon.ico`, `favicon-32x32.png`, `favicon-16x16.png`, `apple-touch-icon.png`, `icon-512.png`. The mark is "VFG" in white on a black square, set in Archivo SemiBold. It does not adapt to theme; the black square can lose definition against a dark browser tab. Acceptable for now. `icon-512.png` is not currently referenced; it exists for a future web manifest.

## Page structure

Header (sticky, with nav and theme toggle) → Hero → Workday → statement band → Beyond the platform → The firm → Where we work → Contact colophon → Footer.

## Positioning

Van Field Group is an **ERP consultancy**. Most of the work is Workday, but the framing is deliberately wider: the firm also handles what sits outside the platform. Do not narrow this back to Workday-only language.

Founded 2014, Chicago. Privately held, independently owned. Delivery is remote and nationwide.

Independence is a structural fact about how the firm is set up, not a selling point and not a criticism of anyone. It is stated once, in the System selection card, and should stay stated once. Do not add further claims about partner status, certifications, or channel relationships in either direction.

## Audience and intent

The site exists for reference and verification rather than lead generation. Most readers already know who the firm is and are confirming details.

Consequences:

- **No CTAs.** No "Get in touch" buttons, no "Book a call," no urgency language.
- **No contact form.** Contact is a quiet colophon at the bottom.
- Copy informs. It does not persuade.

## Voice

Terse, factual, unpretentious. Should read as written by a practitioner, not a marketing department.

Avoid:

- Em-dashes. Use commas, periods, or restructure.
- Consulting-brochure phrases: "deep expertise," "passionate about," "best-in-class," "trusted partner," "we're excited to."
- Warmth language and exclamation points.
- Self-congratulation. A sentence that compliments the firm's integrity is wrong even when true.
- Numbers that will age: headcount, years in business, client counts.
- Jargon meaningful only to practitioners. Write "integration system user and security group architecture," not "ISU design."

The target is a sentence a competitor's marketing department would not write. For example: "Configuration is easy to add and expensive to remove."

## Client confidentiality

The Sectors section describes industries, not organizations. The section header reads "Our clients, not us" so the list is not misread as claims about Van Field Group itself.

**Never name a client.** **Never state or imply that Van Field Group holds government contracts, security clearances, or contract vehicles.** The firm serves clients in these industries; it does not operate in them.

Current sectors: Defense and advanced technology; Financial services; Public media and mission-driven organizations; Communications and professional services; Health technology; Retail and consumer health.

## Working conventions

- Make one change at a time and push it, rather than batching several edits into a single commit.
- Prefer the smallest change that achieves the request. Do not refactor surrounding code that was not part of the ask.
- State what changed and what to look at on the live site.
- Keep responses short.

## Open items

- `icon-512.png` is unreferenced, pending a web manifest.
- Alternate favicon files (`ALT-variant-c-*`) exist as an unused single-letter "V" design.
- The favicon does not respond to the theme toggle. An SVG favicon with a `prefers-color-scheme` query would fix it.
