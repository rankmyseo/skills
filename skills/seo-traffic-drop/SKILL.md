---
name: seo-traffic-drop
description: Find why a site's clicks, visits, or ranks fell. Confirms the drop, finds where it sits (page, query, country, device, search type), then checks tracking, the site's own changes, Google updates, what Google sees, rivals, the market, and search intent, in that order. Use when the owner says traffic, clicks, or ranks dropped, or when a review shows a fall across the whole site, a section, or a page type. For pages the owner can name or count, such as one page or three pages, use seo-content-refresh.
---

# SEO traffic drop

Read `seo` first if you have not read it in this session. Its rules for account writes, guest keys, and reading results apply here.

Goal: the owner knows what fell, where, and the most likely cause, with the evidence for it.

Acceptance: the report names the pages or queries that lost the most clicks, one likely cause with its evidence, what could not be checked, and at most three actions.

Find where it fell before you guess why. Steps that read tracked rank or rivals need RankMySEO. Without it, run the Search Console and GA4 steps with a direct connector and say what is missing.

## The checks, in order

1. **Confirm it.** Use one source, complete days, and the same weekdays in both windows. Compare with the same weeks last year when Search Console has them, to rule out a seasonal dip.
2. **Find where.** In Search Console, split by page, query, country, device, and search type (web, image, video, news). One page, one section, and the whole site point to different causes. When the fall sits on pages you can name or count, plan those pages with `seo-content-refresh`, which checks the page-level causes. RankMySEO's `search_console` gives pages (with `clicksChange` when `pagesComparable` is true), queries for one window, and the daily series; the country, device, and search type splits need Search Console itself, through the owner or a direct connector. Sort pages and queries by the absolute number of clicks lost, not by percentage; a small page that lost 80% can matter less than a big one that lost 10%.
3. **Check the tracking.** If GA4 visits fell and Search Console clicks did not, suspect the tag or the cookie banner before search.
4. **Check your own changes.** Read the change log (`seo-reporting`) for the window. A redesign, a move, or a template change points to the release check in `seo-go-live-check`.
5. **Check Google.** Open the Google Search Status Dashboard (status.search.google.com) for a ranking update or an incident in the window. If an update is still rolling out, wait. Google advises waiting at least a full week after it finishes, then comparing a week after with a week before it started.
6. **Check what Google sees.** On the pages that fell: status code, `noindex`, canonical, and robots.txt. Ask the owner to open the Page indexing, Manual actions, and Security issues reports in Search Console if you cannot reach them. In RankMySEO, run `site_issues`.
7. **Check rivals.** `keyword_history` on the keywords that fell, then `rank_compare` to see who passed the site.
8. **Check the market.** If saved rivals fell too (the `months` series in `competitor_traffic`, same months as the drop), the drop is likely seasonal or market-wide, not something the site did. Check demand with `seo-trends` before changing pages.
9. **Check the intent.** Look at what ranks now for the keywords that fell, if you can search, or ask the owner. If the results show a different kind of page than before (guides where there were product pages, or the reverse), the searcher's intent shifted. Reshape the page with `seo-page-rewrite` rather than adding more of the same.

## How to act on it

- A small drop on a page that still ranks well, such as position 2 to 4, needs no big change. Google advises against changing pages that already perform well.
- A large drop after a core update calls for the people-first checks in `seo-page-rewrite` on the pages that fell most, and on the site as a whole. Do not make quick fixes such as removing an element because someone said it hurts SEO.
- Deleting pages is a last resort. Propose it only for pages written for search and not for people, and only with the owner's yes.
- Recovery after a core update can take months. Say so, and set the next check date.

## Report back

Report what fell, where, the most likely cause and the evidence for it, what you could not check, and at most three actions. Add a row to the change log (`seo-reporting`) for each approved change.

## Do not

- Guess a cause before you know where the drop sits.
- Change a page that still ranks well because of a small move.
- Blame a rival, an update, or the season without the check that shows it.
- Promise a recovery date.
