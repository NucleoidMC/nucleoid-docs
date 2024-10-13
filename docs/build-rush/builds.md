# Adding a build

## Building and saving the structure

!!! warning
    You need to know how to use the structure block and its SAVE mode to create a build.

First off, you need to build your structure in any creative world that you can download generated structures from. Either in a single-player world, or in a server that allows you to do so.

!!! tip
    If you have access to the Nucleoid build server, you can join the original builds map `/map join buildrush:builds`.
    This map contains all the builds that were made by fellow Nucleoid contributors up to 3.0.0.

    To download any generated build on the Nucleoid build server, visit this site: [https://build.nucleoid.xyz/](https://build.nucleoid.xyz/generated/)

You also need to choose a size for your build. Builds must have the same width, length and height.
Let's say you want a size of `n` blocks for you build. This means you need to create a structure of dimensions `n`x`n`x`n`.

You can also add a custom floor for your build, allowing the structure to be `n`x`n+1`x`n`.
Players won't have to build this floor, as it will replace the floor of all plots when building. Please make sure that all blocks of the floor have a solid top surface.

!!! tip
    Do not worry about falling blocks like sand for your floor, as barrier blocks will be placed under the plot floors if the map does not have blocks there.

!!! example
    If you want to create a build of size 7, you can create a structure of dimensions 7x8x7, with the floor being at the bottom of the structure.
    If you do not want this floor, you can create a structure of dimensions 7x7x7.

After finishing your build, save it using the structure block. The name of the structure file can be renamed manually afterward.
Entities are not supported, so make sure to not include them while saving.

Structures are stored under the `structures` folder of the datapack, so save it there when you're done.

## Creating the build file

You now need to add a build configuration that will add information about your build.
Builds are stored in the `build_rush/builds` folder of the datapack, so create a `.json` file there.

Here are the configuration fields of a build:
```json5
{
  "structure": "build_rush:build/my_build",
  "name": {
    "translate": "build.my_build"
  },
  "author": {
    "name": "jeb_",
    "uuid": "853c80ef-3c37-49fd-aa49-938b674adae6"
  }
}
```

| Field         | Description                     | Required | Defaults to |
|---------------|---------------------------------|----------|-------------|
| `structure`   | The path to the structure file. | Yes      |             |
| `name`        | The name of the build.          | Yes      |             |
| `author`      | The author of the build.        | No       |             |
| `author.name` | The name of the author.         | Yes      |             |
| `author.uuid` | The UUID of the author.         | No       |             |

!!! tip
    If a game tries to load any build that is not valid in any way, it will be ignored and a warning will be sent in the console.

A standalone build will not be used in any gamemode, that's because it is the game config that defines the list of builds that it's going to use.
However, you can add your build to the `build_rush:generic` tag, which is used by the generic game modes.

## Notes on contributions

If you are contributing to the Build Rush repository, please make sure to follow this checklist before submitting your pull request:
- Your build is replicable in normal gameplay, on any maps. (no floating blocks)
- Your build features as least redstone mechanics as possible.
- If the name of your build is already used, add an underscore and a number at the end of the name. (`build`, `build_2`, `build_3`, ...)
- Your structure file and your build configuration have the same name.
- The structure is saved under the `structures/builds` folder inside the `build_rush` datapack.
- If the build is not made for a specific gamemode, add it to the `build_rush:generic` build tag.
- The build name is translatable. Use existing translations if possible, if not add a translation key that follows the `build.<name>` pattern.

!!! warning
    Currently, the generic game modes of Build Rush were made for build sizes of 5, 7 and 9. Only size 5 is used for now though. 
