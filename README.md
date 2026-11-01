name: Build APK
on:
  push:
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - name: Unzip project
        run: unzip -q Hesabdari-Android.zip
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.2
      - name: Build
        run: gradle assembleDebug --no-daemon
        working-directory: Hesabdari
      - uses: actions/upload-artifact@v4
        with:
          name: hesabdari-apk
          path: Hesabdari/app/build/outputs/apk/debug/app-debug.apk
