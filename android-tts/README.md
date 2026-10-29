# Offline Android TTS engine

An Android text-to-speech engine that runs fully on-device (no internet needed)
and registers as a **system TTS engine**, so any app that speaks text
(screen readers, e-book readers, navigation, browsers) can use it.

It is built by `.github/workflows/build-tts-apk.yml` from:

- [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) `v2.0.1`: its
  `SherpaOnnxTtsEngine` Android app and prebuilt native libraries
- a [Piper](https://github.com/rhasspy/piper) English voice, by default
  **`en_GB-alan-medium`** (UK English, male), bundled inside the APK

## Getting the APK

1. Open the repository on GitHub, then **Actions → build-tts-apk**.
2. Open the latest successful run, or click **Run workflow** to build a
   different English voice. Other UK male options are
   `en_GB-southern_english_male-medium` and `en_GB-northern_english_male-medium`;
   see the `vits-piper-en_*` files on the
   [tts-models release](https://github.com/k2-fsa/sherpa-onnx/releases/tag/tts-models).
3. Download the `offline-tts-<voice>-apks` artifact and unzip it.

| APK | For |
| --- | --- |
| `...-arm64-v8a.apk` | most phones from 2017 onward (choose this if unsure) |
| `...-armeabi-v7a.apk` | older 32-bit phones |
| `...-x86_64.apk` | emulators and x86 devices |

## Installing and making it the system voice

1. Copy the APK to the phone and open it (allow "install unknown apps" if asked).
2. Open the app once, so it can unpack the voice and play a test sentence.
3. Go to **Settings → Accessibility → Text-to-speech output** (on some phones
   it is under **System → Languages & input**).
4. Set **Preferred engine** to the sherpa-onnx engine, then tap **Play** to test.

## Signing

The workflow signs every build. Without secrets, it uses a new throwaway key
each run, which means you must uninstall the old version before you install a
new build. To sign with your own stable key, add these repository secrets:

- `TTS_APK_KEYSTORE_BASE64`: your `.jks` file, base64-encoded
- `TTS_APK_KEYSTORE_PASSWORD`: the keystore password (also used as the key password)
- `TTS_APK_KEY_ALIAS`: the key alias

## Licenses

sherpa-onnx is Apache-2.0. Each Piper voice has its own license, listed in its
model card.
