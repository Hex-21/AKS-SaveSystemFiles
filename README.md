# AKS-SaveSystemFiles

Description for
https://reforger.armaplatform.com/workshop/68E1601E02CFCF00

# Advanced Persistence Saving Mod

You can use the default (vanilla) persistence system, but this mod adds
additional save formats, giving you more control.

------------------------------------------------------------------------

## Save Formats

Available save formats:

-   Compact JSON (single-line)
-   Pretty JSON (human-readable)
-   Binary (fast & compact)
-   Legacy vanilla formats (SCR for compatibility)

------------------------------------------------------------------------

## Configuration Setup

Below is a minimal server configuration example.

The important part is the `persistence` section inside `gameProperties`.

``` json
{
    "region": "EU",
    "bindAddress": "127.0.0.1",
    "bindPort": 4444,
    "publicAddress": "127.0.0.1",
    "publicPort": 4444,
    "game": {
        "name": "ServerName",
        "password": "",
        "passwordAdmin": "example",
        "admins": [],
        "scenarioId": "{C68BD3FF887CAA28}/example",
        "visible": true,
        "maxPlayers": 50,
        "crossPlatform": true,
        "gameProperties": {
            "missionHeader": {
                "aiPlayerCount": 100,
                "aiDifficulty": "noob",
                "restartDelay": 20,
                "m_sName": "ScenarioName",
                "m_sDetails": "BSP"
            },
            "persistence": {
                "autoSaveInterval": 1,
                "saveRetention": 16,
                "loadSessionSave": true,
                "keepSessionSave": false,
                "hiveId": 1001,
                "databases": {
                    "Main": {
                        "preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/BinarySaveGame.conf"
                    }
                },
                "storages": {
                    "session": {
                        "database": "Main"
                    }
                }
            }
        }
    }
}
```

# Save Types

## 1. Binary (Recommended)

**Preset:** `BinarySaveGame.conf`

-   Fastest save format
-   Smallest file size
-   Recommended for production servers
-   Not human-readable

``` json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/BinarySaveGame.conf"
```

## 2. JSON (Compact)

**Preset:** `JsonSaveGame.conf`

``` json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/JsonSaveGame.conf"
```

## 3. Pretty JSON

**Preset:** `PrettyJsonSaveGame.conf`

> **Warning:** Very large save files

``` json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/PrettyJsonSaveGame.conf"
```

## Legacy Vanilla Formats

### Binary (Legacy)

``` json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/SCR_BinarySaveGame_OLD.conf"
```

### JSON (Legacy)

``` json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/SCR_JsonSaveGame_OLD.conf"
```

# Autosave Settings

``` json
"autoSaveInterval": <minutes>
```

`autoSaveInterval` Defines when saves are made every X min.

``` json
"saveRetention": <number>
```

`saveRetention` Defines how many save files are kept simultaneously (`1–128`).

``` json
"loadSessionSave": true
"keepSessionSave": false
```

-   `loadSessionSave` loads the latest session save when the server
    starts.
-   `keepSessionSave` keeps session save files after the session ends from the round before.

# Important Limits

-   Maximum save file size: **16 MB**
-   This limit may have been increased by Bohemia Interactive, but it
    was still present during my testing.

# Recommendations

-   **Binary** - Recommended for almost all servers.

# Support

https://discord.com/invite/akiras-spielwiese

-   Ping **Hex**
-   Or send a DM.
