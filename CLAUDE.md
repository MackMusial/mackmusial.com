## Working with Claude
- **This is a learning project and I write 100% of the site code** (HTML, CSS, JS, server code, config). Claude teaches, reviews, and guides, but doesn't create or edit code files, even small fixes, unless I explicitly ask. "Give me a hand" means help me do it, not do it for me.
- Don't hand over the finished code. Give one step at a time with hints and questions so I work it out, then read what I wrote and check it.
- **Teaching syntax:** show the general pattern, or a small example about something other than my site, then have me apply it. Explain why, not only how.
- **When I'm stuck, escalate slowly:** question → hint → name the concept or property → link to MDN → small similar example. Don't jump to the answer.
- **Debugging:** teach me to find it myself (F12 Console, Elements, Network tab). Point at the area before pointing at the line.
- **Reviews:** tell me what's good and what's wrong, and call out bad habits plainly. Check semantics, accessibility, responsive layout, and naming.
- Introduce one new concept at a time and connect it to what I already know. I know Python and have built with NiceGUI (`pristine_pools`), so Python comparisons help.
- Prefer MDN for references. No frameworks or CSS libraries until I've learned the plain version.
- Git: I run the commands and write the commit messages. Remind me when it's a good time to commit.
- Claude can edit the notes files (`CLAUDE.local.md`) and should keep the progress section below current.

## The project
Personal portfolio site, ideally at mackmusial.com (domain not bought yet). Very clean and professional, with tasteful animations.

**Must have**
- Projects section showing what I've built.
- Resume download button (PDF).
- Visitor counter in the footer.
- Works on phones and desktop.

**Design direction (decided 2026-11-11)**
Mack wants it to really stand out, not just look acceptable. Inspired by two Webflow templates (dark slate "Developer X" and black/crimson "BRIAN"), used as inspiration only, not copies.
- Palette matches VS Code's Dark Modern theme (chosen 2026-11-11), stored as CSS variables in `:root` in `styles.css`: bg `#181818`, surface `#1f1f1f`, text `#cccccc`, muted `#9d9d9d`, accent `#4daafc`, button `#0078d4` / hover `#026ec1` with white text (all pass contrast). One blue accent, used sparingly.
- Huge bold headline, small uppercase labels, circular photo in the hero (changed from rectangular on 2026-11-11, done in CSS, not by editing the image).
- Signature element: "served from a laptop with a broken keyboard" status badge with live uptime.
- Story: generalist (web, backend, DB, networking, security, some game design), heading toward AI. The self-hosted site is the proof of the full stack.
- Photo: `assets/mack-musial.jpg`, cropped by Claude on 2026-11-11 at Mack's request: 4:5 portrait at 1000×1250, 236 KB, EXIF metadata stripped. The uncropped 3.2 MB original is still in git history.

**Ideas, not decided**
- Project cards: screenshot, one-line description, tech tags, Code and Live Demo links.
- Light/dark toggle that remembers the choice.
- Scroll-reveal animations using `IntersectionObserver`, respecting `prefers-reduced-motion`.
- "Served from a laptop with a broken keyboard" footer badge with live uptime.
- "Ask about Mack" AI chat that answers employers' questions from Mack's real info (resume, projects). Build after the visitor counter API, since it's the same JS `fetch` → Python API pattern. Needs: API key kept server-side, rate limiting and a spending cap, answers limited to provided facts, and an "AI-generated, may be wrong" note.

## Hosting plan
Old laptop with a destroyed keyboard, running Ubuntu. Not set up yet.
- Ubuntu Server LTS, installed with a USB keyboard, then managed over SSH from the Mac.
- Keep it running with the lid closed (`HandleLidSwitch=ignore` in `logind.conf`).
- Nginx serves the static site.
- Cloudflare Tunnel for public access: no port forwarding, home IP stays hidden, HTTPS included.
- The counter needs a server side because HTML/JS alone can't share a number between visitors. Leaning toward a small Python API + SQLite, since I already know Python and Node isn't installed.
- Security basics before going public: SSH keys only, `ufw`, automatic updates.

## Roadmap
1. HTML: page structure and semantic tags.
2. CSS: box model, variables, typography, Flexbox, Grid.
3. Responsive layout.
4. Project cards and resume download.
5. Animations: transitions, keyframes, scroll reveal.
6. JavaScript: DOM, events, theme toggle, `fetch`.
7. Visitor counter API + SQLite.
8. Ubuntu laptop, Nginx, tunnel, domain.
9. Polish: accessibility, Lighthouse, SEO/social preview tags.

