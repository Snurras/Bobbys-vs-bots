# Test build 0.1

The test build is a single file, `index.html`, with no build step and no dependencies apart from Google Fonts. It runs the complete game in the browser.

## How to play test

1. Open https://snurras.github.io/Bobbys-vs-bots/ on a phone or laptop.
2. Enter a nickname, choose how many simulated players to add (3 to 9), and tap **Start solo test**.
3. In the lobby, pick the mode, night length and **Your role in this test** (Random, Bot or Bobby), tap **I'm ready**, then **Start game**.
4. Play through the phases. **Show all roles (test only)** reveals everyone's role; **Quit test** goes back to the start.

Simulated players ready up, vote, pick night targets and always pass the night task. When you are a Bot, the simulated Bots follow whichever name you pick.

## How the code is organised

`index.html` holds three parts:

| Part | What it does |
| --- | --- |
| **Engine** | Pure functions with no DOM access: `start`, `startNight`, `startVote`, `advance`, `nextGame`, `endDinner`, plus role balancing, night resolution, vote counting, win checks and scoring. `advance(game, players, now)` returns the next game state or `null`. |
| **Stores** | `LocalStore` keeps state in memory for the solo test. `DbStore` keeps state in a shared database when the page runs inside Claude as an artifact. Both expose `watch`, `setGame` and `setPlayer`. |
| **App** | Renders one screen per phase, handles taps, plays sounds, and runs a 250 ms loop. On the host's device the loop calls `Engine.advance` and writes the result. In the solo test it also drives the simulated players. |

### Data shape

- **Game document** (written only by the host): code, host id, mode, settings, phase, phase id, phase end time, game number, night and vote counters, player order and names, roles, who is alive, deaths, the last event, the winner, credits for good votes, Ghost hits, and session scores.
- **Player documents** (each written only by that player): nickname, ready flag, the current action (night pick, task hits or vote, tagged with the phase id), and Ghost guesses.

Actions carry the phase id they belong to, so stale actions from an earlier phase are ignored.

The night task is deterministic: the marker's stops and their 3 to 10 second lengths are derived from a hash of the player id and night number. The player's phone and the host's check compute the same schedule without sending it anywhere.

## Known limitations

- **Solo only on GitHub Pages.** Online multiplayer needs a shared backend. Inside Claude the page uses Claude's shared storage. On GitHub Pages it will use Firebase.
- **Roles are not truly secret.** The game document holds every role and the screens simply hide the others. The Firebase version will keep roles in per-player documents that only the server and that player can read.
- **The host's device runs the game.** If it sleeps or closes mid-game, the game stops. The Firebase version moves this logic to Cloud Functions.
- **Clocks.** Timers use each device's clock against the end time the host wrote, so devices with skewed clocks may show slightly different countdowns.
- **Audio** only plays after the player has tapped something on the page, which is a browser rule.
