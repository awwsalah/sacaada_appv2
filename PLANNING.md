# Sacaada_appv2 Bus Transportation Booking App

## 1. Overview

This project aims to build a bus transportation booking application in Flutter with a Firebase backend (Firestore + Authentication). It supports both customers (search and book buses) and admins (manage bus data).

### Primary Objectives

#### Customer Features:

- User Registration & Login (Firebase Auth)
- Search Buses by route, time, or city
- Seat Selection & Booking
- View Booking History

#### Admin Features:

- Admin Login
- Add/Edit/Delete Bus Entries
- (Optional) View All Bookings for reporting

## 2. Tech Stack

### Frontend: Flutter

- Screens: Splash, Login, Registration, Home (Customer), Admin Dashboard, etc.

### Backend: Firebase

- Authentication: Email/Password
- Firestore: Store bus data and bookings
- (Optional) Cloud Functions: Advanced logic or triggers
- Database: Firestore (online) + (Optional) SQLite (offline caching)

## 3. Project Structure

```
lib/
├── main.dart
├── models/
│   ├── bus_model.dart
│   └── booking_model.dart
├── services/
│   ├── auth_service.dart
│   ├── firebase_service.dart
│   └── local_db_service.dart // optional, for offline mode
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
    └── custom_widgets.dart
```

- **models/**: Dart classes representing data (Bus, Booking)
- **services/**: Logic for Firebase Auth, Firestore operations, optional local DB
- **pages/**: Individual screens for the app
- **widgets/**: Reusable UI components

## 4. Requirements

### Functional Requirements

#### Authentication

- Users can register and login via Firebase Auth
- Admin accounts are flagged (e.g., isAdmin in Firestore)

#### Bus Management (Admin)

- Add new bus with name, route, departure_time, available_seats, price
- Edit or remove existing buses in Firestore

#### Bus Search & Listing (Customer)

- List or search buses by route/time
- Display bus details: name, route, departure_time, price, available_seats

#### Seat Booking (Customer)

- Select a seat from available_seats
- Create a booking record in Firestore with user_id, bus_id, seat_number, booking_date
- Remove booked seat from the bus's available_seats

#### Booking History (Customer)

- Display past bookings (/bookings collection) filtered by user_id

#### Offline Mode (Optional)

- Cache essential data (e.g., bookings) locally using sqflite
- Sync to Firestore when online

### Non-Functional Requirements

#### Security & Role-Based Access

- Only admin users can modify the /buses collection
- Use Firestore security rules or custom claims

#### Performance

- App should handle standard query loads effectively

#### Scalability

- Firestore can scale automatically for larger data sets

## 5. Data Model

### Users Collection

```json
/users/{userId} : {
  "email": "user@example.com",
  "isAdmin": false
}
```

### Buses Collection

```json
/buses/{busId} : {
  "bus_name": "Sunrise Express",
  "route": "City A → City B",
  "departure_time": "07:00 AM",
  "available_seats": ["S1", "S2", ...],
  "price": 10.0
}
```

### Bookings Collection

```json
/bookings/{bookingId} : {
  "user_id": "123",
  "bus_id": "abc",
  "seat_number": "S1",
  "booking_date": "2025-03-10T12:34:56Z"
}
```

## 6. Implementation Steps

### Firebase Setup

1. Create Firebase project
2. Enable Authentication (Email/Password) and Firestore
3. Add config files (google-services.json / GoogleService-Info.plist)

### Project Initialization

```yaml
dependencies:
  firebase_core:
  firebase_auth:
  cloud_firestore:
  sqflite: # Optional for offline
  path_provider: # Optional for offline
```

### Authentication Flow

- SplashScreen: Determine if user is logged in, check admin flag → route to admin or customer home
- LoginPage: Email + Password → sign in with Firebase
- RegisterPage: Email + Password → create user doc in Firestore (set isAdmin = false)

### Admin Flow

- AdminHomePage: List buses, allow add/edit/delete
- AdminAddBusPage: Form to create a bus in Firestore

### Customer Flow

- HomePage: List/search buses
- SeatSelectionPage: Show bus details, let user pick seat
- BookingHistoryPage: Show bookings for the logged-in user

### Offline Support (Optional)

- Create local DB with sqflite for caching user bookings
- Sync with Firestore once online again

### Testing & Deployment

- Test: user registration, booking flow, concurrency on seat booking, etc.
- Deploy to Android/iOS (and optionally web if needed)

### Future Enhancements

- Push Notifications (Booking confirmation or reminders)
- Advanced Seat Layout (Grid-based seat selection)
- Analytics Dashboard for admins (bookings over time, seat occupancy, etc.)
