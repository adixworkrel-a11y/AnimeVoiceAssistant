# Anime Voice Assistant (Android/Kotlin)

A lightweight Android app with a real App Widget, explicit speech recognition, clipboard copying, and Google Search. Package: `com.animeassistant.voice`.

## Project structure
- `app/src/main/java/.../MainActivity.kt` — microphone permission, SpeechRecognizer, copy and search actions.
- `AssistantWidgetProvider.kt` — genuine Android home-screen widget.
- `app/src/main/res/layout/activity_main.xml` — app UI.
- `app/src/main/res/layout/widget_assistant.xml` and `res/xml/assistant_widget_info.xml` — widget UI/configuration.
- `app/src/main/res/drawable-nodpi/` — app character assets.
- `assets/source-originals/` — untouched uploaded source illustrations.
- `assets/processed-transparent/` — separate PNG copies preserving the supplied alpha channel.

## Character asset notes
The uploaded PNGs already have RGBA alpha transparency (transparent pixels at their corners). The project therefore preserves their alpha instead of using a color-key removal that could erase white skin, eyes, or clothing. The sitting image still includes its original search bar and decorative art; a reliable character-only extraction would require manual masking where the character overlaps the bar. The source files are preserved unchanged.

## Build
Recommended: Android Studio with JDK 17 and Android SDK Platform 36; Android Gradle Plugin 8.13.2 / Gradle 8.13 / Kotlin plugin 2.2.20 are pinned in the project. Open the `AnimeVoiceAssistant` folder, allow Gradle sync, then choose **Build > Build APK(s)**. Debug APK normally appears at `app/build/outputs/apk/debug/app-debug.apk`. This project archive is source code, not a prebuilt APK; no build was run in this environment.

### Phone-only options
Import the project folder into a compatible Android IDE/build environment on Android that supports Kotlin, Gradle, JDK 17, and Android SDK 36. Availability and Gradle support vary by app. If the IDE cannot install the required SDK/build tools, use a trusted cloud build or a computer with Android Studio. Keep the full project directory structure intact.

## Install and widget
1. Build the debug APK.
2. Install it on your Android phone and launch **Anime Voice Assistant**.
3. Tap **Tap to Speak** and grant microphone permission. Speak; recognized text appears in the text area. You may edit it before copying/searching.
4. Long-press an empty area on your home screen, choose **Widgets**, find **Anime Voice Assistant / Anime Assistant**, then drag it onto the home screen. Tap the character widget to open the app. Resize if your launcher allows it.

## Test checklist
- [ ] First microphone tap requests permission.
- [ ] Denying permission shows an explanatory status.
- [ ] Speaking fills the text field with actual recognition results.
- [ ] Silence/no match and network/service errors show useful messages.
- [ ] Cancel button stops active listening.
- [ ] Copy is disabled for empty text and copies current text otherwise.
- [ ] Search is disabled for empty text and opens a correctly encoded Google query otherwise.
- [ ] Widget appears in launcher widget picker and tap opens the app.
- [ ] Backgrounding the activity cancels an active recognition session.

## Privacy and limitations
The app does not store audio or recognized text permanently. It only requests microphone access after a user tap. Android's speech service may send audio to its provider and may require a network connection; offline recognition depends on the service/language packs installed on the device. The app does not guarantee offline recognition.

## Troubleshooting
- **No speech service:** enable/install a speech recognition service on the phone, then retry.
- **Network error:** check connection or select an available language/service in Android settings.
- **No mic prompt:** open App info > Permissions > Microphone.
- **Widget missing:** ensure the app installed successfully, then reboot/refresh the launcher widget picker. Some launchers cache widgets.
- **Gradle sync fails:** confirm JDK 17, SDK Platform 36, internet access for dependency downloads, and compatible Gradle support in your IDE. Do not mix arbitrary plugin/Gradle versions.
- **Transparent edges look wrong:** use `assets/source-originals/` as the master; do not remove white pixels by color key. For the sitting image's search bar, manually refine a mask in an image editor rather than pretending it is fully removed.
