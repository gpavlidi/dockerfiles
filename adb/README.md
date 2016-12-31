# adb
Docker-adb is a small alpine container with [Android Debug Bridge](https://developer.android.com/studio/command-line/adb.html) installed.
Uses [sorccu/docker-adb](https://github.com/sorccu/docker-adb) image.

### Why?
I keep needing to use ```adb``` frequently whenever I want to sideload apps in an Android device. Thought it 'll be a great candidate for dockerizing since it keeps things neat and portable.

### Usage

After **docker pull gpavlidi/adb**, follow the below 2 steps:

- Launch the adb container from the directory that contains the .apk
```
docker run --rm -it -v ${PWD}:/root/src --name adb gpavlidi/adb
```

- Then use some of the below, depending on what you need to do
```
adb kill-server
adb start-server
adb connect <ip-address-of-fire-tv>
adb install <apk-file-name>
# if upgrading
adb install -r <apk-file-name>
# to uninstall
adb uninstall -k org.xbmc.kodi
```
