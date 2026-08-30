# Waiting Lobby Config

The Waiting Lobby Config determines multiple aspects of the waiting lobby, such as the amount of players needed to start a game and how long the countdown should be.

--8<-- [start:content]

| Field            | Type                                            | Description                                                                               |
| ---------------- | ----------------------------------------------- | ----------------------------------------------------------------------------------------- |
| playerConfig     | [PlayerLimiterConfig](player-limiter-config.md) | The Player Limiter Config for this Waiting Lobby                                          |
| minPlayers       | int                                             | The minimum number of players required to start the game                                  |
| thresholdPlayers | int                                             | The amount of players required to consider the game as ready to start                     |
| playerVoteTimer  | int                                             | The interval of time to re-prompt players to ready up                                     |
| countdown        | [Countdown](#countdown)                         | A record that details the amount of time to countdown from depending on the current state |

It also has multiple overloads when creating a new Waiting Lobby Config to set default values such as:

```java linenums="1"
public WaitingLobbyConfig(int min, int max)
public WaitingLobbyConfig(PlayerLimiterConfig playerConfig, int min, int threshold, Countdown countdown)
```

### Countdown

A small sub-record that stores the amount of time to countdown from whenever the lobby is in a ready or full state

| Field        | Type | Description                                                     |
| ------------ | ---- | --------------------------------------------------------------- |
| readySeconds | int  | The amount of seconds to countdown from when the Lobby is ready |
| fullSeconds  | int  | The amount of seconds to countdown from when the Lobby is full  |

--8<-- [end:content]
