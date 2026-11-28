## Working with Claude
- **This is a learning project and I write 100% of the site code** (HTML, CSS, JS, server code, config). Claude teaches, reviews, and guides, but doesn't create or edit code files, even small fixes, unless I explicitly ask. "Give me a hand" means help me do it, not do it for me.
- Don't hand over the finished code. Give one step at a time with hints and questions so I work it out, then read what I wrote and check it.
- **Teaching syntax:** show the general pattern, or a small example about something other than my site, then have me apply it. Explain why, not only how.
- **When I'm stuck, escalate slowly:** question → hint → name the concept or property → link to MDN → small similar example. Don't jump to the answer. But once I'm clearly stuck after a few rounds, be direct (long Socratic loops frustrate me).
- **Debugging:** teach me to find it myself (F12 Console, Elements, Network tab). Point at the area before pointing at the line.
- **Reviews:** tell me what's good and what's wrong, and call out bad habits plainly. Check semantics, accessibility, responsive layout, and naming.
- Introduce one new concept at a time and connect it to what I already know. I know Python and have built with NiceGUI (`pristine_pools`), so Python comparisons help.
- Prefer MDN for references. No frameworks or CSS libraries until I've learned the plain version.
- Git: I run the commands and write the commit messages. Remind me when it's a good time to commit.
- **Scope:** "do it all" / "fix it all" means the current task, not the whole to-do list. Don't start new pages or features I didn't ask for.
- Claude can edit this file and `CLAUDE.local.md`, and should keep the Status section current (short; replace stale items instead of appending a log).

## The project
Personal portfolio site, ideally at mackmusial.com (domain not bought yet). Very clean and professional, with tasteful animations. Must have: projects section, resume PDF download (done), visitor counter in the footer, works on phones and desktop.

**Story:** generalist (web, backend, DB, networking, security, some game design), heading toward AI. The self-hosted site is the proof of the full stack. Signature: "hosted on my own hardware" (an old laptop with a broken keyboard) with a live server status/uptime.

