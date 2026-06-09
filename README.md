# 🔥 Firebase Remote Config Flutter App

<div align="center">

A Flutter example app demonstrating **Firebase Remote Config** integration for dynamic UI control and real-time configuration management without app redeployment.

[![Flutter](https://img.shields.io/badge/Flutter-3.0+-blue?style=for-the-badge&logo=flutter)](https://flutter.dev)
[![Firebase](https://img.shields.io/badge/Firebase-Latest-orange?style=for-the-badge&logo=firebase)](https://firebase.google.com)
[![Dart](https://img.shields.io/badge/Dart-3.0+-1f425f?style=for-the-badge&logo=dart)](https://dart.dev)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [Configuration](#-configuration)

</div>

---

## 📖 Overview

This project demonstrates a production-ready implementation of **Firebase Remote Config** in Flutter, enabling dynamic control of app UI elements without requiring new app releases. Update colors, images, and configurations in real-time directly from Firebase Console.

**Perfect for:**
- A/B testing UI variations
- Feature flag management
- Real-time promotional content updates
- Dynamic theming and branding

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

- ✅ Firebase initialization with `firebase_core`
- ✅ Automatic fetch and activation of Remote Config
- ✅ Real-time dynamic UI updates
- ✅ Manual refresh functionality

</td>
<td width="50%">

- ✅ Background color customization
- ✅ Dynamic promotional images
- ✅ Graceful fallback to defaults
- ✅ Production-ready error handling

</td>
</tr>
</table>

---

## 🎬 Demo

<div align="center">

### Background Color Update
![Color Update Demo](https://github.com/lianeheidemann/aplicativo_firebaseremoteconfig/raw/main/assets/gifs/gif1_cor_FirebaseRemoteConfig.gif)

### Promotional Content Change
![Promotional Update Demo](https://github.com/lianeheidemann/aplicativo_firebaseremoteconfig/raw/main/assets/gifs/gif2_propaganda_FirebaseRemoteConfig.gif)

</div>

---

## 🛠️ Tech Stack

| Component | Purpose | Version |
|-----------|---------|---------|
| **Flutter** | Cross-platform UI framework | 3.0+ |
| **firebase_core** | Firebase initialization & setup | Latest |
| **firebase_remote_config** | Remote configuration management | Latest |
| **url_launcher** | External URL navigation | Latest |
| **Dart** | Programming language | 3.0+ |

---

## 🚀 Quick Start

### Prerequisites

- **Flutter SDK** 3.0 or higher
- **Firebase CLI** (recommended)
- **Android SDK** or **iOS SDK**
- Firebase project created

### Installation Steps

#### 1. Clone the Repository
```bash
git clone https://github.com/lianeheidemann/aplicativo_firebaseremoteconfig.git
cd aplicativo_firebaseremoteconfig
```

#### 2. Install Dependencies
```bash
flutter pub get
```

#### 3. Configure Firebase

**Using FlutterFire CLI (Recommended):**
```bash
# Install FlutterFire CLI if not already installed
dart pub global activate flutterfire_cli

# Configure Firebase for your project
flutterfire configure
```

**Manual Setup:**
1. Download `google-services.json` from Firebase Console
2. Place it in `android/app/`
3. Ensure `android/build.gradle` includes Firebase plugins

#### 4. Run the Application
```bash
flutter run
```

---

## ⚙️ Configuration Guide

### Remote Config Keys

#### `cor_fundo` (Background Color)
| Property | Value |
|----------|-------|
| **Type** | String (Hex color) |
| **Format** | `#RRGGBB` |
| **Default** | `#FFFFFF` (White) |
| **Effect** | Controls Scaffold background color |
| **Example** | `#FF5733`, `#3498DB`, `#2ECC71` |

#### `propaganda` (Promotional Image)
| Property | Value |
|----------|-------|
| **Type** | String |
| **Default** | `default` |
| **Options** | `alternativa` or any other value |
| **Behavior** | `alternativa` → uses `propaganda_alt.png`<br>`default` → uses `propaganda.png` |

### Firebase Console Setup

1. Navigate to **Firebase Console** → Your Project → **Remote Config**
2. Click **Create Configuration**
3. Add the following parameters:

```
Parameter          | Value              | Type
-------------------|-------------------|-------
cor_fundo         | #FF0000           | String
propaganda        | alternativa       | String
```

4. Click **Publish Configuration**
5. Wait for global propagation (typically 5-10 seconds)
6. Open the app and tap **Refresh** to fetch updates

### Example Configurations

**Red Theme with Alternative Image:**
```json
{
  "cor_fundo": "#FF0000",
  "propaganda": "alternativa"
}
```

**Blue Theme with Default Image:**
```json
{
  "cor_fundo": "#0000FF",
  "propaganda": "default"
}
```

**Green Theme:**
```json
{
  "cor_fundo": "#2ECC71",
  "propaganda": "default"
}
```

---

## 📁 Project Structure

```
aplicativo_firebaseremoteconfig/
├── lib/
│   ├── main.dart                    # Application entry point & Remote Config logic
│   └── firebase_options.dart        # Firebase initialization configuration
├── android/
│   ├── app/
│   │   └── google-services.json     # Firebase Android credentials
│   └── build.gradle                 # Android build configuration
├── assets/
│   └── images/
│       ├── propaganda.png           # Default promotional image
│       ├── propaganda_alt.png       # Alternative promotional image
│       ├── gif1_cor_FirebaseRemoteConfig.gif
│       └── gif2_propaganda_FirebaseRemoteConfig.gif
├── pubspec.yaml                     # Flutter project dependencies
├── firebase.json                    # Firebase project settings
└── README.md                        # This file
```

---

## 💻 Implementation Details

### Core Logic (`lib/main.dart`)

**Remote Config Initialization:**
```dart
final remoteConfig = FirebaseRemoteConfig.instance;

// Set default values
await remoteConfig.setDefaults({
  'cor_fundo': '#FFFFFF',
  'propaganda': 'default',
});

// Fetch and activate configuration
await remoteConfig.fetchAndActivate();
```

**Accessing Configuration Values:**
```dart
String backgroundColor = remoteConfig.getString('cor_fundo');
String imageType = remoteConfig.getString('propaganda');
```

**Manual Refresh:**
```dart
void _refreshConfig() async {
  try {
    await remoteConfig.fetchAndActivate();
    setState(() {});
  } catch (e) {
    print('Error fetching Remote Config: $e');
  }
}
```

---

## 📦 Dependencies

All dependencies are managed in `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^latest
  firebase_remote_config: ^latest
  url_launcher: ^latest
```

Update dependencies:
```bash
flutter pub upgrade
```

---

## 🧪 Testing & Validation

### Test Locally
1. Run the app with `flutter run`
2. Open Firebase Console
3. Publish a new configuration
4. Tap the **Refresh** button in the app
5. Observe UI updates in real-time

### Best Practices
- ✅ Test with various hex color values
- ✅ Test with both propaganda configurations
- ✅ Test network failures and retries
- ✅ Monitor Firebase usage in Console

---

## 💡 Use Cases

| Use Case | Example |
|----------|---------|
| **A/B Testing** | Test different color schemes with user groups |
| **Feature Flags** | Enable/disable features without redeployment |
| **Promotional Content** | Update promotional images and URLs dynamically |
| **Theming** | Switch between light/dark themes in real-time |
| **Regional Content** | Serve region-specific content |
| **Emergency Updates** | Quickly update UI without app store review |

---

## 🔗 Resources

- [Firebase Remote Config Documentation](https://firebase.google.com/docs/remote-config)
- [Flutter Firebase Plugins](https://firebase.flutter.dev)
- [Flutter Documentation](https://flutter.dev/docs)
- [Firebase Console](https://console.firebase.google.com)
- [FlutterFire CLI Guide](https://firebase.flutter.dev/docs/cli)

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Liane Heidemann**

- GitHub: [@lianeheidemann](https://github.com/lianeheidemann)
- Repository: [aplicativo_firebaseremoteconfig](https://github.com/lianeheidemann/.aplicativo_firebaseremoteconfig)

---

<div align="center">

**Built with ❤️ using Flutter & Firebase**

[⬆ Back to Top](#-firebase-remote-config-flutter-app)

</div>
