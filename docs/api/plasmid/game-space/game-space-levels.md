# Game Space Levels

Represents all Levels attached to the [GameSpace](game-space.md)
--8<-- [start:content]

### add(RuntimeLevelConfig)

---

Creates a temporary level based on the config. When the game is closed, this level is deleted.  
Returns the generated ServerLevel

### addPersistent(Identifier, RuntimeLevelConfig)

<!-- prettier-ignore -->
!!! warning
    Experimental

---

Creates (or loads) and adds a persistent level based on the config. When the game is closed, the level is unloaded and saved. If any level using the identifier is already loaded, an exception is thrown  
Returns the generated ServerLevel

### remove(ServerLevel)

---

Removes and deletes the temporary level in this [GameSpace](game-space.md). The level must've been created by [GameSpaceLevels.add](#addruntimelevelconfig)
--8<-- [end:content]
