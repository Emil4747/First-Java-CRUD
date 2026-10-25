# First-Java-CRUD

A beginner Spring Boot project for building a REST CRUD (Create, Read, Update, Delete) API backed by an in-memory H2 database.

> **Status:** early scaffold. The application starts and the context test passes, but no entities, repositories, or controllers have been added yet.

## Tech stack

| Component        | Version / Notes                         |
| ---------------- | --------------------------------------- |
| Java             | 25                                      |
| Spring Boot      | 4.1.2                                   |
| Build tool       | Maven (wrapper included: `mvnw`)        |
| Web              | Spring Web MVC                          |
| Persistence      | Spring Data JPA (Hibernate)             |
| Database         | H2 (in-memory) + H2 web console         |
| Testing          | JUnit 5, Spring Boot test starters      |

## Prerequisites

- JDK 25 installed and on your `PATH` (`java -version` to check)
- No Maven install needed — use the bundled wrapper

## Getting started

```bash
# Clone
git clone https://github.com/Emil73549/First-Java-CRUD.git
cd First-Java-CRUD

# Run the app (starts on http://localhost:8080)
./mvnw spring-boot:run

# Run tests
./mvnw test

# Build a runnable jar
./mvnw clean package
java -jar target/firstjavacrud-0.0.1-SNAPSHOT.jar
```

On Windows, use `mvnw.cmd` instead of `./mvnw`.

## H2 database console

The H2 console is on the classpath but is disabled by default. To use it, add to `src/main/resources/application.properties`:

```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=
```

Then open <http://localhost:8080/h2-console> and connect with JDBC URL `jdbc:h2:mem:testdb`, user `sa`, empty password.

Data lives in memory and is lost when the app stops.

## Project structure

```
.
├── pom.xml                         # Maven build & dependencies
├── mvnw, mvnw.cmd, .mvn/           # Maven wrapper
└── src
    ├── main
    │   ├── java/firstjavacrud
    │   │   └── FirstjavacrudApplication.java   # Spring Boot entry point
    │   └── resources
    │       └── application.properties          # App configuration
    └── test
        └── java/firstjavacrud
            └── FirstjavacrudApplicationTests.java  # Context-load test
```

## Next steps

A typical CRUD feature for this project looks like:

1. **Entity** — a `@Entity` class (e.g. `Product` with `id`, `name`, `price`)
2. **Repository** — `interface ProductRepository extends JpaRepository<Product, Long>`
3. **Controller** — a `@RestController` exposing:

   | Method | Path             | Action          |
   | ------ | ---------------- | --------------- |
   | GET    | `/products`      | List all        |
   | GET    | `/products/{id}` | Get one         |
   | POST   | `/products`      | Create          |
   | PUT    | `/products/{id}` | Update          |
   | DELETE | `/products/{id}` | Delete          |