**Design (decided)**
- Palette = VS Code Dark Modern, as CSS variables in `:root` in `styles.css`: bg `#181818`, surface `#1f1f1f`, text `#cccccc`, muted `#9d9d9d`, accent `#4daafc`, button `#0078d4` / hover `#026ec1`, white button text. Accent used sparingly.
- Mack chose a multicolor look: spinning cyan→blue→violet→pink ring around the circular hero photo, and 4 soft blurred glows in ring colors (pink top-left, cyan top-middle, violet top-right as the main light on the photo, fuchsia bottom). Keep them calm enough that text stays readable.
- Inspiration only, never copies: Webflow "Developer X" and "BRIAN", and a "DevPort" template (`insparation/dev_portfolio.webp`).
- Huge bold name as the h1, small labels, pill-style skill tags, floating glass code card on the photo, falling snowflakes.
- Structure: home page = landing screen (name, photo, glows, resume + "View My Projects" buttons, About, skill pills) + slim footer (©, server status pill, visitor count). Projects on their own `projects.html` sharing `styles.css` (empty for now; homepage gets finished first, Mack's call).
- Photo `assets/mack-musial.jpg` (1000×1250, EXIF stripped). Resume `assets/Mack_Musial_resume.pdf`.

**Ideas, not decided:** project cards (screenshot, one-liner, tech tags, Code/Live Demo links); scroll reveal with `IntersectionObserver` + reduced-motion; auto-updating footer year via JS (kept static for now); a live uptime card instead of fake stat cards ("50+ Projects"); "Ask about Mack" AI chat run on Mack's own hardware with a local model (Llama 3.2 3B tested at ~21 tok/s). Build it after the visitor counter API (same `fetch` → Python API pattern). It needs rate limiting, answers limited to Mack's real facts, and an "AI-generated, may be wrong" note.

**Must be true before launch:** About copy claims "I wrote every line" (several parts were written or pasted by Claude, see below) and "runs on an old laptop"; footer claims self-hosting, server status, and visitor count; the "AI Developer" tagline relies on the local chatbot. The "Server offline" default copy reads as broken and needs Mack's wording. Decide on a public email.

## Hosting plan
Old laptop with a destroyed keyboard, Ubuntu Server LTS (installed with a USB keyboard, then SSH from the Mac). Lid closed via `HandleLidSwitch=ignore` in `logind.conf`. Nginx serves the static site. Cloudflare Tunnel for public access (no port forwarding, hidden home IP, HTTPS). Counter: small Python API + SQLite. Security before going public: SSH keys only, `ufw`, automatic updates.

## Roadmap
1. HTML ✅ 2. CSS basics ✅ 3. Responsive (mostly done) 4. Project cards + resume (resume ✅) 5. Animations (in progress) 6. JavaScript: DOM, events, `fetch` 7. Visitor counter API + SQLite (also a status route; JS toggles a `.is-online` class Mack writes and swaps the text) 8. Ubuntu laptop, Nginx, tunnel, domain 9. Polish: accessibility, Lighthouse, SEO/social tags.

## Status (updated 2026-11-28)
**Built so far:** semantic skeleton; hero flex row (text + `.hero-photo` wrapping `.avatar-ring` conic ring via `@property --angle` + `@keyframes`, `.avatar` uses `aspect-ratio: 1`, `object-fit: cover`); h1 `clamp()`; shared `.button` class with `.resume-link` / `.project-link` backgrounds; `.code-card` (absolute, frosted, mac dots, `<pre><code>` with syntax-color spans, `aria-hidden`); glows (`.glows`, absolute in `body { position: relative }`, radial gradients + blur); Christmas snowflakes (`.snowflakes`, 8 spans holding `&#10052;` ❄, shuffled negative delays, `@keyframes fall` with 3 stops: 0% `translateX(0) translateY(-100vh) rotate(0deg)`, 50% `translateX(5vw) translateY(0) rotate(180deg)`, 100% back to `translateX(0)`/`rotate(0deg)` at `translateY(100vh)`, so flakes sway right and back and reverse spin; a comment explains going back to dust dots after the holidays); About section + skill pills incl. C++ (`:nth-child(5n+k)` colors); footer (sticky via `body` flex column + `main { flex-grow: 1 }`, red offline `.status-dot`); `.container` wrapper; breakpoints at 1040px (stack + center) and 600px (phone); `prefers-reduced-motion` stops ring and snowflakes; `prefers-contrast: more` hides glows; iOS safe areas (`viewport-fit=cover`, `env(safe-area-inset-top)`).

**Badges so far (committed, e5ca49b):** 3 `.badge` divs in `.hero-photo` (server top-left, code bottom-left, AI bottom-right; code card covers top-right). `.badge` holds shared stuff (absolute, 36×36, radius 8px, flex centering); modifiers hold position, gradient, `transform: rotate()` (10deg / -10deg / 15deg). Inline Lucide SVGs (server, code-xml, cpu-ai) at 24×24 (Mack's choice), `stroke="currentColor"`, Lucide classes removed, index.html formatted. Simulator check on iPhone 17: no horizontal scroll.

**In progress: liquid glass code card** (Mack's detour, branch `liquid-glass-code-card`). Done: bg alpha 0.4, blur 18px, `inset` top highlight, drop shadow, slash `rgb()` syntax, one shadow per line, `backdrop-filter: blur(18px) saturate(1.5)` (Mack learned: spaces chain functions, commas separate list items, a `;` ends the declaration). Left: delete trailing spaces after `backdrop-filter:` / `box-shadow:`; add a bottom inner shadow (second `inset`, negative y) for depth; then merge the branch. True refraction needs an SVG filter in `backdrop-filter` = Chrome only, so an exact Apple match isn't possible.

**Then back to badges:** placement (corners of the square are empty because the circle doesn't reach them; nudge onto the ring rim with offsets, try uneven angles; mind the code card on phones), `@keyframes float` (must keep the rotate, since both use `transform`: either repeat rotate in keyframes or use the separate `rotate` property), reduced-motion. Later Christmas ideas: CSS Santa hat on the ring, red/green glows, string of lights.

**Not hand-written by Mack (review or practice these later, they matter for the "every line" claim):** ring code (pasted), glow code, footer status pill (nested flex, `box-shadow`, inline-block dot), the 1040/600 media queries, `.button` refactor, code card positioning, `:focus-visible` outline, `prefers-contrast` rule, badge gradients, Copilot's code-card alpha/blur values.

**Concepts Mack has learned:** rule anatomy, inheritance, UA styles, classes vs ids vs element selectors, descendant, `:nth-child`, pseudo-classes, source order and "last wins"; box model, `box-sizing`, TRouBLe shorthand; px vs rem vs vw, `clamp()`; flex (parent vs direct children, direction, justify/align, wrap, gap, shrink, `min-width: auto`); position relative/absolute/fixed, `inset`, `%` relative to the positioned parent, shrink-to-fit, absolute elements take no space; z-index, `overflow`; gradients, rgb alpha, `filter`; transitions, keyframes, `transform` over `top`, negative `animation-delay`, several transform functions in one `transform`, middle keyframe stops (`%` = when, a missing 100% falls back to the element's own position); media queries; relative paths, `href` vs `src`; DevTools Styles (⚠️ crossed-out = invalid), box model diagram, Network tab, device mode; HTML entities; `aria-hidden`; safe areas; `rotate()` needs a unit, `transform-origin` defaults to center; flex centering trio; shared vs modifier classes (refactor); inline SVG basics (`viewBox`, `currentColor`); `inset` and comma-separated multiple `box-shadow`s; space-chained `backdrop-filter` functions vs comma lists; stale browser cache (hard refresh, Disable cache); git diverged branches.

**Open items**
- Snowflakes are in "Christmas mode" (revert after the holidays). Optional: slower 15–25s durations.
- Badge hex colors mix upper/lower case, and `#8B5CF6` isn't the ring's `#7c3aed`; consider `:root` vars.
- "Server online" is hardcoded until the status API exists.
- From 451 to 1231px, check that the code card doesn't cover the pills/buttons.
- Code card text at phone size (~0.45rem) is too small to read; suggest ≥0.65rem.


## Dev setup
- Mac (sometimes Windows: there use Ctrl instead of Cmd). Live Server extension → http://127.0.0.1:5500, auto-reloads. Hard refresh with Cmd/Ctrl+Shift+R.
- Live Server actually listens on all interfaces, so stop it on public Wi-Fi. Phone preview: the Mac's LAN IP (`ipconfig getifaddr en0`):5500, viewed through iPhone Mirroring (the firewall may need to allow Code). Mack's phone is an iPhone 15 (iOS 26 Safari).
- iOS Simulator: iPhone 17 via `xcrun simctl`, viewed in DeviceHub (`/Applications/Xcode.app/Contents/Applications/DeviceHub.app`, no Simulator.app here). `127.0.0.1:5500` works inside it. Inspect from Mac Safari → Develop menu. Shut down: `xcrun simctl shutdown booted`.
- Work on two machines: `git pull` before starting, push when done.
- Fallback: `python3 -m http.server 8080 --bind 127.0.0.1`.
- Live Server's Cmd+L chords block VS Code's Cmd+L. Copilot next-edit suggestions are on (Esc dismisses, Tab accepts; watch for garbage suggestions).
- Impeccable skill is installed; use it for critique/audit only, Mack writes the code.
