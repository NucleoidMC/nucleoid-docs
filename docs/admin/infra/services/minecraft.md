# Minecraft

The two Minecraft servers are in `/home/minecraft/servers/{play,build}`. There is also a [Velocity](https://velocitypowered.org) proxy in `/home/minecraft/servers/proxy`.

## Adding/updating mods

Most mods should auto-update from GitHub Actions. Other mods like Fabric API don't and the version has to be updated manually in `destinations.toml` (inside the server directory).

##  Velocity

As we often lag behind the latest releases of Minecraft, our Velocity proxy also has [ViaVersion](https://github.com/ViaVersion/ViaVersion) installed, to allow players on the latest version to join, even if we haven't updated yet.

### Updates

Updating Velocity is as simple as downloading the latest JAR file, and replacing `velocity.jar` in `/home/minecraft/servers/proxy` (make sure to update any plugins too). When restarting Velocity, wait until there are no players online, or ask them to stop after the next game.
