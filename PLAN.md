# Trust Page — Plan

## Task
Build a static trust/security page at `/trust` on the gonzih.github.io GitHub Pages site. The page must cover CC Suite's security posture for enterprise/financial services buyers (CCOs, compliance teams).

## Site Analysis
- React SPA (Vite build), served from `index.html` with React Router
- `404.html` redirects unknown paths back into the SPA for client-side routing
- `trust/index.html` will be served *directly* by GitHub Pages (bypassing the 404 redirect), so a standalone static HTML page works perfectly
- Design language: warm cream background (`#efe9dc` / `hsl(38 30% 94%)`), Inter for body, Fraunces for headings, JetBrains Mono for code/mono, radial dot background pattern
- The content spec URL (signal-ccsuite-compliance repo) returned 404 — content built from task description

## Approaches

### A: Standalone static HTML (chosen)
- Create `trust/index.html` as a self-contained page
- Matches design tokens from existing CSS, imports same fonts from Google Fonts
- No build step required, instantly deployable
- Works because GitHub Pages serves `trust/index.html` at `/trust/` natively

### B: Modify React SPA source
- Would require the source repo, not the built output
- Not viable — we only have the compiled dist

### C: Iframe wrapper in React SPA
- Unnecessarily complex, bad UX
- Not viable

## Approach A: Standalone static HTML

### Files to touch
- `trust/index.html` — new trust page (primary deliverable)
- `index.html` — no changes needed (React SPA handles its own nav, can't easily add links from outside)

### Navigation
The main site nav is inside the compiled React bundle — we can't modify it without source. The trust page will link back to the main site but we note this limitation. The task says "add a navigation link" — we'll do best effort by adding a link *from* the trust page back to home, and note that the React nav modification requires source access.

### Content sections
1. Hero — CC Suite identity + one-sentence security statement
2. Data Handling — Anthropic commercial terms opt-out, 30-day retention, sub-processors
3. Code Transparency — GitHub links, Apache 2.0
4. DPA & Legal — how to request, what it covers
5. Compliance Roadmap — pre-SOC 2, honest framing, Q4 2026 Type I, Q2 2027 Type II
6. Incident Response — security@nexussuite.com, 48h SLA
7. Penetration Testing — planned 2026
8. CCO Checklist — SIG Lite / CAIQ mapping table

### Risks
- Cannot add nav link in React SPA without source (React bundle is compiled)
- Content spec URL 404'd — content crafted from task description
- Need to match warm-cream aesthetic without the compiled Tailwind CSS (will write custom CSS)
