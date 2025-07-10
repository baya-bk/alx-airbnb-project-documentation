# Backend Requirement Specifications – Airbnb Clone

This document outlines the functional and technical requirements for key backend features of the Airbnb Clone project.

---

## 1. User Authentication

### Functional Requirements:

- Users should be able to register with their first name, last name, email, and password.
- Users should be able to log in using email and password.
- JWT token should be returned upon successful login.
- Passwords must be securely hashed.

### API Endpoints:

- `POST /api/register`

  - **Input:** `{ "first_name": "John", "last_name": "Doe", "email": "john@example.com", "password": "secret123" }`
  - **Output:** `201 Created`, `{ "token": "jwt_token_here" }`

- `POST /api/login`
  - **Input:** `{ "email": "john@example.com", "password": "secret123" }`
  - **Output:** `200 OK`, `{ "token": "jwt_token_here" }`

### Validations:

- Email must be unique and valid format
- Password must be ≥ 8 characters

### Performance:

- Login response time should be under 500ms

---

## 2. Property Management

### Functional Requirements:

- Hosts can create, update, and delete property listings.
- Properties must include name, description, price, location, and availability.

### API Endpoints:

- `POST /api/properties`

  - **Auth required (host only)**
  - **Input:** `{ "name": "Cozy Room", "location": "Addis Ababa", "price": 45.99 }`
  - **Output:** `201 Created`, property object

- `GET /api/properties?location=Addis`

  - **Output:** list of matching properties

- `PATCH /api/properties/:id`

  - Update selected fields

- `DELETE /api/properties/:id`
  - Remove listing (host only)

### Validations:

- Price must be a positive decimal
- Name and location required

### Performance:

- Property fetch by location should return in < 800ms

---

## 3. Booking System

### Functional Requirements:

- Users can book available properties
- Hosts cannot book their own listings
- Overlapping dates must be rejected

### API Endpoints:

- `POST /api/bookings`

  - **Input:** `{ "property_id": "...", "start_date": "2025-08-01", "end_date": "2025-08-05" }`
  - **Output:** `201 Created`, booking object

- `GET /api/bookings/user`

  - List bookings by the authenticated user

- `DELETE /api/bookings/:id`
  - Cancel a booking (guest only)

### Validations:

- Dates must be in the future
- Property must be available
- Duration ≥ 1 night

### Performance:

- Booking creation and validation within 1s

---
