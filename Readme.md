# 🔐 SupaShield (Node.js + Kafka + JWT)

## 📘 Overview
**SupaShield** is a secure authentication and authorization system built using **Node.js**, **Express.js**, and **JWT**, focusing on token-based authentication (Access & Refresh Tokens) and role-based access control (RBAC).  
It ensures secure API access while enabling real-time, event-driven **security monitoring** via **Apache Kafka**.  
The system is fully **Dockerized**, ensuring scalability and seamless deployment across environments.  
A **design-first approach** was followed — sequence diagrams and architecture flows were created before coding to optimize workflows and service boundaries.

---

## 🚀 Features
- **Microservices Architecture** — Authentication and authorization built as independent modular services for scalability.  
- **RESTful APIs** — Secure endpoints for user login, signup, token management, and role-based access enforcement.  
- **Database Integration** — MySQL database stores users, roles, tokens, and authentication logs with Sequelize ORM.  
- **Kafka Messaging** — Publishes real-time authentication events (login, refresh, failures) for monitoring and anomaly detection.  
- **Design-First Development** — Used sequence diagrams to predefine authentication flow and API interaction before implementation.  
- **Dockerized Setup** — All services containerized for consistent deployment and horizontal scalability.

---

## ⚙️ System Workflow
1. **User Registration & Authentication** — User signs up or logs in; credentials validated via the AuthController.  
2. **Token Generation & Storage** — A short-lived **Access Token (JWT)** and long-lived **Refresh Token** are created and stored securely.  
3. **Kafka Event Logging** — Authentication events (e.g., login success/failure, token refresh) published to Kafka topics.  
4. **Role-Based Access Control (RBAC)** — Middleware verifies tokens and enforces user roles for each API route.  
5. **Token Refresh Handling** — Expired access tokens trigger refresh flow to issue a new JWT securely.  
6. **Security Monitoring** — Kafka consumers detect unusual login activity or repeated failures for real-time alerts.  
7. **Database Persistence** — User profiles, tokens, and logs stored securely in MySQL.  
8. **Scalability & Deployment** — Docker Compose manages independent service containers for deployment.  

---

## 🧩 Key Components

### 🧾 Authentication Service
- Handles user signup, login, and logout requests.  
- Generates and validates JWT access and refresh tokens.  
- Implements middleware for route protection and session validation.  
- Stores user credentials (hashed) and tokens securely in MySQL.  

### 🔑 Token Management System
- Manages the full lifecycle of JWT tokens — issue, verify, refresh, and revoke.  
- Stores refresh tokens for session persistence and replay protection.  
- Implements blacklist/whitelist logic for token invalidation when needed.  

### 🧠 Role-Based Access Control (RBAC)
- Defines user roles (e.g., `Admin`, `Manager`, `User`) with permissions.  
- Middleware enforces route-level access using roles and claims from decoded JWT.  
- Ensures users can access only their allowed resources.  

### 📡 Kafka Event Logging
- Publishes authentication events to Kafka topics (`auth-events`, `security-alerts`).  
- Kafka consumers track failed logins, token misuse, or suspicious sessions.  
- Enables real-time monitoring and audit logging of authentication flow.  

### 🧰 API Gateway & Middleware
- Acts as entry point for all authentication-related requests.  
- Validates JWT tokens before passing requests to downstream routes.  
- Uses Express middleware to populate request context with authenticated user data.  

### 🗄️ Database Layer
- **MySQL** used for structured storage of user, role, and token information.  
- Enforces constraints for referential integrity and audit logging.  
- Uses Sequelize ORM for modeling and database migrations.  

### 🐳 Dockerized Deployment
- Each service containerized with Docker and managed via Docker Compose.  
- Simplifies deployment and scaling across environments.  
- Consistent runtime setup for development, staging, and production.  

---

## 🧱 Architecture Diagram
Below is the high-level architecture showcasing the authentication flow and event-driven Kafka logging.

![Architecture Diagram]
<img width="1832" height="745" alt="image" src="https://github.com/user-attachments/assets/8c3c5bc8-fa40-4367-bf59-cea4761a36f2" />


---

## 🧵 Sequence Diagram
This diagram visualizes how authentication requests, token flows, and Kafka events interact between microservices.

![Sequence Diagram]
<img width="1846" height="646" alt="image" src="https://github.com/user-attachments/assets/edd3a579-ebc8-4461-9b00-9d6ad9ebf358" />


---

## 🧰 Technologies Used
**Backend:** Node.js, Express.js, JWT, Kafka  
**Database:** MySQL (Sequelize ORM)  
**Messaging:** Apache Kafka (Event-driven auth logs)  
**Containerization:** Docker, Docker Compose  
**Tools:** Postman (API Testing), VS Code, pgAdmin/MySQL Workbench  

---

## 🎯 Project Goals
- **Learn Secure Authentication** — Implement modern token-based login and session management.  
- **Explore Kafka Integration** — Use Kafka to track and analyze authentication behavior in real-time.  
- **Design Before Development** — Visualize system flows through diagrams before implementation.  
- **Build for Scale** — Use microservice principles and Docker for scalable deployment.  
- **Enhance Security Monitoring** — Enable alerting on suspicious logins or brute-force attempts.  

---

## 🧭 How to Run

```bash
# Clone the repository
git clone https://github.com/your-username/supashield.git
cd supashield

# Install dependencies
npm install

# Start Kafka & MySQL containers
docker-compose up -d

# Run the server
npm run dev
