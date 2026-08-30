# Player Set

Represents a list of players on a server, however they're not always guaranteed to be online. All functionality will only operate on online players. Extends [PlayerOps](player-ops.md), and thus contains convenience methods to apply operations across the whole player set.  
--8<-- [start:content]

### Constructors

---

**PlayerSet.ofServer(MinecraftServer)**  
**PlayerSet.ofLevel(ServerLevel)**

### contains()

---

Checks if the PlayerSet contains the given player. Has many overloads for convenience:

```java linenums="1"
contains(UUID id)
contains(PlayerRef ref)
contains(ServerPlayer player)
```

Will return true even if the player is offline, in the case of PlayerRefs.

### getEntity(UUID)

---

Looks up any online Player in this set that matches the UUID

### isEmpty()

---

Whether the set is empty

### copy()

---

Returns a mutable copy of this player set

<!-- prettier-ignore -->
??? info "PlayerOps inherited methods"
    --8<-- "api/plasmid/util/player-ops.md:content"
--8<-- [end:content]
