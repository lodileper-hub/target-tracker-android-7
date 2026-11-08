# Target Tracker (v0.24, Android 7 build) - Android app

Works fully offline. Needs Android 7.0 or newer (also runs on newer versions). Landscape only.

Android 7-9 notes: the app asks for "storage" permission on first launch (needed to save videos, screen shots and
profiles; allow it). Camera needs a reasonably current "Android System WebView" - on Android 7 update it (and Chrome)
from the Play Store if the camera does not start.

## Easiest way: let GitHub build the APK for you (nothing to install)

1. Make a free account at github.com and click **New repository** (name it anything, set it to Private).
2. On the new repository page click **uploading an existing file**.
3. Unzip this package on your computer, open the unzipped folder, select EVERYTHING inside it
   (including the `app` folder, `gradle` folder and the hidden `.github` folder) and drag it into the browser.
   Click **Commit changes**.
   - If the `.github` folder did not upload (hidden folders are sometimes skipped): click
     **Add file > Create new file**, type `.github/workflows/build-apk.yml` as the name, paste the contents
     of that file from this package, and commit.
4. Click the **Actions** tab. A run called "Build APK" starts by itself (about 3-5 minutes).
   If nothing is running, choose "Build APK" on the left and press **Run workflow**.
5. When it shows a green tick, open the run, scroll to **Artifacts** and download **TargetTracker-APK**
   (a zip with `app-debug.apk` inside).
6. Copy `app-debug.apk` to the phone (USB, Google Drive, e-mail to yourself...), tap it, and allow
   "Install unknown apps" for the app you opened it from. If Play Protect warns about an unknown developer,
   choose "Install anyway" (the app is signed with a debug key, which is fine for personal use).

If the run shows a red cross, open it, click the failed step, and send me the last ~30 lines of the log.

## Alternative: Android Studio

1. Install Android Studio, choose **Open**, and select this folder.
2. Let it sync (it downloads Gradle and the Android SDK parts by itself).
3. **Build > Build Bundle(s) / APK(s) > Build APK(s)**. The file is in `app/build/outputs/apk/debug/app-debug.apk`.
   Or plug in the phone (USB debugging on) and press the green Run button.

## Using the app

- First launch: allow the camera when asked.
- The controls are in a drawer: tap the menu button at the top right. Tapping the video closes it.
- Saved videos go to Movies/TargetTracker, screen shots to Pictures/TargetTracker, settings/profile
  files to Download/TargetTracker. Saved settings, profiles and all-time counts stay inside the app.
- Updating later: replace `app/src/main/assets/index.html` with your new version and build again.
  Install the new APK over the old one; your saved settings and profiles are kept.

## Updating the app later

1. Replace `TargetTracker-android-project.zip` in the GitHub repository: **Add file > Upload files**, drop the new zip
   (same file name) and commit. The build starts by itself.
2. Download the new APK from the finished run and install it over the old one.
   From this version on every build is signed with the same key (`app/debug.keystore`), so updates install
   over the top and keep your saved profiles, settings and all-time counts.
   (Builds made before this version used a random key. Installing this version over one of those needs an
   uninstall first, which erases that older app's saved data.)
