# RideRent - Backend API Service

RideRent is an enterprise-grade RESTful backend service for a Vehicle Rental & Fleet Management system built with **Spring Boot 3**, **Java 21**, and **Spring Security**. It powers real-time vehicle booking, dynamic pricing, role-based fleet management, automated PDF invoice generation, and customer engagement features.

---

## 🛠️ Tech Stack & Architecture

- **Framework**: Spring Boot 3.3.4 (Spring Web, Spring Security, Spring Data JPA, Spring Validation)
- **Language**: Java 21
- **Security**: JWT (JSON Web Tokens) with stateless session management & BCrypt password hashing
- **Databases Supported**:
  - **H2 Database** (Zero-config embedded DB for development & testing)
  - **PostgreSQL** (Production & Cloud deployment, e.g., Render)
  - **MySQL** (Local/production standalone relational database)
- **Document Generation**: OpenPDF for dynamic PDF rental invoice generation
- **Containerization**: Docker (multi-stage build with Eclipse Temurin JDK/JRE 21)
- **Build Tool**: Apache Maven

---

## 🚀 Key Features

- **Authentication & RBAC**:
  - Secure registration, login, profile management, and password reset flows.
  - Role-Based Access Control (`ROLE_USER` / Customer, `ROLE_ADMIN` / Fleet Administrator).
- **Vehicle Catalog & Fleet Management**:
  - Dynamic vehicle querying and filtering with JPA Specification (by type, price range, brand, transmission, availability).
  - Admin CRUD for vehicles, specifications, images, and status management (`AVAILABLE`, `RENTED`, `MAINTENANCE`).
- **Booking & Reservations Lifecycle**:
  - Instant price quote calculator with coupon discounts and date duration calculation.
  - Reservation creation, modifications, rental date extensions, and cancellations.
- **Payments & Billing**:
  - Demo payment gateway processing with payment status transitions.
  - Automated PDF invoice generation downloadable via endpoint.
- **Customer Engagement & Fleet Maintenance**:
  - Wishlist saving and vehicle availability alerts.
  - Verified customer reviews and vehicle ratings.
  - Maintenance log tracking with scheduling, costs, and service records.
  - Admin dashboard metrics (revenue, active bookings, fleet utilization).

---

## ⚙️ Configuration & Environment Variables

Copy `.env.example` to `.env` or set system environment variables:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `PORT` | HTTP server port | `8085` |
| `SPRING_PROFILES_ACTIVE` | Active Spring profile (`dev`, `mysql`, `postgres`) | `dev` |
| `DB_HOST` | Database host (for MySQL/Postgres) | `localhost` |
| `DB_PORT` | Database port | `3306` (MySQL) / `5432` (PostgreSQL) |
| `DB_NAME` | Database name | `riderent_db` |
| `DB_USERNAME` | Database username | `root` |
| `DB_PASSWORD` | Database password | — |
| `JWT_SECRET` | Secret key for JWT token signing | 256-bit Hex string |
| `CORS_ALLOWED_ORIGINS` | Allowed CORS frontend origins | `http://localhost:5173,http://localhost:3000` |

---

## 🏃 Getting Started

### Prerequisites
- **JDK 21** or later
- **Maven 3.9+**

### 1. Run with In-Memory H2 (Quickest - Zero Config)
```bash
mvn spring-boot:run
```
The application will start on port `8085`. The H2 console will be accessible at:
- URL: `http://localhost:8085/h2-console`
- JDBC URL: `jdbc:h2:mem:riderentdb`
- Username: `sa`
- Password: *(blank)*

### 2. Run with MySQL Profile
```bash
mvn spring-boot:run -Dspring-boot.run.profiles=mysql
```

### 3. Build & Run with Docker
```bash
# Build Docker image
docker build -t riderent-backend .

# Run Docker container
docker run -p 8085:8085 --env-file .env riderent-backend
```

---

## 🔐 Default Administrator Account

Upon initial startup, the system seeds the default administrator account:
- **Email**: `admin@example.com`
- **Password**: `admin123`
- **Role**: `ROLE_ADMIN`, `ROLE_USER`

---

## 📋 API Overview

| Group | Base Endpoint | Description |
| :--- | :--- | :--- |
| **Auth** | `/api/auth` | Register, login, forgot/reset password, profile |
| **Vehicles** | `/api/vehicles` | Public search, vehicle details, admin management |
| **Bookings** | `/api/bookings` | Price quotes, create/modify bookings, extensions, cancellations |
| **Payments** | `/api/payments` | Process demo payments, payment history, invoice PDF download |
| **Reviews** | `/api/reviews` | Vehicle reviews and ratings |
| **Wishlist** | `/api/wishlist` | Customer saved vehicles & availability notifications |
| **Admin** | `/api/admin` | Dashboard analytics, fleet overview, maintenance tracking, user administration |

---

## 📄 License

This project is licensed under the MIT License.
