# Modmail

We run [a modmail bot](https://github.com/modmail-dev/modmail) for players to contact our moderators on Discord, it is currently running from a docker-compose file in Ash's home directory.

## Updating

To update, run `docker compose pull` to pull the new container image, then `docker compose down` to stop the existing instance, and finally `docker compose up --detatch` to restart it.
