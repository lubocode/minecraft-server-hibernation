# Minecraft Server Hibernation
[![mvsh - logo](https://user-images.githubusercontent.com/53654579/90397372-09a9df80-e098-11ea-925c-29e9bdfc0b48.png)](https://github.com/gekigek99/minecraft-server-hibernation)

Go script originally written by [gekigek99](https://github.com/gekigek99/minecraft-server-hibernation)\
Modified for docker usage by [lubocode](https://github.com/lubocode/minecraft-server-hibernation)

This image does **NOT** contain a minecraft server installation.\
Please insert your minecraft server files into the associated volume.
Your minecraft server file should lie in the top level of the volume and should be named minecraft_server.jar\
If you want to deviate from this, use the arguments specified below.
Similarly, if you want to change the amount of RAM for your MC server, have a look at the arguments as well.

The script operates on port 25555 inside the Docker and passes traffic through to 25565 for the MC server, which is MCs standard port. \
Map the internal port to whatever external port fits you. 25565 would save you the hassle of having to specify a port in the MC client server settings.

## Usage example:

```bash
docker run \
    -p 25555:25555 \
    -v /absolute/path/to/mc/folder:/minecraftserver:rw \
    -e minRAM=512M \
    -e maxRAM=2G \
    -e mcPath=/minecraftserver/ \
    -e mcFile=minecraft_server.jar \
    minecraftserver-hibernate
```
The volume name inside the container corresponds to the mcPath string.

**Please report bugs [here](https://github.com/gekigek99/minecraft-server-hibernation/issues)** \
As there are only two people working on the script and only me on the docker implementation, we may miss some bugs from time to time and appreciate all help.
