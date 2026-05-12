# LabStock Pro

An Android application for laboratory stock management.

## Features

- **User Authentication**: Secure login with username and password
- **Dashboard**: Main interface for managing laboratory stocks
- **Print Module**: Generate and print laboratory results

## Requirements

- Android SDK 24+
- Android Studio Giraffe or newer
- Java JDK 11 or newer
- Gradle 8.0+

## Installation & Building

### Using Android Studio

1. Clone the repository:
```bash
git clone https://github.com/younesrouiba1994-pixel/Labstockpro.git
cd Labstockpro
```

2. Open in Android Studio:
   - File → Open → Select the project directory
   - Android Studio will automatically detect and configure the project

3. Build the project:
   - Build → Make Project
   - Or press `Ctrl+F9` (Windows/Linux) / `Cmd+F9` (Mac)

### Using Gradle Command Line

```bash
# Debug APK
./gradlew assembleDebug

# Release APK
./gradlew assembleRelease

# Install on connected device
./gradlew installDebug
```

## Default Credentials

For testing purposes:
- **Username**: `admin`
- **Password**: `1234`

⚠️ **Note**: Change these credentials before deploying to production!

## Project Structure

```
Labstockpro/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/labstock/pro/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── LoginActivity.kt
│   │   │   │   ├── DashboardActivity.kt
│   │   │   │   └── PrintActivity.kt
│   │   │   ├── assets/
│   │   │   │   └── labstock_black_users_print.html
│   │   │   ├── res/
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   └── mipmap/
│   │   │   └── AndroidManifest.xml
│   │   └── test/
│   ├── build.gradle
│   └── proguard-rules.pro
├── build.gradle
├── settings.gradle
├── gradle.properties
└── README.md
```

## Architecture

### Activities

1. **MainActivity**: Splash/entry point - immediately navigates to LoginActivity
2. **LoginActivity**: User authentication with simple validation
3. **DashboardActivity**: Main navigation hub for app features
4. **PrintActivity**: WebView-based print module using HTML assets

## Dependencies

- **AndroidX AppCompat**: 1.6.1
- **Android Material Design**: 1.10.0
- **Kotlin Runtime**: 1.9.10
- **AndroidX Core KTX**: 1.12.0
- **AndroidX Lifecycle**: 2.6.2

## Building for Release

### Prerequisites

Before building a release APK, you need to create a signing key:

```bash
keytool -genkey -v -keystore labstock.jks -keyalg RSA -keysize 2048 -validity 10000 -alias labstock_key
```

### Build Release APK

```bash
./gradlew assembleRelease
```

The signed APK will be available at: `app/build/outputs/apk/release/app-release.apk`

## Continuous Integration

This project includes GitHub Actions workflows that automatically:
- Build the APK on every push
- Run tests
- Upload APK artifacts
- Create releases (with tags)

See `.github/workflows/build-apk.yml` for details.

## API Level Support

- **Minimum SDK**: API 24 (Android 7.0 Nougat)
- **Target SDK**: API 34 (Android 14)

## Permissions

The app requires the following Android permissions:
- `INTERNET`: For web content and potential API calls

## Security Notes

⚠️ **Important Security Considerations**:

1. **Hardcoded Credentials**: The current login uses hardcoded credentials for testing. Replace with proper authentication in production.
2. **Data Storage**: Implement secure storage for sensitive data using Android Keystore.
3. **API Communication**: Use HTTPS with certificate pinning for API calls.
4. **ProGuard**: Enable code obfuscation in release builds.

## Contributing

1. Create a new branch for your feature: `git checkout -b feature/your-feature`
2. Commit your changes: `git commit -am 'Add new feature'`
3. Push to the branch: `git push origin feature/your-feature`
4. Submit a pull request

## License

This project is proprietary. All rights reserved.

## Support

For issues or questions, please open an issue on the GitHub repository.

## Author

**Younes Rouiba** - younesrouiba1994-pixel

---

**Last Updated**: 2026-05-12
