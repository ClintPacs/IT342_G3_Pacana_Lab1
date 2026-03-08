# ✅ BrewBatch — Task Checklist
> IT342 Laboratory 1 | Group 3
> Last Updated: March 2026

---

## ✅ DONE

| Task | Description | Completed By |
|------|-------------|--------------|
| Backend Init | Set up Spring Boot 3.5.11 project with Maven, group `edu.cit.pacana`, artifact `brewbatch` | Pacaña, Clint |
| Database Config | Configured Supabase PostgreSQL connection via Session Pooler in `application.properties` | Pacaña, Clint |
| User Entity | Implemented `User.java` JPA entity with fields: id, username, email, password_hash, full_name, role, is_active, created_at. Role enum: BARISTA, MANAGER, ADMIN | Pacaña, Clint |
| User Repository | Created `UserRepository` with `findByUsername`, `findByEmail`, `existsByUsername`, `existsByEmail` | Pacaña, Clint |
| BCrypt Password | Configured `BCryptPasswordEncoder` with 12 salt rounds in `WebSecurityConfig` | Pacaña, Clint |
| JWT Utils | Implemented `JwtUtils` for token generation and validation using HMAC-SHA256 | Pacaña, Clint |
| Auth Filter | Created `AuthTokenFilter` to intercept and validate JWT per request via `OncePerRequestFilter` | Pacaña, Clint |
| Auth Entry Point | Implemented `AuthEntryPointJwt` returning structured JSON 401 response | Pacaña, Clint |
| UserDetails | Implemented `UserDetailsImpl` and `UserDetailsServiceImpl` for Spring Security integration | Pacaña, Clint |
| Security Config | Configured `WebSecurityConfig` with CORS (localhost:3000 + 10.0.2.2), stateless sessions, open/protected routes | Pacaña, Clint |
| DTOs | Created `RegisterRequest`, `LoginRequest`, `JwtResponse`, `MessageResponse` with Jakarta validation | Pacaña, Clint |
| Auth Service | Implemented `AuthService` with register (duplicate check) and login (JWT generation) logic | Pacaña, Clint |
| Auth Controller | Implemented `POST /api/auth/register`, `POST /api/auth/login`, `POST /api/auth/logout` | Pacaña, Clint |
| User Controller | Implemented protected `GET /api/user/me` endpoint returning full profile | Pacaña, Clint |
| React Init | Bootstrapped React 18 app, single-file `App.js` with all screens | Pacaña, Clint |
| React Auth | Built `AuthContext` with login, logout, token persistence via localStorage | Pacaña, Clint |
| Login Page | Built `LoginScreen` with username + password, error state, loading dots, coffee wireframe design | Pacaña, Clint |
| Register Page | Built `RegisterScreen` with all 5 fields, validation, password match check, success state | Pacaña, Clint |
| Dashboard Page | Built `DashboardPage` with top nav, sidebar, stat cards, profile table, JWT-protected `/api/user/me` call | Pacaña, Clint |
| React Routing | Simple screen state router in `App.js` — login → register → dashboard flow | Pacaña, Clint |
| Android Init | Created Android project with Kotlin + Jetpack Compose, package `com.example.brewbatch`, minSdk 26 | Pacaña, Clint |
| Android Network | Implemented `ApiService.kt`, `RetrofitClient.kt` (base URL: 10.0.2.2:8080), `SessionManager.kt` | Pacaña, Clint |
| Android Login | Built `LoginScreen.kt` in Compose — username + password, error state, JWT token storage | Pacaña, Clint |
| Android Register | Built `RegisterScreen.kt` in Compose — all fields, validation, success banner, redirect to login | Pacaña, Clint |
| Android Dashboard | Built `DashboardScreen.kt` in Compose — top nav, stat cards, profile card, logout, refresh | Pacaña, Clint |
| Android Navigation | Implemented screen navigation in `MainActivity.kt` using Compose state — login/register/dashboard | Pacaña, Clint |
| Backend Connected | Backend successfully connects to Supabase, `users` table auto-created by Hibernate | Pacaña, Clint |
| Web Connected | React frontend connected to Spring Boot backend at localhost:8080 | Pacaña, Clint |
| Mobile Connected | Android app connected to Spring Boot backend via 10.0.2.2:8080 | Pacaña, Clint |

---

## 🔄 IN-PROGRESS

| Task | Description | Assigned To | Target Date |
|------|-------------|-------------|-------------|
| Inventory Module | Design and implement `InventoryItem` entity, service, controller, and React UI | — | — |
| Orders Module | Create `Order` and `OrderItem` entities with full CRUD API and React UI | — | — |
| Android Inventory Screen | Build inventory list screen in Compose showing items and stock status | — | — |
| Android Orders Screen | Build orders screen in Compose for viewing and creating orders | — | — |

---

## 📋 TODO

| Task | Description | Priority | Assigned To |
|------|-------------|----------|-------------|
| Role-Based Access | Restrict endpoints by role — ADMIN, MANAGER, BARISTA | High | — |
| Inventory CRUD UI | Frontend pages for listing, adding, editing, deleting inventory items | High | — |
| Order Management UI | Frontend pages to create, view, and update purchase orders | High | — |
| Alerts Module | Low stock alerts system — backend logic + frontend display + Android screen | High | — |
| Suppliers Module | Supplier management — entity, CRUD API, React UI, Android screen | Medium | — |
| Dashboard Charts | Add Chart.js graphs for sales and inventory trends | Medium | — |
| Error Handling | Global error boundary in React + centralized exception handler in Spring Boot | Medium | — |
| Unit Tests | JUnit tests for `AuthService` + integration tests for auth endpoints | Medium | — |
| Refresh Tokens | Implement JWT refresh token flow to extend sessions | Low | — |
| Dockerize | Add `Dockerfile` and `docker-compose.yml` for easy deployment | Low | — |
| Deploy | Deploy backend to Railway/Render and frontend to Vercel | Low | — |
| API Documentation | Integrate Swagger/OpenAPI for auto-generated API docs | Low | — |

---

## 📎 Notes

- Backend uses **Supabase PostgreSQL** (not MySQL) via Session Pooler connection
- Android emulator connects to local backend via `http://10.0.2.2:8080`
- All passwords hashed with **BCrypt 12 rounds** — never stored as plain text
- JWT tokens expire after **24 hours** (86400000ms)
- Roles available: `BARISTA`, `MANAGER`, `ADMIN`
- Update this checklist after every work session
