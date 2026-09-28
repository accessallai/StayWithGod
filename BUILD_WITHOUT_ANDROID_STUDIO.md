# Build without Android Studio

This project includes a GitHub Actions workflow that builds the debug APK in the cloud.

1. Create a GitHub repository named `StayWithGod`.
2. Upload all files in this project to the repository's `main` branch.
3. Open **Actions** → **Build Stay With God APK**.
4. Run the workflow with **Run workflow**.
5. When it finishes, open the workflow run and download the `StayWithGod-debug-apk` artifact.
6. Extract the downloaded artifact and install `app-debug.apk` on the Android phone.

The build uses JDK 17, Gradle 9.6, Android SDK 37 and Build Tools 36.0.0.
