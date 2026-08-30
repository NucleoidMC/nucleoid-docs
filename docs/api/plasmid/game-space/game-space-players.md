# Game Space Players

Represents all of the Players contained within this [GameSpace](game-space.md). Also provides several utilities to operate on all players at once and manage them within the [GameSpace](game-space.md). Extends [PlayerSet](../util/player-set.md)
--8<-- [start:content]

### simulateOffer(Collection&lt;ServerPlayer&gt;, [JoinIntent](../data/join-intent.md))

---

Simulates a Join Offer to join a Player or group of Players and returns whether they're allowed to join. This logic is controlled by the active [GameActivity](../game-activity.md) through the [GamePlayerEvents#OFFER](../events/game-player-events.md#offer) event.
Returns a [GameResult](../data/game-result.md) that says whether they're allowed to join.

### offer(Collection&lt;ServerPlayer&gt;, JoinIntent)

---

Offers a Player or group of Players to join the game. If they're accepted, they get teleported to the game, otherwise, an error [GameResult](../data/game-result.md) will be returned. This logic is controlled by the active [GameActivity](../game-activity.md) through the [GamePlayerEvents#OFFER](../events/game-player-events.md#offer) event.

### kick(ServerPlayer)

---

Attempts to remove a player from this [GameSpace](game-space.md). When a player is removed, they get teleported back to their previous location.

### spectators()

---

Returns all players with the [Spectate JoinIntent](../data/join-intent.md#spectate)

### participants()

---

Returns all players with the [Play JoinIntent](../data/join-intent.md#play)

### byIntent([JoinIntent](../data/join-intent.md))

---

Returns all players with the specified [JoinIntent](../data/join-intent.md)

### changeIntent(ServerPlayer, [JoinIntent](../data/join-intent.md))

---

Changes the player's stored [JoinIntent](../data/join-intent.md)

<!-- prettier-ignore -->
??? info "PlayerSet inherited methods"
    --8<-- "api/plasmid/util/player-set.md:content"
--8<-- [end:content]
