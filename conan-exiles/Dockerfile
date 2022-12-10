# Pull our base SteamCMD image
FROM thetestgame/steam:stable

# Set our required environment variables
ENV PUID=50500
ENV PGID=50500
ENV UPDATE_OS=1
ENV UPDATE_STEAM=1
ENV UPDATE_SERVER=1
ENV PLATFORM=windows
ENV STEAM_APP_ID=443030
ENV TZ=America/Los_Angeles

# Expose our ports
EXPOSE 27015
EXPOSE 27015
EXPOSE 27016
EXPOSE 7777
EXPOSE 7778

# Copy our startup script into the container
COPY custom_server /data/custom_server