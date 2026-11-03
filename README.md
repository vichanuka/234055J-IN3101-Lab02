# Library Management REST API

> [!IMPORTANT]
> **Academic Disclaimer**: This project is developed solely for educational purposes to fulfill the requirements of the lab sheet. It is intended for coursework demonstration and evaluation only.

A Spring Boot RESTful API for managing a library's book catalog, featuring CRUD operations, Jakarta Bean Validation, MySQL persistence with Spring Data JPA, environment variable configuration, and interactive OpenAPI (Swagger UI) documentation.

---

## 🛠️ Tech Stack

- **Java**: 21
- **Framework**: Spring Boot 4.1.2 (Spring MVC, Spring Data JPA, Spring Validation)
- **Database**: MySQL with Hibernate ORM
- **API Documentation**: Springdoc OpenAPI UI (Swagger 3)
- **Build Tool**: Apache Maven (Wrapper included)

---

## 📋 Features

- **Full CRUD Operations**: Create, read, update, and delete book entries.
- **Data Validation**: Enforces non-blank title and author, and non-negative book prices using Jakarta Bean Validation.
- **Environment-based Configuration**: Easily configure database credentials using a local `.env` file without exposing secrets in code.
- **Interactive Swagger Documentation**: Explore and test API endpoints directly from the browser.
- **Automatic Schema Migration**: Uses Hibernate `ddl-auto=update` to keep database schema synchronized.

---

## 📁 Project Structure

```text
library-api/
├── src/
│   ├── main/
│   │   ├── java/lk/ac/mrt/fit/library_api/
│   │   │   ├── controller/          # REST Controllers (BookController)
│   │   │   ├── model/               # JPA Entities (Book)
│   │   │   ├── repository/          # Spring Data JPA Repositories (BookRepository)
│   │   │   ├── service/             # Business Logic Layer (BookService)
│   │   │   └── LibraryApiApplication.java # Spring Boot Main Entry Point
│   │   └── resources/
│   │       ├── application.properties # Application Configuration
│   │       └── ...
│   └── test/                        # Unit and Integration Tests
├── .env                             # Local environment variables (DB credentials)
├── .gitignore
├── pom.xml                          # Maven build dependencies
└── README.md
```

---

## ⚙️ Prerequisites

Ensure you have the following installed on your machine:
- **JDK 21** or later
- **MySQL Server** (v8.0 or later)
- **Git** (optional, for version control)

---

## 🚀 Getting Started

### 1. Clone or Open the Repository

```bash
cd library-api
```

### 2. Configure the MySQL Database

1. Start your local MySQL service.
2. Open a MySQL terminal or GUI client (e.g., MySQL Workbench) and create the database:
   ```sql
   CREATE DATABASE library_db;
   ```

### 3. Setup Environment Variables (`.env`)

Copy `env.example` (or `.env.example`) to `.env` in the root directory and update it with your MySQL database credentials:

```bash
cp env.example .env
```

```properties
# Database Configuration
DB_URL=jdbc:mysql://localhost:3306/library_db
DB_USERNAME=root
DB_PASSWORD=your_mysql_password
```

> **Note**: The `.env` file is ignored by Git in `.gitignore` to keep credentials secure.

---

## 🏃 Running the Application

### Using the Maven Wrapper

- **Windows (Command Prompt / PowerShell)**:
  ```powershell
  .\mvnw.cmd spring-boot:run
  ```

- **Linux / macOS**:
  ```bash
  ./mvnw spring-boot:run
  ```

The server will start by default on port **`8080`**.

### Building and Running the JAR

To build a standalone executable JAR package:

```bash
# Build
.\mvnw.cmd clean package

# Run
java -jar target/library-api-0.0.1-SNAPSHOT.jar
```

---

## 📖 API Documentation (Swagger UI)

Once the application is running, access the interactive Swagger UI and OpenAPI specifications:

- **Swagger UI**: [http://localhost:8080/swagger-ui/index.html](http://localhost:8080/swagger-ui/index.html)
- **OpenAPI JSON Docs**: [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)

---

## 📡 API Endpoints

Base URL: `/api/books`

| Method | Endpoint | Description | Status Code |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/books` | Retrieve a list of all books | `200 OK` |
| `GET` | `/api/books/{id}` | Retrieve a specific book by ID | `200 OK` / `404 Not Found` |
| `POST` | `/api/books` | Add a new book | `201 Created` / `400 Bad Request` |
| `PUT` | `/api/books/{id}` | Update an existing book by ID | `200 OK` / `404 Not Found` |
| `DELETE` | `/api/books/{id}` | Delete a book by ID | `204 No Content` / `404 Not Found` |

---

## 📝 Request & Response Examples

### 1. Create a Book (`POST /api/books`)

**Request:**
```http
POST /api/books
Content-Type: application/json

{
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 32.99
}
```

**Response (`201 Created`):**
```json
{
  "id": 1,
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 32.99
}
```

### 2. Get All Books (`GET /api/books`)

**Response (`200 OK`):**
```json
[
  {
    "id": 1,
    "title": "Clean Code",
    "author": "Robert C. Martin",
    "isbn": "9780132350884",
    "price": 32.99
  }
]
```

### 3. Get Book by ID (`GET /api/books/1`)

**Response (`200 OK`):**
```json
{
  "id": 1,
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 32.99
}
```

### 4. Update a Book (`PUT /api/books/1`)

**Request:**
```http
PUT /api/books/1
Content-Type: application/json

{
  "title": "Clean Code - 2nd Edition",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 35.50
}
```

**Response (`200 OK`):**
```json
{
  "id": 1,
  "title": "Clean Code - 2nd Edition",
  "author": "Robert C. Martin",
  "isbn": "9780132350884",
  "price": 35.50
}
```

### 5. Delete a Book (`DELETE /api/books/1`)

**Response:**
```http
HTTP/1.1 204 No Content
```

---

## 🧪 Validation Rules

The `Book` model includes the following validation constraints:

| Field | Type | Validation Rule |
| :--- | :--- | :--- |
| `id` | Long | Auto-generated primary key |
| `title` | String | `@NotBlank` — Cannot be empty or null |
| `author` | String | `@NotBlank` — Cannot be empty or null |
| `isbn` | String | Optional ISBN identifier |
| `price` | Double | `@PositiveOrZero` — Must be 0 or greater |

---

## 📄 Disclaimer

This repository is created exclusively for university lab sheet submissions and educational coursework demonstration.

