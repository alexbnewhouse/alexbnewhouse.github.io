# UI/UX Rethink & Recommendation Plan

_Author: planning doc for alexbnewhouse.github.io_
_Last updated: 2026-04-29_

---

## 1. Strategic frame: who is this site for?

Your site has to do double duty for **three distinct audiences**, each of whom lands on it for ~10 seconds before deciding whether to keep reading:

| Audience | Primary question they're asking | What they want to see in <10s |
|---|---|---|
| **Hiring committees (R1 / SLAC)** | "Is this person a serious scholar with a clear research identity and JMP?" | Field, JMP title + 1-line pitch, advisors, publication venues, CV link |
| **Policy / think tank / industry (Trust & Safety, AI labs, gov)** | "Can this person operationalize research into practice? What can they do?" | Methods stack, named impact (Jan 6 Cmte, Roblox, GNET, $1.38M), media credibility |
| **Students & collaborators** | "Can I learn from / work with this person?" | Tutorials, teaching, contact, openness signals |

Your current site **mostly serves audience #1** but buries audience #2's signals (which are arguably your strongest differentiator from other ABDs) and treats audience #3 as an afterthought.

**The core UX thesis:** Lead with what makes you uncommon — *a political scientist who has actually shipped at the intersection of AI, extremism, and policy* — and let the traditional academic signals support that, not the other way around.

---

## 2. Audit of the current site

### What's working
- Clean Quarto + lumen baseline; fast, accessible by default.
- `index.qmd` uses the `trestles` template with profile picture, social links, CV download — solid.
- Navbar is short and scannable.
- Content is dense and substantive (the hard part is done).
- SEO basics are present (description, OG image, Twitter card).

### What's not working

**Information architecture**
- Navbar items are ambiguously sequenced: `Research | Teaching | Dissertation | CV | Writing | Statements`. "Statements" is a job-market term most non-academics won't recognize, and "Dissertation" as a top-level item competes with "Research."
- No dedicated entry point for **policy/industry/media** audiences — your most marketable angle is hidden inside long prose paragraphs.
- `political-text-classification.html` (a real technical artifact) is only reachable via a single inline link buried in `research.qmd`. This is your portfolio piece for industry — it should be first-class.
- `psci_2075_study_guide.qmd`, `intd1027-syllabus.qmd` exist as siblings of top-level pages without a clear hub; this will get worse as you add courses.

**Visual hierarchy**
- `styles.css` is empty. The site is using stock lumen with no personality. Lumen reads as "generic Bootstrap academic."
- Homepage is wall-of-text after the trestles intro. No visual chunking, no scannable cards, no images other than the headshot.
- All headings look the same weight; nothing draws the eye to the JMP, the funding total, or the media list.
- Inline statistics (`$1.38M`, `52 students`, `276K views`) are buried in body copy when they should be hero numbers.
- No favicon, no consistent accent color, no typographic identity.

**Content & messaging**
- Homepage subtitle "Computational Political Scientist" is accurate but generic. It doesn't telegraph *what* you study or *why a search committee should keep reading*.
- The "Research Statement" page and the `## Research Statement` section on `research.qmd` likely duplicate. Same for teaching.
- The Job Market Paper is mentioned in a callout but not given pride of place.
- Media coverage is listed as a bulleted run-on; could be a logo wall.
- No "What's new" / news feed — committees and journalists love a recent-activity signal.

**Conversion / contact**
- Email is present but there's no scheduling link, no "request a paper" CTA, no clear "I'm hiring committees, click here" path.
- CV PDF link is good but appears in many places inconsistently (sometimes button, sometimes plain link).

**Accessibility & polish**
- No skip-to-content link visible.
- Heavy reliance on bold and bullet lists with no semantic structure.
- Heading levels likely skip in places (H2 → H4) inside long pages.

---

## 3. Recommended information architecture

Cut the navbar to **6 items max** with one clear primary CTA:

```
Alex Newhouse                            [ Search ]   [ CV (PDF) ]  ← primary button
─────────────────────────────────────────────────────────────────
Research   Writing   Teaching   Tools & Code   Speaking & Press   About
```

Mapping:
- **Research** → consolidates `research.qmd` + `research-statement.qmd` + `dissertation.qmd`. Use tabs or in-page anchors. Lead with JMP.
- **Writing** → `posts.qmd` (rename from "Writing" to "Notes" or "Blog" if you prefer; "Writing" is fine).
- **Teaching** → consolidates `teaching.qmd` + `teaching-statement.qmd` + tutorial hub + syllabi. One page, sectioned.
- **Tools & Code** *(new)* → `political-text-classification.html`, GitHub repos, models, datasets. This is your industry/T&S calling card.
- **Speaking & Press** *(new)* → media coverage, invited talks, podcast appearances. Currently this content is scattered.
- **About** → short bio, full contact info, photo, "currently" section.

**Hide** "Dissertation" and the "Statements" submenu from the navbar — surface them as anchored sections inside Research and Teaching, plus prominent in-page links. Direct URLs still work.

---

## 4. Homepage (`index.qmd`) redesign

