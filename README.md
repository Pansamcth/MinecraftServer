## Requirements
- **Computer:** A computer with good specifications to support multiple players (recommended: a modern CPU and at least 8GB of RAM).
- **Internet** Connection: A stable connection with sufficient bandwidth.
- **Java Development Kit (JDK):** Install the latest version of JDK.
- **Minecraft Server Software:** Download from the official Minecraft website.

## Install Java
> [!NOTE]
> ## Java Requirement
> | Server Version | Java Version |
> | --- | :---: |
> | 1.8 to 1.11 | Java 8 |
> | 1.12 to 1.16.4 | Java 11 |
> | 1.16.5 | Java 16 |
> | 1.17.1-1.18.1+ | Java 21 |
- **Download the Java Development Kit (JDK)**
  - Open your web browser and go to the [Oracle JDK download page](https://www.oracle.com/java/technologies/downloads/?er=221886#java22).
  - Find the latest version of JDK and click on the "Windows" tab.
  - Download the appropriate installer for your system (e.g., `jdk-xx_windows-x64_bin.exe` for 64-bit Windows).

- **Run the Installer**
  - Once the download is complete, locate the downloaded installer file and double-click it to run.
  - If prompted by the User Account Control (UAC), click "Yes" to allow the installer to make changes to your computer.
- **Install the JDK**
  - The installation wizard will open. Click "Next" to start the installation process.
  - Choose the installation directory. By default, it will be `C:\Program Files\Java\jdk-xx` (where `xx` is the version number).
  - It's usually best to leave this as the default.
  - Click "Next" to continue.
  - The installer will install the JDK and might also install the JRE (Java Runtime Environment).
  - Once the installation is complete, click "Close" to exit the installer.

## Create a Folder and Manage Files
- **Create a folder for the Minecraft server:**
  - Open File Explorer.
  - Create a new folder at your desired location, e.g., `C:\MinecraftServer`

## Create a Server Start Script
- Open Notepad or any text editor.
- Enter the following code into the file:
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
> [!TIP]
> If you want to increase the memory that the program can use, you can change the values of the -Xms and -Xmx parameters to the desired amount. For example, if you want to increase the memory to 8 gigabytes, you can change the command to:
>```ruby
> java -Xms8G -Xmx8G -jar "%downloaded_file%" nogui
> ```

- **Save the File**
  - Click the File menu at the top-left corner of the Notepad or any text editor.
  - Select `Save As....`
  - In the Save As dialog, navigate to the folder where your Minecraft server files are located.
  - In the File name field, type `start.bat`
  - In the Save as type dropdown, select All Files.
  - Click the Save button.

## Start the Server
- Navigate to the folder where you saved the `start.bat` file.
- Double-click the `start.bat` file to run your Minecraft server.
