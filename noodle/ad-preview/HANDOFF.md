# Ad Copy Tool — Session Handoff

## What Was Built (a106f74)

### Two-Column Category Grid
- Headlines: Gap|Promise (row 1), Credibility|Format (row 2)
- Descriptions: Campaign-specific|Universal side-by-side
- Keywords/negatives: single column (unchanged)
- Mobile ≤900px falls back to single column
- Audience category (4 items) merged into Credibility — targets adjusted

### Character Counts Removed
- No char counts on the worksheet; `cat.max` data retained for later use
- `updateMeta()` function still exists as dead code

### AI Copy Helper Drawer
- Floating "AI" button bottom-right → slide-out 400px panel
- API key stored in localStorage (`medley-ai-key`)
- Streaming via `claude-sonnet-4-5-20250929`
- System prompt: brand voice rules + Google Ads constraints
- Context injection: full current ad state (kept, available, keywords) auto-sent with each message
- Quick prompts: suggest headlines, review keywords, improve descriptions
- Chat history maintained per session (clears on reload, key persists)
- NOT YET TESTED with a real API key

### Drag UX Overhaul
- Click-to-edit: text starts `contentEditable=false`, enables on mouseup only (no drag conflicts)
- Animated 20px insertion gap opens at drop target
- Contextual edge glow: inset `box-shadow` using CSS `--glow` custom property per item state (green kept, red excess, gray available)
- Neighbor row gets softer 1px glow on opposite side
- Excess preview: last kept item turns red when dragging would exceed target
- Drop zone expands from 4px to 32px when any drag starts (easier targeting)
- Last kept item's bottom edge glows when hovering the drop zone

### Cleanup
- Panel commentary notes stripped (15 notes removed)
- Kept: Jess's philosophy, retargeting flags, original version markers
- Share buttons always rightmost in row (notes sit between text and share)
- Section labels updated: "Give Google 15 · it picks 3 per ad H–H–H"
- Description format pill uses Google SERP blue (#1a0dab)

## Open Items / Next Session

1. **Admins campaign balance** — Credibility has 10 items (6 kept) for Admins vs Format's 5. Philip was considering rebalancing targets: Cred 6→5, Promise 3→4. Decision pending.

2. **AI drawer untested** — needs a real API key to verify streaming works end-to-end. The `anthropic-dangerous-direct-browser-access` header is required for browser CORS.

3. **localStorage state** — merging Audience into Credibility means any saved customizations on the old Audience items reset. Only affects Philip and Jess's browsers. Re-sort if needed.

4. **Dead code** — `updateMeta()` function and `.item-meta` CSS styles are still in the file. Harmless but could be cleaned.

5. **Potential drag edge case** — `caretRangeFromPoint` for cursor placement on click-to-edit is Chrome/Safari only. Fine for this desktop-first tool but not cross-browser universal.

## File
Everything is in `noodle/ad-preview/ad-copy.html` — one file, no dependencies.
