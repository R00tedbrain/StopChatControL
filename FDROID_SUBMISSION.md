# F-Droid Submission Guide for SecureChats Keyboard BWT

## 📋 Pre-submission Checklist

- [x] App complies with [F-Droid inclusion criteria](https://f-droid.org/docs/Inclusion_Policy/)
- [x] Source code is available under GPL-3.0 license
- [x] No proprietary dependencies
- [x] No tracking or advertisement
- [x] Builds reproducibly with F-Droid tools
- [x] Metadata files prepared (`fdroid/metadata.yml`)
- [x] Fastlane metadata provided
- [x] Release tagged in git (v2.0.0)

## 🔍 App Information

**Package Name:** `com.bwt.securechats`  
**Version:** 2.0.0 (versionCode: 2)  
**License:** GPL-3.0-only  
**Repository:** https://github.com/R00tedbrain/StopChatControL  
**Release Tag:** v2.0.0

## 🏗️ Build Requirements

### NDK Version
- **Required NDK:** 26.1.10909125
- **Reason:** Native libraries (libsignal-android) require this specific NDK version

### Java Version
- **Required Java:** OpenJDK 17
- **Configuration:** Included in `fdroid/build.yml` sudo section

### Gradle
- **Gradle Version:** 8.5.0 (via wrapper)
- **Build Type:** release

## 📦 Dependencies

All dependencies are from Maven Central and Google's Maven repository:

```gradle
implementation 'org.bouncycastle:bcprov-ext-jdk18on:1.78.1'
implementation 'com.google.protobuf:protobuf-javalite:3.21.12'
implementation 'org.signal:libsignal-android:0.73.2'
implementation 'com.fasterxml.jackson.core:jackson-databind:2.14.1'
implementation 'com.fasterxml.jackson.datatype:jackson-datatype-jsr310:2.14.1'
implementation 'androidx.security:security-crypto:1.1.0-alpha03'
coreLibraryDesugaring 'com.android.tools:desugar_jdk_libs:2.0.3'
```

## 🔐 Security & Privacy

### Permissions
- **VIBRATE** - Only permission requested (for haptic feedback)
- **No internet permission** - All cryptographic operations are local
- **No storage permission** - Uses app-private storage only

### Anti-Features
**None** - This app has:
- No tracking
- No advertising
- No proprietary code
- No non-free dependencies
- No non-free network services

## 🛠️ Build Process

### Standard Build
```bash
./gradlew assembleRelease
```

### F-Droid Build
The build process is configured in `fdroid/build.yml`:

1. **Prebuild phase:** Removes debug/testing native libraries
2. **Build phase:** Standard Gradle release build
3. **Post-processing:** Automatic by F-Droid build system

### Known Build Considerations

1. **Native Libraries:** The app includes Signal Protocol native libraries compiled for:
   - arm64-v8a
   - armeabi-v7a

2. **Prebuild cleanup:** Automatically removes:
   - `*.dll` (Windows debug files)
   - `*.dylib` (macOS debug files)
   - `*_debug.so` (Debug libraries)
   - `*_testing.so` (Testing libraries)

## 📄 Metadata Location

- **F-Droid metadata:** `fdroid/metadata.yml`
- **Build configuration:** `fdroid/build.yml`
- **Fastlane metadata:** `fastlane/metadata/android/`
  - Descriptions: `en-US/full_description.txt`, `short_description.txt`
  - Changelog: `en-US/changelogs/2.txt`
  - Screenshots: `en-US/images/`

## 🚀 How to Submit

### Option 1: IzzyOnDroid (Faster, Recommended First)

1. **Fork the repo** (already done)
2. **Create release tag:**
   ```bash
   git tag -a v2.0.0 -m "Release v2.0.0 - Post-Quantum Cryptography"
   git push origin v2.0.0
   ```

3. **Submit to IzzyOnDroid:**
   - Visit: https://gitlab.com/IzzyOnDroid/repo/-/issues
   - Create new issue with title: "New App: SecureChats Keyboard BWT"
   - Include:
     ```
     App Name: SecureChats Keyboard BWT
     Package: com.bwt.securechats
     Repository: https://github.com/R00tedbrain/StopChatControL
     License: GPL-3.0-only
     Description: Post-Quantum E2EE keyboard based on Signal Protocol with Kyber integration
     ```

### Option 2: F-Droid Official (More Thorough)

1. **Prepare metadata merge request:**
   - Fork: https://gitlab.com/fdroid/fdroiddata
   - Create directory: `metadata/com.bwt.securechats.yml`
   - Copy content from `fdroid/metadata.yml`

2. **Create merge request:**
   - Title: "New App: SecureChats Keyboard BWT - Post-Quantum E2EE Keyboard"
   - Description:
     ```markdown
     ## Required
     - [x] The app complies with the inclusion criteria
     - [x] The original app author has been notified
     - [x] All related fdroiddata and RFP issues have been referenced
     - [x] Builds with `fdroid build` and all pipelines pass

     ## Strongly Recommended
     - [x] The upstream app source code repo contains the app metadata in a Fastlane folder structure
     - [x] Releases are tagged

     ## App Details
     Post-Quantum E2EE keyboard implementing Signal Protocol with Kyber integration.
     Based on KryptEY (https://github.com/amnesica/KryptEY) with enhanced security features.
     
     - No internet permission
     - No tracking
     - Server-free E2EE
     - 89+ language localizations
     ```

## 🔄 Update Process (Future Releases)

1. Update `versionCode` and `versionName` in `app/build.gradle`
2. Update `CurrentVersion` and `CurrentVersionCode` in `fdroid/metadata.yml`
3. Add new build entry in `fdroid/metadata.yml` with new commit/tag
4. Create release tag: `git tag -a vX.X.X -m "Release vX.X.X"`
5. Push tag: `git push origin vX.X.X`
6. Submit update to IzzyOnDroid/F-Droid

## 📞 Contact Information

**Developer:** R00tedbrain  
**Email:** rootedbraindevelopers@proton.me  
**Repository:** https://github.com/R00tedbrain/StopChatControL  
**Issues:** https://github.com/R00tedbrain/StopChatControL/issues

## 📚 Additional Resources

- **Original KryptEY:** https://github.com/amnesica/KryptEY
- **F-Droid Inclusion Policy:** https://f-droid.org/docs/Inclusion_Policy/
- **F-Droid Build Metadata Reference:** https://f-droid.org/docs/Build_Metadata_Reference/
- **IzzyOnDroid Repo:** https://apt.izzysoft.de/fdroid/

## ⚠️ Important Notes

1. **First Submission:** This is a clean, fresh start with new repository
2. **Previous Issues:** All previous build issues from old repository have been resolved
3. **Reproducibility:** Build is configured for reproducibility (NDK version pinned, prebuild cleanup)
4. **No Anti-Features:** App is completely free and open source with no tracking
5. **Testing:** App has been tested on multiple Android versions (8.0+)

## ✅ Final Checklist Before Submission

- [x] Repository is public
- [x] Release tag created (v2.0.0)
- [x] Metadata files are correct
- [x] Build.gradle versions match metadata
- [x] License file exists (GPL-3.0)
- [x] README is comprehensive
- [x] Changelog is updated
- [x] Fastlane metadata is complete
- [x] Screenshots are provided
- [x] No proprietary dependencies
- [x] App builds successfully locally

---

**Ready for submission! 🚀**