Replace the current trestles + wall-of-text layout with a **scannable, hierarchy-driven hero** in this order:

1. **Hero band** — name, role, one-sentence elevator pitch, headshot, primary CTAs (CV PDF, Email, Scholar). One-liner example:
   > *PhD candidate (CU Boulder) studying how online communities turn into offline political violence — using transformer NLP, networks, and causal inference.*

2. **"On the market" callout** *(seasonal, while applicable)* — single-line callout box: JMP title, one-sentence finding, link to PDF/abstract, link to job-market materials packet.

3. **Three-card "what I do"** row (Research / Teaching / Tools), each with 1 sentence + a link. Use Quarto's `.grid` + `.g-col-4` or a card layout.

4. **Selected work** — 3–5 papers max, each one-line, linked. Don't try to list everything; that's what the CV is for.

5. **Impact strip** — visual numbers row: `$1.38M funded · 52 students mentored · 276K reads · 3 courses as IoR`. This belongs as styled stat tiles, not prose.

6. **As featured in** — a horizontal logo strip (or styled text strip if logos are licensing-iffy). This is a credibility shortcut policy/industry readers immediately recognize.

7. **Recent** — 3 most recent posts/talks/papers with date stamps. Pulls automatically from `posts/` and a manually maintained `news.yml`.

8. **Contact / footer** — email, social, "best way to reach me," short response-time note.

Each section should be 1–2 screens of scrolling, not 6.

---

## 5. Visual design system

Define a small, consistent system in `styles.css`. Don't reinvent — just give the lumen theme a personality.

### Type
- **Headings:** a serif with character (e.g., `Source Serif 4`, `Crimson Pro`, or `Newsreader`) — signals scholarship without being stuffy.
- **Body:** keep the system sans (Helvetica/Inter) for readability.
- **Code/mono:** `JetBrains Mono` or `IBM Plex Mono` (you teach R; show it).
- Set a comfortable measure (max-width ~70ch on prose pages).

### Color
Pick **one accent** + neutrals. Suggested palette (CU-adjacent without being literal):
- Primary accent: a deep slate-indigo or oxidized copper (`#7B3F00`-ish) — distinctive, prints well on a CV.
- Ink: `#1a1a1a`
- Paper: `#fafaf7` (warm off-white)
- Muted: `#6b6b6b`
- Link: accent, underlined on hover only.

Avoid CU Boulder gold as primary; it's loud on screen and ties you visually to one institution at the exact moment you want to signal portability.

### Components to add via CSS
- `.stat-tile` — large number, small label, used in impact strip.
- `.paper-card` — title, venue, year, one-line summary, link icons (PDF, code, data).
- `.callout-jmp` — distinctive callout style for the job-market paper.
- `.logo-strip` — horizontal grayscale media logos.
- `.tag` — small pills for methods/topics (e.g., `NLP`, `networks`, `extremism`).
- Improved blockquote and `::: callout-note` styling.

### Other
- **Favicon** — set one in `_quarto.yml`. Even a monogram SVG.
- **Open Graph image** — replace the cropped headshot with a custom 1200×630 card showing name + tagline + photo. Massively improves shareability when others link your work.
- **Dark mode** — Quarto supports it cheaply; toggle in navbar. Free polish points.

---

## 6. Page-by-page recommendations

### `research.qmd`
- Move "Research Statement" prose into `research-statement.qmd` only; keep `research.qmd` as a structured catalog.
- Reorder: **JMP → Active projects → Peer-reviewed → Book chapters → Under review → Public writing**.
- Each publication as a `.paper-card` with: title, venue, year, 1-sentence finding, links (PDF / DOI / code / data / press).
- Add a small filter UI by topic tag (extremism, gaming, AI, methods) — Quarto has `listings` that can do this with frontmatter on each paper if you split them into a `papers/` collection. Optional, but cool.
- Pull citation metrics into a small badge row, not a paragraph.

### `cv.qmd`
- Keep the HTML CV; ensure the **PDF is the source of truth**, generated from a single LaTeX/Typst file, and the HTML is auto-derived (or hand-mirrored once per cycle).
- Pin the "Download CV (PDF)" button to the top-right of the page on scroll.
- Add a "Last updated: <date>" line — search committees notice.

### `teaching.qmd`
- Lead with **Teaching Impact** numbers and one student quote (if you can ethically source one).
- Move philosophy below the "what I've taught" table — committees skim *what* before *why*.
- Promote the tutorials into a proper `tutorials/` index page with a card grid; today they're 6 sibling files at the workspace root, which won't scale.
- Each tutorial card: title, level (intro/intermediate), estimated time, prereqs, "Run in RStudio" tip.

### Tutorials (1–6)
- Add a consistent header partial: tutorial number, course context, est. time, "next/previous tutorial" nav at top and bottom.
- Add a small "Was this helpful?" mailto link at the bottom.

### `posts.qmd`
- Already a Quarto listing — add categories, reading time, and ensure RSS is discoverable from the navbar (small icon).
- Pin the most important post at the top via `pinned: true` + custom CSS.

