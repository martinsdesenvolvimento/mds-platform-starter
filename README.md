# MDS Platform Starter

![Java](https://img.shields.io/badge/Java-21-orange)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-4.0.6-brightgreen)
![Starter](https://img.shields.io/badge/Spring-Starter-success)
![Maven](https://img.shields.io/badge/Maven-3.9-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/MDS-Ecosystem-blueviolet)

Spring Boot starter that aggregates all MDS Platform libraries into a single dependency, enabling applications to adopt enterprise architecture standards instantly.

---

## Overview

This starter centralizes the entire MDS ecosystem. Instead of declaring each library individually, applications add **one dependency** and get all reusable modules — error handling, security, caching, CRUD, crypto, tokens, retry, data access, and communication patterns — auto-configured and ready to use.

It replaces the previous `shared-core-lib` parent POM approach with a proper Spring Boot Starter that delivers transitive dependencies and auto-configuration out of the box.

---

## Included Modules

| Module | Description |
|--------|-------------|
| `shared-core-lib` | Foundational utilities, structural patterns, and shared helpers |
| `spring-error-pattern` | Standardized error handling and exception hierarchy |
| `spring-retry-pattern` | Retry and resilience patterns (Resilience4j) |
| `spring-crypto-pattern` | Encryption, hashing, and JWT utilities |
| `spring-token-pattern` | SSO token authentication and management |
| `spring-security-pattern` | Security filters, CORS, and URL parameter validation |
| `spring-data-pattern` | Data access abstractions |
| `spring-liquibase-pattern` | Versioned database migrations with Liquibase |
| `spring-cache-pattern` | Multi-level caching (Caffeine + Redis) |
| `spring-crud-pattern` | Base CRUD controllers, services, and entities |

> **Note:** `spring-comm-pattern` (Feign HTTP client abstractions) is **not included** in the starter by default — add it explicitly if your application requires inter-service communication via Feign.

All modules are delivered as transitive dependencies — no need to declare them individually.

---

## Technical Stack

- Java 21
- Spring Boot 4.0.6
- Maven
- Spring Auto Configuration (`@AutoConfiguration`)
- Modular Architecture

---

## Installation

Add the starter to your `pom.xml`:

```xml
<dependency>
   <groupId>com.mds.platform</groupId>
   <artifactId>mds-platform-starter</artifactId>
   <version>1.0.0-SNAPSHOT</version>
</dependency>
```

That's it. All 10 included MDS modules are now available in your application.

---

## Auto Configuration

The starter registers `MdsPlatformAutoConfiguration`, which:

1. Scans `com.mds.*` packages for Spring components from all modules.
2. Logs a confirmation message at startup.
3. Can be disabled via property:

```yaml
mds:
  platform:
    enabled: false
```

Individual modules retain their own `@ConditionalOnProperty` kill-switches (e.g., `authentication.enabled` for spring-token-pattern, `cache.enabled` for spring-cache-pattern).

---

## Architecture

```
Application
      │
      ▼
MDS Platform Starter (this project)
      │
      ├── shared-core-lib
      ├── spring-error-pattern
      ├── spring-retry-pattern
      ├── spring-crypto-pattern
      ├── spring-token-pattern
      ├── spring-security-pattern
      ├── spring-data-pattern
      ├── spring-cache-pattern
      └── spring-crud-pattern

      (optional, add explicitly)
      └── spring-comm-pattern
```

---

## Project Structure

```
mds-platform-starter/
├── src/
│   └── main/
│       ├── java/
│       │   └── br/com/mds/platform/starter/
│       │       └── MdsPlatformAutoConfiguration.java
│       └── resources/
│           └── META-INF/
│               └── spring/
│                   └── org.springframework.boot.autoconfigure.AutoConfiguration.imports
├── pom.xml
├── .gitignore
└── README.md
```

---

## Properties

| Property | Default | Description |
|----------|---------|-------------|
| `mds.platform.enabled` | `true` | Master kill-switch for the entire starter |

---

## Migration from shared-core-lib

If your project previously used `shared-core-lib` as a parent POM:

1. Remove the `<parent>` reference to `shared-core-lib`.
2. Add `mds-platform-starter` as a regular dependency (see Installation above).
3. All `dependencyManagement` entries are now resolved transitively — no manual version pinning needed.

---

## Future Roadmap

- Selective module activation via properties
- Metrics integration
- Feature toggles per module
- Health indicator aggregation
- AI-assisted configuration

---

Built with ❤️ by Martins Desenvolvimento de Sistemas
