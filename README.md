# bezpecny-soused
Community safety app for iOS &amp; Android - Flutter# 🛡️ Bezpečný soused – Flutter App

Komunitní bezpečnostní aplikace pro iOS a Android – hlídejte okolí společně se sousedy.

---

## 📱 Obrazovky a funkce

| Obrazovka | Popis |
|-----------|-------|
| **Přihlášení** | SMS kód / Google / Apple Sign-In |
| **Nastavení profilu** | Jméno, ulice, číslo bytu |
| **Hlavní obrazovka** | Logo + uživatel + červené tlačítko + mapa + seznam hlášení |
| **Nahlásit incident** | Kamera (foto/video 15s) + popis + GPS |
| **Moje okolí** | Mapa + seznam všech hlášení v 150 m |
| **Moje body** | Gamifikace, levely, sleva na pojištění |
| **Nastavení** | Profil, notifikace, GDPR, odhlášení |

---

## 🚀 Rychlý start

### Požadavky
- Flutter 3.19+
- Dart 3.0+
- Firebase projekt
- Google Maps API klíč
- Xcode 15+ (pro iOS)
- Android Studio (pro Android)

### 1. Klonování a závislosti

```bash
git clone <repo>
cd bezpecny_soused
flutter pub get
```

### 2. Firebase nastavení

1. Vytvořte projekt na [console.firebase.google.com](https://console.firebase.google.com)
2. Přidejte **iOS** a **Android** aplikaci
3. Stáhněte konfigurační soubory:
   - `google-services.json` → `android/app/`
   - `GoogleService-Info.plist` → `ios/Runner/`
4. Zapněte v Firebase Console:
   - ✅ Authentication (Phone, Google, Apple)
   - ✅ Firestore Database
   - ✅ Cloud Storage
   - ✅ Cloud Messaging (FCM)
   - ✅ Cloud Functions

### 3. Google Maps API

1. Jděte na [console.cloud.google.com](https://console.cloud.google.com)
2. Zapněte **Maps SDK for Android** a **Maps SDK for iOS**
3. Vytvořte API klíč
4. Nahraďte `YOUR_GOOGLE_MAPS_API_KEY` v:
   - `android/app/src/main/AndroidManifest.xml`
   - `ios/Runner/Info.plist`

### 4. Firebase Functions deploy

```bash
cd functions
npm install
firebase deploy --only functions
```

### 5. Firestore pravidla

```bash
firebase deploy --only firestore:rules
```

### 6. Spuštění

```bash
# iOS
flutter run -d ios

# Android
flutter run -d android

# Pro release build
flutter build apk --release
flutter build ios --release
```

---

## 📁 Struktura projektu

```
lib/
├── main.dart                    # Entry point, router
├── theme/
│   └── app_theme.dart           # Barvy, fonty, styly
├── models/
│   ├── user_model.dart          # Uživatelský profil
│   └── incident_model.dart      # Model incidentu
├── services/
│   ├── auth_service.dart        # Přihlášení, profil, body
│   ├── incident_service.dart    # Hlášení, GPS, Firestore
│   └── notification_service.dart # Push notifikace
├── screens/
│   ├── auth/
│   │   ├── phone_auth_screen.dart     # Přihlašovací obrazovka
│   │   ├── sms_verification_screen.dart
│   │   └── profile_setup_screen.dart
│   ├── home/
│   │   ├── home_screen.dart      # Bottom nav wrapper
│   │   └── main_tab.dart         # Hlavní obrazovka
│   ├── report/
│   │   └── report_incident_screen.dart  # Nahlášení incidentu
│   ├── neighbourhood/
│   │   └── neighbourhood_screen.dart    # Mapa + seznam
│   ├── points/
│   │   └── points_screen.dart    # Gamifikace
│   └── settings/
│       └── settings_screen.dart  # Nastavení
└── widgets/
    └── incident_card.dart        # Karta incidentu

functions/
└── index.js                     # Firebase Cloud Functions

firestore.rules                  # Bezpečnostní pravidla
```

---

## 🎨 Design systém

| Token | Hodnota | Použití |
|-------|---------|---------|
| `AppColors.primary` | `#007AFF` | Tlačítka, ikony, linky |
| `AppColors.danger` | `#FF3B30` | Červené tlačítko, upozornění |
| `AppColors.success` | `#34C759` | Úspěch, zelené tečky |
| `AppColors.surface` | `#F2F2F7` | Pozadí karet |
| Font iOS | SF Pro | Systémový |
| Font Android | Roboto | Systémový |

---

## 🔒 GDPR & Bezpečnost

- **Anonymní ID** – žádné jméno ani adresa v Firestore incidents
- **GPS pouze při použití** – nikdy na pozadí bez souhlasu
- **Automatické mazání** – incidenty po 7 dnech (Cloud Function)
- **Firestore Rules** – uživatel čte/píše pouze svá data
- **Číslo bytu** – zobrazuje se jen jako text, ne přesná adresa

---

## 📲 Push notifikace – formát

```
Titulek: 🚨 Incident v ulici!
Tělo: V ulici Na Žižkově 12 někdo šmejdí. Nejbližší: TY (3 m). Jdeš?

Akční tlačítka:
  [Jdu ✅]  [Zavolat policii 158 🚨]
```

Notifikace se odesílají pouze uživatelům do **100 m od místa incidentu**.

---

## 🏆 Bodový systém

| Akce | Body |
|------|------|
| Nahlásit incident | 3 |
| Reagovat „Jdu" | 2 |
| Zavolat policii | 5 |
| **Odměna při 5+ bodech** | Sleva na pojištění 🎁 |

---

## 🛠️ TODO pro produkci

- [ ] App icon a splash screen
- [ ] Lokalizace (intl package)
- [ ] Deeplinking pro notifikace
- [ ] Analytics (Firebase Analytics)
- [ ] Crashlytics
- [ ] App Store / Google Play listing
- [ ] TestFlight beta testing
- [ ] Rate limiting pro hlášení (max 5/hod)

