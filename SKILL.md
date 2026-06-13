---
name: vercel-website-build
description: Build a multi-page premium website (HTML/CSS/JS) and ship it live on Vercel. Use when user asks to "build a website", "design a landing page", "create a site for [industry]", "make me a website", or wants a professional deployed site for coaching, investment, advisory, agency, SaaS, or any service business. Output is a live *.vercel.app URL plus source files in the user's chosen folder. Not for editing existing Wix/Squarespace/Webflow sites.
---

## When to use
User wants a professional, designed, *deployed* website (3–8 pages) hosted on Vercel — not a Wix/Squarespace template, not a single-page artifact.

## Step-by-step

1. **Brief — read the Website Strategy Brief.** User provides either an **attached file** (PDF / DOCX / MD / TXT) or a **Google Doc link**. Read the brief: use the Read tool for attached files, or the Google Drive MCP (`read_file_content` / `download_file_content`) for the link. Extract the standard fields: company name, slogan, 1-line positioning, 3–4 target audiences, 3–5 brand personality words, visual mode (dark / editorial / light), what to avoid, contact info (email, phone, principal name + role). If a required field is missing or ambiguous, ask the user for *only* that field before proceeding — do not re-ask anything the brief already covers. If neither a file nor a link is provided, fall back to AskUserQuestion to collect the same fields.

2. **Match a design system to the brand.** Existing options: dark sci-fi for tech/fintech/aerospace (`website1-design`); editorial print for coaching/wellness (`truefulfill-design`); navy + gold institutional (`ahsdesign-design`). **If none fit**, ask the user for one or two reference websites they love (URL or screenshot), then invoke the `skill-creator` skill to scaffold a new design system from those references — extract palette, typography, motion language, layout principles — and save as a new `*-design` skill. State pick + one alternative, confirm before building.

3. **Propose page structure** tailored to industry. *Coaching:* Home, About, Services, Process, Stories, Contact. *Investment:* Home, Thesis, Portfolio, Approach, Team, Contact. *Advisory:* Home, Practice, Engagements, Insights, Team, Contact. *Any other business (default):* Home, About, Services, Contact — expand only if the brief calls for it (e.g., add Portfolio, Pricing, FAQ, Blog). Confirm before building.

4. **Build Home first.** Single self-contained HTML: hero (eyebrow + headline + subhead + two CTAs) → positioning manifesto → three-pillar/service block → data or social-proof strip → criteria/offer grid → principles → CTA band → footer. Inline CSS + JS. Add `<canvas>` particles, IntersectionObserver scroll-reveal, mouse parallax. Stop, share, get feedback before continuing.

5. **Build remaining pages one at a time.** Reuse identical nav, footer, design tokens, type pairing, SVG logo. Cross-link cleanly. Highlight the active page in nav.

6. **Logo as inline SVG using `currentColor`** so it inherits color and adapts to any background. Drop any background block from the source image. 28–34px in nav, 42px in footer.

7. **Defensive coding (non-negotiable).** Wrap ALL JS in `try {} catch {}`. Add `@keyframes revealFallback` so `.reveal` elements auto-fade-in after 0.6s even if JS fails. Feature-detect IntersectionObserver. *One JS syntax error can leave a deployed page looking empty — defend against this.*

8. **Prep for Vercel.** Rename files for clean URLs (`index.html`, `about.html`, etc.). Update all internal nav links. Add `vercel.json` with `{"cleanUrls": true, "trailingSlash": false}`. Add `.vercelignore` for any duplicates.

9. **Deploy.** **(a) GitHub (preferred, auto-redeploys on push):** `git init && git add . && git commit -m "Initial" && git push` to a new repo, then connect at `vercel.com/new`. **(b) CLI:** `cd folder && npx vercel --prod` — first run prompts login + project name.

10. **Verify live.** Fetch the deployed URL, confirm every page renders (no blank pages), internal links work, logo loads, design matches local, mobile breakpoints (1024px, 640px) hold. Fix and redeploy if anything's broken.

## Quality bar — a great website hits all of these
- **5-second hero**: visitor instantly knows what you do / for whom / next action
- **One focal element per section** with extreme negative space, no clutter
- **Premium type stack**: display + body + mono, paired intentionally
- **Subtle motion**: reveals, particles, parallax — never distracting
- **Restraint over hype**: short copy, real specifics, zero buzzwords
- **Consistent design tokens** (colors, spacing, components) across all pages
- **Defensive JS**: try/catch + CSS keyframe fallback — page never appears empty
- **Mobile-responsive**: 1024px and 640px breakpoints tested
- **Clean URLs** without `.html` extensions
- **Fast Lighthouse**: <1.5s LCP, accessible contrast, no console errors
