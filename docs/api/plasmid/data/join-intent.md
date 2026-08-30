# Join Intent

Represents the "intention" of a player or group when joining a [GameSpace](../game-space/game-space.md). It is up to the game implementation how it handles these join states.

### PLAY

The player intends on participating in the game, if they cannot join as a participant, they should not be allowed to join.

### SPECTATE

The player intends on spectating the game, unless the game doesn't allow for spectators, this player should generally always be accepted.

### canPlay()

---

Whether the player can join as a participant

### canSpectate()

---

Whether the player can join as a spectator
