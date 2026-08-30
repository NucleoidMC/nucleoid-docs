# Game Result

Describes the result of an action that involves a player in a [GameSpace](../game-space/game-space.md)

### GameResult.ok()

---

Means the action executed successfully

### GameResult.error(Component)

---

Means an error occured, the Component describes the error message that occurred

### isOk()

---

If the action executed successfully

### isError()

---

Whether an error occurred or not

### error()

---

Gets the error associated with the GameResult, or null if none exists

### errorCopy()

---

Returns a mutable copy of the error, or null if none exists
