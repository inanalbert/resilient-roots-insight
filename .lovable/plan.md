
Yes, this is a good idea. A clean hover-tooltip rewrite using map.project inside the map container is the right fix for this recurring top-left bug.

Plan

1) Rewrite marker hover tooltips in GlobalMap.tsx from scratch
- Remove all existing hover tooltip state/helpers/event wiring currently tied to the previous approach.
- Keep click behavior separate; only hover tooltips will be rewritten (no MapLibre Popup for hover).
- On marker mouseenter:
  - Read marker lng/lat from the signal coordinates.
  - Compute pixel position via map.project([lng, lat]).
  - Create a plain div tooltip and append it to map.getContainer().
  - Use absolute positioning with fixed offsets: left = x + 20px, top = y - 40px.
- On mouseleave:
  - Remove that tooltip div immediately.
- On map move/zoom while hovered:
  - Recompute with map.project and reposition the same div.
- Add robust guards so cleanup never calls .remove on undefined.
- Ensure only one hover tooltip exists at a time.
- Keep tooltip content exactly as requested:
  - Country name
  - Signal title
  - One-line description (shortened safely)
  - Domain or Gen Z category label in accent color

2) Stabilize container-relative positioning
- Confirm map container remains position: relative (already present in className).
- Ensure tooltip z-index/pointer-events are set so it never captures hover and causes flicker.
- Clamp optional extreme positions (edge of viewport) only if needed after test.

3) Enforce exact AI response structure in ai-insight edge function
- Update prompt instructions to require this exact output template for every response:

GLOBAL SIGNAL
2-3 short sentences

JAPAN CONTEXT
2-3 short sentences

CEO IMPLICATION
1-2 short actionable sentences

- Explicitly forbid markdown and special formatting (no asterisks, bullets, headers beyond these exact labels).
- Keep strict brevity and executive tone.

4) Add client-side output normalization in AIInsightPanel.tsx
- Keep/strengthen cleanText to strip any residual markdown tokens before render.
- Add lightweight formatter guard:
  - If response is missing required section labels, reformat into the 3 labeled blocks from available text fallback.
- Preserve line breaks with current whitespace-pre-line rendering.

5) Validation pass (end-to-end)
- Hover test across multiple regions/zoom levels/pan states:
  - Tooltip remains anchored to marker (never jumps top-left).
  - Tooltip disappears on mouseleave and on marker set refresh.
- Mode switching test:
  - Works in both resilience and Gen Z layers.
- AI output test:
  - Multiple generations confirm exact labels, line breaks, short punchy prose, and zero asterisks.

Technical notes
- Root issue is not MapLibre marker data; it is tooltip lifecycle/positioning strategy.
- map.project + map-container absolute overlay is the most deterministic fix for hover UI.
- Keeping hover rendering independent from MapLibre Popup avoids anchor edge cases and CSS side effects.
