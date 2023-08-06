# Adding a map

Please follow the [Plasmid tutorial](/plasmid/maps) on how to create a map template.

A Build Rush map template needs the following regions:
- `center_plot`: the center of the map, where the players will be teleported to at first, and where the chosen build may appear at points. (only 1)
- `plot`: the plots where the players will build. There must be at least as many plots as the max amount of players in the game configuration (see below).

A map can only support one size of builds. The size of the chosen builds is determined by the size of the plots.

All plots must be of the same size (width and length) and be 1 block high.

!!! tip
    If you get anything wrong with your map, the game will not start. You can check the logs to see what went wrong.

## Configuration

Please follow the [Plasmid tutorial](/plasmid/getting-started/#creating-a-config) on how to create a game configuration.

You now need to add a game configuration that will use your map. Game configurations are stored in the `games` folder of the datapack.

Here are the configuration field added by Build Rush, on top of the ones added by Plasmid: 
```json5
{
  // ...
  "players": {
    "min": 1,
    "threshold": 8,
    "max": 16
  },
  "map": {
    "template": "build_rush:my_map",
    "nametag_offset": 5,
    "nametag_size": 2.0
  },
  "builds": "#build_rush:generic"
  // ...
}
```

The game type is `build_rush:standard`.

| Field                | Description                                                   | Required | Defaults to |
|----------------------|---------------------------------------------------------------|----------|-------------|
| `players`            | The configuration of number of players.                       | Yes      | None        |
| `map`                | The configuration of the map.                                 | Yes      | None        |
| `map.template`       | The map template to use.                                      | Yes      | None        |
| `map.nametag_offset` | The offset of the name tag above the player's plot.           | No       | 10          |
| `map.nametag_size`   | The size of the name tag above the player's plot.             | No       | 5.0         |
| `builds`             | The list of builds to use. Can be a list of builds, or a tag. | Yes      | None        |

For the builds list, you can use the `#build_rush:generic` tag that includes most of the available builds.

!!! note
    The builds field can contain any builds, even if they are not compatible with the map. Only the compatible ones will get filtered out.

!!! note
    If you are contributing to the Build Rush original repository, please make sure to follow this checklist before submitting your pull request:
    - Your game configuration is in the correct subfolder: `small` is for maps compatible with 5x5 builds, `medium` is for 7x7, and `large` is for 9x9.
    - Your game configuration is listed in the `random` game configuration in the same subfolder.
    - The game configuration follows this example:
    ```json5
    {
      // ...
      "name": {                                        
        "translate": "game.build_rush.small.with_map",   // change "small" with "medium" or "large" depending on the size of your plots
          "with": [
          {
            "translate": "map.build_rush.my_map"         // change "my_map" with the identifier of your map
          }
        ]
      },
      "icon": "minecraft:diamond",                       // as your game will show up in the list of games, you need an item to represent it
      // ...
    }
    ```
    - Your game configuration has an icon.
    - The build list is large enough, to counter the feeling of repetitiveness. Use the `#build_rush:generic` if you don't have enough builds.