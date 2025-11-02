# Normalization to 3NF

This schema is **in 3NF** with the following reasoning.

## 1NF
- All attributes are atomic (no repeating groups or arrays in a single column).
- Each table has a primary key.
- All rows are unique.

## 2NF
- No partial dependencies because every table's PK is a single-attribute surrogate key (UUID).
- All non-key attributes depend on the whole key in their respective tables.

## 3NF
- No transitive dependencies from non-key attributes to other non-key attributes:
  - **User**: name/email/password/phone/role each describe the user, not each other.
  - **Property**: name/description/location/price are independent descriptors of the property; host_id references User.
  - **Booking**: dates, total_price, and status describe a booking instance. (We ensure derived attributes like `total_price` are stored by policy; it depends on `pricepernight` * number of nights at booking time; consider keeping as snapshot to preserve history.)
  - **Payment**: amount, payment_date, and method describe the payment; booking_id is the reference.
  - **Review**: rating/comment/created_at describe a review of a property by a user.
  - **Message**: message_body/sent_at describe a message between users.

### Notes / Minor Design Decisions
- **Enums** (role, booking status, payment method) are domain constraints, not new entities; this retains 3NF.
- **Total price** in Booking is a materialized/snapshotted value; acceptable for analytics and audit. If you prefer strict derivation, you could compute on the fly and omit the column.
- To prevent **overlapping bookings** per property, an `EXCLUDE` constraint using a `daterange` is provided in the schema (needs `btree_gist` extension). This is a business rule, not a normalization issue.
- Timestamps are system-managed defaults; no normalization impact.

## Potential Extensions (Still 3NF)
- **Amenities** (Property N—M Amenity via PropertyAmenity).
- **Photos** (Property 1—N Photo).
- **Favorites** (User N—M Property via Favorite).
- **Availability/Calendar** (Property 1—N BlockedDate or CalendarEvent).