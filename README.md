# Mystery Cartridge

A retro multi-game cartridge for Android. Every time you fully close and reopen
the app, it inserts a game you haven't seen yet. Once all 33 cartridges have
been found, the collection reshuffles and a new cycle begins.

The whole game lives in one file: `www/index.html`. The `android/` folder is the
native Android wrapper (built with Capacitor) that turns it into an installable app.

---

## Option A: build the APK on GitHub (nothing to install)

1. Create a free account at github.com if you don't have one.
2. Create a new repository (for example `mystery-cartridge`). Private is fine.
3. On the new repository page choose **uploading an existing file**, then drag in
   everything from this folder **except `node_modules`** (it isn't included in the zip anyway).
4. Check that the file `.github/workflows/build-apk.yml` was uploaded. Some computers
   hide folders that start with a dot. If it's missing: **Add file → Create new file**,
   name it `.github/workflows/build-apk.yml`, paste in the contents of that file, and commit.
5. Open the **Actions** tab. A run called "Build Android APK" starts automatically
   (or press **Run workflow**). It takes about 5 minutes.
6. When it shows a green tick, open the run and download **mystery-cartridge-apk**
   under *Artifacts*. Unzip it to get `app-debug.apk`.

## Option B: build it on your own computer

You need Node.js 22+, Android Studio, and Java 21 (Android Studio includes it).

```
npm install
npx cap sync android
npx cap open android
```

Android Studio opens the project. Plug in your phone with USB debugging on and
press the green Run button, or use *Build → Build APK(s)*.

---

## Installing on your phone

1. Send `app-debug.apk` to your phone (Google Drive, email, USB, or download it
   directly on the phone from the GitHub Actions page).
2. Tap the file. Android will ask you to allow installs from that app (for example
   Files or Chrome). Allow it, then tap **Install**.
3. Google Play Protect may warn that the app is from an unknown developer. That's
   normal for a test build you made yourself; choose to install anyway.

## Testing tips

- **Getting a new cartridge:** swipe the app away in the recent-apps screen, then
  open it again. If you reopen it within 2 minutes, you continue the same cartridge
  (this protects you when Android closes apps in the background).
- **Pause menu → Power off** does the same thing as fully closing the app.
- **Sound** can be turned off in the pause menu.
- **Logbook** shows every cartridge you've found and your best scores.
- Uninstalling the app erases all progress.

## Updating the game

Edit `www/index.html`, upload the new version to the repository, and GitHub builds
a fresh APK automatically. Install it over the old one; progress is kept.

## Publishing on Google Play (later)

The APK built here is a *debug* build for testing. Publishing needs a signed
*release* build (an `.aab` file) and a Google Play developer account.
