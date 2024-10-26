```ruby
@title Server Console
@echo off
echo ------------------------------------------------------
echo                (%time%) Server is starting!         
echo ------------------------------------------------------

set JAVA_HOME=C:\Program Files\Java\jdk-21
set PATH=%JAVA_HOME%\bin;%PATH%

set Server_file=***Your Jar file***
set -Xms=4096M
set -Xmx=4096M
set Java_optioms=-XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+ParallelRefProcEnabled -XX:+PerfDisableSharedMem -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:G1HeapRegionSize=8M -XX:G1HeapWastePercent=5 -XX:G1MaxNewSizePercent=40 -XX:G1MixedGCCountTarget=4 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1NewSizePercent=30 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:G1ReservePercent=20 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxGCPauseMillis=200 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true

:StartServer
echo Starting the Minecraft server with the following options:
echo - Minimum Heap Size: %-Xms%
echo - Maximum Heap Size: %-Xmx%
echo ------------------------------------------------------
java -Xms%-Xms% -Xmx%-Xmx% %Java_optioms% -jar "%Server_file%" --nogui

cd C:\path\to\directory
powershell -Command "(Get-Content eula.txt) -replace 'eula=false', 'eula=true' | Set-Content eula.txt"

echo ------------------------------------------------------
echo                (%time%) Server restarting!          
echo ------------------------------------------------------
timeout 5
goto StartServer
```
> [!WARNING]
> This script requires Java [JDK 21](https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html) to function. The JAVA_HOME variable is set to the JDK 21 directory path, and this path is added to the PATH environment variable. This setup ensures that the Minecraft server uses JDK 21 to run, along with specific Java options configured in the script to enhance performance.

> [!TIP]
> ## Here are the server types that can be used in Minecraft (Java Edition):
> - **[Vanilla (Minecraft.net)](https://www.minecraft.net/en-us/download/server)** - Supports Datapacks from Mojang.
> - **[Spigot](https://getbukkit.org/download/spigot)** - Supports Plugins and is suitable for large servers.
> - **[Paper](https://papermc.io/downloads/paper)** - A fork of Spigot that enhances performance and supports Spigot plugins.
> - **[Purpur](https://purpurmc.org/downloads)** - A fork of Paper that is more flexible and customizable.
> - **[Forge](https://files.minecraftforge.net/net/minecraftforge/forge/)** - Designed for Mods, suitable for adding new content to the game.
> - **[Fabric](https://fabricmc.net/use/server/)** - A modding platform that emphasizes speed and flexibility.
