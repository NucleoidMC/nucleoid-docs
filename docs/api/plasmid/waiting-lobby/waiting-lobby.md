# Game Waiting Lobby

The Waiting Lobby API provides a universal GameAttachment that handles everything you'd expect from the lobby phase of a minigame. It affects things like block breaking, player damage, provides a ready-up system and handles private games for you automatically.  
This api exposes three main classes: the [Waiting Lobby](waiting-lobby.md), [WaitingLobbyConfig](../config/waiting-lobby-config.md) and the [PlayerLimiterConfig](../config/player-limiter-config.md), all necessary for the Waiting Lobby to work.  
The Waiting Lobby is a global implementation used by a lot of Plasmid Minigames, while not necessary, it is recommended that you also implement the Waiting Lobby for the sake of consistency between games. The only methods it exposes are to add the waiting lobby and to change the sidebar's contents.  
![Image showing what the waiting lobby looks like](../../../assets/images/api/waiting-lobby.png)  
--8<-- [start:content]

### GameWaitingLobby.addTo([GameActivity](../game-activity.md), [WaitingLobbyConfig](../config/waiting-lobby-config.md))

---

This is a static method that applies this waiting lobby implementation to the [GameActivity](../game-activity.md), given the [WaitingLobbyConfig](../config/waiting-lobby-config.md). You are not meant to initialize the WaitingLobby using the constructor, as it is private.

### setSidebarTitle(Component)

---

Sets the Title of the Waiting Lobby Sidebar.

### setSidebarLines(List&lt;Component&gt;)

---

Sets the content of the sidebar to the list of Components provided.
--8<-- [end:content]
