### Use Case: Rental Marketplace Platform

**Description**: The Airbnb Clone backend enables guests to search and book properties listed by hosts, with secure payments, reviews, notifications, and admin oversight.

**Actors**:

- **Guest**: Searches, books, and reviews properties.
- **Host**: Lists and manages properties.
- **Admin**: Manages users, listings, bookings, and payments.

**Main Flow**:

1. **Registration/Login**: Users sign up as guest/host (email/password or OAuth), get JWT, update profiles (photos in AWS S3/Cloudinary).
2. **Listings**: Hosts create/edit/delete property listings (details, images).
3. **Search/Booking**: Guests filter properties (location, price, amenities), book with date validation, pay via Stripe/PayPal.
4. **Booking Management**: Confirm/cancel bookings, track status, send notifications (SendGrid/Mailgun).
5. **Reviews**: Guests review properties; hosts respond.
6. **Payouts**: Hosts receive automatic payouts post-booking.
7. **Admin**: Monitors users, listings, bookings via RBAC dashboard.

**Alternatives**:

- Invalid login: Error message, retry option.
- Booking conflict: Suggest alternatives.
- Payment failure: Retry prompt.
- Unauthorized access: RBAC denies action.

**Exceptions**:

- Server errors logged with clear messages.
- Security via encryption, firewalls, rate limiting.
- Backups prevent data loss.

**Non-Functional**:

- Scalable modular design with load balancers.
- Fast performance via Redis caching, optimized queries.
- Secure with JWT, AES-256, HTTPS/TLS.
- Reliable with pytest unit/integration tests.

**Frequency**: Daily use for browsing, booking, managing.

**Assumptions**: Users have internet, third-party services are active, complies with regulations.
