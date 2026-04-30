# AWS S3 Image Upload Service

A full-stack web application that allows users to register, authenticate, and upload profile images securely to AWS S3. This project demonstrates real-world backend architecture using Spring Boot, JWT authentication, PostgreSQL, and cloud storage integration.

---

## 🚀 Features

- User registration and authentication using JWT
- Secure REST APIs built with Spring Boot
- Upload and retrieve images from AWS S3
- PostgreSQL database integration with Flyway migrations
- Role-based security using Spring Security
- Dockerized PostgreSQL setup
- React frontend with drag-and-drop file upload

---

## 🛠️ Tech Stack

### Backend
- Java 17
- Spring Boot
- Spring Security
- Spring Data JPA
- PostgreSQL
- Flyway
- AWS SDK (S3)

### Frontend
- React
- Axios
- React Dropzone

### DevOps / Tools
- Docker
- Maven

---

## 📂 Project Structure
# Project Structure

```text
aws-s3-image-service/
├── .ci/
│   └── build-publish.sh
├── .github/
│   └── workflows/
├── .idea/
├── .mvn/
│   └── wrapper/
│       └── maven-wrapper.properties
├── backend [amigoscode-api]/
│   ├── .mvn/
│   │   └── wrapper/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   └── resources/
│   │   └── test/
│   │       ├── java/
│   │       └── resources/
│   ├── target/
│   ├── mvnw
│   ├── mvnw.cmd
│   ├── pom.xml
│   └── README.md
├── frontend/
│   ├── angular/
│   │   ├── src/
│   │   │   ├── app/
│   │   │   │   ├── components/
│   │   │   │   │   ├── customer/
│   │   │   │   │   ├── customer-card/
│   │   │   │   │   ├── header-bar/
│   │   │   │   │   ├── login/
│   │   │   │   │   ├── manage-customer/
│   │   │   │   │   ├── menu-bar/
│   │   │   │   │   ├── menu-item/
│   │   │   │   │   └── register/
│   │   │   │   ├── models/
│   │   │   │   ├── services/
│   │   │   │   │   ├── authentication/
│   │   │   │   │   ├── customer/
│   │   │   │   │   ├── guard/
│   │   │   │   │   └── interceptor/
│   │   │   │   ├── app.component.html
│   │   │   │   ├── app.component.scss
│   │   │   │   ├── app.component.spec.ts
│   │   │   │   ├── app.component.ts
│   │   │   │   ├── app.module.ts
│   │   │   │   └── app-routing.module.ts
│   │   │   ├── assets/
│   │   │   ├── environments/
│   │   │   ├── favicon.ico
│   │   │   ├── index.html
│   │   │   ├── main.ts
│   │   │   └── styles.scss
│   │   ├── .editorconfig
│   │   ├── angular.json
│   │   ├── package.json
│   │   ├── package-lock.json
│   │   ├── README.md
│   │   ├── tsconfig.app.json
│   │   ├── tsconfig.json
│   │   └── tsconfig.spec.json
│   └── react/
│       ├── node_modules/
│       ├── public/
│       ├── src/
│       ├── .dockerignore
│       ├── .env
│       ├── Dockerfile
│       ├── index.html
│       ├── package.json
│       ├── package-lock.json
│       └── vite.config.js
├── .gitignore
├── docker-compose.yml
├── Dockerrun.aws.json
└── README.md
```

## ⚙️ Setup Instructions

### 1. Clone the repository 
```bash
git clone https://github.com/<your-username>/aws-s3-image-service.git
cd aws-s3-image-service
```

### 2. Start PostgreSQL using Docker
```bash
docker start postgres
```
Database runs on:
```bash
localhost:5332
```

### 3. Configure Backend
Update application.yml if needed:
```bash
spring:
  datasource:
    url: jdbc:postgresql://localhost:5332/customer
    username: amigoscode
    password: password
```

### 4. Run Backend
```bash
cd backend
mvn spring-boot:run
```

Backend runs on:
http://localhost:8080

### 5. Run Frontend
```bash
cd frontend/react
npm install
npm run dev
```

Frontend runs on:
http://localhost:5173

## 🔐 Authentication & Security

- Implemented **JWT-based authentication** for secure access to APIs  
- Users can **register and login** to receive a JWT token  
- All protected endpoints require:
  ```http
  Authorization: Bearer <token>
  ```
  Integrated Spring Security filter chain with custom JWTAuthenticationFilter
Passwords are securely stored using hashing (BCrypt)

Unauthorized access returns:
```bash
{
  "message": "Full authentication is required"
}
```
## 🐳 Docker Setup
PostgreSQL containerized using Docker

Port mapping:
localhost:5332 → PostgreSQL (5432)

Start container:
```bash
docker start postgres
```

## 🗄️ Database & Migrations
PostgreSQL used as primary database
Managed using Flyway

Migration scripts located in:
backend/src/main/resources/db/migration

## ☁️ AWS S3 Integration
Upload and retrieve images from S3 bucket
Configurable via application.yml

Mock mode available for local testing:
```bash
aws:
  s3:
    mock: true
```

## API Usage Flow

1. Register a user
2. Login → Receive JWT token
3. Add token in headers
4. Access protected endpoints
5. Upload / retrieve images
