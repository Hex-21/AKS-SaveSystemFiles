# AKS-SaveSystemFiles
Description for https://reforger.armaplatform.com/workshop/68E1601E02CFCF00

# Advanced Persistence Saving Mod

You can use the default (vanilla) saving system, but this mod adds additional formats—giving you more control over storage size and whether your save files are human-readable.

---

## Saveformats

- Multiple save formats:
  - Compact JSON (one-line)
  - Pretty JSON (human-readable)
  - Binary (fast & small)

---

## Configuration Setup

Below is a minimal example of a server config.  
The important part is the `persistence` section inside `gameProperties`.

```json
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
                "autoSaveInterval": 5,
                "hiveId": 1001,
                "databases": {
                    "main": {
                        "preset": "{A79D2893C8F8F4A9}Configs/Systems/Persistence/Database/BinSaveGame.conf"
                    }
                },
                "storages": {
                    "session": {
                        "database": "main"
                    }
                }
            }
        }
    }
}
```

---

## Save Types

### 1. JSON (One-Line)
**Preset:** `PersistenceJsonSaveGame.conf`

- Compact JSON format (single line)
- Saves disk space
- Still readable if needed

```json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/PersistenceJsonSaveGame.conf"
```

---

### 2. JSON Pretty
**Preset:** `JsonSaveGamePretty.conf`

- Human-readable format
- Easy to inspect and debug
- Larger file size

> Warning: If your save file approaches **16 MB**, saving may fail(it should be fixed but its arma so we will never know).

```json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/JsonSaveGamePretty.conf"
```

---

### 3. Binary (Recommended)
**Preset:** `PersistenceBinSaveGame.conf`

- Fastest and smallest format
- Best for long-running servers
- Not human-readable

```json
"preset": "{68E1601E02CFCF00}Configs/Systems/Persistence/Database/PersistenceBinSaveGame.conf"
```

---

### 4. Vanilla Binary (No Mod Required)

You can also use the base game’s binary saving without this mod:

```json
"preset": "{A79D2893C8F8F4A9}Configs/Systems/Persistence/Database/BinSaveGame.conf"
```

---

## Autosave Settings

```json
"autoSaveInterval": <minutes>
```

- Defines how often the game saves (in minutes)

### Important Limits

- Maximum saves: **999**
- Maximum file size: **16 MB**
- Maybe already increased by Arma but that wasn't the case when I tested it.

### Recommendations

| Use Case                  | Interval |
|---------------------------|----------|
| Long sessions             | 60 min   |
| Frequent crash protection | 10 min   |

> Example:  
> With a 10-minute interval, it takes ~7 days to reach 999 saves.

---

## Tips

- Use **Binary** for performance and stability
- Use **Pretty JSON** only for debugging or development
- Use **One-Line JSON** if you want a balance between size and readability

---

## Support

Need help or have questions?

https://discord.com/invite/akiras-spielwiese

- Ping **Hex**
- Or send a direct message

---

## Notes
