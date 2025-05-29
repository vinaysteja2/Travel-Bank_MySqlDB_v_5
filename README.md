# Travel-Bank_MySqlDB_v5.0

## Overview

**Travel-Bank_MySqlDB_v5.0** is a modular microservices-based banking application built using Spring Boot (v3.4.1) and Spring Cloud (2024.0.0). The system is designed to handle Accounts, Loans, and Cards functionalities independently through microservices. The backend services connect to their respective dedicated MySQL databases, and all services are orchestrated using Docker Compose.

---

## Architecture

The application is divided into the following major components:

- **Accounts Microservice** (`accounts-ms`)
- **Loans Microservice** (`loans-ms`)
- **Cards Microservice** (`cards-ms`)
- **Configuration Server** (`configserver-ms`)
- **MySQL Containers** for each service:
  - `accountsdb`
  - `loansdb`
  - `cardsdb`

Each service runs in its own container, and configuration is centrally managed by the `configserver`.

---

## Project Highlights

- **Spring Boot 3.4.1**
- **Java 21**
- **Spring Cloud 2024.0.0**
- **Spring Data JPA**
- **Spring Cloud Config**
- **MySQL as dedicated databases per service**
- **Docker-based orchestration**
- **Spring Actuator for health checks**
- **JIB Plugin for container image creation**

---

## Dockerized Services Setup

The system utilizes Docker Compose to manage the entire application stack. Below is an overview of the service setup:

### ✅ MySQL Database Containers

Each microservice uses a dedicated MySQL container:

- **accountsdb**
  - Port: `3306`
  - Database: `accountsdb`

- **loansdb**
  - Port: `3307`
  - Database: `loansdb`

- **cardsdb**
  - Port: `3308`
  - Database: `cardsdb`

Each DB is defined using a shared configuration from `common-config.yml`.

### ✅ Spring Boot Microservices

- **configserver-ms**
  - Loads configuration properties for all services.
  - Port: `8071`
  - Health endpoint: `/actuator/health/readiness`

- **accounts-ms**
  - Port: `8080`
  - Connects to `accountsdb`

- **loans-ms**
  - Port: `8090`
  - Connects to `loansdb`

- **cards-ms**
  - Port: `9000`
  - Connects to `cardsdb`

---

## How to Run

### Prerequisites

- Docker & Docker Compose installed
- Java 21 and Maven (for local development/testing)

### Steps

1. **Clone the Repository**

```bash
git clone https://github.com/<your-github-username>/Travel-Bank_MySqlDB_v5.0.git
cd Travel-Bank_MySqlDB_v5.0
```

2. **Build the Microservices (Optional)**

```bash
mvn clean install
```

3. **Start All Services via Docker Compose**

```bash
docker compose -f docker-compose.yml up --build
```

4. **Verify Running Containers**

```bash
docker ps
```

5. **Test Health Endpoints**

- Config Server: http://localhost:8071/actuator/health
- Accounts: http://localhost:8080/actuator/health
- Loans: http://localhost:8090/actuator/health
- Cards: http://localhost:9000/actuator/health

---

## Project Structure

```bash
.
├── docker-compose.yml
├── common-config.yml
├── accounts/            # Accounts Microservice
├── loans/               # Loans Microservice
├── cards/               # Cards Microservice
└── configserver/        # Central config server
```

---

## Maven Build & Containerization

All services use `spring-boot-maven-plugin` and `jib-maven-plugin` for container builds:

```xml
<plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>jib-maven-plugin</artifactId>
    <version>3.4.2</version>
    <configuration>
        <to>
            <image>vinaysteja0231/${project.artifactId}:v5.0</image>
        </to>
    </configuration>
</plugin>
```

---

## Technologies Used

- Java 21
- Spring Boot
- Spring Cloud Config
- Spring Data JPA
- MySQL
- Docker & Docker Compose
- JIB Plugin
- Springdoc OpenAPI

---

## Future Enhancements

- Add Eureka Service Registry
- Add API Gateway
- Enable centralized logging (ELK/EFK stack)
- Add security (Spring Security, OAuth2)

---

## Author

**Vinay Teja**

- Docker Hub: [vinaysteja0231](https://hub.docker.com/u/vinaysteja0231)

---

## License

This project is licensed under the MIT License - see the LICENSE file for details.
