1. Open a terminal and create the file:
```bash
nano ~/.local/share/nautilus/scripts/Create\ Symlink
```
```bash
#!/bin/bash
# Get the selected file or folder and ensure it's valid
SOURCE=$(realpath "$NAUTILUS_SCRIPT_SELECTED_FILE_PATHS")
if [ -z "$SOURCE" ]; then
    zenity --error --text="No file or folder selected!"
    exit 1
fi

# Prompt user for the target directory
TARGET_DIR=$(zenity --file-selection --directory --title="Select target directory for the symlink")

if [ -n "$TARGET_DIR" ]; then
    # Extract the name of the source file/folder
    SOURCE_NAME=$(basename "$SOURCE")
    
    # Create the symbolic link
    ln -s "$SOURCE" "$TARGET_DIR/$SOURCE_NAME" 2>/tmp/symlink_error.log
    if [ $? -eq 0 ]; then
        # Fix permissions and ownership
        chmod -R 755 "$TARGET_DIR/$SOURCE_NAME"
        chown -R $(whoami):$(whoami) "$TARGET_DIR/$SOURCE_NAME"
        zenity --info --text="Symbolic link created successfully at $TARGET_DIR/$SOURCE_NAME"
    else
        ERROR_MSG=$(< /tmp/symlink_error.log)
        zenity --error --text="Failed to create symbolic link:\n$ERROR_MSG"
    fi
else
    zenity --error --text="Operation cancelled. No target directory selected."
fi

# Get the selected file or folder and ensure it's valid
SOURCE=$(realpath "$NAUTILUS_SCRIPT_SELECTED_FILE_PATHS")
if [ -z "$SOURCE" ]; then
    zenity --error --text="No file or folder selected!"
    exit 1
fi

# Prompt user for the target directory
TARGET_DIR=$(zenity --file-selection --directory --title="Select target directory for the symlink")

if [ -n "$TARGET_DIR" ]; then
    # Extract the name of the source file/folder
    SOURCE_NAME=$(basename "$SOURCE")
    
    # Create the symbolic link
    ln -s "$SOURCE" "$TARGET_DIR/$SOURCE_NAME" 2>/tmp/symlink_error.log
    if [ $? -eq 0 ]; then
        # Fix permissions and ownership
        chmod -R 755 "$TARGET_DIR/$SOURCE_NAME"
        chown -R $(whoami):$(whoami) "$TARGET_DIR/$SOURCE_NAME"
        zenity --info --text="Symbolic link created successfully at $TARGET_DIR/$SOURCE_NAME"
    else
        ERROR_MSG=$(< /tmp/symlink_error.log)
        zenity --error --text="Failed to create symbolic link:\n$ERROR_MSG"
    fi
else
    zenity --error --text="Operation cancelled. No target directory selected."
fi

```
2. Make the Script Executable
Run the following command to make the script executable:
```bash
chmod +x ~/.local/share/nautilus/scripts/Create\ Symlink
```
3. Restart Nautilus
To ensure the script appears in the right-click context menu, restart Nautilus:

```bash
nautilus -q
nautilus &
```
