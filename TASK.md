# Sacaada_appv2 Bus Transportation Booking App Tasks

## 1. Setup & Configuration

- Create Firebase Project in the Firebase Console
- Register Android/iOS apps, download config files (`google-services.json` / `GoogleService-Info.plist`)
- Enable Email/Password Authentication and Cloud Firestore in Firebase
- Initialize a new Flutter project (`flutter create bus_booking_app`)
- Install dependencies in `pubspec.yaml` (firebase_core, firebase_auth, cloud_firestore, etc.)

## 2. Authentication

### Sign Up Flow

- Create a `register_page.dart` with email/password fields and connect to Firebase Auth
- Store additional user data (e.g. isAdmin) in `/users/{userId}` on signup

### Login Flow

- Create a `login_page.dart` for existing user login
- On success, check Firestore for isAdmin flag, then direct to Admin or Customer home

## 3. Splash & Routing

### Splash Screen (`splash_screen.dart`)

- Check if a user is logged in, then query Firestore for isAdmin
- Route admin users to AdminHomePage; otherwise, route customers to HomePage

### Route Definitions

- In `main.dart`, set initial route to Splash, and define named routes for login, register, home, admin home, etc.

## 4. Customer Flow

### Home Page (`home_page.dart`)

- List or search buses (Firestore query)
- Display basic info: bus name, route, departure time, price

### Seat Selection (`seat_selection_page.dart`)

- Fetch available seats from Firestore (buses collection)
- Allow user to pick a seat
- On booking, create a record in `/bookings` and remove the seat from the bus's available_seats

### Booking History (`booking_history_page.dart`)

- Query `/bookings` by user_id
- Display seat number, bus ID, booking date/time

## 5. Admin Flow

### Admin Home Page (`admin_home_page.dart`)

- Display a list of buses from `/buses`
- Include options to edit or delete bus entries

### Add/Edit Bus (`admin_add_bus_page.dart`)

- Form to create a new bus document: bus_name, route, departure_time, available_seats[], price
- Optionally support editing an existing bus

## 6. Optional Offline Mode

### Local DB Setup (`local_db_service.dart`)

- Use sqflite and path_provider to store offline data (e.g., user's recent bookings)

### Sync Logic

- When online, push local changes to Firestore
- Handle conflict resolution (e.g., seat already booked)

## 7. UI/UX & Styling

### Consistent Theming

- Apply a uniform color scheme or theme across all pages

### Responsive Layouts

- Ensure pages look good on various screen sizes (phones, tablets)

### User Feedback

- Provide success or error messages via SnackBar, dialogs, or in-line notifications

## 8. Security & Deployment

### Firestore Security Rules

- Restrict `/buses` write operations to admin users only
- Restrict `/bookings` create operations to authenticated users

### Final Testing

- Verify sign-up, login, booking flow, concurrency on seat booking, etc.

### Deploy

- Generate an APK or iOS build to distribute or test

## 9. Future Enhancements (Optional)

- Payment Integration (Stripe, PayPal, etc.)
- Push Notifications for booking confirmation or schedule changes
- Analytics Dashboard (daily bookings, popular routes, etc.)
- Advanced Seat Map (visual grid layout)
