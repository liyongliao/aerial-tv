# MiTV-MFTR0 update channel

This branch builds the Xiaomi TV variant of Aerial installed as `com.ts.launcher`. The app checks `update/version.txt` and downloads `update/aerial-standard.apk` from this branch. An update is offered only when the dotted version in `version.txt` exceeds the installed `versionName` prefix. Before installation, the app checks the APK package, signing certificate, and `versionCode`; Android still asks the owner to confirm.

## Install on MiTV-MFTR0

Download [aerial-standard.apk](aerial-standard.apk) from this directory. To replace an earlier `com.ts.launcher` build without clearing its settings, use `adb install -r aerial-standard.apk`, or install the APK through the TV's package installer. Select this app as the default Home launcher if Android asks. The APK has a different package and signature from upstream Aerial, so it will not replace `app.orchard.tv`.

After installation, open Home and check that the wallpaper appears, Settings opens, and standby wake returns to Home. If another launcher is still the default, select this one in Android's Home settings; the control center's setup page links here.

To publish an update:

1. Increment both `versionCode` and the dotted part of `versionName` in `app/build.gradle.kts`.
2. Build `:app:testStandardReleaseUnitTest :app:assembleStandardRelease :app:lintVitalStandardRelease` with the same signing key used by the installed APK.
3. Verify the APK's package, version, signing certificate, and SHA-256. Copy it to `update/aerial-standard.apk`.
4. Write the dotted version to `update/version.txt`, then push the APK and version file together in one commit. Wait for both raw GitHub URLs to return the new content.
5. Install on the TV and test Home, video wallpaper, standby wake, and the in-app update flow before treating the release as validated.

The upstream `app.orchard.tv` APK has a different package and signing certificate and cannot update this fork. Do not include TV addresses, household settings, or signing keys in this branch.
