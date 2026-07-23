# 🎾 Tennis Mabar App

A mobile-first web app for managing **Americano-format** casual tennis sessions (*mabar* = main bareng, Indonesian for "playing together"). Handles court shuffling, score tracking, and session summaries — designed to be used on the court, on your phone.

**[→ Open the app](https://mabartennis.netlify.app)**

---

## What is Americano?

Americano is a rotating doubles format where partners shuffle every round and players accumulate individual points equal to the games their team wins. At the end of the session, the player with the most points wins.

---

## Features

- **Doubles or Singles** — choose the game mode at setup: classic Americano doubles (2 vs 2, 4 players per court) or Singles (1 vs 1, 2 players per court). Everything — shuffling, standings, live sharing, history editing — works in both modes.
- **Smart shuffling** — players who sat out last round get priority; players who just played are deprioritized. Within each group, selection is random. Repeat partnerships and repeat opponents are minimised across rounds using match history (in Singles, repeat opponents are minimised). For sessions up to 3 courts, partner pairings are chosen by checking every possible pairing for the round and picking the one with the fewest repeats, rather than a faster but less thorough one-pair-at-a-time guess.
- **Full 12-round schedule** — "Generate Matches" creates round 1 plus 11 upcoming rounds you can scroll through, so everyone knows what's coming. Each upcoming round has its own 🔀 redraw button, **＋ Add round** extends the plan past 12, and the whole schedule updates live when you mark absences, swap players, or add someone mid-session. The schedule is guaranteed accurate — the round you play is exactly the one shown.
- **Play rounds in any order** — tap **▶ Play** on any upcoming round to play it now (e.g. someone stepped out and a later round fits who's on court). Your current lineup is parked in that round's slot — marked **⏸ parked** — with any typed scores kept, waiting until you come back to it. Nothing else is reshuffled.
- **Gender-balanced doubles** — mark players ♂/♀ with one tap on the player list. In doubles, an all-female pair is never matched against an all-male pair; mixed pairings are unrestricted. Female players get a small ♀ mark on court cards so balance is visible at a glance.
- **Flexible courts** — set 1 to 6 courts at the start; the app fills them optimally each round.
- **Four sort modes** — view standings by **Raw Pts** (games won), **Win %** (wins ÷ courts played), **Pts %** (points scored ÷ maximum possible), or **Match Pts** (a flat 2 points for a win, 1 for a loss — rewards winning the match itself over the scoreline). Available in both the in-game Standings tab and the Summary screen. Exact ties (same value on the active mode) are broken automatically by point differential — total games won minus games lost across the session.
- **Small-sample protection** — in Win % and Pts % mode, players need at least the median number of rounds played (among everyone who's played) to rank in the top 3. A player who joined late and went 1-for-1 won't out-rank someone with a full, proven record — they still appear in the list with their real stats, just not on the podium. Raw Pts and Match Pts are unaffected, since both already reward playing more rounds.
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
2. Pick a game mode — **👥 Doubles** (2 vs 2) or **👤 Singles** (1 vs 1)
3. Enter a session name and set how many courts are available
4. Add all players, and tap the ♂/♀ chip to mark each player's gender
5. Tap **Generate Matches** — round 1 starts and a full 12-round schedule appears below the courts
6. Enter scores after each match, tap **Save & next round**
7. Use **Reshuffle** to re-draw the current round before scores are entered, or 🔀 on any upcoming round to redraw it
   — or tap **▶ Play** on an upcoming round to play it right now; your current lineup parks in its place until you return to it
8. Mark players who are stepping out under **Skip upcoming rounds** — the schedule adjusts instantly
9. Tap **＋ Player joining?** to add someone mid-session, or **＋ Add round** to extend the schedule past 12
10. Use the **Points / Win % / Pts %** toggles to change how standings are sorted
11. Tap **📡 Share live** in the round card to copy a link — send it to the group so everyone can follow along on their own phone
12. When done, tap **End** → **Finish session** to see the summary and share results
13. On the Summary screen, upload a background photo and use the **Reposition ↕** slider to frame the shot

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

**Fairer standings & pairings**
- New 4th sort mode, **Match Pts**: a flat 2 points for winning a match and 1 for losing, regardless of the scoreline. Unlike Raw Pts (which gives partial credit for games won even in a loss), Match Pts rewards *winning the match itself* — a narrow 4-3 loss and a 0-4 blowout loss are worth the same. It's still a total, not a rate, so like Raw Pts it doesn't need the small-sample protection below.
- Renamed the original **Points** mode to **Raw Pts**, to distinguish it clearly from Match Pts now that there are two points-based modes.
- Standings ties (identical value on the active sort mode, across *all four* modes — which can genuinely happen) are now broken automatically by point differential: total games won minus games lost across the session. It only ever adjudicates players who are perfectly tied already — it never changes a ranking that wasn't tied, so a 4-3 win still counts exactly the same as a 4-0 win everywhere else in Raw Pts.
- If differential is *also* tied, standings fall back to alphabetical instead of the old arbitrary "whoever was added to the roster first"
- **Win % / Pts % no longer let a small sample take the podium**: players need at least the median rounds-played (among those who've played) to rank in the top 3 — a latecomer who went 1-for-1 can no longer outrank someone with a full, proven record. They still show up in the standings with their real stats; they just don't hold a medal. Raw Pts and Match Pts are untouched, since both already reward playing more rounds.
- Partner pairing now searches every possible pairing for the round (up to 3 courts) and picks the one with fewest repeat partnerships, instead of a faster greedy guess that could lock in a worse pairing without realizing it

**Full 12-round schedule**
- "Start game" is now **Generate Matches**: round 1 plus 11 upcoming rounds are drawn immediately, listed below the courts so players can see what's coming and prepare
- Each upcoming round has a 🔀 button to redraw it (rounds after it re-derive automatically); **＋ Add round** extends the plan beyond 12
- "Save & next round" works exactly as before — it plays the schedule in order
- The schedule regenerates automatically when you mark absences, add/remove players, swap someone into the current round, or retro-edit a past round
- Round card now shows "Round X of Y"
- The "Skip next round" card is now **Skip upcoming rounds** — checked players are excluded from the whole schedule until unchecked
- **▶ Play any round next**: tap ▶ Play on an upcoming round to make it the active round — the current lineup (typed scores included) is parked in its slot with a ⏸ tag until you play it later; nothing else is redrawn. Per-round 🔀 keeps parked lineups pinned in place.

**Gender & balanced doubles**
- Every player has a ♂/♀ chip (setup screen and Players tab) — tap to toggle; new players default to ♂
- In doubles, the matchmaker never pits an all-female pair against an all-male pair (mixed pairs are unrestricted); if a draw would force it, pairings are redrawn
- Female players show a small ♀ next to their name on court cards and in the schedule

**Singles mode (1 vs 1)**
- New **Game mode** choice on the setup screen: 👥 Doubles (2 vs 2) or 👤 Singles (1 vs 1)
- Singles courts hold 2 players; sessions start from just 2 players
- The shuffle engine minimises repeat opponents across rounds (partner logic doesn't apply)
- Standings, sort modes, live sharing, round history, and the player editor all work identically in both modes
- The round card shows a "• Singles" tag so you always know which mode the session is in

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
