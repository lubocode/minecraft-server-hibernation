# Image for compiling script
FROM golang:latest AS buildstage
# Copy script, change to subdir and compile
COPY minecraft-server-hibernation.go /usr/src/
WORKDIR /usr/src/
RUN go build minecraft-server-hibernation.go

# Image for running script
FROM openjdk:8-jre-slim
LABEL \
    maintainer="lubocode@outlook.com" \
    org.label-schema.name="minecraftserver-hibernation" \
    org.label-schema.description="OpenJDK 8 image with GO script for automatically starting and stopping the supplied Minecraft server." \
    org.label-schema.url="https://www.minecraft.net/download/server/" \
    org.label-schema.vcs-url="https://github.com/lubocode/minecraft-server-hibernation"
# Add bash and screen utility to start and stop MC server
# Sudo needed to correct permissions on screen folder
RUN apt update; \
        apt install bash screen sudo; \
        mkdir -p /var/run/screen; \
        sudo chmod 777 /var/run/screen;
# Add a runtime user
RUN useradd --create-home --shell /bin/bash runtimeuser
USER runtimeuser
WORKDIR /home/runtimeuser/
# Expose Port specified in script
EXPOSE 25555
# Volume for user to insert Minecraft server Java file
VOLUME ["/minecraftserver"]
# Environment variables to change script parameters at runtime
ENV minRAM=512M \
    maxRAM=2G \
    mcPath=/minecraftserver/ \
    mcFile=minecraft_server.jar
# Copy compiled go script from first stage
COPY --from=buildstage /usr/src/minecraft-server-hibernation .
ENTRYPOINT ./minecraft-server-hibernation -minRAM=${minRAM} -maxRAM=${maxRAM} -mcPath=${mcPath} -mcFile=${mcFile}
