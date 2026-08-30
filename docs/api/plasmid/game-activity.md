# Game Activity

Every [GameSpace](game-space/game-space.md) in Plasmid is controlled by a GameActivity that handles the event loop and all game logic contained to this game. For a GameActivity to be considered active, it must be applied to a [GameSpace](game-space/game-space.md). There can only be one active GameActivity at once, however it can be easily changed by using the [setActivity](game-space/game-space.md#setactivityconsumergameactivity) method of [GameSpaces](game-space/game-space.md).  
--8<-- [start:content]

### getGameSpace()

---

Returns the current [GameSpace](game-space/game-space.md) attached to this GameActivity.

### setRule([GameRuleType](game-rule-type.md), [EventResult](../stimuli/event-result.md))

---

Sets whether a given [GameRuleType](game-rule-type.md) can be executed based on the [EventResult](../stimuli/event-result.md).

### allow([GameRuleType](game-rule-type.md))

---

Equivalent to setRule([GameRuleType](game-rule-type.md), [EventResult.ALLOW](../stimuli/event-result.md#allow));

### deny([GameRuleType](game-rule-type.md))

---

Equivalent to setRule([GameRuleType](game-rule-type.md), [EventResult.DENY](../stimuli/event-result.md#deny));

### listen([StimulusEvent](../stimuli/stimulus-event.md)&lt;T&gt;, T listener)

---

Registers a listener for the [StimulusEvent](../stimuli/stimulus-event.md) that gets triggered in this Activity.

### addResource(AutoCloseable)

---

Adds a resource that gets closed automatically when the GameActivity is deleted.
--8<-- [end:content]
