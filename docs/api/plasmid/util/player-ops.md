# Player Ops

Utility to apply various operations to a group of players
--8<-- [start:content]

### sendPacket(Packet)

---

Sends a packet to all players

### sendMessage(Component)

---

Sends a message to all players

### showTitle

---

Displays a title for all players. Has many overloads for convenience such as

```java linenums="1"
showTitle(Component title, int lengthTicks)
showTitle(Component title, int fadeInTicks, int stayTicks, int fadeOutTicks)
showTitle(Component title, Component subtitle, int fadeInTicks, int stayTicks, int fadeOutTicks)
```

### sendActionBar(Component)

---

Send a message in all player's action bars. Also has a convenience method to set the duration of the message:

```java linenums="1"
sendActionBar(Component message, int fadeInTicks, int stayTicks, int fadeOutTicks)
```

### playSound(SoundEvent)

---

Plays a sound to all players. Also has a convenience method to set the SoundSource, volume and pitch:

```java linenums="0"
playSound(SoundEvent sound, SoundSource category, float volume, float pitch)
```

### addStatusEffect(MobEffectInstance)

---

Adds a status effect to all players
--8<-- [end:content]
