# MinecraftServer

```ruby
@title Server Console
@echo off

set "jar_url=https://mineacademy.org/api/paper/latest"
set "downloaded_file=paperclip.jar"

curl -o "%downloaded_file%" "%jar_url%"

:StartServer
java -Xms4G -Xmx4G -jar "%downloaded_file%" nogui

cd C:\path\to\directory
powershell -Command "(Get-Content eula.txt) -replace 'eula=false', 'eula=true' | Set-Content eula.txt"

echo (%time%) Server restarting!
timeout 5
goto StartServer
```
