---
description: The essential guide to essential knowledge for essential stuff
---

# Mac Superuser

## Troubleshooting

### [Apps will not connect to internet](https://apple.stackexchange.com/questions/6147/some-applications-on-macbook-pro-think-internet-is-not-connected-when-it-is)

```
dscacheutil -flushcache
```

### [External HDD won't mount](https://apple.stackexchange.com/questions/268998/external-hard-drive-wont-mount)

#### Diagnostics

```
ps aux | grep fsck
```

```
sudo kill -9 2587
```

###



* [Remove monitor audio output](https://discussions.apple.com/thread/6044880)
  * I think I found a solution! It's not about the audio output - it's about what display is your 'main display'. You need to go to System preferences > Display > Arrangement. Here, drag that little white title bar on the main display screen, which currently will be on the HDMi display, to your mac display. Apple will always keep the audio output corresponding to the main display as the main audio source. Once you change the main display to your inbuilt display, the HDMi audio output is never used by default! This solved it for me.
  * A simple fast way to select connected Audio Output devices, is to hold the Alt (option) key and click the Sound icon on your Menu Bar.

### Bypass Gatekeep to use apps from anywhere

1. Use[ terminal to disable settings](https://macpaw.com/how-to/allow-apps-anywhere)
2. Control + RMB open an app

## Apps

* **Utilities**
  * Magnet: [https://apps.apple.com/us/app/magnet/id441258766?mt=12](https://apps.apple.com/us/app/magnet/id441258766?mt=12)

## Essentials Shortcuts

| Shortcut             | Function        |
| -------------------- | --------------- |
| Cmd shift A          | Applications    |
| Command + Spacebar   | Finder bar      |
| Cmd + Shift + G      | Go to path      |
| Option + RMB on file | Get file name   |
| Shift-Cmd-Q          | Log out         |
| F3                   | Mission Control |
| Cmd-F3               | Show Desktop    |



### Get path directory of file (hold option + RMB)

![](../../../.gitbook/assets/MAC\_copyPathname.gif)

## Notes

* Make use of Finder top bar
* Preview in 'collage"
