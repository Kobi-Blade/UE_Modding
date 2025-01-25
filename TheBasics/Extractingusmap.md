# Extracting `usmap` using Unreal Engine Scripting System

This guide provides detailed instructions to install and configure the Unreal Engine Scripting System (UE4SS/RE-UE4SS) for extracting `usmap` files from a game.

## Step 1: Install the Unreal Engine Scripting System

1. **Download UE4SS**:
   - Visit the official repository: [UE4SS-RE](https://github.com/UE4SS-RE/RE-UE4SS) and download the latest version.

2. **Install UE4SS**:
   - Extract the downloaded files into the bin directory, (Binaries\Win64) next to the game executable.

---

## Step 2: Modify the Configuration File

Once UE4SS is installed, adjust its configuration file to enable features required for extracting the `usmap`.

1. **Locate the Configuration File**:
   - Look for the configuration file, typically named `UE4SS-settings.ini`.

2. **Edit the Configuration File**:
   - Open the `.ini` file in a text editor (e.g., Notepad++ or VSCode) and apply the following changes:

   ```ini
   [Debug]
   ConsoleEnabled = 0
   GuiConsoleEnabled = 1
   GuiConsoleVisible = 1

---

## Step 3: Extract `usmap` file

1. **Launch the game**:
   - Verify that the GUI console appears (it should be visible if configured in `UE4SS-settings.ini`).

3. **Output Mapping File**:
   - Use the Dumper tab of the UE4SS Debugging Tool to output the .usmap file.
   - The file will be output to: `Binaries\Win64\Mappings.usmap`
