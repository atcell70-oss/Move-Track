# Move-Track Ops Runbook

## Current operating model

- GitHub Pages serves the front-end.
- Firebase Realtime Database holds the live data.
- `index.html` is the main board.
- `vehicles.html` and `wh.html` are fallback/secondary views.
- `status.html` is the basic health check page.

## Golden rule

Do not change Firebase database paths unless deliberately planned.

Known paths currently in use:

```text
board
locations
locations2
statuses
vehicles
fuelcards
rooms
fpnumbers
evac
```

## Safe change process

1. Download the current working files:
   - `index.html`
   - `vehicles.html`
   - `wh.html`
2. Save them locally as known-good backups.
3. Make one change at a time.
4. Commit to `main`.
5. Wait 1-2 minutes for GitHub Pages to deploy.
6. Test with a cache-bypass URL:

```text
https://atcell70-oss.github.io/Move-Track/?v=test
```

7. Press `Ctrl + Shift + R`.
8. Confirm:
   - Main board loads
   - Vehicles page loads
   - WH page loads
   - Status page loads

## User troubleshooting

If a user reports a blank page:

1. Ask them to press `Ctrl + F5`.
2. Ask them to close and reopen Chrome/Edge.
3. Ask them to try:

```text
https://atcell70-oss.github.io/Move-Track/?v=latest
```

4. If main board is down, use fallbacks:

```text
https://atcell70-oss.github.io/Move-Track/vehicles.html
https://atcell70-oss.github.io/Move-Track/wh.html
```

## Common issue types

### Blank main page, vehicles/WH work

Likely front-end issue in `index.html`.

### All pages load but data is missing

Likely Firebase rules, Firebase outage, network, or database path issue.

### Only one user affected

Likely browser cache or stale PWA/service worker cache.

### Everyone affected after a change

Rollback to the last known-good `index.html`.

## Rollback

1. Open GitHub repo.
2. Open the last working commit or local backup.
3. Replace the broken file.
4. Commit.
5. Test with `?v=rollback`.
