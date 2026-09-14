THE FOUNDRY  |  Copyright (c) 2026 Yannie D. Forest. All rights reserved.
NO LICENCE IS GRANTED. No copying, adaptation, redistribution, reverse
engineering or commercial use without the author's written permission.
See LICENCE.txt. Every distributed copy carries a build marker.
--------------------------------------------------------------------------

BUILDING THE FOUNDRY APK FOR YOUR FIRE TABLET
=============================================

This project turns The Foundry into a real Android app: one installable APK that
shows the seal on the home screen and runs completely offline. Fire OS is Android
underneath, so the APK sideloads onto a Fire tablet directly, with no app store.

You do NOT need to write any code. Choose ONE of the three routes below. Read the
"What to expect" note in README_FIRE.txt first: running models on a tablet is
limited to very small models, and larger ones may not load at all.

--------------------------------------------------------------------------
ROUTE 1 (EASIEST, NOTHING TO INSTALL): LET GITHUB BUILD IT
--------------------------------------------------------------------------
1. Make a free account at github.com.
2. New repository, any name, Private is fine. Create it.
3. "uploading an existing file": drag in the CONTENTS of this folder (the app
   folder, the .github folder, build.gradle, settings.gradle, gradle.properties).
   Commit. If the hidden .github folder did not upload, add the workflow by hand
   from GITHUB_WORKFLOW_paste_this.txt (see README_FIRE.txt step 5).
4. Actions tab: the build runs automatically, about three to five minutes.
5. For the tablet, use the repository's Releases page and tap the-foundry.apk.
   The Artifacts link works on a signed in computer and gives the same APK.

--------------------------------------------------------------------------
ROUTE 2 (ONE FREE TOOL): ANDROID STUDIO
--------------------------------------------------------------------------
1. Install Android Studio (free, developer.android.com/studio).
2. Open it, choose Open, select this folder.
3. Let Gradle sync finish (it downloads what it needs).
4. Build, then Build Bundle(s) / APK(s), then Build APK(s).
5. The APK is under app/build/outputs/apk/debug/app-debug.apk.

--------------------------------------------------------------------------
ROUTE 3 (COMMAND LINE): IF YOU ALREADY HAVE THE ANDROID SDK
--------------------------------------------------------------------------
From inside this folder, with a Gradle 8.x on your PATH:
    gradle :app:assembleDebug
The APK lands at app/build/outputs/apk/debug/app-debug.apk.
This project ships no gradle wrapper, so call "gradle" directly, not ./gradlew.

--------------------------------------------------------------------------
WHAT THIS WRAPPER ADDS OVER A PLAIN WEBVIEW
--------------------------------------------------------------------------
Two things, both necessary for The Foundry specifically:
  1. The page is served from a secure local address rather than a file:// URL,
     which is what allows the engine's WebAssembly, storage and module loading to
     work at all.
  2. A file chooser is wired in, so the "click to choose" model picker can select
     your engine and GGUF files. A plain WebView ignores file inputs.

--------------------------------------------------------------------------
INSTALLING ON THE TABLET (all routes end here)
--------------------------------------------------------------------------
1. Tablet: Settings, Security & Privacy, turn on "Apps from Unknown Sources".
2. Put app-debug.apk on the tablet by USB or email.
3. Tap it in the Files app and approve the install.
4. The Foundry appears on the home screen with the seal as its icon.

WHY THERE IS NO READY-MADE APK IN THIS DOWNLOAD
Compiling an Android APK needs Google's Android build tools, which cannot run in
the workspace that produced these files. Each route above runs those tools for
you, Route 1 without installing anything on your own machine. This APK has not
been compiled or tested here; if a cloud run fails, the log is attached to the
run so the exact cause can be identified.
