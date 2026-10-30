# Launcher Recovery Reference

## Hume integration

- Repository: https://github.com/MuddyPaws12/hume-launcher
- Branch: `feature/home-recovery`
- Commit: `a787a3abb9231de0ff4a0db57d6a435b226febef` (`Add optional Home launcher recovery`)
- The integration keeps Android's HOME role as the primary mechanism and adds an optional accessibility recovery service. It does not disable Google TV's launcher.
- Build verified with JDK 17 and Android SDK 34. Debug APK version: `7.9-debug.1`, version code `97`.
- Draft prerelease: https://github.com/MuddyPaws12/hume-launcher/releases/tag/untagged-c96599c52c9c75baaf26
- The draft asset is debug-signed, cannot update the official-signed Hume install, and has not been tested on a physical TV. Do not publish as a stable release without testing and release signing.

## Monet APK analysis

- Analyzed upstream Monet Launcher `v1.1.0`; APK SHA-256: `3fdd45e7ed85f4a26ab6a56924e8a9c298c42c3cb036cb121d15ed6504b9a69c`.
- jadx `1.5.6` and apktool `3.0.3` were used. Apktool decoded successfully; jadx reported 363 decompilation errors, so this is partial static analysis.
- Findings: `HomeActivity` is registered as Android HOME; an optional ADB preset assigns the HOME role; a boot receiver handles boot/update/user-present events; and an opt-in accessibility service detects Google TV launcher windows and can recover Monet to the foreground. The APK does not disable Google TV's launcher.
- The service declares `canRetrieveWindowContent=false`. A separate user-triggered screenshot feature exists.
- Detailed findings are in [Monet analysis](monet-analysis.md). Full APKs and decompilation outputs are excluded from Git because they contain proprietary app material. They remain only in the local `Monet Reverse Engineer/` folder.

## Limits

The Monet analysis is static and the Hume recovery behavior has not been tested on a physical TV. OEM behavior may differ. The draft APK uses a local debug key; its ignored `debug.keystore` is not part of this repository.