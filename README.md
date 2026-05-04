# Patient Management System

A comprehensive, microservices-based Patient Management system built with modern Java, Spring Boot, and AWS infrastructure (via LocalStack). 

## Architecture & Microservices

This repository is structured as a collection of independent microservices and supporting modules:

*   **`api-gateway`**: Central entry point for the system. Built using Spring Cloud Gateway to route HTTP requests to the appropriate backend microservices.
*   **`auth-service`**: Authentication and Authorization service utilizing Spring Security and JWT. Manages user identities and protects downstream services.
*   **`patient-service`**: Core domain service responsible for managing patient records. Uses Spring Data JPA and connects to a PostgreSQL database.
*   **`infrastructure`**: Infrastructure-as-Code (IaC) module utilizing AWS CDK to provision cloud resources. Includes scripts to deploy to **LocalStack** for local development and testing.
*   **`integration-tests`**: Contains end-to-end integration tests to verify the interactions between the gateway, auth, and patient services.
*   **`api-requests`**: A collection of HTTP request files (likely for IntelliJ HTTP Client) for easily testing `auth-service` and `patient-service` endpoints during development.
*   **`grpc-requests`**: Contains gRPC request definitions/payloads (e.g., for `billing-service` integrations).

## Tech Stack

*   **Java**: Java 17 & Java 21 (varies per service)
*   **Framework**: Spring Boot 3.x, Spring Cloud Gateway
*   **Security**: Spring Security, JWT (jjwt)
*   **Database**: PostgreSQL (Production/Runtime) & H2 (Testing)
*   **Infrastructure**: AWS CDK, AWS CloudFormation, LocalStack
*   **Build Tool**: Maven

## Prerequisites

*   **Java Development Kit (JDK)**: JDK 17+ (Java 21 recommended for newer services like `auth-service` and `api-gateway`).
*   **Maven**: For building the individual projects.
*   **Docker & LocalStack**: For running local infrastructure (databases and AWS mock services).
*   **AWS CLI**: Required for interacting with LocalStack via the provided deployment scripts.

## Getting Started

1.  **Start Infrastructure (LocalStack & DBs)**
    Ensure your local Docker daemon is running, and spin up LocalStack. You can deploy the AWS resources using the provided bash script:
    ```bash
    cd infrastructure
    ./localstack-deploy.sh
    ```

2.  **Build the Services**
    Navigate to each service directory and build using Maven wrapper (or your local Maven installation):
    ```bash
    cd patient-service
    ./mvnw clean install -DskipTests
    ```
    *(Repeat for `auth-service` and `api-gateway`)*

3.  **Run the Applications**
    Start the services in the following recommended order:
    1. `auth-service`
    2. `patient-service`
    3. `api-gateway`

    You can run them via your IDE or using the Spring Boot Maven plugin:
    ```bash
    ./mvnw spring-boot:run
    ```

## Testing

### API Testing
You can utilize the HTTP request collections found in the `api-requests/` folder. If you are using IntelliJ IDEA, you can run these directly from the IDE to simulate client interactions for both `auth-service` and `patient-service`.

### Integration Tests
Run the system-wide integration tests to ensure all services are communicating correctly:
```bash
cd integration-tests
mvn test
```

## License

*(Add appropriate license information here)*