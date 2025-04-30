# airbnb-clone-project
## Team Role
### Business analyst (BA)
- A business analyst dives deep into a customer’s workflows and analyzes stakeholder feedback to help a client formulate what their wants look like and align a customer’s vision with what a development team is producing.
- They translate an abstract product idea into a set of tangible requirements.
### Product owner (PO)
- Holding more responsibility for a product’s success than any other development team member, a product owner is a decision-maker. Balancing both business needs and market trends, they define a business strategy, shape up the product vision, make sure it satisfies customer needs, and manage a product backlog. Associated mainly with flexible Agile environments, a product owner is particularly useful in scenarios where requirements and workflows frequently change.
### Project manager (PM)
- In sequential models, a project manager is responsible for distributing tasks across team members, planning work activities, and updating project status.
- In Agile projects where the focus is on self-management, transparency, and shared ownership, a PM sets up the vision of a product, maintains transparency, fosters communication, searches for improvements in the development process, and makes sure a team delivers more value with each iteration.
### UI/UX designer
- There are two aspects to the product design process—user interface (UI) and user experience (UX) design.
- A UI designer devises intuitive, easy-to-use, and eye-pleasing interfaces for a product, while the UX part stands for thinking out an entire journey of a user’s interaction with a product. A UX designer is thus involved in such activities as user research, persona development, information architecture design, wireframing, prototyping, and more.
### Software developer
- Engineers and stabilizes the product
- Solves any technical problems emerging during the development lifecycle
- A software developer does the actual job and codes an application. And just like an app features a front end and a back end, there are front-end and back-end developers.
- Front-end developers create the part of an application that users interact with, ensuring that an app offers an equally smooth experience to all—no matter the device, platform, or operational system.
### Quality assurance (QA) engineer
- Makes sure an application performs according to requirements
- Spots functional and non-functional defects
- The job of a quality assurance engineer is to verify whether an application meets the requirements—both functional and non-functional. Functional requirements define what an application should do, while non-functional requirements specify how it should do that. To verify both, QA specialists run various checks, followed by analyzing the test results and reporting on the application quality.
### DevOps engineer
- Facilitates cooperation between development and operations teams
- Builds continuous integration and continuous delivery (CI/CD) pipelines for faster delivery
- Even in Agile environments, development and operations teams can be siloed. DevOps engineers serve as a link between the two teams, unifying and automating the software delivery process and helping strike a balance between introducing changes quickly and keeping an application stable. Working together with software developers, system administrators, and operational staff, DevOps engineers oversee and facilitate code releases on a CI/CD basis.

## Technology Stack
- **Django**: A high-level Python web framework used for building the RESTful API.
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs.
- **PostgreSQL**: A powerful relational database used for data storage.
- **GraphQL**: Allows for flexible and efficient querying of data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool for consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.

## Database Design

This section outlines the core entities required for the project and describes their key fields and relationships.

### Key Entities and Fields

#### 1. Users
- **id**: Unique identifier for each user.
- **name**: Full name of the user.
- **email**: User’s email address (unique).
- **password_hash**: Encrypted password for authentication.
- **role**: Defines if the user is a guest, host, or admin.

#### 2. Properties
- **id**: Unique identifier for each property.
- **user_id**: References the owner (host) from the Users table.
- **title**: Name or title of the property.
- **address**: Physical location of the property.
- **description**: Detailed information about the property.

#### 3. Bookings
- **id**: Unique identifier for each booking.
- **user_id**: References the guest from the Users table.
- **property_id**: References the booked property.
- **start_date**: Start date of the booking.
- **end_date**: End date of the booking.

#### 4. Reviews
- **id**: Unique identifier for each review.
- **user_id**: References the reviewer from the Users table.
- **property_id**: References the reviewed property.
- **rating**: Numeric rating given by the user.
- **comment**: Textual feedback from the user.

#### 5. Payments
- **id**: Unique identifier for each payment.
- **booking_id**: References the associated booking.
- **user_id**: References the user who made the payment.
- **amount**: Total payment amount.
- **status**: Payment status (e.g., pending, completed, failed).

---

### Entity Relationships

- **User–Property**: A user (host) can own multiple properties. Each property belongs to one user.
- **User–Booking**: A user (guest) can make multiple bookings. Each booking is made by one user.
- **Property–Booking**: A property can have multiple bookings over time. Each booking is for one property.
- **User–Review–Property**: A user can leave multiple reviews, each for a different property. Each review is linked to both a user and a property.
- **Booking–Payment**: Each booking can have one or more payments. Each payment is associated with a specific booking and user.

