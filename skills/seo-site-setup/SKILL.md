---
name: seo-site-setup
description: Technical and on-page setup for a website that is being built or fixed. Covers rendering, HTML structure, on-page basics, link attributes, robots.txt, sitemap naming, structured data validation, speed, images, languages, and measurement. For AI crawler rules, llms.txt, and accessible names, use seo-agent-readiness. Use before a site goes live, or when the owner asks what is missing.
---

# SEO site setup

Read `seo` first if you have not read it in this session. Its rules for account writes, guest keys, and reading results apply here.

Goal: search engines and AI tools can read every public page, every page says what it is, the markup validates, and the owner can measure it from day one.

Acceptance: for any public page, the owner can see the title, description, one H1, canonical link, and main text in the raw HTML. The schema validates with no errors. robots.txt allows search crawlers and points to the sitemap.

Make the changes yourself, in the files or builder you can reach. If you cannot reach the site, write each change out exactly (where it goes, the old value, the new value, and the reason) and give it to the owner. If you do not know the stack, ask once.

## 1. Address and URL form

- Pick one host, with `www` or without it. Redirect the other with a 301 (permanent) redirect.
- Use HTTPS only. Redirect HTTP to HTTPS.
- Pick one URL form, with or without a trailing slash. Redirect the other form to it. The same page must not answer 200 on both forms.
- Each page sets a canonical link that uses the chosen form.

## 2. Rendering: main text in the first HTML response

- Put each page's text, title, description, and links in the HTML the server sends. Use server-side rendering, static generation, or prerendering. Prefer this over client-side rendering, where the browser builds the page with JavaScript.
- Why: Google's crawler runs JavaScript. In published tests, several AI crawlers do not, so client-rendered text can be invisible to them.
- Test: `curl -s https://example.com/page | grep -i "a phrase from the main text"`. If the phrase is missing, the page depends on JavaScript. Fix that before launch.

## 3. HTML structure

- Set `lang` on the `html` element.
- One `h1` per page. Headings follow in order: h2 before h3, never skip a level.
- Use landmarks: `header`, `nav`, `main`, `article`, `section`, `aside`, `footer`.
- Buttons are `button` elements. Links are `a` elements with an `href`.
- Every form input has a label. Every informative image has alt text. Decorative images get empty alt.
- Include the viewport meta tag so the page works on phones.
- Use real tables for tables and real lists for lists.
- Every button, link, and field needs a name that assistive tools and browser agents can read. The rules are in `seo-agent-readiness`, section 3.

## 4. On-page basics

- **Title:** unique to the page, under 60 characters, main keyword near the start.
- **Description:** unique to the page, 140 to 160 characters, saying what the reader gets.
- **H1:** matches the page's intent in plain words.
- **First paragraph:** answers the search in two or three sentences.
- **Canonical link:** points to the page itself, in the chosen URL form.
- **Open Graph:** title, description, and an image of about 1200 by 630 pixels for sharing.
- **Link text:** describes the target, for example "cost of rank tracking", not "click here".

## 5. Link attributes

- Internal links: a plain `a` element with no `rel` attribute. Do not put `nofollow` on internal links.
- Paid or affiliate links: `rel="sponsored"`.
- User-generated links, such as comments and forum posts: `rel="ugc"`.
- Other links you do not want to endorse: `rel="nofollow"`.
- Google treats these values as hints, not commands. To keep a page out of Search, use `noindex`. To keep a crawler off a path on your own site, use robots.txt.
- Several values can be combined, for example `rel="sponsored ugc"`.

## 6. robots.txt

- Serve `/robots.txt` at the site root, as plain text, with a 200 status.
- Allow public pages for search crawlers. Do not block CSS or JavaScript files.
- Add a `Sitemap` line that points to the sitemap file.
- Keep staging, preview, and admin areas out of the sitemap, and add `noindex` or a password.

