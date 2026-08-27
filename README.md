# Digital Content Platform API

Spring Boot REST API for managing digital content, users, and purchases. The project was developed as part of an OOP course and uses PostgreSQL for data persistence.

## Features

- RESTful API for digital content, users, and purchases
- PostgreSQL database with JDBC
- Layered architecture: Controller → Service → Repository
- OOP principles: inheritance, polymorphism, encapsulation, and abstraction
- SOLID principles
- Design patterns: Singleton, Factory, Builder
- Generics, lambdas, reflection, and interface default/static methods
- DTOs and custom exception handling
- Global exception handler

## Architecture

```
Controller
    ↓
Service
    ↓
Repository
    ↓
PostgreSQL
```

## Design Patterns

### Singleton

Used for shared application resources:

- `DatabaseConfig`
- `LoggerService`

### Factory

`DigitalContentFactory` creates different types of digital content such as `Game`, `Movie`, and `MusicAlbum`.

### Builder

`PurchaseBuilder` provides a fluent API for constructing `Purchase` objects.

## SOLID Principles

- **SRP:** Controllers, services, and repositories have separate responsibilities.
- **OCP:** `DigitalContent` can be extended with new content types.
- **LSP:** `Game`, `Movie`, and `MusicAlbum` can be used through the `DigitalContent` abstraction.
- **ISP:** Interfaces such as `Validatable`, `PricedItem`, and `CrudRepository` have focused responsibilities.
- **DIP:** Services depend on abstractions and use dependency injection.

## API Endpoints

### Digital Content

Method| Endpoint| Description
GET| "/api/content"| Get all content
GET| "/api/content/{id}"| Get content by ID
POST| "/api/content"| Create content
PUT| "/api/content/{id}"| Update content
DELETE| "/api/content/{id}"| Delete content
GET| "/api/content/search?keyword="| Search content
GET| "/api/content/available"| Get available content

### Users

Method| Endpoint| Description
GET| "/api/users"| Get all users
GET| "/api/users/{id}"| Get user by ID
POST| "/api/users"| Create user
PUT| "/api/users/{id}"| Update user
DELETE| "/api/users/{id}"| Delete user

### Purchases

Method| Endpoint| Description
GET| "/api/purchases"| Get all purchases
GET| "/api/purchases/{id}"| Get purchase by ID
GET| "/api/purchases/user/{userId}"| Get user's purchases
POST| "/api/purchases"| Create purchase
DELETE| "/api/purchases/{id}"| Delete purchase

## Database

The application uses PostgreSQL with three main tables:

- `users`
- `digital_content`
- `purchases`

`digital_content` supports multiple content types through inheritance and a `content_type` field.

## Example Request

```
POST /api/content
Content-Type: application/json
```

```
{
  "name": "Inception",
  "releaseYear": 2010,
  "available": true,
  "contentType": "MOVIE",
  "description": "Mind-bending thriller",
  "creatorCountry": "USA",
  "creatorBio": "Christopher Nolan",
  "rentable": true,
  "durationMinutes": 148
}
```

## Project Structure

```
src/main/java/kz/aitu/digitalcontent/
├── controller/       # REST controllers
├── service/          # Business logic
├── repository/       # Data access
├── model/            # Domain entities
├── dto/              # Data transfer objects
├── exception/        # Custom exceptions and handlers
├── patterns/         # Design patterns
├── utils/            # Utility classes
├── Application.java
└── OOPFeaturesDemo.java

src/main/resources/
└── application.properties

pom.xml
README.md
```

## Requirements

- Java 17+
- Maven 3.6+
- PostgreSQL 12+

## Running the Project

1. Create a PostgreSQL database:

```
CREATE DATABASE digitalcontent;
```

2. Configure the database credentials in `DatabaseConfig.java` or the application configuration.

3. Build the project:

```
mvn clean install
```

4. Run the application:

```
mvn spring-boot:run
```

The API will be available at:

```
http://localhost:8080
```

## Testing

The API can be tested using Postman. The project includes screenshots demonstrating API requests, CRUD operations, and the database structure (see docs/screenshots).