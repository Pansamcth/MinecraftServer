# Minecraft Server Console Script
This batch script is designed to automate the startup of a Minecraft server using Java JDK 21. It includes customizable settings for memory allocation and JVM options to optimize performance. Below is a breakdown of the script's functionality:
1. Set Java Environment:
   - The script sets the `JAVA_HOME` environment variable to the JDK 21 installation path and updates the `PATH` to include the JDK binaries.
2. Server Configuration:
   - The `Server_file` variable should be replaced with the name of your server JAR file (e.g., `paper-1.21.1.jar`).
   - Memory settings are configured to allocate a minimum and maximum heap size of 4096MB.
3. Java Options:
   - The script includes various JVM options aimed at improving server performance, such as enabling the G1 garbage collector and optimizing memory usage.
4. Server Startup:
   - The script enters a loop to start the Minecraft server, displaying the current time and the memory settings being used.
   - It uses the `java` command to run the specified server JAR file without a graphical user interface (`--nogui`).
5. EULA Acceptance:
   - The script changes the `eula.txt` file to accept the End User License Agreement by replacing `eula=false` with `eula=true` using PowerShell.
Restart Loop:
   -If the server stops for any reason, the script waits for 5 seconds and then restarts the server automatically.

This script simplifies the management of a Minecraft server by ensuring that it runs with optimal settings and handles restarts automatically.
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
