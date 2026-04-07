# Task Management Platform

A Spring Boot based task management backend project with user authentication, JWT authorization, project management, and backlog task operations. This repository is prepared as a portfolio-ready backend showcase.

## Highlights

- End-to-end backend implementation with `Spring Boot + Spring Security + JWT + JPA`
- Core CRUD APIs for Project and Backlog Task management
- Unified request validation using `@Valid + BindingResult`
- User-scoped data access via `Principal` in protected endpoints
- MySQL persistence with JPA/Hibernate entity mapping

## Tech Stack

- Java 8
- Spring Boot 2.7.14
- Spring Web
- Spring Data JPA
- Spring Security
- JWT (`jjwt`)
- MySQL
- Maven

## Project Structure

```text
.
├─ tmptool
│  ├─ pom.xml
│  └─ src/main
│     ├─ java/io/gwteaching/tmptool
│     │  ├─ controller
│     │  ├─ services
│     │  ├─ repositories
│     │  ├─ security
│     │  └─ dto/payload
│     └─ resources
│        └─ application.properties
├─ Readme.md                # Existing request-flow notes
└─ scscreenshots/           # Screenshots for portfolio display
```

## Core Features

### 1) User Authentication

- `POST /api/users/register`: Register a new user
- `POST /api/users/login`: Login and receive JWT
- Protected API header format: `Authorization: TMP <token>`

### 2) Project Management

- `POST /api/project`: Create project
- `GET /api/project/{projectId}`: Get project by ID
- `GET /api/project/all`: Get all projects for current user
- `PUT /api/project`: Update project
- `DELETE /api/project/{projectId}`: Delete project

### 3) Backlog Task Management

- `POST /api/backlog/{projectId}`: Add task to backlog
- `GET /api/backlog/{projectId}`: List tasks by project
- `GET /api/backlog/{projectId}/{projectSequence}`: Get one task
- `PUT /api/backlog/{projectId}/{projectSequence}`: Update task

## Quick Start

### 1. Requirements

- JDK 8
- Maven 3.6+
- MySQL 5.7+ or 8.x

### 2. Configure Database

Update `tmptool/src/main/resources/application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/tmptool
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

Create database first:

```sql
CREATE DATABASE tmptool;
```

### 3. Run Application

From `tmptool` directory:

```bash
mvn spring-boot:run
```

Server default URL: `http://localhost:8080`

## API Examples

### Register

```http
POST /api/users/register
Content-Type: application/json

{
  "username": "demo",
  "fullName": "Demo User",
  "password": "123456",
  "confirmPassword": "123456"
}
```

### Login

```http
POST /api/users/login
Content-Type: application/json

{
  "username": "demo",
  "password": "123456"
}
```

Use returned token in protected requests:

```http
Authorization: TMP <token>
```

## Request Flow (Controller -> MySQL)

`Client -> Security Filter -> Controller -> Validation -> Service -> Repository -> JPA/Hibernate -> MySQL -> Response`

For detailed flow notes, see `Readme.md`.

## Engineering Practices Demonstrated

- Layered REST API design
- JWT-based authentication and authorization
- Validation and consistent error mapping
- User-context driven access control
- Maven-based dependency and build management

## Current Limitations & Improvements

- JWT expiration in code is currently short (`60s`) for demo usage
- Add Swagger/OpenAPI for better API discoverability
- Add unit/integration tests for stronger reliability
- Add GitHub Actions CI for automatic build and test checks

## Portfolio Checklist

- Put API/Postman screenshots into `scscreenshots/`
- Add `LICENSE` (recommended: MIT)
- Add `CHANGELOG.md` for iteration history
- Add your personal contribution and design decisions in this README

## License

No explicit open-source license is set yet. For public portfolio usage, adding an `MIT License` is recommended.