Rules for AI crawlers (search answers, model training, and reading on a person's request) need the owner's answers first. They are in `seo-agent-readiness`, section 1. Do not write one here on a guess.

After any hosting or CDN change, open `/robots.txt` again. Some one-click settings add rules that block search crawlers by accident.

## 7. Sitemap

- The file name can differ from `sitemap.xml`. Any name works if robots.txt points to it with a `Sitemap` line.
- List only canonical, indexable URLs that return 200. Keep `lastmod` accurate.
- Make sure the XML parses.
- Submit it in Search Console. Bing does not index a sitemap URL that only redirects.

## 8. AI crawlers, llms.txt, and agents

Run `seo-agent-readiness` before launch. It holds the AI crawler rules for robots.txt, the `llms.txt` file, accessible names for every control, and the agent reference scans.

## 9. Structured data (JSON-LD), validated

- Use JSON-LD. Mark up only what is visible on the page.
- Homepage: Organization and WebSite. Inner pages: BreadcrumbList. Posts: Article. Local business: LocalBusiness with a real address (see `seo-local`).
- Product pages in a shop: Product with `name`, `image`, and an `offers` block that has `price` and `priceCurrency` (more in `seo-product-pages`). Use one page per product, not a category page. Put the markup in the first HTML response; Google says markup added by JavaScript makes shopping crawls less frequent and less reliable. Use one URL per currency.
- Do not mark up the business's own star rating on its own site. Google shows review stars for LocalBusiness only on sites that collect reviews about other businesses.
- Do not add FAQPage or HowTo for a search appearance. Google no longer shows those rich results. Structured data is not required for Google's AI features.
- Validate every template. Use the Schema.org validator for syntax and vocabulary. Use Google's Rich Results Test for the features Google still supports. The target is zero errors. Review warnings; do not ignore them.
- Validate again after every change to a template or a CMS plugin.
- A plain fetch can miss JSON-LD that JavaScript injects. Check the rendered page or validate the live URL.

## 10. Speed

- PageSpeed Insights shows a lab score (a simulated test) and field data (real visits). Use the lab score to find what to fix. Measure the result with field data.
- Field targets at the 75th percentile, on mobile and desktop: LCP 2.5 seconds or less, INP 200 milliseconds or less, CLS 0.1 or less.
- Google says chasing a perfect PageSpeed score for SEO may not be the best use of time. Start with the big items: image size and format, font loading, scripts that block rendering, and large JavaScript bundles.
- After launch, read the Core Web Vitals report in Search Console.

## 11. Images and media

- Compress images. Set width and height so the layout does not jump while the page loads.
- Lazy-load images below the fold. Do not lazy-load the hero image.
- Use an `img` element with a `src`, even inside `picture`. Google does not index images set in CSS.
- Name files for what they show (`black-leather-sofa.jpg`, not `IMG00023.jpg`). Place each image near the text it belongs to.
- Alt text describes the image in context. Do not fill it with keywords; Google says that can be treated as spam.
- Set `og:image` to an image that represents the page. Not the logo, and not an image of text.

## 12. Languages

- One language per URL. Each language gets its own page. Research each language's keywords on its own.
- If you use hreflang: each version lists itself and its matches, the links are reciprocal, every target returns 200, and the codes are valid (`en-GB`, not `en-UK`). Use full URLs with `https://`.
- Add `x-default` for the page a visitor should see when no language matches, such as a language picker or the main language.
- Google does not read the language from `hreflang`, the `lang` attribute, or the URL. It reads the page. A page with only the menu translated is still a duplicate.

## 13. Measurement, before launch

- **Search Console:** verify the domain with a DNS TXT record if the owner can edit DNS. It survives redesigns. Submit the sitemap. The Generative AI performance report appears once the site has enough AI impressions.
- **Search generative AI control:** confirm it is set to include the site.
- **GA4:** one tag on every page. Cookie consent can lower the counts, so tell the owner.
- **Conversions:** once the owner defines what counts as a lead, set up the key events with `seo-conversion-tracking`.
- **RankMySEO (recommended, not required):** `add_project` and `add_keyword` after the owner's yes. Search Console and GA4 can be connected in the dashboard or read directly.

## Report back

List what is done, what is not, and what the owner must do personally (DNS, consent banner, and builder settings). Label each item:

- **verified:** you checked the live page or file yourself
- **implemented but unverified:** the change is made but not live yet
- **blocked:** needs the owner's access or a decision, and you name it
