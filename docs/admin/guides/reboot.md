# What to do after a reboot

A short guide on making Nucleoid run again.

## Ensure stuff that is supposed to auto run did actually auto-run

Run `sudo systemctl status` and check that the overall status is not `Degraded`. If it is, run `sudo systemctl`, and find the failed services.

## Start up standalone services

Switch to the `minecraft` user with `sudo su minecraft -s /usr/bin/fish`, and start up the following services under screen (`screen -R <name of service>`) in the following order:

| Service | Path | Launch command |
| ------- | ---- | -------------- |
| [mitosis](https://github.com/ashhhleyyy/mitosis) | `/home/minecraft/services/mitosis` | `env RUST_LOG=info ./mitosis` |
| [face-api](https://github.com/NucleoidMC/player-face-api) | `/home/minecraft/services/face-api` | `./player-face-api` |
| [backend](https://github.com/NucleoidMC/nucleoid-backend) | `/home/minecraft/services/backend` | `env RUST_LOG=nucleoid_backend=info ./nucleoid-backend` |

Poke Ash and maybe she can turn some of these into systemd services.

## Stats website

As the `minecraft` user, go into `/home/minecraft/services/stats` and run `docker compose start`.

## Minecraft servers

Using the same `screen` commands, as the `minecraft` user, run `./server-wrapper` inside each server directory:

- `/home/minecraft/servers/play`
- `/home/minecraft/servers/build`

## Velocity

In a `screen` session as the `minecraft` user, `cd` into `/home/minecraft/servers/proxy` and run `java -Xmx256M velocity.jar`.

## BONUS: Modmail

`docker compose start` in `/home/ash/modmail` (please make Ash move it out of her home directory at some point)

## Testing everything is working

First, head to https://nucleoid.xyz and check the contributors section loads correctly and that Minecraft avatars are working.

Then, check on https://stats.nucleoid.xyz/leaderboards that the list has loaded correctly, and that the translations have been loaded.
