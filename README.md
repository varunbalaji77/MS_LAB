# Complete Microservice Application

This document serves as a guide to understand and run the complete microservice application. Follow the steps carefully to set up and use the application effectively.

## How to Read This Document

1. Read the document thoroughly to understand the application workflow and architecture. Do not run the application or dive into the code initially.
2. Focus on understanding the workflow diagram.
3. You do not need knowledge of Java, Spring Boot, or Angular to comprehend the microservice concept.
4. Once you complete the document, proceed to set up the application on your local system by following the prerequisites and setup steps.
5. Observe the terminal logs when running the applications for better understanding.

---

## Overview of the Microservice Application

This application consists of five separate services:

1. **microservice-ui** (frontend)
2. **service-registry**
3. **api-gateway**
4. **product-service**
5. **offer-service**

### What is a Microservice?

A microservice is a modern architecture for designing software applications, consisting of independently deployable and scalable services. Key characteristics include:

- **Independently Deployable:** Each service can be deployed separately.
- **Independently Scalable:** Each service can scale based on its own requirements.

In this application:

- `product-service` and `offer-service` are the microservices.
- `service-registry` provides service discovery.
- `api-gateway` handles dynamic service routing and load balancing.

---

## Prerequisites for Windows

### Step 1: Clone the Project

1. Open a terminal and run the following command:
   ```
   git clone https://github.com/hnjaman/complete-microservice-application.git
   ```
2. Navigate to the newly created `complete-microservice-application` directory.

### Step 2: Install Java and Maven

1. Install **Java 8** or higher (Java 11 is recommended).
2. Install **Apache Maven 3.6.0** or higher.
3. Verify installation by running:
   ```
   java -version
   mvn -version
   ```

### Step 3: Install RabbitMQ

1. Download RabbitMQ from the [official website](https://www.rabbitmq.com/install-windows.html).
2. Follow the installation steps and ensure RabbitMQ is running.
3. By default, it runs at `http://localhost:15672/` with the credentials:
   - Username: `guest`
   - Password: `guest`

### Step 4: Install Lombok Plugin

1. Install the Lombok plugin in your IDE (e.g., IntelliJ IDEA or Eclipse).
2. Enable annotation processing in your IDE settings.

### Step 5: Install Node.js and Angular CLI

1. Install **Node.js 12** or higher.
2. Install Angular CLI using the command:
   ```
   npm install -g @angular/cli@8.3.25
   ```
3. Verify the installation:
   ```
   node -v
   ng version
   ```

---

## Running the Application

### 1. Run `microservice-ui` (Frontend)

1. Open a terminal and navigate to the `microservice-ui` directory.
   ```
   cd microservice-ui
   ```
2. Install dependencies and start the application:
   ```
   npm install
   ng s --port 3000 --open
   ```
3. The frontend will launch at `http://localhost:3000/store`.

### 2. Run `service-registry`

1. Open a terminal and navigate to the `service-registry` directory.
   ```
   cd service-registry
   ```
2. Build and run the application:
   ```
   mvn clean install
   mvn spring-boot:run
   ```
3. The service registry will be available at `http://localhost:8761/`.

### 3. Run `api-gateway`

1. Open a terminal and navigate to the `api-gateway` directory.
   ```
   cd api-gateway
   ```
2. Build and run the application:
   ```
   mvn clean install
   mvn spring-boot:run
   ```
4. The API Gateway will run at `http://localhost:8000/`.

### 4. Run `product-service`

1. Open a terminal and navigate to the `product-service` directory.
   ```
   cd product-service
   ```
2. Build the application:
   ```
   mvn clean install
   ```
3. Launch two instances of the service:
   ```
   java -jar target/product-service-0.0.1-SNAPSHOT.jar --server.port=8081
   java -jar target/product-service-0.0.1-SNAPSHOT.jar --server.port=8180
   ```

### 5. Run `offer-service`

1. Open a terminal and navigate to the `offer-service` directory.
   ```
   cd offer-service
   ```
2. Build and run the application:
   ```
   mvn clean install
   mvn spring-boot:run
   ```
3. The application will run at `http://localhost:8082/`.

---

## Key Features and Concepts

1. **Service Registry:**
   - Centralized service discovery using Eureka.
   - All services register dynamically with `service-registry`.

2. **API Gateway:**
   - Entry point for backend services.
   - Handles routing and load balancing using Zuul.

3. **Event-Driven Development (EDD):**
   - RabbitMQ is used for service-to-service communication.
   - `offer-service` sends events to `product-service` to update product details.

4. **Database Configuration:**
   - `product-service` and `offer-service` use separate databases.
   - Access the H2 database console:
     - `product-service`: `http://localhost:8081/h2`
     - `offer-service`: `http://localhost:8082/h2`
     - Credentials:
       - JDBC URL: `jdbc:h2:~/[product|offer]`
       - Username: `root`
       - Password: `root`

---

## Conclusion

This is a complete microservice application. You can extend it by adding new services integrated with the `service-registry` and `api-gateway`. Explore tools like Hystrix, Zipkin, and Feign for additional features.

## Watch the Video

To learn more about our project, you can watch the video below:

[Watch the video](videos/video.mp4)

