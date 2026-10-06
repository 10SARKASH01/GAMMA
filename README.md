# GAMMA — Offline Android Translator

A standalone native Android application for Samsung Galaxy S24 and other ARM64 phones with at least 8 GB RAM. Microphone capture, Whisper recognition, Gemma 4 E2B translation, and neural speech output run on the phone. Internet is needed only for initial model setup.

This repository contains the Android application. The Raspberry Pi application is maintained separately in [gemma-translator](https://github.com/10SARKASH01/gemma-translator).

Supported languages: **Arabic, English, Spanish, Japanese, Chinese, Korean, Persian, Urdu, and French**. All language pairs use local Gemma translation. Persian and Urdu have neural Piper voices; Arabic, English, Spanish, Japanese, Korean, and French use Supertonic 3; Chinese uses Kokoro. Arabic, Persian, and Urdu text renders with RTL direction.

## Install and use

Install the generated `android/dist/gemma-translator-s24-release.apk` through Samsung My Files. Open Gemma Translator, tap **Download offline models**, and allow microphone permission when recording. Initial downloads total approximately **3.6 GB**; keep at least **4.5 GB free** before setup. Then choose two languages, hold either person's **Talk** button, speak, and release. Try airplane mode after setup to verify offline operation.

See the [complete installation, architecture, and verification guide](android/README.md).

## Build

Install JDK 21 and Android SDK API 35/build-tools 35.0.0. Configure `JAVA_HOME` and `ANDROID_HOME` or `ANDROID_SDK_ROOT`.

Windows PowerShell:

```powershell
git clone https://github.com/10SARKASH01/GAMMA.git
cd GAMMA/android
./build-apk.ps1 -Variant release
```

Linux/macOS:

```sh
git clone https://github.com/10SARKASH01/GAMMA.git
cd GAMMA/android
bash ./build-apk.sh release
```

Build scripts run 48 JVM tests and Android lint, assemble the APK, and copy it to `android/dist/`. Gradle downloads the pinned speech runtime automatically and verifies its checksum. Models are installed through the app's setup screen.

The release build uses the local Android debug signing key for sideloading. Keep the same signing key for updates, or configure your own release key before publishing to an app store. The app targets ARM64 and Android 9/API 28 or later. Actual S24 microphone accuracy, GPU compatibility, speed, heat, and voice quality still need phone testing.

## Source and licenses

The Android distribution uses GPLv3-or-later, with third-party licenses retained. See [third-party notices](android/THIRD_PARTY_NOTICES.md), [speech model details](android/SPEECH_MODELS.md), and [attribution](ATTRIBUTION.md).

Generate the corresponding-source archive alongside the release APK:

```sh
python android/package-source.py --apk android/dist/gemma-translator-s24-release.apk
```

The source packager downloads and verifies pinned native dependency source archives, then writes `android/dist/gemma-translator-s24-corresponding-source.zip`. Keep that archive available with redistributed APKs.
