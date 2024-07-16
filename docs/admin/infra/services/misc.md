# Other services

I have undoubtedly forgotten something, if you notice anything is missing, poke Ash on Discord.

## Grafana

Installed through APT, uses GitHub for logins and pulls data from postgres (which is written to by [backend](backend.md)).

## Databases

Make sure both of these are running before you try to start backend, otherwise it won't work.

### Postgresql

If you have to update this to a new major version, good luck - Google is your friend.

### Clickhouse

Every single update seems to change the default config file, which means apt/dpkg will ask you how to resolve it. When you do, take all the changes from the new config, and re-apply our specific parts (mainly disabling some of the logs as they take up a lot of storage).

## Mitosis and face-api

These are just small standalone serivces, managed in basically the same way as [backend](backend.md).
