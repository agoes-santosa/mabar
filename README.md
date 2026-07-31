# 🎾 Tennis Mabar App

A mobile-first web app for managing **Americano-format** casual tennis sessions (*mabar* = main bareng, Indonesian for "playing together"). Handles court shuffling, score tracking, session summaries, and a running monthly rating for the club — designed to be used on the court, on your phone.

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
- **Club roster** — the setup screen offers your saved players as tappable chips instead of making you retype names. Tapping one brings in that player's canonical spelling and saved gender. The search box doubles as add-new, and typing a name close to an existing one (e.g. "Lukas" when "Lucas" is in the roster) asks whether you meant the existing player before creating a second one. Regulars show by default with occasional players one tap away, but **search always reaches everyone** — nobody is hidden behind a threshold. The roster maintains itself: starting a session records its line-up, so new players are added and returning ones keep their spelling. Correcting a player's ♂/♀ in a session updates the roster too, so the fix carries into every future session instead of being redone each time.
- **Manage roster** — a small link under the roster chips (Setup screen), PIN-gated, for fixing a name after the fact. **Rename** rewrites that player everywhere — round history, courts, resting/absent lists, schedules, and the partner/opponent history — so their record stays in one piece instead of splitting across two spellings. **Merge** does the same into an existing player, but refuses outright — before it even asks you to confirm — if the two names ever appear together in one session, since that means they're two different people who played on the same day. The PIN (default `1234`, set in the source) is a guard against an accidental tap on a destructive action, not real security — same honest trade-off as the referee PIN.
- **Gender-balanced doubles** — mark players ♂/♀ with one tap on the player list. In doubles, an all-female pair is never matched against an all-male pair; mixed pairings are unrestricted. Female players get a small ♀ mark on court cards so balance is visible at a glance.
- **Fixed partners & fixed teams** — tap the **Team** chip on any player to put them in Team 1–6. One rule covers both uses: *teammates partner each other whenever both are on court, and never face each other.* So a team of exactly **2 is a fixed pair** (they're always partners, and rest together rather than being split), while a **bigger team plays as a team** — it fields whole sides across courts, and an odd member partners outside the team for that round. Everyone defaults to no team and shuffles freely as before. Works in Singles too, where it simply means teammates never play each other. Teams show a coloured T-tag on court cards and in the schedule, and the setup screen warns you if a team can't be seated (a 3-person team can't share one doubles court) or if a pair will end up playing every round.
- **Flexible courts** — set 1 to 6 courts at the start; the app fills them optimally each round.
- **Four sort modes** — view standings by **Raw Pts** (games won), **Win %** (wins ÷ courts played), **Pts %** (points scored ÷ maximum possible), or **Match Pts** (a flat 2 points for a win, 1 for a loss — rewards winning the match itself over the scoreline). Available in both the in-game Standings tab and the Summary screen. Exact ties (same value on the active mode) are broken automatically by point differential — total games won minus games lost across the session.
- **Small-sample protection** — in Win % and Pts % mode, players need at least the median number of rounds played (among everyone who's played) to rank in the top 3. A player who joined late and went 1-for-1 won't out-rank someone with a full, proven record — they still appear in the list with their real stats, just not on the podium. Raw Pts and Match Pts are unaffected, since both already reward playing more rounds.
- **Live standings** — leaderboard updates after every round, with full round-by-round history.
- **Score & player editing** — correct any score, or even *who actually played*, in any past round — mid-session or from the Summary screen; all stats recalculate automatically.
- **Player management** — mark absences before a round, swap players between courts and the sitting-out bench, or add players mid-session.
- **Session summary** — podium (with played count per player), full leaderboard from rank #4 down, and round history. For rated sessions, each player's rating and its change from that session are shown too — on the live summary, and retroactively on every past session. Add a background photo with a gradient fade effect, reposition it with a slider, and export or share as an image.
- **Live sharing** — tap "📡 Share live" during a session to get a short link. Anyone who opens it sees a live read-only view: courts, scores, standings — updating in real time as rounds are saved. When the session ends, the link automatically shows the final summary/podium.
- **Live matches & session history** — the app opens to a menu: jump into any session currently being played, browse every session ever played (grouped by month), or start a new one. Opening a past or live session reuses the same real-time viewer as a shared link, including all four sort modes. A session left untouched for 24 hours ends and locks itself automatically, so an abandoned game doesn't sit "live" forever.
- **Monthly standings & ratings** — a 4th menu option with a running Elo rating per player (starting at 1000, the same system chess uses), browsable month by month. Ranked by rating rather than raw win rate, since rating accounts for who you played with and against — beating a strong opponent is worth more than beating a weak one, which Win % can't tell apart. Needs 10+ matches *in that month* to be ranked; fewer than that and a player still shows, just below the ranked table with a **provisional** badge, so a small unrepresentative sample can't top it. Tap any name for their head-to-head record against every opponent that month (compact 2-column list) and their full match history. A small **Explanation on ratings** link opens a plain-language walkthrough of the calculation.
- **Casual sessions** — mark a session **😎 Casual** at setup (next to the courts counter) and it's saved, shared and listed in history exactly like any other session — it's simply skipped when ratings are computed. Handy for a one-off hit-around that shouldn't move anyone's standing.
- **Referee handover** — every session has a private 4-digit PIN, shown only to whoever's currently running it. From a live session (Live matches → tap it → scroll down), anyone with the PIN can take over as referee on their own device. Only one device can write to a session at a time — the moment control changes hands, the previous device is notified instantly and drops to a read-only view, with nothing it already saved lost.
- **No install needed** — runs entirely in the browser, no account or internet required after first load.
- **Offline-friendly** — session state is saved in `localStorage` so closing the tab won't lose your data.

---

## How to use

1. Open the app — you'll land on the menu; tap **New session** to start (or **Live matches** / **Session history** to jump into an existing one)
2. Pick a game mode — **👥 Doubles** (2 vs 2) or **👤 Singles** (1 vs 1)
3. Enter a session name, set how many courts are available, and leave the session **🏅 Rated** (default) or mark it **😎 Casual** if it shouldn't count toward monthly standings
4. Add players — tap them from the roster chips, or type a new name and tap **Add**. Set each player's ♂/♀ chip, and the **Team** chip if anyone should have a fixed partner or belong to a fixed team
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

### Fixed partners and teams

If any player has a team, one extra rule applies throughout: **teammates partner each other whenever both are on court, and never face each other.**

Because a court side holds two players, a team of exactly 2 is therefore a fixed pair, and a larger team fills whole sides. This changes *who gets selected*, not just who partners whom — teams are chosen in intact blocks, so a pair is never picked without its other half. A team can hold at most one side per court (two players per court in doubles, one in singles); past that its own members would have to play each other, so the extra members rest that round. An odd-sized team pairs up as far as it can and its leftover member partners outside the team, rotating each round so it isn't always the same person.

Where a team and gender balance genuinely conflict — an all-male pair that can only face an all-female pair — the team wins, since it was set deliberately.

The cost is rotation freedom. Measured over 12 rounds, teams make almost no difference (a spread of 3.2 rounds vs 2.8 without, at 9 players on 2 courts). The exception is a field barely bigger than one court: at 5 players on 1 court a fixed pair plays every round, because resting both would need 4 unteamed players and only 3 exist. The setup screen calls that out.

---

## Monthly standings & ratings

Ratings are **derived, not stored** — every time the standings screen opens, the app replays every rated session's round history from scratch and recomputes each player's Elo rating on the spot. Nothing is written to a player record.

This is a deliberate departure from the more obvious "store a rating, update it after each session" design, and it removes two whole classes of bug that design would otherwise need separate guards for:

- **A rating change can't be double-applied.** There's no stored delta to apply twice, so a dropped connection or an accidental double-tap simply can't corrupt anything — no idempotency guard needed.
- **Editing a past round's score just works.** Recomputing naturally picks up the correction; there's no need to lock a finished session's scores to keep a stored rating trustworthy.

Tuning the formula later — the K-factor, the starting rating, the qualification bar — needs no data migration either, since every month's standings just reflect it the next time they're opened. At club scale the recompute is effectively free (a few milliseconds for a month's worth of matches).

**How the number moves:** Elo, the same system chess uses. Everyone starts at **1000**. Before each match, both sides' current ratings predict who *should* win; the actual result moves each player's rating toward or away from that prediction — beat a stronger opponent and you gain more, lose to a weaker one and you lose more. Every point gained by one player is lost by another, so the total across all players never inflates or drifts on its own. In doubles, a team's expected score comes from the *average* of the two partners' ratings, and the same full movement applies to both. Court-by-court within a round, each match scores against ratings **as they stood before that round** — one court's result never leaks into another's expectation the same round.

**Ranking gate:** a player needs 10+ matches *in that month* to appear in the ranked table — matches, not sessions, since someone can attend several sessions while mostly resting between them. Below that they still show, in a separate "not enough matches to rank" group with a **provisional** badge, so a small unrepresentative sample (a lucky 2-for-2, say) can't top the table. Ratings still move for provisional players — they just aren't ranked yet.

**Casual sessions** are skipped entirely when ratings are computed — not just excluded from the ranked table, but never touched at all, so they can't nudge anyone's number even invisibly. Sessions saved before the casual/rated option existed have no flag and are treated as rated, so standings computed from old data are unaffected.

---

## Tech

- Single HTML file — HTML, CSS, and vanilla JavaScript
- No framework, no backend, no build step
- State persisted in `localStorage` under key `mabar_v2`
- [Firebase Cloud Firestore](https://firebase.google.com/docs/firestore) (compat SDK via CDN) for live session sharing and the club roster
- [`html2canvas`](https://html2canvas.hertzen.com/) for PNG export of the summary card
- Web Share API for native mobile sharing

### Firestore layout

```
sessions/{code}                  # one document per session
  ├── payload                    # the whole session state, JSON-encoded
  ├── sessionName, round, isFinished, isRated, updatedAt
  ├── controllerId               # which device currently holds the referee baton
  └── refPin                     # 4-digit handover PIN

clubs/cmtc/players/{key}         # the club roster
  ├── name                       # canonical spelling, the one sessions store
  ├── gender                     # feeds the gender-balance rule; editing it in a session syncs back here
  ├── sessionCount, lastPlayedAt # drive picker ordering and grouping
  └── createdAt
```

There is no ratings collection — see "Monthly standings & ratings" above for why
ratings are computed from `sessions` on every read instead of stored anywhere.

Roster document ids are a normalised form of the name (lowercased, accents and
punctuation stripped), so two spellings of one person can't create two documents.
Sessions still store plain name strings — the roster only supplies the spelling, so
the session format is unchanged and older sessions keep working untouched. Renaming
or merging a player (Setup → Manage roster) rewrites that name across every session
that contains it and, for a rename, moves the roster document to match.

Manage roster is gated by a fixed PIN — `ROSTER_PIN` near the top of the roster code
in `index.html` — change it there if you want a different one.

Rules must allow the `clubs` path as well as `sessions`:

```
match /clubs/{document=**} { allow read, write: if true; }
```

If that rule is missing the app still runs — the roster picker simply doesn't appear
and names are typed as before.

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

### v3.5 (July 2026)

**Monthly standings & ratings**
- New 4th menu option, **Monthly standings** — a running Elo rating per player, browsable month by month with a ‹ › picker. Ranked by rating rather than raw win rate, since rating accounts for who you played with and against.
- Ratings are **derived on every read, never stored** — the whole month's history replays in a few milliseconds. This sidesteps two failure modes a stored-rating design would otherwise need separate fixes for: a rating change can't be double-applied (no delta exists to apply twice), and correcting a past round's score just reflows into the ratings instead of requiring finished sessions to be locked.
- **Ranking gate is 10+ matches in the month, not sessions or attendance** — a player who attended several sessions but mostly rested doesn't qualify just for showing up. Below the gate, players still appear in a separate "not enough matches to rank" group with a **provisional** badge, rather than being hidden or allowed to top the table off a tiny sample.
- **Player detail screen** — tap any name for a hero card (rating + change that month), head-to-head record against every opponent faced (compact 2-column grid, colour-coded), and full match history (result, score, partners, opponents, session, round, date, and rating change per match). A **‹ Back to standings** button returns to the list.
- **Explanation on ratings** — a small link opens a plain-language walkthrough of the Elo calculation, with the provisional threshold pulled live from the same constant the engine uses so the two can't drift out of sync.
- **Ratings shown on session summaries** — every player's rating and its change from that session now appear on the podium and leaderboard, on the live end-of-session Summary and retroactively on every past session. Loads in the background so the summary still renders instantly and works offline.
- Verified against the real July data: 33 players, zero-sum check passed exactly (33,000 across all ratings, zero drift), and rating continuity confirmed across a month boundary with a synthetic test (August correctly starts exactly where July ends).

**Casual / unrated sessions**
- New **🏅 Rated** / **😎 Casual** toggle at setup, next to the courts counter. A casual session is saved, shared and listed in history exactly like any other — it's just skipped entirely when ratings are computed, so it can't nudge anyone's number even invisibly.
- Sessions saved before this option existed have no flag and are treated as rated, so standings computed from old data are unaffected. Verified with a controlled test: an identical session moved a player's rating by 0 when marked casual and by the expected amount when marked rated.

**Manage roster — rename & merge**
- A small PIN-gated link under the roster picker (Setup screen) for fixing a name after the fact instead of living with it.
- **Rename** rewrites that player everywhere a name is stored — round history, courts, resting/absent lists, schedules, and the partner/opponent history maps (whose keys are name pairs, re-sorted after renaming) — and moves the roster document to match.
- **Merge** does the same into an existing player, but **refuses before it even asks for confirmation** if the two names ever appear together in one session — that means they were two different people playing on the same day, and merging would fuse two records with no way to separate them again. Verified against the real data: merging "Ocha" into "Augtri" (who genuinely played together 6 times) was refused outright, while merging two players who never overlapped went through cleanly with counts summed correctly.
- Gated by a fixed 4-digit PIN (default `1234`) — three wrong attempts returns to setup; correct entry unlocks the tool for the rest of the page visit, and a reload re-locks it. This is a guard against an accidental tap on a destructive action, not real security, the same honest trade-off the referee PIN already makes.
- Editing a player's ♂/♀ from inside a session now writes back to the roster, so a correction carries into every future session instead of needing to be redone each time.

**Setup screen layout**
- The Rated/Casual toggle now sits side by side with Number of courts in one compact card, instead of its own full-width card — saves vertical space without losing either control.

### v3.4 (July 2026)

**Club roster — consistent names**

Groundwork for league standings: a league can only tally a player's record if that
player is always spelled the same way. Ten sessions of typed names had drifted into
53 distinct strings for 35 actual people.

- **Roster picker on the setup screen** — saved players appear as tappable chips. Tapping one brings in that player's canonical spelling and saved gender, so the same person is spelled the same way every session.
- **Search doubles as add-new.** Regulars (2+ sessions) show by default with occasional players behind a "Show N occasional players" toggle — but search reaches everyone, so the grouping only affects the default view and never hides anyone.
- **Similar-name guard.** Typing a name close to an existing one offers *Use &lt;existing&gt;* or *Add as new*, warning that a new name splits that player's league record. Matches on the spelling variants that actually caused the drift: oe/u, k/c, y/i, z/s, v/b, silent h, and doubled letters.
- **Self-maintaining.** Starting a session records its line-up — new players are created, returning ones get their count and last-played refreshed.
- **Degrades safely.** If the roster can't be read the picker simply doesn't render and typing works exactly as before, so a missing Firestore rule can't break the app.

**Historical data cleanup (one-off)**
- Merged the accumulated duplicates across all 10 saved sessions — case variants (`agoes`/`Agoes`), spelling variants (`Josh`/`Jos`, `Lucas`/`Lukas`, `Zaky`/`Zaki`, `Vebi`/`Vebby`), and a typo (`Augti`). 53 name strings resolved to 35 people.
- The rename covered every field that stores a name, not just the player list: round history, current courts, resting and absent lists, schedules, and the `partnerHistory`/`opponentHistory` maps whose keys are name pairs (re-sorted after renaming, and summed where two keys collapsed into one).
- Session timestamps were deliberately left untouched, so history ordering and dates are unchanged.
- Genders were reconciled where sessions disagreed. Because ♂ is the app's default, a ♀ marking is deliberate evidence while ♂ may just mean nobody set it — so any ♀ marking wins, which also resolves ties that a majority vote can't.

### v3.3 (July 2026)

**Fixed partners & fixed teams**
- New **Team** chip on every player (setup screen and Players tab) — tap it to open a picker and assign Team 1–6, or leave it on "No team". The picker shows how many players are already in each team. Everyone defaults to no team, so existing behaviour is unchanged unless you use this.
- One rule drives both use cases: *teammates partner each other whenever both are on court, and never face each other.* A team of exactly 2 is a fixed pair; a larger team plays as a team, fielding whole sides across courts.
- Teams change **who gets selected**, not just who partners whom — players are picked in intact team blocks, so a fixed pair is never selected without its other half, and the two rest together instead of being split.
- An odd-sized team pairs up as far as it can, and its leftover member partners outside the team for that round — rotating who that is, so it isn't always the same person.
- A team can hold at most one side per court, so any extra members rest that round rather than being forced to play each other.
- Works in **Singles** too, where the rule reduces to "teammates never play each other" — handy for a 2-vs-2 team singles format.
- Teams show a coloured **T** tag on court cards and throughout the schedule, so you can see at a glance that the draw respected them.
- **Setup validation**: combinations that genuinely can't be seated are blocked with an explanation rather than quietly leaving a court short (a 3-person team can't share one doubles court; everyone on one team leaves nobody to play). A softer amber warning covers the case where a pair will unavoidably play every round.
- Where a team and gender balance conflict, the team wins — it was set deliberately.
- Side effect: teams make the pairing search **faster**, because they prune it. 12 players on 3 courts drops from ~17ms to ~6ms with one fixed pair, and to well under 1ms when everyone is paired.
- Verified across 21 configurations — 6,300 live rounds plus 6,300 pre-generated schedule rounds — with zero rule violations, zero short courts, and no measurable change to rotation fairness except the tight-field case noted above.

### v3.2 (July 2026)

**Live matches & session history**
- The app now opens to a menu instead of straight into session setup: **Live matches**, **New session**, **Session history** — plus a **Continue** card above them if this device has a session already in progress.
- **Live matches** lists every session updated in the last 6 hours, with a live count badge on the menu tile.
- **Session history** lists every session ever played, grouped by month.
- Opening any session from either list — live or finished — reuses the same real-time read-only viewer as a shared link, so scores update live if it's still being played.
- The four sort modes (Raw Pts / Win % / Pts % / Match Pts) are now available in that viewer too, including for sessions saved before some of the newer fields existed — their stats are recomputed from round history on the fly.
- A session left untouched for 24 hours ends and locks itself automatically, so an abandoned game doesn't sit in the live list forever.

**Referee handover**
- Every session gets a private 4-digit PIN at creation, shown only to whoever currently holds it (small grey text near the share button) — there's no login, so the PIN is the only thing that gates control.
- From a live session's viewer — Live matches → tap the session → scroll down — anyone with the PIN can tap **🔑 Take over as referee** to claim control on their own device. Deliberately not on the main menu, since it only makes sense in the context of one specific session.
- Only one device can write to a session at a time. Every save re-checks who currently holds control before writing, so two referees can never silently overwrite each other.
- The instant someone else takes over, the previous device is notified in real time and drops to the read-only viewer with a one-time explanation banner — nothing it had already saved is lost.

**Landing page polish**
- Title sits just above the three menu buttons, centered together as one group, instead of pinned to the top with a gap underneath.
- Reordered to Live matches → New session → Session history.
- The menu narrows to a compact centered column on wider screens; unchanged on phones.
- Small "Made by Agoes Santosa" footer under the menu.

### v3.1.1 (July 2026)

**Fixed: gender balance could still be broken, and could cause repeat pairings**
- Found the root cause of both: gender balance was only enforced when deciding *which pair faces which pair* — but with a small group (e.g. exactly one court), there's only one possible matchup, so a female-pair-vs-male-pair could be unavoidable once partners were already picked. The fix makes gender balance part of choosing partners in the first place, not just an afterthought at the court-matching step.
- Verified across every player count and gender split from 4–12 players (200+ randomized trials): zero forced female-pair-vs-male-pair matchups, where they used to occur regularly.
- Repeat partnerships are unaffected or slightly improved — the fix only changes behavior when gender balance and repeat-minimisation would otherwise conflict; it doesn't touch anything else.
- Runs in well under 100ms even for 3 full courts, so there's no delay generating a round or a 12-round schedule.
- Found and fixed a second, separate bug during this: when "Generate Matches" builds the schedule, round 1 itself hadn't been counted yet when planning rounds 2–12 — so round 2 could cheaply repeat one of round 1's exact partnerships, since the planner didn't know it had just happened. Now round 1 (or whichever round is currently in progress) is always counted before planning what comes after it.

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
