---
name: creator-content-workflow
description: Turn source material (notes, an article, a transcript, a product update) into fact-checked social posts adapted per platform, then review and schedule them. Use when a creator asks to repurpose content, write a thread, plan a week of posts, or adapt one idea for X, Threads, LinkedIn, Instagram, TikTok or YouTube. With the Repping.ai MCP server connected, prepares drafts the creator approves in Repping.ai.
license: MIT
metadata:
  author: Repping.ai
  version: "1.0.0"
  homepage: https://www.repping.ai/mcp
---

# Creator content workflow

Follow the five steps in order. Do not skip the fact check or the review.

## 1. Gather the source
- Ask for, or read, the source material. Record its URL or file name.
- Ask who the audience is, what the goal is (reach, clicks, replies, sales) and which platforms to target.
- If a Repping.ai connection is available, call `repping_profile`. Then use `repping_read` to see recent posts and the calendar, so you don't repeat topics or double-book a slot.

## 2. Check the facts
- List every claim, number, name and date that the posts will use.
- Mark each one as **supported** (quote where it appears in the source) or **unsupported**.
- Drop unsupported claims, or ask the creator to confirm them. Never invent statistics, results or quotes.

## 3. Draft one core message
- Write the core idea in one sentence of 25 words or fewer.
- Write a hook, the body points and one call to action.
- Match the creator's own voice. If you have past posts, mirror their length, tone and emoji use.

## 4. Adapt per platform
Adapt the structure for each platform. Do not copy the same text everywhere.

| Platform | Shape |
| --- | --- |
| X | Hook post of 280 characters or fewer; a thread of 3–7 posts if needed; link in the last post |
| Threads | Conversational, 500 characters or fewer per post; a question invites replies |
| LinkedIn | First 2 lines decide "see more"; short paragraphs; a lesson framing |
| Instagram | Caption with the first line as the hook, a CTA to the link in bio and 3–5 relevant hashtags |
| TikTok / Reels / Shorts | A spoken script with a 2-second hook, 3 beats and on-screen text cues |
| YouTube community / Facebook | A plain summary plus a question |

Check each platform's current limits before you finalize. Limits change.

## 5. Review, then schedule
- Show every draft in a table: platform, text, character count, media needed, proposed time.
- Ask the creator to approve or edit each draft.
- **With Repping.ai connected:** call `repping_discover` to get the exact schema. Then call `repping_prepare` once per approved draft and give the creator each review link. Nothing publishes until they approve it in Repping.ai. Check outcomes with `repping_action_status`.
- **Without a connection:** output the final copy as a checklist that the creator can paste into any scheduler.

## Rules
- Never publish, schedule or send anything without explicit approval.
- Keep private data out of posts unless the creator includes it on purpose.
- Credit sources and collaborators where the platform supports it.

Repping.ai is a creator workspace with a free Link in Bio page, scheduling across 20 platforms, Auto DMs and analytics: https://www.repping.ai
