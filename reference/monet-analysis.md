# Monet Launcher Static Analysis

## Artifact and tools

- Analyzed upstream Monet Launcher `v1.1.0`.
- APK SHA-256: `3fdd45e7ed85f4a26ab6a56924e8a9c298c42c3cb036cb121d15ed6504b9a69c`.
- jadx `1.5.6` and apktool `3.0.3` were used. Apktool decoded successfully; jadx reported 363 decompilation errors, so parts of the Java output are incomplete.

## Launcher behavior

- `HomeActivity` is registered for Android's `MAIN` + `HOME` + `DEFAULT` intent and as a Leanback launcher activity.
- An optional ADB preset assigns the Android HOME role (Android 10+) or calls `cmd package set-home-activity` on older versions. The APK does not disable Google TV's launcher.
- `BootReceiver` handles boot completion, app replacement, and user-present events. Additional autostart behavior is configurable.
- An opt-in accessibility service filters key events and observes window-state changes. It detects Google TV's `com.google.android.apps.tv.launcherx` windows and has delayed recovery logic to bring Monet Home forward.
- A separate optional TCL autostart preset does not change the default launcher.
- Accessibility metadata sets `canRetrieveWindowContent=false`. A separate user-triggered screenshot feature exists and is not part of launcher recovery.

## Caveats

This is static analysis, not a runtime test. The app is obfuscated and jadx output is partial. Actual recovery depends on Android TV/OEM behavior and was not tested on a device.

The APKs and full decompilation outputs are excluded from Git and retained only in the local `Monet Reverse Engineer/` folder.