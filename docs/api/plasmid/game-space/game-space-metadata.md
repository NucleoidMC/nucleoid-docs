# Game Space Metadata

Stores all static metadata related to the creation of a [GameSpace](game-space.md) such as how it should be referenced, what game configuration was responsible for creating it and etc.
--8<-- [start:content]

| Field        | Type                                                 | Description                                                                                                                  |
| ------------ | ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| id           | UUID                                                 | The globally unique ID for this [GameSpace](game-space.md)                                                                   |
| userId       | Identifier                                           | The user referenceable ID for this [GameSpace](game-space.md). It is only guaranteed to be unique while this game is running |
| sourceConfig | Holder&lt;[GameConfig](../config/game-config.md)&gt; | The [GameConfig](../config/game-config.md) that generated this [GameSpace](game-space.md)                                    |

--8<-- [end:content]
