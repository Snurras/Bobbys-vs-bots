# Game design

This describes the rules as implemented in test build 0.1.

## Roles

| Role | Goal | Knows |
| --- | --- | --- |
| **Bobby** (human) | Find the Bots and banish them all | Only their own role |
| **Bot** | Eliminate Bobbies until none are left | Their own role and the other Bots |
| **Ghost** | Score points in the prediction side game | Nothing new: roles stay hidden until the game ends |

Anyone eliminated or banished becomes a Ghost.

### Balancing

Bots = number of players divided by 4, rounded down, with at least 1. Minimum 4 players.

| Players | Bots | Bobbies |
| --- | --- | --- |
| 4 to 7 | 1 | 3 to 6 |
| 8 to 11 | 2 | 6 to 9 |
| 12 to 15 | 3 | 9 to 12 |

## Game flow

```
Lobby → Roles → First discussion → Night → Morning → (win?) → Discussion → Vote → Banishment → (win?) → Night → …
                                                         ↓                                           ↓
                                                     Game over                                   Game over
```

| Phase | Ends when | Moved on by |
| --- | --- | --- |
| Lobby | Host taps Start (host and at least 4 players ready) | Host |
| Roles | 10 s | Automatic |
| Discussion | Host taps "Night falls" (first round) or "Open the vote" | Host |
| Night | Night timer (15, 30, 45 or 60 s) | Automatic |
| Morning | 8 s, then win check | Automatic |
| Vote | Everyone alive has voted, or 60 s | Automatic |
| Banishment | 8 s, then win check | Automatic |
| Game over | Host taps "Next game" or "End dinner" | Host |

Players who are not ready when the host starts sit that game out and join the next one.

## The night

Every living player sees the same kind of screen: a list of names they keep tapping until the timer ends. From across the table a Bot and a Bobby look identical.

- **Same layout for both sides:** title, timer, a status pill, and a list of every other living player.
- **Shuffled per phone:** each player gets their own name order every night, so where a thumb goes says nothing.
- **Full timer always:** the night never ends early, so finishing fast gives nobody away.
- **Feedback:** a name shows **red** when it is marked and **green** once you have tapped it.
- **Scroll-safe:** a tap only counts if your finger lifts where it pressed, so scrolling the list never picks a name.

**Bots** tap a name to target it. Each Bot's pick shows as a dot next to the name; your own pick turns green, other Bots' picks show red. When every living Bot has picked the same Bobby the name locks. When the timer ends, the locked name is eliminated. If the Bots never agree, nobody is eliminated. Bots cannot target other Bots.

**Bobbies** do a decoy task. A marker sits on one name and jumps to another after a random 3 to 10 seconds. Tap the marked name before it jumps. The status pill shows how many stops you need to catch: about 60% of the marker's stops that night (fewer on a 15 s night). If the host has "failing the night task eliminates you" turned on, a Bobby who falls short is eliminated too.

## Morning

The eliminated player's phone plays a sound and shows a full-screen message. Everyone else sees who was eliminated:

| | Adult mode | Kids mode |
| --- | --- | --- |
| Victim's screen | "You have been deleted", glitch effect, eerie sound | "You've been unplugged!", soft power-down sound |
| Announcement | "[name] was found terminated" | "[name] ran out of battery" |
| Failed night task | "[name] suffered a system failure" | "[name] tripped over a cable" |

## Voting and banishment

Voting is open: everyone sees who voted for whom as votes come in. You vote by tapping the circle next to a name (tapping the name itself does nothing, so scrolling cannot cast a vote), and a player can change their vote until the vote closes. The player with the most votes is banished and their role is revealed ("[name] was a Bot" / "[name] was a Bobby"). A tie, or no votes at all, means nobody is banished that round.

## Winning

Checked after every morning and every banishment.

- **Bobbies win** when no Bots are left.
- **Bots win** when no Bobbies are left.

## Ghost mode

Eliminated players stay in the game through a side game that never affects the main game.

- **Back a side:** pick Bobbies or Bots to win. Worth more if picked in the same round you died.
- **Unmask the Bots:** mark every living player you think is a Bot.
- **Call the night:** guess who the Bots will eliminate next.
- **Call the vote:** guess who will be banished next.

Ghosts never see roles before the game ends, and their guesses stay hidden until the end-of-game recap.

## Scoring and dinner sessions

A host runs a session of several games. After each game the host taps **Next game** (same players, new roles, scores kept) or **End dinner** (podium with the top three).

| Event | Points |
| --- | --- |
| Your team wins (alive or not) | 3 |
| You survive to the end on the winning team | 1 |
| As a Bot, you are never banished | 2 |
| As a Bobby, you voted for a Bot who got banished | 1 each time |
| Ghost: backed the winning side | 1, or 2 if picked in the round you died |
| Ghost: correctly unmasked a Bot | 1 per Bot |
| Ghost: correctly called a night or a vote | 1 each |

## Adult and Kids mode

The host chooses the mode in the lobby. The rules are identical; only words, sounds and look change. Adult mode is dark with glitch effects and an eerie sound; Kids mode is bright with friendly wording and a soft sound.

## Open questions for play testing

- Should failing the night task eliminate a Bobby, or only make them look suspicious?
- Should the game end when Bots equal or outnumber Bobbies, as in many Traitors-style games?
- Should a tied vote get a quick re-vote between the tied players?
- Are the timers and point values right?
