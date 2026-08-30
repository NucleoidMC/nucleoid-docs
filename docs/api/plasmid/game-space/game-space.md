# Game Space

A GameSpace represents any active instance of a game and the space it occurs in, it controls all ServerLevels created by the game, contains all joined players and handles all related game logic.  
--8<-- [start:content]

### getServer()

---

Returns the MinecraftServer linked to this GameSpace

### getMetadata()

---

Returns all of the [static metadata](game-space-metadata.md) associated to this GameSpace

### getPlayers()

---

Returns all of the [players](game-space-players.md) associated with this GameSpace

### getLevels()

---

Returns all of the [levels](game-space-levels.md) associated with this GameSpace

### getLifecycle()

---

Returns the [lifecycle manager](../game-lifecycle.md) of this GameSpace

### getState()

---

Returns the [current state](game-space-state.md) of this GameSpace

### getTime()

---

Returns the time passed (in ticks) since this game was created

### getStatistics()

---

Returns the [statistics manager](../statistics/statistics-manager.md) for this GameSpace

### isClosed()

---

Returns whether the GameSpace is closed

### addPlayerFilter(Predicate&lt;[PlayerRef](../util/player-ref.md)&gt;)

---

Adds a player filter that gets applied whenever a player joins the gamespace. Applied before any game activity specific filtering. If the predicate returns `true`, the player is allowed to join or `false` otherwise

### removePlayerFilter(Predicate&lt;[PlayerRef]&gt;)

---

Removes the player filter from being applied. Needs to be the same reference, or else the equality check fails.

### isPlayerAllowed(PlayerRef)

---

Tests whether this player is allowed to join based on the active filters. Returns `true` if they're allowed, false otherwise

### setActivity(Consumer&lt;[GameActivity](../game-activity.md)&gt;)

---

Replaces the old [GameActivity](../game-activity.md) with the one provided by the consumer. The old activity gets closed and all players get removed. After this, the sequence of events that get triggered are:

- [GameActivityEvents.CREATE](../events/game-activity-events.md#create)
- [GamePlayerEvents.ADD](../events/game-player-events.md#add) for every player in the GameSpace
- [GameActivityEvents.ENABLE](../events/game-activity-events.md#enable)

### requestStart()

---

Submits a request to start the game. What this request means is game-dependant, and games may choose to not listen to this event at all unless they want to respond to the `/game start` command or the [WaitingLobby](../waiting-lobby/waiting-lobby.md).  
Returns a [GameResult](../data/game-result.md) that describes whether the game has started successfully or not.
--8<-- [end:content]
