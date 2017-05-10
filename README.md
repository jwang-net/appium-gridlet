# appium-gridlet
the manlet of appium grids

has some dockerfiles
has some node configs

Build base Dockerfile and then build emulator Dockerfiles.

```
docker build -t android-node-base ./base/
docker build -t android-7-emulator ./android_7_emulator/
docker build -t android-5-emulator ./android_5_emulator/
```
