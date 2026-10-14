# VirtualBackup Android compatibility test project

This is a modern Android Studio project scaffold based on the uploaded Enyby/VirtualBackup source.

## Important limitations
- This is **not a finished or verified APK**. It is source code prepared for inspection/building.
- The original app copies another app's private data directories using `cp`. On a normal, non-rooted Android 16 phone, Android's app sandbox prevents this. Updating the manifest cannot bypass that restriction.
- The original app's package and generated `R` import were inconsistent; this scaffold aligns the namespace/import to `com.virtualbackup`.
- The target SDK is intentionally kept at 28 for this compatibility experiment, but this does not guarantee installability or functionality on Android 16.
- The original 25 KB APK you uploaded had empty native-library entries; those are not included here because the project has no native source/build for them.

## Build
1. Install Android Studio on a computer and install JDK 17 + Android SDK Platform 35.
2. Open this folder in Android Studio.
3. Let Gradle sync. If prompted, install Android Gradle Plugin dependencies.
4. Build > Build Bundle(s) / APK(s) > Build APK(s).
5. Test only on a spare/test profile first; do not use it for valuable app data.

## What this can and cannot do
This project is useful to test whether a rebuilt UI APK installs. It is **not capable of backing up or restoring other apps' private data on a stock, non-rooted Android 16 device**. A realistic no-root version should back up APKs and user-selected files, and use Android's supported backup/transfer APIs where available.


## Build from your phone with GitHub Actions (no PC)

1. Sign in to GitHub in your phone browser and create a **new empty repository** (do not add a README or license).
2. Download this ZIP, extract it using your phone's file manager, and upload the *contents* of this folder to the repository's `main` branch. Make sure `.github/workflows/build.yml` is included. Some mobile interfaces hide dot-folders; if so, use GitHub's web upload interface and verify the workflow file exists in `.github/workflows/`.
3. Open the repository's **Actions** tab, select **Build VirtualBackup test APK**, then tap **Run workflow** (or wait for the first push workflow to run).
4. When it finishes, open the successful run, scroll to **Artifacts**, and download `VirtualBackup-Android16-debug`. Extract the artifact ZIP to get the APK.
5. Only install it if the build succeeds. Android may show a warning for apps installed outside Play Store.

If the build fails, open the run and copy the first red error lines; those are needed to correct the source.

This workflow builds a **debug/test APK**, not a release APK. A successful build only proves the project compiles. It does not make the original app able to copy other apps' private data on a non-rooted Android 16 phone.
