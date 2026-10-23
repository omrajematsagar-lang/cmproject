# SafeGuard — Women & Personal Safety Mobile Application

SafeGuard is a production-ready mobile safety application engineered with zero external server dependencies (100% on-device, standalone, NO Python required).

---

## Key Features

- **Screen-Off / Locked Phone Power Button SOS**:
  - Double-click the physical **Power Button** rapidly (within 2.5 seconds) even when your phone is turned off, asleep, or locked in your pocket.
  - Automatically wakes the device display, breaks through the lock screen, acquires GPS coordinates, dials the nearest Police Station (112), and sends an SOS SMS to trusted guardians.
- **Direct Nearby Police Station Contact (112)**:
  - Dynamically calculates the nearest police station from live GPS coordinates via the on-device Haversine algorithm.
  - Directly dials emergency police dispatch (112 / 100) and provides victim coordinates.
- **Differential Emergency Payloads**:
  - **To Police Station (112)**: Transmits victim profile (medical notes, age, blood group) and precise GPS latitude/longitude.
  - **To Trusted Guardians**: Sends automated SMS containing live Google Maps tracking link (`https://maps.google.com/?q=lat,lon`).
- **Comprehensive Mobile Permissions & Sleep Defense**:
  - Background location tracking (`ACCESS_FINE_LOCATION`, `ACCESS_BACKGROUND_LOCATION`).
  - Direct Phone Call execution (`CALL_PHONE`) and Emergency SMS (`SEND_SMS`).
  - Battery Optimization Exemption (`REQUEST_IGNORE_BATTERY_OPTIMIZATIONS`) so Android never kills the emergency listener during deep sleep.
  - Foreground Service (`FOREGROUND_SERVICE_LOCATION`) & Boot auto-start (`RECEIVE_BOOT_COMPLETED`).
- **Additional Triggers**:
  - Hardware Volume Button double-clicks.
  - 100% Offline On-Device Spoken Voice Keyword spotting.
  - 10-Second cancellation window to prevent false alarms.
  - Ambient audio evidence recording with local storage.
  - Route Watch cab corridor deviation detector (alerts if vehicle diverts > 200m).

---

## Project Structure (100% Standalone — No Python)

```text
cm project/
├── output/                        # Compiled Android APK output
│   └── safeguard.apk             # Standalone installable Android APK
├── mobile/                        # React Native / Native Android Project
│   ├── App.js                     # Main mobile shell & emergency state router
│   ├── android/                   # Native Android OS layer (Gradle 9, JDK 17, SDK 35)
│   │   ├── app/src/main/java/com/safeguard/safetyapp/
│   │   │   ├── MainActivity.kt            # Lockscreen-piercing activity & hardware listener
│   │   │   ├── MainApplication.kt        # React Native application root
│   │   │   ├── PowerButtonSosService.kt  # 24/7 Screen-Off Power Button listener & police dispatcher
│   │   │   ├── SafeGuardNativeModule.kt  # Android native module bridge to JavaScript
│   │   │   ├── SafeGuardPackage.kt       # React Native package declaration
│   │   │   └── BootReceiver.kt           # Device reboot persistence receiver
│   │   └── app/src/main/AndroidManifest.xml
│   └── src/
│       ├── components/            # UI components (Countdown, Header, Audio, Route)
│       ├── screens/               # Screens (SosScreen, RouteWatch, Guardians, Vault, Profile)
│       └── services/
│           └── emergencyService.js # Haversine police calculator & Native Android bridges
├── BUILD-APK.bat                  # 1-Click Android APK Builder (Builds safeguard.apk into output/)
├── 1-CLICK-RUN-APP.bat            # Instant desktop browser preview
├── RUN-ON-PHONE.bat               # Instant Expo Go QR code for testing on physical phone
├── tools/                         # Bundled local JDK 17 compiler
└── README.md
```

---

## How to Build the APK into the Output Folder

Double-click `BUILD-APK.bat`. It will:
1. Automatically configure JDK 17 and Android SDK.
2. Compile the Android application using Gradle.
3. Place the final APK in:
   ```text
   output\safeguard.apk
   ```
4. Automatically open the `output` folder on your computer.

---

## How to Install the APK on Your Mobile Phone

1. Connect your Android phone to your PC via USB cable (or transfer `output\safeguard.apk` via WhatsApp, Google Drive, or Bluetooth).
2. Tap the APK on your phone and tap **Install**.
3. Open **SafeGuard**:
   - Tap **"Grant All Mobile Permissions"** to enable GPS Location, Direct Police Calling (112), and SMS.
   - Tap **"Disable Battery Limits"** so SafeGuard can detect Power Button double-clicks even when your phone screen is off in your pocket.
4. Try double-clicking your **Power Button** twice quickly — SafeGuard will immediately wake up and protect you!
"# cmproject" 
