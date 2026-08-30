# Game Space Manager

Handles opening and getting all open [GameSpaces](game-space.md) in this Server. There can only be one GameSpaceManager active on the server, and it can be referenced using GameSpaceManager.get()
--8<-- [start:content]

### GameSpaceManager.get()

---

Gets the active GameSpaceManager

### open(Holder&lt;[GameConfig](../config/game-config.md)&gt;)

---

Opens a new [GameSpace](game-space.md) based on the specified [GameConfig](../config/game-config.md)

### byId(UUID)

---

Gets the [GameSpace](game-space.md) based on the UUID

### byUserId(Identifier)

---

Gets the [GameSpace](game-space.md) based on the user-referenceable ID. This is only guaranteed to be unique while the [GameSpace](game-space.md) is active

### byLevel(Level)

---

Gets the [GameSpace](game-space.md) based on the level

### byPlayer(Player)

---

Gets the [GameSpace](game-space.md) based on a Player that is inside the [GameSpace](game-space.md)

### hasGame(Level)

---

Whether a given Level is associated to a [GameSpace](game-space.md)

### inGame(Player)

---

Whether the Player is in a game
--8<-- [end:content]
