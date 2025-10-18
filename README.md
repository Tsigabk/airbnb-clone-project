# airbnb-clone-project
Airbnb Clone Project in the ALX ProDev Backend SE Course

Technology Stack
- Django: A high-level Python web framework used for building the RESTful API.
- Django REST Framework: Provides tools for creating and managing RESTful APIs.
- PostgreSQL: A powerful relational database used for data storage.
- GraphQL: Allows for flexible and efficient querying of data.
- Celery: For handling asynchronous tasks such as sending notifications or processing payments.
- Redis: Used for caching and session management.
- Docker: Containerization tool for consistent development and deployment environments.
- CI/CD Pipelines: Automated pipelines for testing and deploying code changes.

Database Design

Key Entities
- The application consists of five main entities: Users, Properties, Bookings, Payments, and Reviews.
These entities are interconnected to support core functionalities such as property management, booking, payment processing, and user feedback.

1. Users
- Stores information about individuals using the platform (both hosts and guests).
Key Fields
  - id (Primary Key): Unique identifier for each user.
  - name: Full name of the user.
  - email: User’s email address (must be unique).
  - password_hash: Hashed password for authentication.
  - role: Defines whether the user is a host or a guest.
Relationships
  - A user (host) can list multiple properties.
  - A user (guest) can make multiple bookings and write multiple reviews.
    
2. Properties
- Represents accommodations listed by users (hosts)
Key Fields
  - id (Primary Key): Unique identifier for each property.
  - user_id (Foreign Key): References the Users table.
  - title: Property name or title.
  - location: Address or general location of the property.
  - price_per_night: Cost to book the property per night.
Relationships
  - A property belongs to a user (host).
  - A property can have multiple bookings and reviews.
    
3. Bookings
- Tracks reservations made by guests for properties.
Key Fields
  - id (Primary Key): Unique booking identifier.
  - user_id (Foreign Key): References the Users table (guest).
  - property_id (Foreign Key): References the Properties table.
  - start_date: Check-in date.
  - end_date: Check-out date.
  - status: Booking status (e.g., pending, confirmed, cancelled).
Relationships
  - A booking belongs to one user (guest) and one property.
  - A booking can have one associated payment.
    
5. Payements
- Stores payment transaction details related to bookings.
Key Fields
  - id (Primary Key): Unique identifier for each payment.
  - booking_id (Foreign Key): References the Bookings table.
  - amount: Total payment amount.
  - payment_method: Payment type (e.g., credit card, PayPal).
  - status: Payment status (e.g., successful, failed, pending).
Relationships:
  - A payment belongs to a booking.
  
7. Reviews
- Contains feedback from guests about properties they have booked.
Key Fields
  - id (Primary Key): Unique identifier for each review.
  - user_id (Foreign Key): References the Users table (guest).
  - property_id (Foreign Key): References the Properties table.
  - rating: Numeric rating (e.g., 1–5).
  - comment: Written review content.
Relationships
  - A review belongs to one user (guest) and one property.
  - A property can have multiple reviews.
 
