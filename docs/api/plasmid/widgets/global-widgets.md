# Global Widgets

Utility for applying [GameWidgets](game-widget.md) to all players in a given [GameActivity](../game-activity.md)

### static addTo([GameActivity](../game-activity.md))

---

Creates a game-activity-wide instance of GlobalWidgets. All widgets added to this will be displayed to all players.

### addWidget([GameWidget](game-widget.md))

---

Adds a new [GameWidget](game-widget.md) to all players in the activity.
Returns the [GameWidget](game-widget.md) for you to customize.

### addSidebar()

### addSidebar(Component)

### addSidebar(Predicate&lt;ServerPlayer&gt;)

### addSidebar(Component, Predicate&lt;ServerPlayer&gt;)

---

Adds a new [SidebarWidget](sidebar-widget.md) to all players in the activity.
Returns the [SidebarWidget](sidebar-widget.md) for you to customize.

### addScrollableSidebar(int)

### addScrollableSidebar(int, Component)

### addScrollableSidebar(int, Predicate&lt;ServerPlayer&lt;)

### addScrollableSidebar(Component, int, Predicate&lt;ServerPlayer&lt;)

Adds a new [ScrollableSidebarWidget](scrollable-sidebar-widget.md) to all players in the activity.
Returns the [ScrollableSidebarWidget](scrollable-sidebar-widget.md) for you to customize.

### addBossBar(Component)

### addBossBar(Component, BossBarColor, BossBarOverlay)

---

Adds a new [BossBarWidget](bossbar-widget.md) to all players in the activity.
Returns the [BossBarWidget](bossbar-widget.md) for you to customize.

### removeWidget([GameWidget](game-widget.md))

---

Removes a [GameWidget](game-widget.md) from the list of widgets applied

### close()

---

Removes all [GameWidgets](game-widget.md) applied.
