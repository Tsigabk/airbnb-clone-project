# AirBnB ERD Requirements

This document lists entities, attributes, keys, and relationships, and includes a Draw.io diagram file you can open with https://app.diagrams.net.

## Entities & Attributes

### User
- **user_id**: UUID, PK, indexed
- **first_name**: VARCHAR, NOT NULL  
- **last_name**: VARCHAR, NOT NULL  
- **email**: VARCHAR, UNIQUE, NOT NULL  
- **password_hash**: VARCHAR, NOT NULL  
- **phone_number**: VARCHAR, NULL  
- **role**: ENUM('guest','host','admin'), NOT NULL  
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

### Property
- **property_id**: UUID, PK, indexed  
- **host_id**: UUID, FK → User(user_id)  
- **name**: VARCHAR, NOT NULL  
- **description**: TEXT, NOT NULL  
- **location**: VARCHAR, NOT NULL  
- **pricepernight**: DECIMAL, NOT NULL  
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- **updated_at**: TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP

### Booking
- **booking_id**: UUID, PK, indexed  
- **property_id**: UUID, FK → Property(property_id)  
- **user_id**: UUID, FK → User(user_id)  
- **start_date**: DATE, NOT NULL  
- **end_date**: DATE, NOT NULL  
- **total_price**: DECIMAL, NOT NULL  
- **status**: ENUM('pending','confirmed','canceled'), NOT NULL  
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

### Payment
- **payment_id**: UUID, PK, indexed  
- **booking_id**: UUID, FK → Booking(booking_id)  
- **amount**: DECIMAL, NOT NULL  
- **payment_date**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP  
- **payment_method**: ENUM('credit_card','paypal','stripe'), NOT NULL

### Review
- **review_id**: UUID, PK, indexed  
- **property_id**: UUID, FK → Property(property_id)  
- **user_id**: UUID, FK → User(user_id)  
- **rating**: INTEGER CHECK 1..5, NOT NULL  
- **comment**: TEXT, NOT NULL  
- **created_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

### Message
- **message_id**: UUID, PK, indexed  
- **sender_id**: UUID, FK → User(user_id)  
- **recipient_id**: UUID, FK → User(user_id)  
- **message_body**: TEXT, NOT NULL  
- **sent_at**: TIMESTAMP, DEFAULT CURRENT_TIMESTAMP

## Relationships
- **User (host) 1 — N Property** via Property.host_id  
- **User (guest) 1 — N Booking** via Booking.user_id  
- **Property 1 — N Booking** via Booking.property_id  
- **Booking 1 — 1..N Payment** via Payment.booking_id  
- **User 1 — N Review** via Review.user_id  
- **Property 1 — N Review** via Review.property_id  
- **User 1 — N Message (sent)** via Message.sender_id  
- **User 1 — N Message (received)** via Message.recipient_id

Open the visual diagram file in this folder: **`airbnb-erd.drawio`**.