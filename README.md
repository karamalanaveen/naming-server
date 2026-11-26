# Naming Server (Netflix Eureka Discovery Server)

Centralized service registration and discovery server built with **Java 17**, **Spring Boot 3**, and **Spring Cloud Netflix Eureka Server**.

---

## 📌 Features

1. **Spring Cloud Eureka Server**:
   - Centralized registry where microservices (`product-service`, `coupon-service`, `employee-service`, etc.) register their network locations dynamically.
2. **Standalone Configuration**:
   - Configured with `eureka.client.register-with-eureka=false` and `eureka.client.fetch-registry=false` so the server does not register with itself.
3. **Web Dashboard**:
   - Built-in web console to inspect registered instances, instance statuses (UP/DOWN), lease information, and system health.
4. **Clean Logging**:
   - Standardized console log formatting with relevant log levels configured for Netflix Eureka components.

---

## 🏗️ Architecture & Package Layout

```
src/main/java/com/example/namingserver/
└── NamingServerApplication.java
src/main/resources/
└── application.properties
```

---

## ⚙️ Configuration Properties

| Property | Description | Default Value |
|----------|-------------|---------------|
| `spring.application.name` | Application name in Eureka registry | `naming-server` |
| `server.port` | HTTP port for Eureka server | `8761` (configurable via `SERVER_PORT`) |
| `eureka.client.register-with-eureka` | Whether to register as an Eureka client | `false` |
| `eureka.client.fetch-registry` | Whether to fetch registry entries | `false` |
| `eureka.instance.hostname` | Hostname of the Eureka instance | `localhost` |

---

## 🚀 Building & Running

```bash
# Navigate to naming-server directory
cd naming-server

# Build the project
mvn clean install

# Run the Eureka Discovery Server
mvn spring-boot:run
```

Once started, open your browser and navigate to:
👉 **[http://localhost:8761](http://localhost:8761)** to access the **Eureka Service Registry Dashboard**.

---

## 🔗 How Other Microservices Register With This Server

To register client microservices (e.g. `product-service` or `coupon-service`) with this Eureka server:

1. Add the Eureka Client dependency in the client's `pom.xml`:
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

2. Add the following to the client's `application.properties`:
```properties
spring.application.name=product-service
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
```
