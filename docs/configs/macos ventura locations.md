Macos Ventura removed locations from the settings panel. Here is how you can set or switch to different locations from the terminal.
```
networksetup -getcurrentlocation 
networksetup -listlocations 
networksetup -createlocation <location name> [populate] 
networksetup -deletelocation <location name> 
networksetup -switchtolocation <location name>
```
