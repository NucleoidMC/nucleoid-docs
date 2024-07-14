# Minecraft

The two Minecraft servers are in `/home/minecraft/servers/{play,build}`. There is also a [velocity](https://velocitypowered.org) proxy in `/home/minecraft/servers/proxy`.

## Adding/updating mods

Most mods should auto-update from Github Actions. Other mods like Fabric API don't and the version has to be updated manually in `destinations.toml` (inside the server directory)..
