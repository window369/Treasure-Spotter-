# TreasureSpotter — Android Studio Build Guide

## What's in this project
A full Android app that wraps the TreasureSpotter web app in a native WebView,
with proper camera permissions, localStorage support, and Play Store-ready structure.

---

## Step 1 — Open in Android Studio
1. Extract this ZIP to a folder on your device
2. Open Android Studio
3. Choose **File → Open** (or "Open an Existing Project")
4. Navigate to the extracted `TreasureSpotter` folder and open it
5. Wait for Gradle sync to finish (may take a few minutes first time)

---

## Step 2 — Set your SDK path
1. Open the file `local.properties` in the project root
2. Find the line `#sdk.dir=/path/to/your/android/sdk`
3. Replace with your actual SDK path, e.g.:
   - Termux: `sdk.dir=/data/data/com.termux/files/home/android-sdk`
   - Standard Linux: `sdk.dir=/home/USERNAME/Android/Sdk`
4. Save the file

---

## Step 3 — Build a debug APK (test on your phone)
In Android Studio:
- Go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**
- The APK will appear at:
  `app/build/outputs/apk/debug/app-debug.apk`
- Transfer to your phone and install (enable "Install from unknown sources" in settings)

---

## Step 4 — Build a release APK (for Play Store)
You need to sign the APK first:

1. Go to **Build → Generate Signed Bundle / APK**
2. Choose **APK**
3. Click **Create new keystore** (first time only)
   - Save it somewhere safe — you need this file FOREVER for updates
   - Fill in your details (name, country code like GB)
4. Fill in passwords and click **Next**
5. Choose **release** build variant
6. Click **Finish**

The signed APK will be at:
`app/build/outputs/apk/release/app-release.apk`

---

## Step 5 — Upload to Play Store
1. Go to play.google.com/console and register (one-time £20 fee)
2. Create a new app → Android App
3. Fill in store listing (title, description, screenshots)
4. Upload your `app-release.apk` under **Release → Production**
5. Set your price
6. Submit for review (usually 1–3 days)

---

## Updating the app in future
To change anything (colours, features, AI prompt):
- Edit `app/src/main/assets/index.html`
- Rebuild the APK (bump `versionCode` and `versionName` in `app/build.gradle` first)
- Upload new APK to Play Store as an update

---

## Troubleshooting
- **Gradle sync fails**: Make sure `local.properties` has the correct SDK path
- **Camera not working**: The app requests camera permission on launch — tap Allow
- **API calls failing**: Check your Anthropic API key in the app settings
- **Build errors**: In Android Studio, go to File → Invalidate Caches → Restart
