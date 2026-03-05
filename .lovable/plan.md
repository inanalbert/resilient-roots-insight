
Implementation plan (exactly aligned to your prompt)

1) Update marker wrapper styling in `src/components/dashboard/GlobalMap.tsx`
- In `createMarkerElements`, ensure the wrapper only has:
  - `width`
  - `height`
  - `position: relative`
  - `overflow: visible`
  - `cursor: pointer`
- Remove any wrapper-level `marginLeft`, `marginTop`, `transform`, or other manual offset/position hacks.

2) Enforce marker creation with center anchor in all map modes
- In both resilience and Gen Z marker creation paths, set marker construction to:
```ts
new maplibregl.Marker({ element: markerEl, anchor: "center" }).setLngLat(signal.coordinates).addTo(map)
```
- Remove any `top-left` anchor usage.

3) Guard against hidden offset regressions
- Search `GlobalMap.tsx` for any remaining wrapper offset logic (`margin*`, wrapper `transform`, translate hacks) and remove them if present.
- Keep tooltip behavior independent of marker wrapper positioning so marker placement remains fully controlled by MapLibre.

4) Validation pass
- Verify markers stay correctly georeferenced while zooming and panning.
- Confirm no manual wrapper offsets remain.
- Confirm hover tooltip still renders without reintroducing marker drift.
