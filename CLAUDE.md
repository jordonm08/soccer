# Pitch Perfect

A static single-page schedule viewer for **Denver Summit FC** (NWSL) and **STL City SC** (MLS).

## What it is

- Single `index.html` — no build step, no framework, no dependencies
- All game data is hardcoded as JS arrays (no API calls)
- Deployed via GitHub Pages

## Architecture

- All code lives in `index.html` — CSS in `<style>`, JS in `<script>`
- Games are defined with the `game(date, time, tz, team, opp, home, venue)` helper
- Times are stored with IANA timezone strings and converted to the browser's local timezone at render time using `Intl.DateTimeFormat`
- Two datasets: `SUMMIT` (NWSL) and `STL` (MLS), merged into `ALL`

## Teams

| Constant | Team | League | Color var |
|---|---|---|---|
| `SUMMIT` | Denver Summit FC | NWSL | `--summit` (#34c97a green) |
| `STL` | STL City SC | MLS | `--stl` (#e03a3a red) |

## Key behaviors

- Games in the past render at 35% opacity
- Today's game gets a gold border and "TODAY" badge
- "Up Next" strip shows the next 5 upcoming games
- Filter tabs: All Games / Denver Summit / STL City / Home Only
- Times display in the **browser's local timezone** with abbreviation (e.g. "4:30 PM MDT")

## Updating schedules

Add or edit entries in the `SUMMIT` or `STL` arrays. The `game()` signature:

```js
game(dateStr, timeStr, ianaTimezone, team, opponent, isHome, venue)
// e.g.
game('2026-04-25', '6:45 PM', 'America/Denver', 'summit', 'San Diego Wave FC', true, "DICK'S Sporting Goods Park")
```

## Deploy

Push to `main` — GitHub Actions deploys to GitHub Pages automatically.