This structure ensures data integrity and supports the core functionalities of the project, such as property listing, booking, reviewing, and payment processing.

## Feature Breakdown

Below are the main features of the project, each designed to deliver a seamless property rental experience for users, hosts, and administrators.

### User Management
This feature allows users to register, log in, and manage their profiles securely. It supports different user roles such as guests, hosts, and admins, ensuring that each user has access to the appropriate functionalities within the platform.

### Property Management
Hosts can list new properties, update details, upload photos, and manage availability through this feature. It enables efficient property discovery for guests by supporting property search, filtering, and detailed property pages.

### Booking System
Guests can book available properties for specific dates, view their booking history, and manage upcoming reservations. This feature handles booking conflicts, ensures date availability, and provides hosts with a clear overview of their bookings.

### Review System
After completing a stay, guests can leave ratings and written reviews for properties. This feature helps build trust within the community, assists future guests in making informed decisions, and provides valuable feedback to hosts.

### Payment Processing
The platform supports secure online payments for bookings, including payment status tracking and history. This feature ensures a smooth financial transaction process between guests and hosts, increasing convenience and trust for all parties.

### Admin Dashboard
Administrators have access to a dedicated dashboard for monitoring users, properties, bookings, and payments. This feature allows for moderation, reporting, and overall management of the platform to maintain quality and security.

## API Security

This section outlines the security measures implemented to protect the API, users, and sensitive data across the project.

### Key Security Measures

#### 1. **Authentication (JWT Tokens)**  
All API endpoints require JWT (JSON Web Tokens) for user identity verification. Tokens are issued after successful login and expire after a short duration.  
**Why it matters**: Prevents unauthorized access to user accounts and ensures only legitimate users can perform actions like bookings or payments.

#### 2. **Role-Based Authorization**  
Users are granted permissions based on their roles (guest, host, admin). For example, only hosts can update property details, and admins can moderate reviews.  
**Why it matters**: Restricts sensitive actions (e.g., payment processing, admin controls) to authorized roles, minimizing misuse or data breaches.

#### 3. **Rate Limiting**  
API requests are throttled to a defined number per minute per user/IP address. Critical endpoints (e.g., login, payments) have stricter limits.  
**Why it matters**: Mitigates DDoS attacks, brute-force login attempts, and API abuse, ensuring system stability.

#### 4. **Input Validation & Sanitization**  
All user inputs are validated against strict schemas and sanitized to remove malicious code (e.g., SQL injections, XSS).  
**Why it matters**: Protects databases and backend systems from exploitation, ensuring data integrity and preventing breaches.

#### 5. **HTTPS Encryption**  
All API communication uses HTTPS with TLS 1.2+ to encrypt data in transit.  
**Why it matters**: Safeguards sensitive data (passwords, payment details) from interception during transmission.

#### 6. **Logging & Monitoring**  
API activity is logged (without storing sensitive data), and anomalies (e.g., repeated failed logins) trigger alerts.  
**Why it matters**: Enables rapid detection of suspicious behavior, aiding incident response and compliance audits.

---

### Security by Feature  
- **User Management**: Authentication and authorization ensure only valid users access profiles.  
- **Payments**: HTTPS and input validation protect financial data during transactions.  
- **Property/Bookings**: Rate limiting and role-based controls prevent spam or unauthorized modifications.  
- **Reviews**: Sanitization blocks malicious content, maintaining platform trust.  

These measures collectively ensure compliance with GDPR, PCI-DSS, and other standards while fostering user trust.

## CI/CD Pipeline

A CI/CD (Continuous Integration/Continuous Delivery) pipeline is an automated workflow that guides software development teams through building, testing, and deploying code changes. By automating these processes, the pipeline minimizes human error, ensures consistency, and enables faster, more reliable software releases. This automation is crucial for maintaining high code quality, accelerating delivery cycles, and quickly addressing bugs or vulnerabilities.
Implementing a CI/CD pipeline is important for this project because it allows for rapid integration of new features and bug fixes, ensures that all code changes are thoroughly tested before deployment, and reduces the risk of introducing errors into production. This leads to a more robust, stable, and secure application, while also fostering better collaboration among development and operations teams.

**Common tools for CI/CD pipelines include:**
- **GitHub Actions:** Automates workflows for building, testing, and deploying code directly from GitHub repositories.
- **Docker:** Packages applications and dependencies into containers for consistent deployment across environments.
- **Other options:** GitLab CI, CircleCI, Jenkins, and similar platforms can also be used to orchestrate and automate the CI/CD process.

By leveraging these tools, the project can achieve streamlined software delivery, higher reliability, and faster response to user needs.

