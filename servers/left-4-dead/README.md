# Left 4 Dead

> This is **NOT** an official Valve docker container.

Dedicated Left 4 Dead server using Docker.

## Version Tags

| Tag          | Description                        |
|--------------|------------------------------------|
| stable       | Ubuntu 20.04:                      |
| latest       | Ubuntu 20.04: This **WILL** break. |
| experimental | Ubuntu 20.04: This **WILL** break. |
* Containers are automatically rebuilt weekly on Tuesday.

## Parameters

| Parameter        | Function                                                                                 | Default        |
|------------------|------------------------------------------------------------------------------------------|----------------|
| SERVER_DIR       | Location for server files.                                                               | `/data/server` |
| STEAM            | Location of steamcmd client.                                                             | `/steam`       |
| STEAM_APP_EXTRAS | Optional. Additional options and values for steam app update, e.g setting BETA versions. | ``             |
| UPDATE_OS        | Update core OS on startup. `1` enable, `0` disable.                                      | `1`            |
| UPDATE_STEAM     | Update steamcmd on startup. `1` enable, `0` disable.                                     | `1`            |
| UPDATE_SERVER    | Update dedicated server specified by `STEAM_APP_ID` on startup. `1` enable, `0` disable. | `1`            |
| PUID             | User ID to run steamcmd under as well as mount permissions.                              | `50510`        |
| PGID             | Group ID to run steamcmd under as well as mount permissions.                             | `50510`        |
| LANG             | Language environment to use in containers.                                               | `en_US.UTF-8`  |
| LANGUAGE         | Language environment to use in containers.                                               | `en_US:UTF-8`  |
| LC_ALL           | Language environment to use in containers.                                               | `en_US.UTF-8`  |

## Ports

| Port  | Protocol | Required? | Description                  |
|-------|----------|-----------|------------------------------|
|`27015`| UDP      | Mandatory | Gameplay traffic.            |
|`27015`| TCP      | Optional  | SRCDS RCON port.             |
|`27016`| UDP      | Optional  | Steam announce traffic.      |

## Volumes

| Volume  | Function                           |
|---------|------------------------------------|
| /data   | User data location for the server. |

## Docker Compose

```
version: "3"

services:
  l4d:
    image:             thetestgame/left-4-dead:stable
    restart:           unless-stopped
    container_name:    l4d
    ports:
      - '27015:27015'
      - '27015:27015/udp'
      - '27016:27016/udp'
    environment:
      - PUID=50510
      - PGID=50510
    volumes:
      - game_data:/data:/data

volumes:
    game_data:
```

### Add custom server configuration.
`server.cfg`
``` ini
hostname                    "{NAME}"
sv_password                 "{PASS}"
sv_allow_lobby_connect_only 0
sv_steamgroup_exclusive     0
sv_gametypes                "coop,survival,versus,teamversus"
mp_gametypes                "coop,survival,versus,teamversus"
rcon_password               "{RCON PASS}"
sv_rcon_banpenalty          360
sv_rcon_log                 1
sv_rcon_maxfailures         3
sv_rcon_minfailuretime      600

// General Play
motd_enabled          1
mp_disable_autokick   1
sv_allow_wait_command 0
sv_alltalk            0
sv_alternateticks     0
sv_cheats             0
sv_consistency        1
sv_contact            ""
sv_downloadurl        ""
sv_pausable           0
sv_lan                0
sv_region             1

// Rate settings
sv_minrate    40000   // Min bandwidth rate allowed on server
sv_maxrate    50000   // Max bandwidth rate allowed on server
sv_mincmdrate 0       // Minimum cmd rate (match server tickrate)
sv_maxcmdrate 67      // Minimum cmd rate (match server tickrate)

// Server Logging
sv_log_onefile 0      //Log server information to only one file.
sv_logbans     1      //Log server bans in the server logs.
sv_logecho     1      //Echo log information to the console.
sv_logfile     1      //Log server information in the log file.
sv_logflush    0      //Flush the log file to disk on each write (slow).
sv_logsdir     "logs" //Folder in the game directory where server logs will be stored.
```
See [Left 4 Dead CVARS](https://developer.valvesoftware.com/wiki/List_of_L4D_Cvars)
