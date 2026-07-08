# 🎾 Tennis Mabar App

A mobile-first web app for managing **Americano-format** casual tennis sessions (*mabar* = main bareng, Indonesian for "playing together"). Handles court shuffling, score tracking, and session summaries — designed to be used on the court, on your phone.

**[→ Open the app](https://mabartennis.netlify.app)**

---

## What is Americano?

Americano is a rotating doubles format where partners shuffle every round and players accumulate individual points equal to the games their team wins. At the end of the session, the player with the most points wins.

---

## Features

- **Smart shuffling** — players who sat out last round get priority; players who just played are deprioritized. Within each group, selection is random. Repeat partnerships and repeat opponents are minimised across rounds using match history.
- **Next round preview** — always visible below the courts, so players can prepare before the current round ends. Updates live when you mark absences, swap players, or add someone mid-session; tap **🔀 Shuffle** to redraw it. The preview is guaranteed accurate — what it shows is exactly what will be played.
- **Flexible courts** — set 1 to 6 courts at the start; the app fills them optimally each round.
- **Multiple sort modes** — view standings by **Points**, **Win %** (wins ÷ courts played), or **Pts %** (points scored ÷ maximum possible). Available in both the in-game Standings tab and the Summary screen.
- **Live standings** — leaderboard updates after every round, with full round-by-round history.
- **Score & player editing** — correct any score, or even *who actually played*, in any past round — mid-session or from the Summary screen; all stats recalculate automatically.
- **Player management** — mark absences before a round, swap players between courts and the sitting-out bench, or add players mid-session.
- **Session summary** — podium (with played count per player), full leaderboard from rank #4 down, and round history. Add a background photo with a gradient fade effect, reposition it with a slider, and export or share as an image.
- **Live sharing** — tap "📡 Share live" during a session to get a short link. Anyone who opens it sees a live read-only view: courts, scores, standings — updating in real time as rounds are saved. When the session ends, the link automatically shows the final summary/podium.
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
10. Tap **📡 Share live** in the round card to copy a link — send it to the group so everyone can follow along on their own phone
11. When done, tap **End** → **Finish session** to see the summary and share results
12. On the Summary screen, upload a background photo and use the **Reposition ↕** slider to frame the shot

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
- [Firebase Cloud Firestore](https://firebase.google.com/docs/firestore) (compat SDK via CDN) for live session sharing
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

### v3.1 (July 2026)

**Fix the right player, get the right standings**
- Round history editor now edits **players, not just scores** — tap **Edit** on any past round (Standings tab or Summary screen) and every court slot becomes a dropdown. Swap in who actually played, save, and points / played count / wins / Win % / Pts % all recalculate. The round's resting list auto-corrects too.
- Guard against selecting the same player twice in one round.
- (Swapping *before* saving a round already credited the right player — this closes the gap for rounds that were saved with the wrong lineup.)

**Always-on next round preview**
- The preview no longer hides behind a "👀 Preview next" toggle — it's permanently visible below the courts so the next four can get ready.
- New **🔀 Shuffle** button redraws the preview; tap as many times as you like.
- The preview updates automatically when you mark someone under "Skip next round", swap a player, or add/remove players mid-session — from any tab.
- Still guaranteed accurate: the round that gets played is exactly the last preview shown.

**UI polish**
- Court player names now sit next to the score they belong to — team 1 right-aligned, team 2 left-aligned.
- Swap is now a compact **⇄** icon button beside each name (no more dropdown): one resting player swaps instantly, several resting players open a small picker.

### v3 (June 2026)

**Live sharing**
- Firebase Cloud Firestore integration — session state syncs to the cloud on every save (1.5s debounced)
- Each session gets a 6-character share code (e.g. `A3K7P2`) generated at game start
- "📡 Share live" button in the round card — opens native share sheet on mobile, copies to clipboard on desktop
- Share link: `mabartennis.netlify.app/?code=XXXXXX` — clean short URL, no filename
- Player view at `?code=XXXXXX`: read-only, real-time updates via Firestore listener; shows courts, scores, standings
- When session ends, player view automatically switches to the final summary/podium

**Other**
- Renamed main file to `index.html` — serves at root URL on Netlify, no filename in the address bar

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
