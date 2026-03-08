# ☕ BrewBatch — Inventory & Order Management for Coffee Shops

> **IT342 Laboratory 1 |**
> A full-stack application to streamline inventory tracking and order management for coffee shops.

---

## 📌 Project Description

BrewBatch is a full-stack application (web + mobile) built to help coffee shop owners and staff efficiently manage their day-to-day operations. The system provides:

- **Secure user authentication** using JWT tokens
- **Inventory management** to track coffee beans, syrups, cups, and supplies
- **Order tracking** from placement to completion
- **Role-based access** for ADMIN, MANAGER, and BARISTA staff
- **Real-time dashboard** with key metrics at a glance
- **Android mobile app** for on-the-go access

---

## 🛠️ Technologies Used

| Layer      | Technology                                          |
|------------|-----------------------------------------------------|
| Backend    | Spring Boot 3.5.11, Spring Security 6               |
| Database   | PostgreSQL (Supabase), Spring Data JPA, Hibernate   |
| Auth       | JWT (jjwt 0.11.5), BCrypt (12 rounds)               |
| Frontend   | React 18, React Router v6                           |
| Mobile     | Android (Kotlin), Jetpack Compose, Retrofit2        |
| HTTP       | Axios (web), Retrofit2 + OkHttp (mobile)            |
| Build      | Maven (backend), npm (frontend), Gradle (mobile)    |

---

## 📁 Project Structure

```
IT342_G3_Pacana_Lab1/
├── backend/                              # Spring Boot application
│   ├── src/main/java/edu/cit/pacana/brewbatch/
│   │   ├── config/                       # WebSecurityConfig
│   │   ├── controller/                   # AuthController, UserController
│   │   ├── dto/                          # RegisterRequest, LoginRequest, JwtResponse, MessageResponse
│   │   ├── model/                        # User.java (JPA entity)
│   │   ├── repository/                   # UserRepository
│   │   ├── security/                     # JwtUtils, AuthTokenFilter, AuthEntryPointJwt
│   │   │                                   UserDetailsImpl, UserDetailsServiceImpl
│   │   └── service/                      # AuthService
│   ├── src/main/resources/
│   │   └── application.properties
│   └── pom.xml
├── frontend/                             # React frontend
│   ├── src/
│   │   └── App.js                        # All screens (Login, Register, Dashboard)
│   └── package.json
└── mobile/                               # Android Kotlin app
    ├── app/src/main/java/com/example/brewbatch/
    │   ├── network/                      # ApiService, RetrofitClient, SessionManager
    │   ├── LoginScreen.kt
    │   ├── RegisterScreen.kt
    │   ├── DashboardScreen.kt
    │   └── MainActivity.kt
    └── app/build.gradle.kts
```

---

## ⚙️ Setup — Backend (Spring Boot)

### Prerequisites
- Java JDK 17 (Microsoft OpenJDK 17.0.18 recommended)
- Maven 3.6+
- IntelliJ IDEA

### Steps

**1. Configure Supabase credentials**

Edit `backend/src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:postgresql://aws-1-ap-south-1.pooler.supabase.com:5432/postgres
spring.datasource.username=postgres.YOUR_PROJECT_REF
spring.datasource.password=YOUR_PASSWORD
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
app.jwt.secret=BrewBatchSuperSecretKeyForJWTSigningMustBe256BitsLong!
app.jwt.expiration-ms=86400000
```

**2. Run the backend in IntelliJ**

Open `BrewbatchApplication.java` → click ▶ Run

The API will be available at: `http://localhost:8080`

> Hibernate will auto-create the `users` table on first run.

---

## ⚙️ Setup — Frontend (React)

### Prerequisites
- Node.js 18+ and npm

### Steps

**1. Install dependencies**
```bash
cd frontend
npm install
```

**2. Start the development server**
```bash
npm start
```

The app will open at: `http://localhost:3000`

> Make sure the backend is running first before opening the frontend.

---

## ⚙️ Setup — Mobile (Android)

### Prerequisites
- Android Studio Ladybug (2024.2.1) or later
- Android SDK API 34+
- Java JDK 17

### Steps

**1. Open the project**

Open Android Studio → File → Open → select the `mobile/` folder

**2. Sync Gradle**

Click **Sync Now** when prompted

**3. Run on emulator**

Click ▶ Run — the app connects to the backend via `http://10.0.2.2:8080`

> `10.0.2.2` is the Android emulator's alias for your PC's `localhost`.
> Make sure the backend is running in IntelliJ before launching the emulator.

---

## 🔌 Connecting Frontend to Backend

**1. CORS (Backend — WebSecurityConfig.java)**
```java
config.setAllowedOrigins(List.of(
    "http://localhost:3000",
    "http://10.0.2.2:8080"
));
```

**2. Proxy (Frontend — package.json)**
```json
"proxy": "http://localhost:8080"
```

**3. Mobile base URL (RetrofitClient.kt)**
```kotlin
private const val BASE_URL = "http://10.0.2.2:8080/"
```

**4. JWT Flow**
```
User logs in → POST /api/auth/login
Backend returns JWT token
Web: stores token in localStorage
Mobile: stores token in SharedPreferences
Every subsequent request: Authorization: Bearer <token>
Backend validates token via AuthTokenFilter
```

---

## 📡 API Endpoint Reference

| Method | Endpoint             | Auth Required | Description                      |
|--------|----------------------|---------------|----------------------------------|
| POST   | `/api/auth/register` | ❌ No          | Register a new user              |
| POST   | `/api/auth/login`    | ❌ No          | Login and receive JWT token      |
| GET    | `/api/user/me`       | ✅ Yes (JWT)   | Get authenticated user's profile |

### Sample Requests

**Register**
```json
POST /api/auth/register
{
  "username": "barista01",
  "fullName": "Jane Doe",
  "email": "barista@brewbatch.com",
  "password": "coffee123",
  "role": "BARISTA"
}
```

**Login**
```json
POST /api/auth/login
{
  "username": "barista01",
  "password": "coffee123"
}
```

**Response:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "type": "Bearer",
  "id": 1,
  "username": "barista01",
  "email": "barista@brewbatch.com",
  "role": "ROLE_BARISTA"
}
```

**Get Profile**
```
GET /api/user/me
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...
```

---

## 🗄️ Database Table

**Platform:** Supabase (PostgreSQL)
**Table:** `users`

| Column        | Type         | Constraints                  |
|---------------|--------------|------------------------------|
| id            | BIGINT       | PRIMARY KEY, AUTO INCREMENT  |
| username      | VARCHAR(100) | NOT NULL, UNIQUE             |
| email         | VARCHAR(150) | NOT NULL, UNIQUE             |
| password_hash | VARCHAR(255) | NOT NULL, BCrypt hashed      |
| full_name     | VARCHAR(150) | NOT NULL                     |
| role          | VARCHAR(50)  | NOT NULL, DEFAULT BARISTA    |
| is_active     | BOOLEAN      | DEFAULT TRUE                 |
| created_at    | TIMESTAMP    | DEFAULT NOW()                |

---

## 📄 License

For academic use only — IT342, Academic Year 2024–2025.
