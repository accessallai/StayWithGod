# Stay With God

A private, offline-first Android app that gently brings Scripture, personal prayer and personal affirmations back to the foreground during active phone use.

## Important Android behavior

This first version deliberately avoids AccessibilityService, UsageStats permission, notification-reading access, screen capture, and reading other apps.

Because Android does not expose a general-purpose API for a normal app to observe global touch/keyboard activity without those broader capabilities, the active-use timer uses **screen interactive + device unlocked** as its privacy-preserving activity signal. It pauses when the screen is off or the device is locked. Switching apps does not reset the timer.

On Android 14+, foreground services must declare an appropriate type. This project uses `specialUse` because this private reminder service does not fit camera/media/location/data-sync categories. Android may still restrict background starts on some versions. After reboot, the app intentionally does not force a restricted foreground-service launch; opening the app resumes the service.

## Open in Android Studio

1. Install Android Studio with Android SDK Platform 37 and JDK 17.
2. Open the `StayWithGod` folder.
3. Let Gradle sync.
4. Run on an emulator or physical Android phone.
5. On first launch, turn reminders on.
6. In Settings, enable **Display over other apps**.
7. For development/testing, select **30 seconds** as the interval.
8. Build with **Build > Build App Bundle(s) / APK(s) > Build APK(s)**.

## Command line

If Android Studio generated/accepted the Gradle wrapper, use:

`./gradlew :app:assembleDebug`

The debug APK is normally produced at:

`app/build/outputs/apk/debug/app-debug.apk`

## Privacy

No network permission is declared. Prayers, affirmations, recent reminder IDs and counts are stored locally with Android DataStore. No account, analytics, advertising, location, contacts, microphone, camera, SMS, notification-reading or accessibility permission is used.

## Test checklist

- Install and open.
- Turn reminders on.
- Grant overlay permission.
- Set interval to 30 seconds.
- Leave the app and use another app.
- Confirm the floating card appears.
- Dismiss it and confirm the timer restarts.
- Turn screen off: timer pauses.
- Unlock: timer resumes.
- Add/edit/delete a prayer.
- Add/edit/delete an affirmation.
- Disable one custom entry and confirm it is not selected.
- Disable a reminder type and confirm the selector respects it.
- Disable overlay permission and confirm notification fallback.
- Reboot and verify the app does not attempt an unsafe background service launch; reopen the app to resume.

## Architecture

`model/` — reminder model and types  
`data/` — local DataStore and bundled Scripture data  
`repository/` — selection logic  
`service/` — foreground service, overlay and boot receiver  
`MainActivity.kt` — Compose screens and ViewModel
