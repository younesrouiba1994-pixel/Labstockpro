# LabStock Pro - Setup & Build Guide

## Quick Start

### Option 1: Using Android Studio (Easiest)

1. **Install Prerequisites**
   - Download and install [Android Studio](https://developer.android.com/studio)
   - During installation, ensure you select Android SDK components

2. **Clone & Open Project**
   ```bash
   git clone https://github.com/younesrouiba1994-pixel/Labstockpro.git
   ```
   - Open Android Studio
   - File → Open → Navigate to the cloned folder
   - Android Studio will automatically sync Gradle

3. **Build & Run**
   - Connect an Android device or start an emulator
   - Click "Run" (green play button) or press `Shift+F10`
   - Select your target device
   - The app will build and install automatically

### Option 2: Using Command Line

1. **Install Prerequisites**
   ```bash
   # macOS (using Homebrew)
   brew install android-sdk android-ndk

   # Ubuntu/Debian
   sudo apt-get install android-sdk android-ndk

   # Windows
   # Download from https://developer.android.com/studio
   ```

2. **Clone Repository**
   ```bash
   git clone https://github.com/younesrouiba1994-pixel/Labstockpro.git
   cd Labstockpro
   ```

3. **Build Debug APK**
   ```bash
   # Linux/macOS
   ./gradlew assembleDebug

   # Windows
   gradlew.bat assembleDebug
   ```
   Output: `app/build/outputs/apk/debug/app-debug.apk`

4. **Install on Device**
   ```bash
   ./gradlew installDebug
   ```

## Building Release APK

### Step 1: Create Signing Key

```bash
keytool -genkey -v -keystore labstock.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias labstock_key
```

You'll be prompted for:
- Keystore password
- Key password
- First and Last Name
- Organization Unit
- Organization
- City/Locality
- State/Province
- Country Code

### Step 2: Configure Signing

Create `local.properties` in the project root:

```properties
sdk.dir=/path/to/android/sdk
RELEASE_STORE_FILE=labstock.jks
RELEASE_STORE_PASSWORD=your_keystore_password
RELEASE_KEY_ALIAS=labstock_key
RELEASE_KEY_PASSWORD=your_key_password
```

### Step 3: Build Release APK

```bash
./gradlew assembleRelease
```

Output: `app/build/outputs/apk/release/app-release.apk`

## Automated Builds with GitHub Actions

The project includes automatic building. When you push code:

1. GitHub Actions triggers automatically
2. Builds debug and release APKs
3. Uploads artifacts (available for download)
4. Creates releases for tagged commits

### For Signed Releases (Optional)

Add these GitHub Secrets to your repository settings:

```
SIGNING_KEY = <base64 encoded .jks file>
ALIAS = labstock_key
ALIAS_PASSWORD = your_key_password
KEY_STORE_PASSWORD = your_keystore_password
```

To get base64 of your keystore:

```bash
# macOS/Linux
base64 < labstock.jks

# Windows PowerShell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("labstock.jks"))
```

## Troubleshooting

### Build Issues

**Problem**: `Could not find tools.jar`
```bash
# Solution: Set JAVA_HOME
export JAVA_HOME=$(which java)
```

**Problem**: `Gradle sync failed`
- Try: File → Sync Now in Android Studio
- Or: `./gradlew clean build`

**Problem**: Android SDK not found
```bash
# Create local.properties with SDK path
echo "sdk.dir=/path/to/android/sdk" > local.properties
```

### Runtime Issues

**Problem**: App crashes on startup
- Check Android Studio's Logcat tab
- Ensure device API level matches minSdk (24+)

**Problem**: WebView not loading HTML
- Ensure `labstock_black_users_print.html` exists in `app/src/main/assets/`

## Development Workflow

### Making Code Changes

1. Create a new branch: `git checkout -b feature/my-feature`
2. Make your changes in Android Studio
3. Build and test: `./gradlew assembleDebug`
4. Commit and push: `git add . && git commit -m "..." && git push`
5. Create a Pull Request on GitHub

### Testing

```bash
# Run unit tests
./gradlew test

# Run instrumented tests on device
./gradlew connectedAndroidTest

# Build and install debug app
./gradlew installDebug
```

## Android Emulator Setup

If you don't have a physical device:

```bash
# List available emulators
emulator -list-avds

# Create a new emulator (Android Studio GUI recommended)
# Then run:
emulator -avd emulator_name
```

## Project Configuration Files

| File | Purpose |
|------|---------|
| `build.gradle` | Root Gradle config, plugin versions |
| `app/build.gradle` | App-specific build config, dependencies |
| `gradle.properties` | Build property flags |
| `settings.gradle` | Project structure, module includes |
| `local.properties` | Local SDK/signing configuration |
| `gradle/wrapper/gradle-wrapper.properties` | Gradle version |

## APK Signing Explained

- **Debug APK**: Auto-signed with Android debug key, for testing only
- **Release APK**: Must be signed with your own key for distribution

## Distribution

### Via Google Play Store

1. Create a Google Play Developer account ($25 one-time)
2. Sign your APK with your release key
3. Create app listing with screenshots, description
4. Upload APK to Play Store Console
5. Fill out store information and publish

### Direct Distribution

1. Sign your release APK (see above)
2. Host on your website or repository
3. Users download and install manually
4. Use GitHub Releases for automatic hosting

## Gradle Wrapper

The project uses Gradle Wrapper (`./gradlew`), so you don't need to install Gradle separately:
- It automatically downloads the specified Gradle version
- Ensures consistent builds across machines
- Safe to commit to repository

## Environment Variables (Optional)

```bash
# Speed up Gradle builds
export GRADLE_OPTS="-Xmx2048m"

# Use offline mode if dependencies are cached
./gradlew --offline build
```

## Next Steps

1. ✅ Clone the repository
2. ✅ Open in Android Studio
3. ✅ Build debug APK
4. ✅ Test on device/emulator
5. ✅ Modify code as needed
6. ✅ Build release APK
7. ✅ Distribute your app

---

**For more help**: Visit [Android Developers Documentation](https://developer.android.com/docs)
