name: Build APK
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q zoro-mc-host.zip
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.7
      - run: cd zoro-mc-host && gradle assembleDebug
      - uses: actions/upload-artifact@v4
        with:
          name: zoro-mc-host-debug
          path: zoro-mc-host/app/build/outputs/apk/debug/*.apk
