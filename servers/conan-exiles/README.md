# Conan Exiles

> This is **NOT** an official Funcom docker container.

Generic Conan Exiles dedicated server using Docker.

## Version Tags

| Tag          | Description                                                 |
|--------------|-------------------------------------------------------------|
| stable       | Ubuntu 20.04: wine.                                         |
| latest       | Ubuntu 20.04: winehq STABLE packages. This **WILL** break.  |
| experimental | Ubuntu 20.04: winehq STAGING packages. This **WILL** break. |
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
| PUID             | User ID to run steamcmd under as well as mount permissions.                              | `1000`         |
| PGID             | Group ID to run steamcmd under as well as mount permissions.                             | `1000`         |
| LANG             | Language environment to use in containers.                                               | `en_US.UTF-8`  |
| LANGUAGE         | Language environment to use in containers.                                               | `en_US:UTF-8`  |
| LC_ALL           | Language environment to use in containers.                                               | `en_US.UTF-8`  |

## Ports

| Port  | Protocol | Required? | Description                  |
|-------|----------|-----------|------------------------------|
|`27015`| UDP      | Mandatory | Gameplay traffic.            |
|`27015`| TCP      | Optional  | SRCDS RCON port.             |
|`27016`| UDP      | Optional  | Steam announce traffic.      |
|`7777` | TCP/UDP  | Mandatory | Mod download/Game traffic.   |
|`7778` | UDP      | Mandatory | Pinger traffic.              |

## Volumes

| Volume  | Function                           |
|---------|------------------------------------|
| /data   | User data location for the server. |