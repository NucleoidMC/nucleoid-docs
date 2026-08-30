# Game Space State

Stores all of the necessary data to control the joining of Players and for managing them in this [GameSpace](game-space.md).
--8<-- [start:content]

### players()

---

Gets all players in the [GameSpace](game-space.md)

### spectators()

---

Gets all players with the [Spectate JoinIntent](../data/join-intent.md#spectate)

### maxPlayers()

---

Returns the maximum amount of players allowed

### state()

---

Returns the [current state](#state) of the [GameSpace](game-space.md)

### canSpectate()

---

Whether the [GameSpace](game-space.md) accepts new spectators

### canPlay()

---

Whether the [GameSpace](game-space.md) accepts new players

### State

A small sub-record to record the [GameSpace](game-space.md)'s current state. Used to broadcast to the client the current state as well. Contains a Component message to send to the player and a boolean to determine whether the client can see this state.  
Has many static entries detailing different states such as

```java
public static final State WAITING = new State(Component.translatable("text.plasmid.game_state.waiting"), false);
public static final State STARTING = new State(Component.translatable("text.plasmid.game_state.starting"), false);
public static final State ACTIVE = new State(Component.translatable("text.plasmid.game_state.active"), false);
public static final State CLOSING = new State(Component.translatable("text.plasmid.game_state.closing"), true);
```

--8<-- [end:content]
