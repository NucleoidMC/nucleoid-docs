# HTTP API

Nucleoid's backend service provides a few API endpoints for querying information about the server and players.

The official backend API is available on [https://api.nucleoid.xyz/](https://api.nucleoid.xyz/)

## Status

### Server status
!!! example
    ```
    GET https://api.nucleoid.xyz/status/play

    {
        "game_version": "1.16.4",
        "server_ip": "nucleoid.xyz",
        "games": [
            {
                "name": "Bedwars",
                "type": "bedwars:bedwars",
                "player_count": 1
            }
        ],
        "players": [
            {
                "name": "Tom_The_Geek",
                "id": "07e92b46-8386-4067-8f72-8ab96e606fb7"
            }
        ]
    }
    ```

This endpoint allows you to query the status of any of the Nucleoid servers.
Currently the following servers are available to query:

- `play`: The main server on hosted on `nucleoid.xyz` and `play.nucleoid.xyz`
- `build`: The whitelisted server used for map building, hosted on `build.nucleoid.xyz`

| Field | Description |
|-------|-------------|
| `game_version` | The version of Minecraft the server is running |
| `server_ip` | The public IP of the server, optional |
| `games` | A list of all open minigames on the server |
| `players` | A list of all players on the server |

## Statistics

### Get all player stats
!!! example
    ```
    GET https://api.nucleoid.xyz/stats/player/07e92b46-8386-4067-8f72-8ab96e606fb7

    {
        "bedwars": {
            "damage_dealt": 1238.8,
            "final_kills": 56.0,
            "kills": 84.0,
            "blocks_placed": 532.0,
            "beds_destroyed": 21.0
        }
    }
    ```

Allows for querying all the statistics of a player.

!!! note
    The response is relatively unstructured, as players may have different combinations of games they have collected statistics for.

    The best way to describe the response of this endpoint is by describing the data format on the backend.
    The data returned is described in rust as
    ```rust
    type PlayerStatisticsResponse = HashMap<String, HashMap<String, f64>>;
    ```
    Rust's `HashMap`s are similar to dictionaries in other languages or objects in JavaScript.

### Get player stats for a game
!!! example
    ```
    GET https://api.nucleoid.xyz/stats/player/07e92b46-8386-4067-8f72-8ab96e606fb7/bedwars

    {
        "bedwars": {
            "damage_dealt": 1238.8,
            "final_kills": 56.0,
            "kills": 84.0,
            "blocks_placed": 532.0,
            "beds_destroyed": 21.0
        }
    }
    ```

Allows for filtering the returned statistics by a particular game/namespace.
It will return a response in the same format as [Get all player stats](#get-all-player-stats), just without stats for minigames other than the specified one.

### Get stats for game
!!! warning
    Currently, game IDs are not displayed anywhere in game or in the API, so this endpoint is relatively unusable.

!!! example
    ```
    GET https://api.nucleoid.xyz/stats/game/bda420f0-b480-4f8b-bcc5-7c6c63d51643

    {
        "07e92b46-8386-4067-8f72-8ab96e606fb7": {
            "bedwars": {
                "final_kills": 8,
                "blocks_placed": 76,
                "beds_destroyed": 3,
                "kills": 12,
                "damage_dealt": 154.85
            }
        },
        "00000000-0000-0000-0000-000000000000": {
            "bedwars": {
                "teams": 4
            }
        }
    }
    ```

Allows for querying the statistics after a particular game has been played.

!!! note
    Like the other statistics endpoints, this data is quite unstructured, and is best described with the following:
    ```rust
    type GameStatisticsResponse = HashMap<uuid::Uuid, HashMap<String, HashMap<String, f64>>>;
    ```
    The `uuid::Uuid` type can be substituted for `String` if your language doesn't have a specific type for `UUID`s.
