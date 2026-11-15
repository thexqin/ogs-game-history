# Changelog

## v2.2 — 12 November 2026

Full review of the folder, code and documentation.

**New analysis**
- Sessions and momentum: win rate in the first game of a session, straight after a win, straight after a loss, and after two or more straight losses; win rate by game number within a session.
- Toughest regular opponents and best records against regulars (met at least 5 times).
- Notable games with links: strongest opponent beaten, biggest upset win, most surprising loss, longest live game, quickest live win.
- Playing habits: active days, games per active day and per week, busiest day, longest break, number of sessions and games per session.
- By-year table gains the rating change across each year's ranked games.
- Two more findings in "What stands out": average rating gap to opponents, and the after-win against after-loss difference.

**New feature**
- **Update with new games**: fetches only games newer than the loaded data, usually a single request. A stopped or failed update merges nothing.

**Accuracy**
- Opponents with a provisional rating (deviation above 160) are left out of rating comparisons, "strongest win" and notable games.
- Hour, time-of-day and weekday analysis now use real-time games only; a correspondence game's end time says little about when it was played.
- Rows with fewer than 15 decided games are faded, with a footnote explaining why.
- Duplicate game records (possible when a game finishes mid-fetch) are ignored.

**Robustness**
- Short server errors (HTTP 502–504) are retried up to three times.

**Documentation**
- README rewritten: contents list, report guide, how each figure is calculated, JSON format, code layout, verification table, troubleshooting.
- Header comment in the HTML describing the script's five parts.

**Verification**
- Paging, Max games and the update path tested in Node with a stubbed network.
- Re-rendered both reports with 900 mock games at desktop and phone widths: no script errors, no sideways overflow.

## v2.1 — 12 November 2026

Prompted by feedback that switching tabs changed the top figures but it was unclear which charts were ranked and which were all games.

- Banner under the tabs states what the report counts, how many games are left out, and what share of the history is ranked.
- Every card is labelled "All games" or "Ranked only".
- The tabs stay pinned to the top while scrolling.
- Rating chart is now drawn from ranked games in both reports and labelled "Same in both reports". Unranked games never change the rating, so this chart was always going to look alike in both; now it says so.
- Rating and peak-rating figures use ranked games only, for the same reason.
- Latest-games table gained a heading and scope label.
- Verified that a local file (origin `null`) can call the OGS API.

## v2.0 — 12 November 2026

**Reports**
- Two reports behind tabs: **All games** and **Ranked only**. Every figure, chart and table is recomputed for the selected scope.
- The All-games report keeps a ranked/unranked comparison; the Ranked report drops it.

**New charts** (inline SVG, hover or tap for values)
- Rolling win rate over a moving window (10, 20 or 50 games depending on history length) with a 50% reference line.
- Games per month, quarter or year (chosen from the length of the history), wins and losses stacked.
- Wins and losses by hour of day.
- Rating chart redrawn with a crosshair tooltip showing rating and approximate rank.

**New analysis**
- Results by opponent strength: five rating-gap bands, actual win rate beside the win rate the ratings predict.
- "What stands out": plain-language findings (colour gap, performance against rating expectation, record against stronger players, best and weakest board size, speed, time of day and weekday, recent form, share of losses on time, peak rating). Groups under 15 decided games are never mentioned.
- Colour by board size, time of day, day of week, live game length, humans and bots, game type (regular, tournament, ladder).
- New headline figures: peak rating, longest losing run, strongest opponent beaten, number of different opponents, typical live game length.
- Last 20 results strip.

**Data handling**
- Game speed is read from `time_control_parameters` (the field OGS actually fills); v1 guessed it from `time_per_move`.
- Rengo (team) games are skipped.
- Fetch page size raised from 50 to 100, halving the number of requests.
- Saved JSON gains an `app_version` field. Files saved by v1 still load.

**Fixes**
- The Stop button and progress bar were visible when they should have been hidden (a CSS rule overrode the `hidden` attribute).

**Verification**
- Live API and cross-origin access confirmed in a real browser.
- Rendered with 900 mock games in headless Chrome at 1100px and 390px: no script errors, no sideways overflow, tooltips working.
- Not yet done: a full fetch of a real long history through the page itself.

## v1.0 — 12 November 2026

- Single HTML file: look up an OGS player, fetch all finished games, save as JSON, load JSON back.
- One report: win rate overall, as Black, as White, ranked, unranked; breakdowns by board size, speed, handicap and year; how wins and losses ended; streaks; rating chart; ten most frequent opponents; latest 30 games.
- Statistics tested with mock data in Node. Live fetch untested at release.
