# Applescript

|                               |                                                          |
| ----------------------------- | -------------------------------------------------------- |
| <p>tell / end tell</p><p></p> | - begin statement end - end statement                    |
| keystroke                     | keystroke using {command down, option down} key code 123 |

\-- name all processes tell application "System Events" to name of processes

\--Setting SettingBounds tell application "Finder" to set the bounds of the window 1 to {x,y,width,height} -- SettingBounds using System events tell application "System Events" to tell process "After Effects" set position of window 1 to {0, 50} set size of window 1 to {600, 650} end tell
