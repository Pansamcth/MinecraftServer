# PURPUR AUTO UPDATED AND RESTART

## Enter the following code into the file:
```ruby
@title Server Console
@echo off
echo (%time%) Server has starting!...
echo (%time%) Update found, downloading...

set "jar_url=https://mineacademy.org/api/purpur/latest"
set "downloaded_file=server.jar"
curl -o "%downloaded_file%" "%jar_url%"

echo (%time%) Jar Update  succassfully!
echo (%time%) Launching Server
echo ------------------------------------------------------

:StartServer
java -Xms8G -Xmx8G -jar "%downloaded_file%" nogui

cd C:\path\to\directory
powershell -Command "(Get-Content eula.txt) -replace 'eula=false', 'eula=true' | Set-Content eula.txt"

echo (%time%) Server restarting!
timeout 5
goto StartServer
```
> [!NOTE]
> ## Additional Explanation
> - **Downloading the Server File:** The script downloads the latest version of the Minecraft server from MineAcademy.
> - **Automatically Accepting EULA:** The script automatically edits the eula. txt file to accept the EULA.
> - **Looping:** If the server stops, the script waits for 5 seconds and then restarts the server automatically.

> [!TIP]
> If you want to increase the memory that the program can use, you can change the values of the -Xms and -Xmx parameters to the desired amount. For example, if you want to increase the memory to 8 gigabytes, you can change the command to:
>```ruby
> java -Xms8G -Xmx8G -jar "%downloaded_file%" nogui
> ```
