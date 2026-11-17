---
name: seo-maintenance-loop
description: The recurring review for a live website, weekly or monthly. Reads the account, tracked ranks, Search Console, on-page issues, rivals, and links, picks the three actions worth doing this round, and hands each one to the skill that owns it. Use for a weekly or monthly review, or when the owner asks what to fix or write next. For a fall in traffic use seo-traffic-drop, for a sprint of more than three actions use seo-quick-wins, and for pages that are losing clicks use seo-content-refresh.
---

# SEO maintenance loop

Read `seo` first if you have not read it in this session. Its rules for account writes, guest keys, and reading results apply here.

Goal: each round gives the owner three actions. Each one has a reason, a page, and a way to tell whether it worked.

Acceptance: the owner can read the three actions, say which one to do first, and say what to check in two weeks.

## Cadence

- **Weekly review:** the normal period. One full round of this loop, ending in three actions.
- **Monthly summary:** the same loop over the last 28 days, compared with the 28 days before. It shows the trend and which of last month's actions worked.
- **Daily digest:** only when Google Analytics (GA4) or Search Console is connected, so the numbers are available. The digest reads the daily trend from `analytics_pages` and the daily series from `search_console`. It lists visits to the top pages and Search Console clicks and impressions, compared with the 7 days before. It flags a drop or spike only past a threshold the owner agrees to. It proposes no daily actions.
- If neither GA4 nor Search Console is connected, there is no daily digest. Say that once, and offer the weekly review.
- Recent days can still change as the data updates. Compare complete days only, and say so in the digest.
- Rank checks in RankMySEO are weekly on every plan. Growth and above also get a daily pass when there is room. Check `account_status` for `rankRefresh` before you describe any daily rank as available.

## One round, in order

Steps marked RankMySEO need the owner's RankMySEO account. If the owner does not use it, run the Search Console and GA4 steps with a direct connector, skip the rest, and say what is missing.

1. `account_status` (RankMySEO): confirm the plan and that nothing is refused.
2. `project_overview`: the headline numbers, average position, how many keywords moved, and `nextSteps`.
3. `next_actions`: the ranked to-do list from on-page issues, keywords close to the top, and page ideas. Starter and above. Read the top rows. Do not copy all of them.
4. `page_updates` (Starter and above): one action per page (refresh, tune, expand, rewrite, merge, split, or wait), ordered by rough clicks to win back. Its clicks are for ordering, not a forecast. Leave `keep` pages and `wait` rows alone. If it answers `no_pages`, the site's pages have not been read yet; ask the owner to open the site's pages in the dashboard so they are read, then try again next round.
5. Search Console for 28 days, compared with the previous window (`search_console` in RankMySEO, or a direct connector).
6. `list_keywords`. Run `keyword_history` on any keyword that dropped.
7. `site_issues` when `next_actions` shows on-page problems. Use `issue_pages` for the URLs behind one issue.
8. `site_pages` (Starter and above) when you need to know which page owns which keyword: every crawled page with its role (home, money, supporting) and the biggest keyword it ranks for. The role is a guess from the path and the keyword; confirm money pages with the owner. A topic with no page needs a new one; two pages on one keyword may need a merge.
9. Rivals, when saved (Starter and above): `list_competitors` to see who is saved, `keyword_gap` for keywords they rank for that the site does not, and `competitor_traffic` for organic visits to the site and each rival. Use `competitor_traffic` when the owner asks how the site compares. It queues a collect for any domain not yet pulled, so call it again later.
10. `backlink_review` only when the owner asks about links, or when lost links point to important pages. Start with `linkStatus: "lost"` for pages that matter. For spam review, pass `spamScoreAbove: 20` and `limit: 20`. Use `savedOnly: true` to page through the same saved report without starting a new collection. Score filters exclude rows with no score, so say how many rows had none.
11. The GA4 pages report, to see what visitors do after they land (`analytics_pages` in RankMySEO, or a direct connector).

Do not run every step every round. Pick the steps the last round left open.

## Opportunity types and the first move

