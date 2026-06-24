# 🎾 Tennis Mabar App

A mobile-first web app for managing **Americano-format** casual tennis sessions (*mabar* = main bareng, Indonesian for "playing together"). Handles court shuffling, score tracking, and session summaries — designed to be used on the court, on your phone.

**[→ Open the app](https://mabartennis.netlify.app)**

---

## What is Americano?

Americano is a rotating doubles format where partners shuffle every round and players accumulate individual points equal to the games their team wins. At the end of the session, the player with the most points wins.

---

## Features

- **Smart shuffling** — players who sat out last round get priority; players who just played are deprioritized. Within each group, selection is random. Repeat partnerships and repeat opponents are minimised across rounds using match history.
- **Next round preview** — tap "👀 Preview next" to see tentative pairings before saving the current round. The preview is guaranteed accurate — what it shows is exactly what will be played.
- **Flexible courts** — set 1 to 6 courts at the start; the app fills them optimally each round.
- **Multiple sort modes** — view standings by **Points**, **Win %** (wins ÷ courts played), or **Pts %** (points scored ÷ maximum possible). Available in both the in-game Standings tab and the Summary screen.
- **Live standings** — leaderboard updates after every round, with full round-by-round history.
- **Score editing** — correct any score mid-session or from the Summary screen; all stats recalculate automatically.
- **Player management** — mark absences before a round, swap players between courts and the sitting-out bench, or add players mid-session.
- **Session summary** — podium (with played count per player), full leaderboard from rank #4 down, and round history. Add a background photo with a gradient fade effect, reposition it with a slider, and export or share as an image.
- **No install needed** — runs entirely in the browser, no account or internet required after first load.
- **Offline-friendly** — session state is saved in `localStorage` so closing the tab won't lose your data.

---

## How to use

1. Open the app on your phone
2. Enter a session name and set how many courts are available
3. Add all players
4. Tap **Start game** — courts and partners are assigned automatically
5. Enter scores after each match, tap **Save & next round**
6. Use **Reshuffle** to re-draw courts before scores are entered (round number stays the same)
7. Mark players who are stepping out under **Skip next round**
8. Tap **＋ Player joining?** to add someone mid-session
9. Use the **Points / Win % / Pts %** toggles to change how standings are sorted
10. When done, tap **End** → **Finish session** to see the summary and share results
11. On the Summary screen, upload a background photo and use the **Reposition ↕** slider to frame the shot

---

## How the shuffle works

Each round, active players are split into two pools:

- **Preferred pool** — players who sat out last round (or have never played). Always fill slots first.
- **Fallback pool** — players who just played last round. Fill remaining slots only if needed.

Selection within each pool is random, so no priority debt accumulates and late arrivals don't get unfairly favoured with consecutive rounds. For exact group sizes where the preferred pool would equal the number of slots (e.g. 8 players, 1 court), one player is swapped between pools once everyone has had at least one turn — this prevents the same two groups from alternating forever.

Once players are selected, the app minimises repeat partnerships and promotes former partners to face each other as opponents.

---

## Tech

- Single HTML file — HTML, CSS, and vanilla JavaScript
- No framework, no backend, no build step
- State persisted in `localStorage` under key `mabar_v2`
- [`html2canvas`](https://html2canvas.hertzen.com/) for PNG export of the summary card
- Web Share API for native mobile sharing

---

## Deployment

Hosted on [Netlify](https://netlify.com) (free tier), auto-deployed from this repository. Any push to `main` goes live in ~30 seconds.

---

## Local development

No setup required. Just open `index.html` in a browser.

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
open index.html   # macOS
# or double-click index.html on Windows
```

---

## Changelog

### v2 (June 2026)

**Algorithm**
- Replaced `courtsPlayed`-based priority (caused late arrivals to play 2–3 consecutive rounds) with a recency-based two-pool system
- Group-lock fix: 8-player sessions no longer alternate the same two groups forever; deliberate pool swap kicks in from round 3 onward

**New features**
- Win % and Pts % sort modes — two new ways to rank players beyond raw points
- Edit scores from the Summary screen — no longer need to be in the active game to correct a past score
- Podium now shows played count per player
- Leaderboard on the Summary screen starts at rank #4 — top 3 are already on the podium
- Background photo gradient fade — photo shows clearly behind the podium, fades to solid black toward the player list; works cleanly at any session length
- Background photo reposition slider — drag to frame the shot after uploading

**Bug fixes**
- Preview next round showed ~50% wrong names — preview and actual generation were reading different history states; fixed by caching the preview and reusing it directly
- Reposition slider had no effect on landscape photos — `background-position-y` requires vertical overflow which `background-size: cover` eliminates for landscape images; switched to `transform: translateY()` which works for all orientations
- Background photo stretched in exported PNG — switched from `<img object-fit>` (unreliable in html2canvas) to `<div background-size: cover>`
- Player names truncated to one letter on Android portrait — fixed by stacking name above swap button instead of side-by-side
- Swap button inconsistent width on left vs right team — fixed with `align-items: flex-start`

---

## Contributing

This is a personal project but feedback and suggestions are welcome — open an issue or reach out.

---

Made by **Agoes Santosa**
