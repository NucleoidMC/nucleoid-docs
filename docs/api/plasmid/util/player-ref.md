# Player Ref

Simple record to represent both online and offline players based on their UUID. Provides many convenience methods to turn existing classes into PlayerRefs such as
--8<-- [start:content]

```java linenums="16"
public static PlayerRef of(Player player)
public static PlayerRef of(GameProfile profile)
public static PlayerRef of(NameAndId nameAndId)
public static PlayerRef ofUnchecked(UUID id)
```

Contains a single field, storing the user's UUID.  
Has many utility methods to get the player based on a PlayerRef such as

```java linenums="33"
public ServerPlayer getEntity(GameSpace gameSpace)
public ServerPlayer getEntity(ServerLevel world)
public ServerPlayer getEntity(MinecraftServer server)
```

Also has many utility methods to determine whether the player is online

```java linenums="47"
public boolean isOnline(GameSpace gameSpace)
public boolean isOnline(ServerLevel world)
public boolean isOnline(MinecraftServer server)
```

...and to execute code if the player is online

```java linenums="59"
public void ifOnline(GameSpace gameSpace, Consumer<ServerPlayer> consumer)
public void ifOnline(ServerLevel world, Consumer<ServerPlayer> consumer)
public void ifOnline(MinecraftServer server, Consumer<ServerPlayer> consumer)
```

--8<-- [end:content]
