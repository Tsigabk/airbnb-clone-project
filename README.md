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
 
Feature Breakdown
  1. User Management
This feature handles user registration, authentication, and profile management. Users can sign up as either hosts (to list properties) or guests (to book properties). It ensures secure login, data protection, and personalized access throughout the platform.

2. Property Management
Hosts can create, update, and delete property listings. Each property includes essential details such as title, location, price per night, and description. This feature allows hosts to showcase their listings while giving guests an easy way to browse available properties.

3. Booking System
Guests can view property availability and make reservations for specific dates. The system prevents double-booking and tracks the booking status (e.g., pending, confirmed, cancelled). It ensures a seamless experience for both guests and hosts during the reservation process.

4. Payment Processing
This feature manages secure payments for property bookings. It records payment details such as amount, status, and method, ensuring transparency and reliability in all transactions. Successful integration guarantees trust between guests and hosts.

5. Review and Rating System
Guests can share their experiences by leaving reviews and ratings on properties they have booked. Reviews enhance transparency and help future guests make informed decisions, while providing hosts with valuable feedback to improve their offerings.

6. API Endpoints
The project provides RESTful API endpoints for all major entities — Users, Properties, Bookings, Payments, and Reviews. This allows seamless communication between the frontend and backend, ensuring scalability and easy integration with external services.

API Security Overview
- Securing the backend APIs is a critical part of the Airbnb Clone Project. Since the application manages sensitive data such as user information, booking details, and payment records, robust security measures are implemented to protect both users and the system from unauthorized access or malicious activity.
  
1. Authentication
  - All API endpoints that handle sensitive operations require user authentication using secure methods such as JWT (JSON Web Tokens) or OAuth 2.0.
  - Why it’s important: Authentication ensures that only verified users can access protected resources, preventing impersonation and unauthorized access to user accounts.

2. Authorization
  - Once authenticated, users are granted access based on their roles (e.g., host, guest, admin). Role-based access control (RBAC) ensures that users can only perform actions permitted for their role.
  - Why it’s important: Authorization prevents users from performing restricted actions — for example, a guest cannot edit another host’s property or view sensitive booking data.

3. Data Encryption
  - Sensitive information such as passwords and payment details are encrypted both in transit (using HTTPS/TLS) and at rest (using hashing or encryption algorithms).
  - Why it’s important: Encryption protects confidential user data from being exposed in case of data interception or server breaches.

4. Rate Limiting
  - The API enforces rate limiting to control the number of requests a client can make in a given time period.
  - Why it’s important: This prevents abuse such as brute-force login attempts, denial-of-service (DoS) attacks, and excessive load on the server.

5. Input Validation & Sanitization
  - All user inputs are validated and sanitized before processing to prevent malicious attacks like SQL injection, XSS, or command injection.
  - Why it’s important: Input validation ensures the API processes only clean and expected data, maintaining the integrity and reliability of the backend.

6. Secure Payment Processing
  - Payments are handled through trusted and compliant third-party gateways that support encryption and fraud detection mechanisms.
  - Why it’s important: Protecting payment data is essential for user trust and compliance with standards such as PCI DSS.

7. Logging & Monitoring
  - All API requests and activities are logged and monitored for suspicious behavior. Alerts can be triggered for repeated failed login attempts or unauthorized access patterns.
  - Why it’s important: Continuous monitoring helps detect and respond to potential security threats in real time.
    
CI/CD Pipeline Overview
- What is CI/CD?

  - CI/CD (Continuous Integration and Continuous Deployment) is a development practice that automates the process of building, testing, and deploying code.
      - Continuous Integration (CI) ensures that new code changes are automatically tested and merged into the main branch without breaking existing functionality.
      - Continuous Deployment (CD) automates the release process, deploying the latest version of the application to production or staging environments with minimal manual intervention.

  - Why CI/CD is Important
        - Implementing a CI/CD pipeline ensures faster development cycles, higher code quality, and fewer deployment errors
        - It helps the Airbnb Clone Project by:
              - Automatically testing API endpoints and database integrations on every commit.
              - Reducing the risk of bugs reaching production.
              - Enabling rapid feature delivery and continuous improvement.
              - Maintaining consistent environments across development, staging, and production.

  - Tools Used
        - Several tools can be integrated to support the CI/CD workflow:
              - GitHub Actions – Automates testing, building, and deployment directly from the repository.
              - Docker – Provides containerized environments to ensure consistent deployment across systems.
              - Jenkins or Travis CI – Can be used for advanced CI/CD pipeline customization.
              - AWS / Azure / Render / Heroku – Cloud platforms for deploying the backend API and database services.
              - Postman / Pytest / Jest – Used for running automated API and unit tests during the pipeline process.

  - Example Workflow
      - Developer pushes code to GitHub.
      - GitHub Actions triggers automated tests and lint checks.
      - If tests pass, the app is built and deployed to a staging server (using Docker).
      - After approval, the latest build is automatically deployed to production.
