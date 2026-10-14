Pixel Dungeon
=============

Traditional roguelike game with pixel-art graphics and simple interface.

Pixel Dungeon on GooglePlay: 
https://play.google.com/store/apps/details?id=com.watabou.pixeldungeon

Official web-site: 
http://pixeldungeon.watabou.ru/

Developer's blog: 
http://pixeldungeon.tumblr.com/

To build the game you will need my unnamed game library:
https://github.com/watabou/PD-classes

Build and debug (VSCode)
========================

Prerequisites:

1. JDK 8 to 11 (Gradle 4.10 does not run on JDK 17+): set `JAVA_HOME` to it
   (or have `java` on PATH). Temurin 8: https://adoptium.net/temurin/releases/?version=8
2. Android SDK, with `ANDROID_HOME` set (or a `local.properties` file with
   `sdk.dir=...`). Required components:

   ```
   sdkmanager "platforms;android-22" "build-tools;28.0.3"
   ```
   (newer Android CLI uses `/` instead of `;`: `"platforms/android-22"` ...)
3. An emulator AVD or an Android phone over USB. To create the default AVD:

   ```
   sdkmanager "system-images;android-28;google_apis;x86_64"
   avdmanager create avd -n pd-api28 -k "system-images;android-28;google_apis;x86_64" -d pixel
   ```
   (another AVD name: `gradlew runDebug -PavdName=Name`)

Steps:

```
git clone <this-repo>
cd pixel-dungeon
gradlew.bat assembleDebug     # Windows (./gradlew on Linux/macOS)
```

In VSCode (extensions "Language Support for Java" and "Debugger for Java"):
press F5 — the `runDebug` task starts the emulator if no device is connected,
installs the APK, launches the app waiting for the debugger and attaches on
port 8700.

Note: modern Android Studio cannot open this project (AGP 3.2/Gradle 4.10 are
from 2018 and AS forces an upgrade). Use the VSCode flow above.

Optional: for full IntelliSense of `android.*` classes, add your local
`android.jar` to `.vscode/settings.json` (machine-specific, adjust the path):

```json
"java.project.referencedLibraries": [
    "C:/Users/you/AppData/Local/Android/Sdk/platforms/android-22/android.jar"
]
```
