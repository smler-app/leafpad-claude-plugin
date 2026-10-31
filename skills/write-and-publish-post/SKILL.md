---
name: write-and-publish-post
description: Draft, SEO-check, and publish a LeafPad blog post. Use when the user wants to write, create, or publish a post on LeafPad.
---

# Write and publish a LeafPad post

Use the LeafPad MCP tools from this plugin. Authenticate via `/mcp` (OAuth through Scalekit) if the server is not connected.

## Workflow

1. **Pick the site** — Call `leafpad_list_organizations` and confirm which `organization_slug` to use.
2. **Optional context** — Call `leafpad_get_company_data` with a question about the product or brand so the draft matches company content.
3. **Optional tags** — Call `leafpad_list_tags` if the user wants existing tags reused.
4. **Create a draft** — Call `leafpad_create_post` with:
   - `organization_slug` (required)
   - `name` (title, required)
   - `html_content` (body HTML; do **not** include an H1 — the title is stored separately)
   - optional `slug`, `seo_title`, `seo_description` (aim ~150–160 characters), `seo_keywords`, `tags`
   - leave `published` false (default) so the post stays a draft until the user agrees to publish
5. **SEO check** — Call `check_draft_seo` with the new `post_id`. Fix gaps with `leafpad_update_post` if needed.
6. **Optional featured image** — Call `leafpad_generate_image` with a prompt that matches brand style, then attach the returned CDN URL via `leafpad_update_post` if the tool surface allows, or tell the user the URL to set in the editor.
7. **Publish only with consent** — After the user explicitly agrees, call `publish_post` with `organization_slug` and `post_id`. Do not publish without agreement.

## Guardrails

- Never invent organization slugs or post IDs; always read them from tool results.
- Prefer drafts first; publishing is irreversible from the user's point of view.
- Keep body HTML without a top-level H1.
- If the user only wants a draft, stop after create + SEO check.