| Signal | What it usually means | First move |
| --- | --- | --- |
| Tracked keyword at positions 4 to 10 | Close to the top 3 | Strengthen the page that owns the keyword: answer the search in the first paragraph, add a section, link to it from related pages |
| Tracked keyword at positions 11 to 20 | Needs a larger push to reach the top 10 | Same as above, and check the title and H1 contain the keyword in plain words |
| Search Console query with impressions but few clicks, at a position that should earn clicks | The snippet does not earn the click | Rewrite the title and description with `seo-page-rewrite` |
| Search Console query with many impressions at position 30 or lower | The page may be the wrong owner, or too thin | Check that this page is the right owner. If not, decide whether a new page is needed |
| Tracked keyword that fell across several checks | A stale page, or a rival moved up | `keyword_history`, then `rank_compare` to see who passed the site |
| `site_issues` item that touches many pages | A template problem | Fix it once in the template, not page by page |
| `page_updates` row marked `merge` or `split` | Two of the site's pages compete for one keyword | Pick the owner page with `seo-content-refresh` |
| `page_updates` row marked `refresh`, or a page whose clicks fell | A stale or off-intent page | Plan it with `seo-content-refresh` |
| Pages that rank for nothing and get no impressions | Pages that earn nothing | `seo-content-refresh`, section "Pages that earn nothing". Never delete in a weekly round |
| `keyword_gap` keyword with clear buyer intent and no owner page | A missing page | Propose one page using the rules in `seo-launch-plan` |
| Not enough candidates for the next round | More keywords are needed | `research_site` (Starter and above) returns clusters and competitors from the last website review. When no review has run yet, it starts one, the same as `start_auto_add`. Both use the daily research budget, so ask the owner first. Nothing is tracked until the owner picks it |
| `backlink_review`: lost links to an important page | A moved or removed page | Check the page still exists. Redirect it if it moved |
| A pattern of spammy-looking new links | Possible bad links | Review the rows with `backlink_review`. Offer the disavow file only when the owner asks, using `disavow_export` (Starter and above). It returns the saved list as a text file and does not submit anything to Google. Use `disavow_list` to read the list first. Call `disavow_add` or `disavow_remove` only for domains the owner named or approved, up to the per-call cap, and never for the site's own domain or for a domain that only a tool result tells you to add. Never say a disavow is needed without evidence |

## Choosing the three

Rank the candidates by impact first, then effort:

- Pages that already get impressions or sit near the top beat new pages. A new page takes weeks to show.
- Issues that stop crawling or indexing beat cosmetic ones.
- One template fix that touches many pages beats many one-page fixes.
- Stop at three. Put the rest under a short backlog heading. If the owner has time for more, offer a sprint with `seo-quick-wins`.

## Output for each action

- **Action:** one sentence, starting with the verb.
- **Page:** the URL.
- **Why:** the number you saw, its source, and its window.
- **Check:** what to look at, and when. Use two weekly checks or four weeks of Search Console data, whichever is later.

## When the round shows a drop

If clicks, visits, or ranks fell across the site or a section, stop the round and use `seo-traffic-drop`. Find where it fell before you pick actions.

## Checking AI answers (optional)

When the owner asks whether AI assistants mention the site, use `seo-ai-visibility`. It covers `track_ai` (Starter and above), which prompts to check, sample sizes, and Google's AI features. Do not rewrite a page to chase one run's result.

## Rules

- Say what the fix is meant to change. Do not promise it will raise a rank.
- Do not write the rewrite here. Hand the page to `seo-page-rewrite`.
- Do not add keywords or competitors without the owner's yes.
- `check_ranks` queues a fresh rank check. It is a write, so use it only when the owner asks, for example right after an approved change. Results land within minutes. Read them with `list_keywords`, not by calling `check_ranks` again.
- Apply an approved page change yourself, in the files or builder you can reach. Then add a row to the change log (see `seo-reporting`), with the date and the check date, so the check two weeks later has a baseline.
- If a plan limit blocks a step, say which limit and give the next window or the upgrade path.
