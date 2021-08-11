# Backend

[![GitHub contributors](https://img.shields.io/github/contributors/NucleoidMC/nucleoid-backend?logo=github&style=for-the-badge)](https://github.com/NucleoidMC/nucleoid-backend)
[![GitHub last commit](https://img.shields.io/github/last-commit/NucleoidMC/nucleoid-backend?logo=github&style=for-the-badge)](https://github.com/NucleoidMC/nucleoid-backend)

Nucleoid uses a backend service written in rust as a central point for storing and handling data.
It is currently used for the following things:

- HTTP API used to query information about the server and players.
- Discord bot and relays to link ingame chat to Discord channels.
- Statistics storage in a [ClickHouse](https://clickhouse.tech/) database
- Recording performance metrics from the Minecraft servers into a postgresql database.
