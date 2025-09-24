# Employee CRUD Application with CI/CD

This project is a Spring Boot application that provides a CRUD (Create, Read, Update, Delete) interface for managing employees. It uses Thymeleaf for the frontend, H2 as the in-memory database, and Docker for containerization.

---

## Features

- **CRUD Operations**: Manage employees with create, read, update, and delete functionality.
- **H2 Database**: In-memory database for development and testing.
- **Pagination and Sorting**: View employees with pagination and sorting options.
- **Dockerized**: Easily build and run the application using Docker.
- **CI/CD Ready**: Structured for continuous integration and deployment.

---

## Prerequisites

Ensure you have the following installed:
- Java 21 or higher
- Maven
- Docker
- Git

---

## H2 Database Configuration

The application uses an in-memory H2 database. The configuration is defined in `application.properties`:

```properties
# H2 Database Configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=user
spring.datasource.password=root

# H2 Console Configuration
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

### Accessing the H2 Console

1. Start the application.
2. Navigate to `http://localhost:8086/h2-console`.
3. Use the following credentials:
   - **JDBC URL**: `jdbc:h2:mem:testdb`
   - **Username**: `user`
   - **Password**: `root`

---

## Sample SQL Commands

Here are some SQL commands to interact with the `employees` table:

### Create the `employees` Table
```sql
CREATE TABLE employees (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100)
);
```

### Insert Sample Data
```sql
INSERT INTO employees (first_name, last_name, email) VALUES ('John', 'Doe', 'john.doe@example.com');
INSERT INTO employees (first_name, last_name, email) VALUES ('Jane', 'Smith', 'jane.smith@example.com');
```

### Query All Employees
```sql
SELECT * FROM employees;
```

### Update an Employee
```sql
UPDATE employees SET email = 'updated.email@example.com' WHERE id = 1;
```

### Delete an Employee
```sql
DELETE FROM employees WHERE id = 1;
```

---

## Build and Run Instructions

### Using Docker

1. **Delete the existing Docker image (if it exists):**
   ```bash
   docker rmi -f crud_app:latest
   ```

2. **Rebuild the Docker image:**
   ```bash
   docker-compose build
   ```

3. **Run the Docker container:**
   ```bash
   docker-compose up
   ```

### Without Docker

1. **Build the application:**
   ```bash
   mvn clean package
   ```

2. **Run the application:**
   ```bash
   java -jar target/springboot-thymeleaf-crud-web-app-0.0.1-SNAPSHOT.jar
   ```

---

## Git Commands

### Initialize a New Repository
```bash
git init
git add .
git commit -m "Initial commit"
```

### Clone an Existing Repository
```bash
git clone https://github.com/NAMPALLY-PRANAY/employee_crud_cicd.git
```

### Push to a Remote Repository
```bash
git remote add origin https://github.com/NAMPALLY-PRANAY/employee_crud_cicd.git
git branch -M main
git push -u origin main
```

---

## CI/CD Pipeline

### Suggested CI/CD Workflow

1. **Build Stage**:
   - Use Maven to build the project and run tests.
   - Example:
     ```bash
     mvn clean package
     ```

2. **Dockerization**:
   - Build a Docker image for the application.
   - Example:
     ```bash
     docker build -t crud_app:latest .
     ```

3. **Deployment**:
   - Deploy the Docker container to a staging or production environment.
   - Example:
     ```bash
     docker-compose up -d
     ```

4. **Testing**:
   - Run integration tests to ensure the application works as expected.

---

## Project Structure

```
crud/
├── Dockerfile
├── mvnw
├── mvnw.cmd
├── pom.xml
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── net/
│   │   │       └── javaguides/
│   │   └── resources/
│   │       ├── application.properties
│   │       └── templates/
│   │           ├── index.html
│   │           ├── new_employee.html
│   │           └── update_employee.html
│   └── test/
│       └── java/
│           └── net/
│               └── javaguides/
└── target/
    └── employeedb.war
```

---

## Author

This project is developed by **npran**.