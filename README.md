# Sacaada_appv2 Bus Transportation Booking App

A Flutter application for booking bus tickets, featuring separate admin and customer flows. Uses Firebase for user authentication and Firestore data storage. Optional offline caching can be done via SQLite.

## Features

### Customer Flow

- User Registration & Login (Firebase Authentication)
- Search Buses by route/time
- Seat Selection & Booking
- View Booking History

### Admin Flow

- Admin Login (detected via isAdmin flag in Firestore)
- Manage Buses: add, edit, or delete bus entries
- (Optional) View Bookings for reporting purposes

## Tech Stack

- **Frontend**: Flutter (Dart)
- **Backend**: Firebase (Authentication, Firestore)
- **Database**: Firestore for real-time data, optionally sqflite for offline caching
- **Platform Support**: Android, iOS, (optional: Web, Desktop)

## Getting Started

### 1. Prerequisites

- Flutter SDK (version 3.0+ recommended)
- Dart (installed with Flutter)
- An IDE (VS Code, Android Studio) or text editor of your choice
- Firebase account (create a project at Firebase Console)

### 2. Firebase Setup

1. Create a Firebase Project in the Firebase Console
2. Register Your App (Android and/or iOS) in Firebase
3. Download the following config files:
   - Android: `google-services.json` → place in `android/app/`
   - iOS: `GoogleService-Info.plist` → place in `ios/Runner/`
4. Enable Firebase Auth (Email/Password) and Cloud Firestore in the Firebase Console

### 3. Flutter Project Setup

1. Clone or download this repository
2. Open the project folder in your IDE
3. Install Dependencies:
   ```bash
   flutter pub get
   ```

### 4. Configuration in pubspec.yaml

```yaml
name: bus_booking_app
description: A simple bus transportation booking app.

dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.10.0
  firebase_auth: ^4.6.0
  cloud_firestore: ^4.5.0
  # Optional for offline caching:
  sqflite: ^2.2.0
  path_provider: ^2.0.15
```

### 5. Running the App

```bash
# For Android
flutter run

# For iOS (requires Xcode and an iOS device/simulator)
flutter run
```

If you have multiple devices/emulators connected, specify one with:

```bash
flutter run -d <device-id>
```

### 6. Project Structure

```
lib/
├── main.dart
├── models/
│   ├── bus_model.dart
│   └── booking_model.dart
├── services/
│   ├── auth_service.dart
│   ├── firebase_service.dart
│   └── local_db_service.dart  # For offline SQLite caching
├── pages/
│   ├── splash_screen.dart
│   ├── login_page.dart
│   ├── register_page.dart
│   ├── home_page.dart
│   ├── seat_selection_page.dart
│   ├── booking_history_page.dart
│   ├── admin_home_page.dart
│   └── admin_add_bus_page.dart
└── widgets/
    └── custom_widgets.dart     # Reusable UI components
```

#### Key Components:

- **main.dart**: Initializes Firebase, sets up routes, includes the entry point main()
- **models/**: Data classes for Bus and Booking
- **services/**: Firebase and local DB operations
- **pages/**: All UI screens (Splash, Login, Admin, etc.)
- **widgets/**: Custom widgets used throughout the app

### 7. Usage Guide

#### Splash Screen

- Checks if a user is logged in and whether they are an admin
- Routes admin users to AdminHomePage and normal users to HomePage

#### Login & Register Pages

- Use FirebaseAuth to create or sign in users
- New users have isAdmin = false in /users/{userId} by default

#### Customer Flow

- HomePage: Lists or searches buses
- SeatSelectionPage: Chooses seat and books
- BookingHistoryPage: Shows user's past bookings

#### Admin Flow

- AdminHomePage: Lists all buses, allows deletion
- AdminAddBusPage: Creates or updates bus records

#### Offline Mode (optional)

- Store user actions in SQLite if offline
- Sync with Firestore once connected

### 8. Admin vs. Customer

- Admin is determined by isAdmin = true in the /users collection (or via custom claims if you set that up)
- Security: Add Firestore Security Rules to restrict write access to bus documents for non-admins

### 9. Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature-name`)
3. Commit your changes
4. Push to your branch and create a Pull Request

### 10. License

This project is available under the MIT License. Feel free to modify and distribute as per the license terms.

### 11. Troubleshooting & Common Issues

- **Firebase Initialization Errors**: Make sure the google-services.json or GoogleService-Info.plist files are correctly placed and your android/build.gradle and ios/Runner/ files are set up per Firebase docs
- **AndroidX Issues**: Ensure your Flutter project uses AndroidX (most recent Flutter projects do by default)
- **Seat Booking Conflicts**: Use Firestore transactions to handle multiple users booking the same seat at once

---

Thank you for using the Simple Bus Transportation Booking App!
If you encounter any issues or have suggestions, please open an issue or submit a pull request.
# sacaada_appv2
