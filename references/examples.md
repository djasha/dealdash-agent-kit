# DealDash Agent Examples

## Read-Only Start

1. Call `context.search` with `scope=mine-and-shared`.
2. Call `screenshots.list_latest`.
3. Call `deals.view_logs`.
4. Call `deals.due_views`.
5. Summarize what is visible and what needs approval.

## Find A Promo Code

1. `context.search` with `q=<promo code>` and `types=deals,view_logs,screenshots,memory`.
2. If one clear deal appears, use that deal id for narrow follow-ups.
3. If multiple results appear, ask the user which one they mean.

## Shorten A Link

1. Confirm the destination URL.
2. Ask approval because this creates a DealDash short link.
3. Call `short_links.create_from_url`.
4. Return the short URL and destination.

## Upload An Image

1. Confirm the user wants a DealDash screenshot/link record.
2. Convert SVG, HEIC, or TIFF to PNG/JPG/WebP first.
3. Call `screenshots.upload_photo`.
4. Return `shortUrl`, `directUrl`, and `screenshotId`.

## Save Memory

1. Propose a short title and content.
2. Ask approval.
3. Call `memory.create`.
4. Mention it can be archived later with `memory.archive`.
