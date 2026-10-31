---
name: schedule-rewrites
description: Find decaying LeafPad pages and schedule AI rewrites or review refresh proposals. Use when the user wants to refresh content, schedule rewrites, or fix pages losing traffic.
---

# Schedule LeafPad rewrites and refresh proposals

Use the LeafPad MCP tools from this plugin. Authenticate via `/mcp` if needed.

## Find work

1. Call `leafpad_list_organizations` and confirm `organization_slug`.
2. Call `find_pages_needing_attention` to list pages losing search traffic and any refresh proposals waiting for a decision.
3. For a specific proposal, call `get_refresh_proposal` before approving or rejecting.

## Approve or reject a planner proposal

- After the user reviews the proposal and agrees, call `approve_refresh` with `organization_slug` and `proposal_id`. Approving can change a live page.
- To decline without changing the live page, call `reject_refresh`.
- Never approve a refresh without the user's agreement.

## Schedule a rewrite of an existing post

1. Resolve the target with `leafpad_list_posts` (and optionally `leafpad_get_post` or Search Console via `leafpad_get_search_console_data`).
2. Call `leafpad_schedule_rewrites` with `organization_slug` and a `rewrites` array. Each item needs:
   - `post_id` (from `leafpad_list_posts`)
   - `date` (ISO 8601 datetime when the rewrite should start)
   - optional `instructions`, `target_keywords` (up to 12; first is primary), `url`, `volume`, `kd`, `intent`
3. Confirm the calendar with `leafpad_list_scheduled_posts`.
4. Adjust pending rows with `leafpad_update_scheduled_post` or remove them with `leafpad_delete_scheduled_posts` before they run.

## Notes

- Rewrites of existing posts use `leafpad_schedule_rewrites`. New AI-generated posts use `leafpad_add_scheduled_posts` (charges apply per LeafPad pricing); do not confuse the two.
- Without `target_keywords`, rewrites lean on Search Console queries (requires Search Console connected).
- On sites with the refresh planner enabled, a scheduled rewrite may wait while the planner is on.
