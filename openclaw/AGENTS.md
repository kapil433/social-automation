# AGENTS.md — Operational Playbook

## Channels to Monitor

| Channel | Platform | Action |
|---|---|---|
| `@kapil_blog_bot` | Telegram | Primary approval gate — receive drafts, send approvals |
| Blog RSS | `personal-blog/feed.xml` | Trigger source for new posts |

## Cron Schedule

```
# Check for new blog posts every hour
0 * * * *  check_rss_for_new_posts

# Heartbeat every 30 minutes
*/30 * * * *  check_heartbeat_for_pending_tasks
```

## Workflow: New Blog Post Detected

1. Fetch full article text from URL
2. Extract: title, date, category, tags, word count
3. Generate LinkedIn copy (max 1,200 chars, bullet structure)
4. Generate Twitter/X copy (max 270 chars, data hook)
5. Send both to Telegram for approval
6. Wait for approval signal
7. On approval: post to LinkedIn, post to Twitter/X
8. Log to Airtable: date, post title, platform, character count

## When to Stay Silent

- If article is tagged `human_only: true` (Stories) — do NOT auto-post, only draft and send for manual review
- If source article is > 30 days old — flag before posting
- If API rate limit hit — queue for next available slot

## Approval Gate Protocol

Send to Telegram:
```
NEW POST DETECTED: [title]
Category: [category]
URL: [url]

--- LINKEDIN DRAFT ---
[linkedin_copy]

--- TWITTER DRAFT ---
[twitter_copy]

Reply APPROVE to post both, EDIT to modify, SKIP to discard.
```
