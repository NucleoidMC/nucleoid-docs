# Game Config

A Game Config is a specific variation of a [GameType](../game-type.md), what this means is very game-specific, but it is expected that games utilize GameConfigs to change game behaviour in a data-driven way, such as changing maps or adding different game mechanics.  
You are not meant to instantiate this class in code, but rather use datapacks to store them based on a given Codec. You can define what Codec a GameConfig will use to parse when creating your [GameType](../game-type.md)

| Field       | Type                                 | Description                                                                                       |
| ----------- | ------------------------------------ | ------------------------------------------------------------------------------------------------- |
| type        | [GameType](../game-type.md)&lt;T&gt; | The [GameType](../game-type.md) associated with this GameConfig                                   |
| name        | Component                            | The name for this GameConfig, defaulted to the [GameType](../game-type.md) name if none specified |
| shortName   | Component                            | The shorthand name for this GameConfig, defaults to the normal name if none specified             |
| description | List&lt;Component&gt;                | The provided description of the game, defaults to an empty list                                   |
| icon        | ItemStackTemplate                    | The icon for the GameConfig, defaults to grass block                                              |
