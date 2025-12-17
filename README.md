# flutter-apk-aab-autosave

Auto-save your Flutter release **APK** and **AAB** with versioned names into a `build_outputs/` folder using a tiny Gradle hook.

No more:
- hunting for `app-release.apk` deep inside `build/app/outputs/...`
- manually renaming files like `myapp_v1.0.16.apk`
- accidentally overwriting old builds

Instead, every `flutter build` drops clean, versioned files in one place.

---

## What this does

After you run:
- flutter build apk --release
- flutter build appbundle --release

This script:

- hooks into `assembleRelease` and `bundleRelease` Gradle tasks  
- copies the generated files into `<project-root>/build_outputs/`  
- renames them to:
- build_outputs/
  - AppName_vVersionName_release.apk
  - AppName_vVersionName_release.aab

Example:
  - Shikshawadi_v1.0.16_release.apk
  - Shikshawadi_v1.0.16_release.aab

---

## Setup

1. Open `android/app/build.gradle` in your Flutter project.

2. Ensure `defaultConfig` has a `versionName`.

3. Scroll to the **bottom** of `android/app/build.gradle` and paste this script.

4. Update: `def appName = "APP_NAME"` with your actual App Name.


---

## Usage

Build as usual:
- flutter build apk --release
- flutter build appbundle --release


Then check:
project-root/build_outputs/
  - YourAppName_vVersionName_release.apk
  - YourAppName_vVersionName_release.aab

You can now directly upload/share these without manual renaming or copying.

---

## Notes

- Paths assume the default Flutter Android output structure:
  - APK: `build/app/outputs/flutter-apk/app-release.apk`
  - AAB: `build/app/outputs/bundle/release/app-release.aab`
- Works with the standard Flutter Android release flow.
- If you use **flavors** or different build types, you can extend the script by adding more `tasks.named("assemble<Variant>")` / `tasks.named("bundle<Variant>")` blocks.

---

## License

MIT – feel free to copy, tweak, and use in your own projects and CI pipelines.









