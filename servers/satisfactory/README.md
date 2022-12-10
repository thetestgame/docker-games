# Satisfactory

> This is **NOT** an official Satisfactory docker container.

Dedicated Satisfactory server using Docker.

## Version Tags

| Tag          | Description                        |
|--------------|------------------------------------|
| stable       | Latest stable release build        |
| latest       | Latest stable release build        |
| experimental | Latest experimental release build  |
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
|`15777`| UDP      | Mandatory | Query Port. This is the port that you need to enter in the game when you first connect to a dedicated server. This port can be redirected freely. |
|`15000`| TCP      | Optional  | Beacon Port. This port is automatically incremented if multiple instances of the server are launched and the default is in use already. As of Update 6, this port can be redirected freely. |
|`7777` | UDP      | Optional  | Game Port. This port can be redirected freely using the -Port paramater upon server startup, e. g. "-Port=10000" to change the game port to UDP port 10000. At present, if the default port is in use, the next higher one will be checked until a free port is found, and it will be used. |

## Volumes

| Volume  | Function                           |
|---------|------------------------------------|
| /data   | User data location for the server. |
