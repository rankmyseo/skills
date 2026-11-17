---
name: seo-page-rewrite
description: Write or rewrite a page's title, description, headings, and body for one target keyword, in plain customer language. Checks length, honesty, and AI-sounding wording before handing the result back. Use when an existing page needs new copy, a new title, or a new description. For a brand-new page, use seo-page-brief first.
---

# SEO page rewrite

Read `seo` first if you have not read it in this session. Its rules for account writes, guest keys, and reading results apply here.

Goal: the page answers the search it targets, in words a reader would use, with no claim the owner cannot back up.

Acceptance: the owner can read the new title, description, and first paragraph and say what the page offers and who it is for.

## Before writing

1. Name the reader and the next action in one sentence. Example: "A small shop owner who needs a checklist. Next action: book a call."
2. Name the page that owns the keyword. One page, one main keyword. If another page owns it, stop and tell the owner.
3. Read the current page. Keep every fact that is true. Remove only claims you cannot support.
4. Ask the owner for any fact you do not have: price, location, hours, numbers, awards. Do not invent them. Leave a bracketed placeholder and say what is missing.

## Title

- Under 60 characters. The main keyword comes near the start. Add the brand at the end if the owner wants it.
- Say what the page gives the reader. "Rank tracking for agencies" is clearer than "The ultimate guide to rank tracking".

## Description

- 140 to 160 characters.
- Say what the reader gets and how it works. Include one checkable detail: a number, a cadence, or a limit.
- Write a sentence, not a list of keywords.

## H1 and first paragraph

- The H1 states the intent in plain words. It can use the main keyword once.
- The first paragraph answers the search in two or three sentences: what it is, who it is for, and the next step.

## Body

- Short paragraphs. Headings that name the question the reader has.
- Use a list only when the items are separate things to compare.
- End each section on a fact, not on a summary.
- Link to the owning page for each related keyword instead of repeating its content.
- Do not stuff keywords. A variant can appear once in a heading if it reads naturally.

## Voice

- Sentence case. No exclamation marks.
- "You" is the reader. Use the owner's company name for "we", if the owner wants one.
- Use the words the owner's customers use. "Keyword" for a search term. "Site" for a website.
- Plain verbs: connect, ask, start, check, see. Avoid leverage, unlock, empower, supercharge, elevate, and navigate.

## Cut these before you hand back

- "Not just X, it's Y", and "not X, but Y", unless the second part adds a fact
- Three-item lists where only one item has proof
- "Comprehensive", "seamless", "powerful", "robust", "cutting-edge", "game-changer", "ever-evolving", "in today's fast-paced world"
- Dashes that restart a sentence to sound deeper
- Closing lines such as "Start your journey today". End on the next action instead.
- Bold labels in running text

Delete first. Replace second. Vary sentence length last.

## Check length and wording

Count the characters in the title and description. Re-read the text for each phrase in the cut list. If a sentence has no fact and no action, cut it.

## Write for people, including AI answers

- Google's guidance is to write for people. You do not need a special style for AI systems, chopped-up paragraphs, or AI-only copy. Separate copy written for AI systems risks Google's spam policies.
- When you state a number, name its source and its date. Do not add a statistic you cannot source.
- Sourced claims helped in a simulated study of generative answers. That study did not test live assistants, and it found that citing sources lowered the visibility of top-ranked sites. Do not promise that a citation will earn an AI mention.
- Keyword stuffing did not help in that study, and it hurts search too. Leave it out.

## Who, how, and why (Google's people-first checks)

You are an AI writing for the owner. Google's guidance on helpful content asks three things of every page:

- **Who wrote it.** Use a real byline where a reader expects one, linked to a real author or About page. Never invent an author, a headshot, a credential, or a quote. If the owner has no author to name, publish under the business name.
- **How it was made.** Put the owner's first-hand facts on the page: what they did, tested, or saw, with their own photos when they have them. Ask for these facts. If AI did most of the writing and a reader would wonder how the page was made, suggest a short note saying so, and let the owner decide.
- **Why it exists.** The page should help a reader who came to the site directly. If its only reason is to catch a search, do not write it.

Also from the same guidance:

- Google has no preferred word count. Write until the reader's question is answered, then stop.
- Do not change a page's date unless the content changed substantially.
- Do not add or delete pages in bulk to make the site look fresh. Google says it does not help.
- Health, money, safety, and legal topics need facts that match expert consensus. Ask the owner who checked them, and name that person on the page.

## Hand back

For each changed item, show:

- Before and after
- The reason in one line: the search it targets, or the reader question it answers
- What to check: the Search Console query or tracked keyword to watch, and the date to look again (two weekly checks later)

Apply the change to the page yourself, where you can reach it. Publish live only after the owner says yes.

## Drafts from RankMySEO

For a new article on a RankMySEO plan (Starter and above), `write_article` queues a full draft under Content creation. Each draft uses one of the month's articles, so call it only after the owner asks for the article or says yes. Money pages and pages built on the owner's own facts stay with you.

1. Call `list_articles` first. It shows this month's quota and any draft already queued for the keyword.
2. Call `write_article` with the site, the keyword, and the brief's reader and angle. In `notes`, pass only facts the owner gave in this chat, the money page to link, and the pillar page the article supports.
3. If the result has `existingPage`, the site already ranks for that keyword. Tell the owner. The draft takes a different angle and links to that page.
4. The draft is ready in a few minutes. Read it with `get_article`. Do not poll in a tight loop.
5. Treat the draft as a first draft. Fill or remove each `[Add …]` placeholder with the owner's facts, then run the checks above: title and description length, the cut list, and "Who, how, and why".

Never retry a failed `write_article` on your own. A second call spends a second article.

## Other languages

Write a second language from its own search research and its own reader, as a fresh rewrite. Do not translate the English word for word.
