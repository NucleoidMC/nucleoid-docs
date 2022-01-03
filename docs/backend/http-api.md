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

### Get statistics stats

!!! example
    ```
    GET https://api.nucleoid.xyz/stats/stats

    {
        "unique_players": 141,
        "games_played": 540,
        "entries": {
            "player": 10125,
            "global": 0,
            "total": 10125
        },
        "grand_total": {
            "player": 662742.2732343078,
            "global": 0,
            "total": 662742.2732343078
        }
    }
    ```

Returns some information about the amount of statistics that have been recorded in total.

## Leaderboards

### Get leaderboard

!!! example
    ```
    GET https://api.nucleoid.xyz/leaderboard/nucleoid:games_played

    [
        {
            "player": "0529de78-7795-4382-ba3c-350fe3159cc3",
            "ranking": 1,
            "value": 151
        },
        {
            "player": "c705fc7d-0962-4d1e-905b-b83d81d9b4ec",
            "ranking": 2,
            "value": 136
        },
        {
            "player": "c40d10d3-f2ee-47a6-92ec-63b53b6fdf01",
            "ranking": 3,
            "value": 109
        },
        ...
    ]
    ```

Returns the top 10 of the specified leaderboard.

#### Leaderboard entry object

| Field | Description |
| ----- | ----------- |
| `player` | The UUID of the player |
| `ranking` | The player's position in the leaderboard |
| `value` | The score/statistic value the player has in this leaderboard |

!!! warning
    This endpoint may be changed in future to allow querying a specific section of the leaderboard.

### Get player rankings

!!! example
    ```
    GET https://api.nucleoid.xyz/player/5ad3ab57b55646359ba99a9a0568965a/rankings

    {
        "nucleoid:games_played": [34, 15],
        "destroy_the_monument:games_won": [14, 1],
        "destroy_the_monument:total_kills": [19, 8],
        "destroy_the_monument:damage_dealt": [19, 237.21775656938553],
        "electricfloor:longest_time": [27, 70.85],
        "electricfloor:blocks_converted": [15, 536]
    }
    ```

Allows for querying a player's locations in the leaderboards.
Each item in the returned item corresponds to one leaderboard, and the value is a pair, `[ranking, value]`, which have the same meaning as in the [Leaderboard entry object](#leaderboard-entry-object)
