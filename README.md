# Platform: API Gateway

### Student Information
- **Student Name**: Dilsara Thiranjaya
- **Student Number**: 2301692050
- **Slack Handle**: Dilsara Thiranjaya
- **GCP Project ID**: dilsara

---


This repository contains the Spring Cloud API Gateway for the Library Management System.

## Architectural Purpose

In a microservices architecture, exposing individual services directly to clients creates tight coupling and security risks. The **API Gateway** acts as a single point of entry ("Front Door") for all external traffic destined for the backend microservices.

It routes incoming requests, handles cross-cutting concerns (like CORS, security, rate limiting), and abstracts the backend complexity from the clients.

## Technical Stack

- **Java**: 25
- **Spring Boot**: 4.0.3
- **Spring Cloud**: 2025.1.0
- **Build Tool**: Maven

### Key Capabilities

1.  **Dynamic Routing**: It intercepts requests and routes them to the correct backend service based on the URL path.
2.  **Service Discovery Integration**: It uses the Eureka Discovery Client so it doesn't need hardcoded IPs; it finds services by their logical name (e.g., `lb://book-service`).
3.  **Cross-Origin Resource Sharing (CORS)**: It is globally configured to accept requests from all origins (`*`), preventing CORS errors when frontends attempt to consume the API.
4.  **Centralized Configuration**: It pulls its core configuration properties from the centralized Config Server at `http://config.platform:9000`.

## Routing Configuration

By default, the Gateway runs on **Port 8080** and routes traffic as follows:

-   Requests to `/api/books/**` $\rightarrow$ Forwarded to the `book-service`
-   Requests to `/api/members/**` $\rightarrow$ Forwarded to the `member-service`
-   Requests to `/api/files/**` $\rightarrow$ Forwarded to the `file-service`

## Running the Application

Before starting the API Gateway, ensure that both the Config Server and the Eureka Service Registry are up and running, as the Gateway depends on them during its initialization sequence.

```bash
mvn spring-boot:run
```