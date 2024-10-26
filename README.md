```ruby
@title Server Console
@echo off
echo ------------------------------------------------------
echo                (%time%) Server is starting!         
echo ------------------------------------------------------

:: กำหนดตัวแปร JAVA_HOME ให้ชี้ไปยังโฟลเดอร์ของ JDK
set JAVA_HOME=C:\Program Files\Java\jdk-21
:: เพิ่ม JAVA_HOME ลงใน PATH เพื่อให้สามารถเรียกใช้งาน Java จาก command prompt ได้
set PATH=%JAVA_HOME%\bin;%PATH%

:: กำหนดตัวแปร Server_file ให้ชี้ไปยังไฟล์เซิร์ฟเวอร์ Minecraft
set Server_file=purpur-1.21.1-2328.jar
:: ตั้งค่าขนาด Heap ขั้นต่ำ (-Xms) และขนาด Heap สูงสุด (-Xmx)
set -Xms=4096M
set -Xmx=4096M
:: กำหนด Java options สำหรับการปรับประสิทธิภาพ JVM เพื่อให้เซิร์ฟเวอร์ทำงานได้ดีขึ้น
set Java_optioms=-XX:+AlwaysPreTouch -XX:+DisableExplicitGC -XX:+ParallelRefProcEnabled -XX:+PerfDisableSharedMem -XX:+UnlockExperimentalVMOptions -XX:+UseG1GC -XX:G1HeapRegionSize=8M -XX:G1HeapWastePercent=5 -XX:G1MaxNewSizePercent=40 -XX:G1MixedGCCountTarget=4 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1NewSizePercent=30 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:G1ReservePercent=20 -XX:InitiatingHeapOccupancyPercent=15 -XX:MaxGCPauseMillis=200 -XX:MaxTenuringThreshold=1 -XX:SurvivorRatio=32 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true

:StartServer
echo Starting the Minecraft server with the following options:
echo - Minimum Heap Size: %-Xms%
echo - Maximum Heap Size: %-Xmx%
echo ------------------------------------------------------
:: เรียกใช้ไฟล์เซิร์ฟเวอร์ Minecraft ด้วยคำสั่ง java พร้อมกับค่า options และตั้งค่า --nogui เพื่อลดการใช้ทรัพยากร
java -Xms%-Xms% -Xmx%-Xmx% %Java_optioms% -jar "%Server_file%" --nogui

:: เปลี่ยนไปยังโฟลเดอร์ที่มีไฟล์ eula.txt
cd C:\path\to\directory
:: แก้ไข eula.txt เพื่อยอมรับเงื่อนไขการใช้งานโดยเปลี่ยน 'eula=false' เป็น 'eula=true'
powershell -Command "(Get-Content eula.txt) -replace 'eula=false', 'eula=true' | Set-Content eula.txt"

echo ------------------------------------------------------
echo                (%time%) Server restarting!          
echo ------------------------------------------------------
:: หยุดการทำงานเป็นเวลา 5 วินาทีก่อนเริ่มเซิร์ฟเวอร์ใหม่
timeout 5
:: กลับไปยังจุดเริ่มต้นของสคริปต์เพื่อเริ่มเซิร์ฟเวอร์ใหม่อีกครั้ง
goto StartServer
```
