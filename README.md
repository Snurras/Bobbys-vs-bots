# Bobby vs Bots

A hidden-role party game for the dinner table, with no game master. Everyone plays on their own phone. A few players are secretly **Bots** hiding among the humans, the **Bobbies**. Each night the Bots quietly eliminate a Bobby; each day the table discusses and votes to banish someone. The Bobbies win when every Bot is banished, the Bots win when no Bobbies are left.

Inspired by the TV show *The Traitors*.

**Play the test build:** https://snurras.github.io/bobbys-vs-bots/

> **Status: test build 0.1.** The full game runs in the browser as a solo test against simulated players. Online multiplayer comes with the Firebase version (see [Roadmap](#roadmap)).

## What's in this version

- Lobby with nicknames, Ready, and host settings (Adult or Kids mode, night length 15/30/45/60 s, whether failing the night task eliminates you)
- Secret role draw: 1 Bot per 4 players, rounded down, at least 1
- First discussion, then a repeating loop: night, morning, discussion, open vote, banishment with role reveal
- Night screen that looks the same for both sides: Bots converge on a target, Bobbies do a tapping task with a moving marker
- "You have been deleted" screen with sound for the eliminated player
- Ghost mode: eliminated players keep playing a prediction side game
- Dinner sessions: scores carry over across games and the evening ends on a podium
- Solo test mode with 3 to 9 simulated players, a role picker (play as Bot or Bobby), and a "show all roles" toggle

## Documentation

- [Game design](docs/game-design.md): rules, phases, night task, voting, Ghost mode, scoring, Adult and Kids mode
- [Test build](docs/test-build.md): how the code is organised, how to play test it, and known limitations

## Running locally

The whole game is one file. Open `index.html` in a browser, or serve the folder:

```sh
npx serve .
```

## Deploying

Every push to `main` deploys `index.html` to GitHub Pages through `.github/workflows/pages.yml`. Pages must be set to **Source: GitHub Actions** in the repo settings.

## Roadmap

1. **Test build (this version):** playable solo test, rules and screens settled through play testing.
2. **Online multiplayer on Firebase:** anonymous guest sign-in, host accounts, Firestore for live game state, roles kept secret on the server, game logic in Cloud Functions so the host's phone can sleep.
3. **Polish:** reconnecting after a phone locks, better sounds and art, tuning timers and points from play tests.
