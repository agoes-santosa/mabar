# Tennis Mabar App

I made this mainly for myself as I like to play casual tennis sessions and need to shuffle the players in Americano-format in order to ensure everyone got to play. 
This app handles court shuffling, score tracking, and session summaries, primarily designed to be used on the court, on your phone.

---

## What is Americano?

Americano is a rotating doubles format where partners shuffle every round and players accumulate individual points equal to the games their team wins. 
At the end of the session, the player with the most points wins.

---

## Features

- **Smart shuffling**: prioritizes players who've played fewer court rounds so everyone gets equal time. Avoids repeat partnerships across rounds.
- **Flexible courts**: set 1 to 6 courts at the start; the app fills them optimally each round.
- **Live standings**: leaderboard updates after every round.
- **Player management**: mark absences before a round, or add/remove players mid-session.
- **Session summary**: podium, full leaderboard, round history. Add a background photo and export as an image to share.
- **Offline-friendly**: session state is saved in `localStorage` so closing the tab won't lose your data.

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
9. When done, tap **End** → **Finish session** to see the summary and share results

---

## Tech
Quite literally just a single HTML (combination of HTML, CSS, and JavaScript) file made with Claude Code.

---

## Deployment

Hosted on [Netlify](https://mabartennis.netlify.app/) (free tier), auto-deployed from this repository. Any push to `main` goes live in ~30 seconds.

---

## Contributing

This is a personal project but feedback and suggestions are welcome — open an issue or reach out.

---

Made by **Agoes Santosa**
