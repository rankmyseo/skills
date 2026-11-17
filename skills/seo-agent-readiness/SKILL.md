---
name: seo-agent-readiness
description: Make a site readable by AI crawlers and usable by browser agents and assistive technology. Covers the owner's three choices about AI search answers, model training, and on-request reading in robots.txt, an llms.txt file with an honest label, accessible names and ARIA for every control, and the agent reference scans. Use while a site is built, before it goes live, or when the owner asks about blocking AI crawlers, GPTBot, llms.txt, or whether agents can use the site. For whether AI answers name the site, use seo-ai-visibility.
---

# SEO agent readiness

Read `seo` first if you have not read it in this session. Its rules for account writes, guest keys, and reading results apply here.

Goal: AI crawlers read the pages the owner wants them to read, and a browser agent or a screen reader can find and use every control.

Acceptance: robots.txt matches the owner's three answers, every button, link, and field on the key pages has a name, and the owner knows what `llms.txt` does and does not do.

Do this after the basics in `seo-site-setup`. Main text in the first HTML response (its section 2) matters most here too, because several AI crawlers do not run JavaScript.

## 1. AI crawler choices in robots.txt

The base robots.txt rules are in `seo-site-setup`, section 6. Add the AI rules only after the owner answers.

**Ask the owner these three questions before you write AI rules. Do not guess the answers:**

1. Do you want your pages to appear in AI search answers, where an assistant searches the web and cites sources? Blocking those crawlers removes you from those answers.
2. Do you allow AI companies to train their models on your content? Blocking training crawlers does not affect whether your pages appear in AI search answers.
3. Do you allow AI tools to read a page when a person asks about it?

Each vendor uses separate names for search, training, and reading on a person's request. Block only the names that match the owner's answer:

| Vendor | AI search answers (question 1) | Model training (question 2) | Read on a person's request (question 3) |
| --- | --- | --- | --- |
| OpenAI | `OAI-SearchBot` | `GPTBot` | `ChatGPT-User`. OpenAI says robots.txt rules may not apply to it |
| Anthropic | `Claude-SearchBot` | `ClaudeBot` | `Claude-User` |
| Perplexity | `PerplexityBot` | Perplexity says its crawler is not used for training | `Perplexity-User`. Perplexity says it generally ignores robots.txt |
| Google | `Googlebot`. AI Overviews and AI Mode come from the normal Search index | `Google-Extended`, which also covers Gemini grounding | Not controlled by robots.txt |
| Apple | `Applebot` (Siri, Spotlight, Safari) | `Applebot-Extended` | Not listed |

Other facts that matter for the answers:
- Blocking a training name leaves the search name allowed. A site can block `GPTBot` and still appear in ChatGPT search answers through `OAI-SearchBot`.
- Never block `Googlebot` to stop AI use. That removes the site from Google Search, including AI Overviews.
- Google-Extended does not affect Google Search. Blocking it does affect Gemini answers grounded in your content.
- If robots.txt has no rule for `Applebot` but has one for `Googlebot`, Applebot follows the Googlebot rule.
- A rule for one person-request name does not cover the others, and some of them ignore robots.txt. If the owner says no to question 3, say that robots.txt cannot fully enforce it.
- Changes can take about a day to apply, per OpenAI and Perplexity.
- Record the owner's answers as Content Signals in robots.txt when the owner wants that (`ai-train`, `search`, `ai-input`).
- Vendors add and rename crawlers. Before writing the rules, open each vendor's crawler page and confirm the names in this table are current.

## 2. llms.txt (optional, with an honest label)

- Put a file named `llms.txt` at the site root. Include a short summary of what the site is, who it serves, and links to the key pages, including pricing.
- Be precise about what it does. It is valid for some uses: developer tools and coding agents that read it when pointed at it, and Lighthouse's experimental agent audit that checks for it. Google Search does not use it, and Google's guide says it is not needed for Google's AI features. No major AI vendor has documented reading other sites' `llms.txt` files.
- Add it when the owner wants agent discovery, and say that is the reason. Do not promise rankings or AI citations from it.
- If the reference scan in section 4 marks it as missing, explain that it is an agent-discovery check, not a Google check.

## 3. Accessible names and ARIA (WCAG, and what agents read)

Why this matters for search and AI: WCAG requires every control to have a programmatic name and role. Browser agents read the page's accessibility tree, which holds those names and roles, to find buttons, links, and fields. A control with no name is invisible to both assistive technology and agents.

- **Use native HTML first.** A `button` already has keyboard support, a role, and states. A `div` with `role="button"` needs all of that rebuilt by hand. The first rule of ARIA is to use a native element when one fits.
- **Button with visible text:** the text is the name. Nothing else is needed.
- **Icon-only button:** add `aria-label` that names the function ("Close", "Add to cart"). Set the icon's SVG to `aria-hidden="true"`.
- **Link:** the link text says where it goes. Avoid "read more" and "click here". An icon-only link gets an `aria-label`.
- **Form input:** a `label` element linked with `for` and `id`. Placeholder text is not a label.
- **Image:** informative images get alt text that describes them. Decorative images get empty alt.
- **Match visible text:** when a control shows visible text, its accessible name must contain that text, with the visible words first (WCAG 2.5.3, Label in Name). A visible "Search" button named "Find products" fails for voice users who say "Search".
- **Name the function, not the look.** Name an X icon "Close". Start action names with a verb ("Edit John Doe"). Do not repeat the role in the name, so no "button" or "link" in the text.
- **aria-labelledby or aria-label:** if the label text already appears on the page, point to it with `aria-labelledby`. Use `aria-label` only when no visible text exists. Do not use both on one element.
- **Do not put `aria-label` on elements that prohibit naming,** such as paragraphs, spans, and plain divs.
- **Custom widgets** (menus, tabs, accordions, dialogs) need the right role, plus states such as `aria-expanded`, `aria-controls`, and `aria-selected` that update as the widget changes. Keep focus visible, and keep every control usable by keyboard.
- **Do not hide usable controls.** Never put `aria-hidden="true"` on something a person or agent can focus or click.
- **Overlays:** a cookie banner or popup must not cover the controls underneath it.
- **Use ARIA sparingly.** Wrong ARIA can do more harm than none, and pages with more ARIA have tended to show more detected errors.
- **Check it:** open the browser's accessibility tree for each key page, and confirm every button, link, and field has a name. Then run a keyboard-only pass.

## 4. Reference scans, after the build

- Scan the site at isitagentready.com. It scores robots.txt, the sitemap, AI bot rules, Content Signals, llms.txt, markdown negotiation, and other agent standards.
- Report the failing checks, in priority order. Fix only what the owner approves.
- Also run Lighthouse's Agentic Browsing category, available in Chrome 150 and later. It checks that every interactive element has an accessible name, that the accessibility tree is well formed, and that layout is stable. The category is informational for now, so report its results without a score.
- A failing check on llms.txt or on agent protocols does not mean a Google problem. Say so.

## Report back

List the owner's three answers and the robots.txt rules that follow from them, the controls that had no name and the fix for each, and the failing scan checks in priority order. Label each item verified, implemented but unverified, or blocked.

## Do not

- Write an AI crawler rule before the owner answers the three questions.
- Block `Googlebot` to stop AI use.
- Promise rankings or AI citations from `llms.txt` or from a passing scan.
- Present a failing agent check as a Google problem.