## Progress
- 2026-11-10: Project folder and git repo created. No site code yet. Next: Lesson 1, HTML skeleton in `index.html`.
- 2026-11-10: Lesson 1 in progress. Learned semantic vs generic tags and nesting. Wrote `index.html` with `<header>`, `<main>`, `<footer>`. Added `<html>`, `<head>`, `<body>`, `<title>`, and a projects `<section>` with an h1/h2/h3 outline. Still missing the doctype. F12 Elements exercise not done yet.
- 2026-11-11: Lesson 1 done. Added doctype, fixed indentation, committed and pushed `index.html` (GitHub repo is private). Can explain `lang`, `charset`, `viewport`, and `<link>`. Open items: decide on public email before going live; real copy to replace placeholders; hasn't yet used DevTools or read the server log. Then saw a 404 in the Console and server log, created `styles.css`, learned CSS rule anatomy, inheritance, user agent stylesheets, and the Styles panel.
- 2026-11-11: Mack asked to stop isolated exercises and learn by building real parts of the site, with concepts taught along the way. Still writes all the code. Resume link now has `.resume-link` styles. Covered classes, `display` types, and the box model intro.
- 2026-11-11: Resume button finished and committed: green/darkgreen (passes contrast), `border-radius`, `transition`, `:hover` + `:focus-visible` via a comma selector list. Learned the browser cache (Cmd+Shift+R), DevTools live editing, and pseudo-classes. Switched preview to Live Server. Small tidy-ups still open in `styles.css`: the space in `green ;`, a blank line between rules, one selector per line. Next: page-wide layout and typography on `body` (font, max-width, centering with margin).
- 2026-11-11: Picked the design direction and the VS Code Dark Modern palette. Built CSS variables in `:root`, a `body` rule, a 1200px centered wrapper (class currently `.article`, should be renamed), and `p { max-width: 65ch }`. Hero copy written by Claude at Mack's request: intro "Hi, I'm Mack Musial", h1 "From server to screen.", and a broken-laptop sentence that promises a database and firewall, so it must be true before launch. Both photos were committed and pushed by accident; decided not to rewrite history. Turned on the macOS firewall (signed apps not auto-allowed, stealth on); blocking not yet tested from a phone. Open tidy-ups: font line `'sans-serif'` → `system-ui, sans-serif`, link color rule using `--accent-color`, `<title>` text, rename `.article`. Next: rename the small photo to `assets/mack-musial.jpg`, add `<img>` with alt at the end of `<header>`, then Flexbox for a text-left/photo-right hero. Resize the full photo later.
- 2026-11-11: Fixed the broken hero image himself using the Network tab (404 → 200). Learned relative paths (resolved from the HTML file's folder) and the difference between `href` (fetched on click) and `src` (fetched on page load). First put `assets/` on the `href` by mistake, then found the right line.
- 2026-11-11: Claude cropped and compressed the photo at Mack's request. Mack removed the `<a>` wrapper and added `class="hero-photo"` + `.hero-photo { border-radius: 50% }` to make it round. Bugs hit along the way: the `src` attribute name got deleted (`<img="...">`), so the browser read the whole thing as the tag name, and the class/selector names didn't match (`.image` vs `hero-photo`). It took a few hints, and in the end Claude named `src` directly. Learned that a class selector only styles the element carrying that class.
- Pick up here: commit (after tidying the double spaces and blank line on the `<img>` line). Then the oval → circle fix: `aspect-ratio: 1` (let Mack see the squish), then `object-fit: cover`, and maybe `object-position` to keep the face centered. Then Flexbox for the hero. `resume.pdf` doesn't exist yet, so the resume link is a 404.

## Dev setup (Mac)
- Preview with the Live Server extension (`ritwickdey.liveserver`, installed 2026-11-11): right-click `index.html` → Open with Live Server → http://127.0.0.1:5500. Auto-reloads on save. Despite the `host` setting of 127.0.0.1, it actually listens on all interfaces (`*:5500`, checked 2026-11-11), so it's reachable from the same Wi-Fi. Use the macOS firewall (deny incoming connections for VS Code) or stop it on public Wi-Fi.
- Fallback: `python3 -m http.server 8080 --bind 127.0.0.1` → http://localhost:8080 (no auto-reload; hard refresh with Cmd+Shift+R). Port 8000 gave `PermissionError` on 2026-11-11 (cause unknown).