### New: `tools.qmd` (Tools & Code)
- Cards for: `political-text-classification`, any GitHub repos worth featuring, datasets you've released, dashboards.
- For each: 1-line problem statement, methods, result/metric, link to repo + paper + demo.

### New: `speaking.qmd` (Speaking & Press)
- Three sections: **Invited talks**, **Conference presentations**, **Media**.
- Media as a logo strip + a chronological list with outlet, headline, date, link.
- Add a "Book me to speak" mailto with a short blurb on topics.

### `dissertation.qmd`
- Make it a **single, designed page** with: title, abstract, committee, status, chapter-by-chapter status table (use a Quarto table), and links to any chapter drafts you're willing to share.
- This page becomes a great link to drop in cold emails.

---

## 7. Trust, recency, and credibility signals

Search committees and policy people both reward freshness. Add:

- **`_news.yml`** + a homepage "Recent" widget. Five most recent items, dated, mixing papers/talks/press.
- **"Last updated" stamps** on `cv.qmd`, `research.qmd`, `teaching.qmd`.
- **Persistent IDs** linked from the homepage: ORCID (✅ have), Google Scholar (✅), OpenAlex (add), Semantic Scholar (add). These help bots and humans verify you.
- **"Currently"** block in About: 2–3 lines on what you're working on this term. Updated quarterly.

---

## 8. Job-market polish (seasonal)

While on the market, add:

- A **`/jobmarket`** (unlisted-from-navbar but linkable) page with: JMP abstract, PDF, references (with permission), teaching evals/letters summary, sample syllabi, statements. One link to send to chairs.
- An **availability line** on the homepage: "On the academic job market, 2026–27."
- Make sure the **Open Graph card** says "Job market 2026–27" in small type during the cycle.

---

## 9. Accessibility & technical hygiene

- Ensure heading levels never skip (H1 → H2 → H3).
- All images get meaningful `alt` text (your headshot's is fine; tutorial figures may not have any).
- Color contrast ≥ 4.5:1 for body text against background. Test the chosen accent.
- Add `lang="en"` (Quarto does by default; verify).
- `prefers-reduced-motion`: avoid scroll-triggered animations.
- Run Lighthouse — target ≥95 across the board. Lumen + minimal CSS should get there easily.
- Set up a `404.qmd` with a search box and links to the main pages.

---

## 10. SEO & discoverability

- Add a `sitemap.xml` (Quarto can emit one) and link it in `robots.txt`.
- Per-page `description:` frontmatter (you have some; ensure all pages have it, ≤155 chars).
- Per-page `image:` frontmatter for OG cards (or generate per-page cards from a template).
- Use **schema.org Person / ScholarlyArticle** JSON-LD on the homepage and paper pages. One template snippet, big payoff for Google Scholar / Knowledge Graph.
- Ensure the canonical name "Alex Newhouse" appears in the H1 of the homepage and in `<title>` consistently.

---

## 11. Phased execution plan

Don't do this as one big-bang rewrite. Three phases.

### Phase 1 — High-leverage, low-effort (this week)
1. Trim navbar to 6 items; add CV button as primary action.
2. Write `styles.css` with the design system (type, color, basic component classes).
3. Add favicon + custom OG image.
4. Rewrite homepage (`index.qmd`) with the hero → cards → impact strip → recent structure.
5. Add a "Last updated" stamp to `cv.qmd` and `research.qmd`.
6. Promote `political-text-classification.qmd` with a homepage card.

### Phase 2 — Structural (next 2–3 weeks)
7. Build new `tools.qmd` and `speaking.qmd` pages; migrate scattered content into them.
8. Build `tutorials/` hub page; move tutorial files into a subfolder (update links).
9. Restructure `research.qmd` into paper-card collection; add tag/filter if desired.
10. Add `_news.yml`-driven "Recent" widget on homepage.
11. Add JSON-LD schema to homepage and `cv.qmd`.

### Phase 3 — Polish (ongoing)
12. Dark mode toggle.
13. Per-page OG cards.
14. `/jobmarket` packet page (seasonal).
15. Accessibility audit + Lighthouse fixes.
16. Logo wall for media (verify usage rights or use plain-text alternative).

---

## 12. What to explicitly *not* do

- Don't switch off Quarto. It's the right tool; the issues are content/design, not platform.
- Don't add a flashy hero animation, particle background, or auto-typing tagline. Anti-signal for academic committees.
- Don't try to make this look like a startup landing page. Stay closer to *NYT Opinion columnist's personal page* than *YC seed-stage SaaS*.
- Don't add a chatbot, a newsletter popup, or analytics consent banners beyond what's strictly needed.
- Don't list everything. The CV is the canonical exhaustive record; the site should curate.

---

## 13. Success criteria

You'll know the redesign worked when:

- A search committee chair can find your JMP, advisors, and CV in under 10 seconds without scrolling past the fold.
- A T&S/policy recruiter can find evidence of shipped technical work (the BERT classifier, datasets, code) within one click of the homepage.
- A student can find tutorials and your email within one click.
- The site looks recognizably *yours* — not a Quarto default — across homepage, CV, and a paper page.
- Lighthouse: Performance ≥95, Accessibility ≥95, SEO ≥95.
