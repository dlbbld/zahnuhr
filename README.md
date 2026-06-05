# Zahnuhr

A teeth-brushing timer ("Zahnuhr") for children, by Philipp Gressly Freimann.
It guides kids through the brushing steps as a timed slideshow with sounds, and
is translated into roughly 20 languages.

Package: `eu.gressly.android.zahnuhr`

## Requirements

- JDK 17
- Android SDK with platform **android-35** and **build-tools 35.x**
  (Android Studio installs these automatically)

## Build

Open the project in Android Studio and press **Run**, or from the command line:

```sh
./gradlew assembleDebug      # debug APK  -> app/build/outputs/apk/debug/
./gradlew assembleRelease    # signed release APK (needs keystore.properties)
./gradlew bundleRelease      # signed App Bundle (.aab) for Google Play
```

On Windows use `gradlew.bat`.

## Release signing

Release builds are signed from a keystore described by a `keystore.properties`
file in the project root (kept out of version control). Example:

```properties
storeFile=app/upload-keystore.jks
storePassword=<your password>
keyAlias=upload
keyPassword=<your password>
```

Create an upload key with:

```sh
keytool -genkeypair -v -keystore app/upload-keystore.jks \
    -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

If `keystore.properties` is absent, release builds are produced unsigned.

> ⚠️ **Updating an existing Google Play listing?** You must sign with the app's
> *original* signing key (or the upload key registered with Play App Signing) —
> a freshly generated key will be rejected, because Android only accepts updates
> signed with the same identity as the installed app.

## Toolchain / SDK levels

- Gradle 8.9, Android Gradle Plugin 8.7.3
- `compileSdk` / `targetSdk` 35 (Android 15), `minSdk` 21

## History

Originally an Eclipse ADT project (2013–2015). Migrated to Gradle and updated
for current Google Play requirements (target API 35) in 2026.
