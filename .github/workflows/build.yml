name: Gerar APK

on:
  workflow_dispatch:

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 35
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      - uses: android-actions/setup-android@v3

      - name: Preparar projeto e SDK
        run: |
          sdkmanager 'platforms;android-36' 'build-tools;35.0.0'
          unzip -q OpenFrameMotion-source-0.1.0.zip -d source
          chmod +x source/OpenFrameMotion/gradlew

      - name: Compilar APK
        working-directory: source/OpenFrameMotion
        run: ./gradlew assembleDebug --stacktrace

      - uses: actions/upload-artifact@v4
        with:
          name: OpenFrameMotion-APK
          path: source/OpenFrameMotion/app/build/outputs/apk/debug/app-debug.apk
          if-no-files-found: error
