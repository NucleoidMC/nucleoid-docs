# Adding a map

## Creating the map template

Please follow the [Plasmid tutorial](/plasmid/maps) on how to create a map template.

A Build Rush map template needs the following regions:
- `center_plot`: the center of the map, where the players will be teleported to at first, and where the chosen build may appear at points. (only 1)
- `plot`: the plots where the players will build. There must be at least as many plots as the max amount of players in the game configuration (see below).

A map can only support one size of builds. The size of the chosen builds is determined by the size of the plots.

All plots must be of the same size (width and length) and be 1 block high.

!!! tip
    If you get anything wrong with your map, the game will not start. You can check the logs to see what went wrong.

Map templates are stored in the `map_templates` folder of the datapack, so save it there when you're done.

## Creating the game configuration

Please follow the [Plasmid tutorial](/plasmid/getting-started/#creating-a-config) on how to create a game configuration.

You now need to add a game configuration that will use your map.
Game configurations are stored in the `games` folder of the datapack, so create your `.json` file there.

Here are the configuration fields added by Build Rush, on top of the ones added by Plasmid: 
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
    "nametag_size": 2.0,
    "author": {
      "name": "jeb_",
      "uuid": "853c80ef-3c37-49fd-aa49-938b674adae6"
    }
  },
  "builds": "#build_rush:generic"
  // ...
}
```

The game type is `build_rush:standard`.

| Field                | Description                                                   | Required | Defaults to         |
|----------------------|---------------------------------------------------------------|----------|---------------------|
| `players`            | The configuration of number of players.                       | Yes      |                     |
| `map`                | The configuration of the map.                                 | Yes      |                     |
| `map.template`       | The map template to use.                                      | Yes      |                     |
| `map.nametag_offset` | The offset of the name tag above the player's plot.           | No       | 10                  |
| `map.nametag_size`   | The size of the name tag above the player's plot.             | No       | 5.0                 |
| `map.author`         | The author of the map.                                        | No       |                     |
| `map.author.name`    | The name of the author.                                       | Yes      |                     |
| `map.author.uuid`    | The UUID of the author.                                       | No       |                     |
| `builds`             | The list of builds to use. Can be a list of builds, or a tag. | Yes      | #build_rush:generic |

The `#build_rush:generic` tag includes most of the available builds.

!!! note
    The builds field can contain any builds, even if they are not compatible with the map. Only compatible builds from the entry list will get used.

## Notes on contributions

If you are contributing to the Build Rush repository, please make sure to follow this checklist before submitting your pull request:
- Your map template and game configuration have the same name.
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
          "translate": "map.build_rush.my_map"         // change "my_map" with the identifier of your map (and translate it in lang/en_us.json)
        }
      ]
    },
    "icon": "minecraft:diamond",                       // as your game will show up in the list of games, you need an item to represent it
    // ...
  }
  ```
- Your game configuration has an icon.
- The build list is large enough, to counter the feeling of repetitiveness. If you don't have enough builds, leave the builds empty for the game to use the `#build_rush:generic` tag.