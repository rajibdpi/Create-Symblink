### Need to create a bash file named 'Create\ Symlink':
```bash
~/.local/share/nautilus/scripts/
```
### 1. Download the script to this ' ~/.local/share/nautilus/scripts/' folder:
- ### Open Terminal and run
- using wget
```bash
wget -O ~/.local/share/nautilus/scripts/Create\ Symlink https://raw.githubusercontent.com/rajibdpi/symblink/refs/heads/main/Create%20Symlink
```
- using curl 
```bash
curl -o ~/.local/share/nautilus/scripts/Create\ Symlink https://raw.githubusercontent.com/rajibdpi/symblink/refs/heads/main/Create%20Symlink
```
### 2. Make the Script Executable
Run the following command to make the script executable:
```bash
chmod +x ~/.local/share/nautilus/scripts/Create\ Symlink
```
### 3. Restart Nautilus
To ensure the script appears in the right-click context menu, restart Nautilus:

```bash
nautilus -q
nautilus &
```
