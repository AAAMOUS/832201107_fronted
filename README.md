# Code Style Guide

> Reference: [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

## 1. File Organization

- **File Naming**: Each Java file should contain only one public class or interface, and the file name should match the name of the public class/interface.
- **Class Declaration Order**:
  - Public constants
  - Instance variables
  - Constructors
  - Public methods
  - Private methods

## 2. Naming Conventions

- **Class Names**: Use PascalCase, e.g., `ContactsController`.
- **Variable Names**: Use camelCase, e.g., `contactsService`.
- **Constant Names**: Use all uppercase letters with underscores between words, e.g., `MAX_SIZE`.

## 3. Code Formatting

- **Indentation**: Use 4 spaces for indentation, do not use tabs.
- **Line Length**: Each line of code should not exceed 100 characters; line breaks can be used when necessary.
- **Spacing**: Leave spaces around operators, e.g., `a + b`.
- **Braces Style**: Opening braces `{` should be on the same line as the statement, and used with control statements such as `if`, `for`, etc.

## 4. Comments

- **Class Comments**: Each class should have a comment above its declaration describing its purpose and functionality.
- **Method Comments**: Each method should have a comment briefly describing its purpose, parameters, and return values.
- **Comment Style**: Use Javadoc comment style, as shown below:
  ```java
  /**
   * Handles GET requests to search for a list of contacts.
   *
   * @return A Result object containing the list of contacts.
   */
  public Result getContacts() {
      // Method implementation
  }
## 5. PSP Table (Personal Software Process)

The following PSP table is used to record estimated and actual time spent on each module, helping analyze and optimize the development process.

| PSP Phase                | Task                             | Estimated Time (min) | Actual Time (min) | Notes                                              |
|--------------------------|----------------------------------|----------------------|-------------------|----------------------------------------------------|
| **Planning**             | Requirements Analysis           | 30                   | 25                | Analyze project requirements and define features    |
|                          | Time Estimation                 | 10                   | 12                | Estimate time for each module                      |
| **Development**          | Design                          | 20                   | 18                | Design database structure and code architecture     |
|                          | Database Script                 | 15                   | 20                | Create SQL script for database and table structure  |
|                          | Code Implementation - Controller | 40                  | 45                | Implement ContactsController                       |
|                          | Code Implementation - Service Layer | 30              | 28                | Implement ContactsService business logic           |
|                          | Code Implementation - Data Access Layer | 25         | 30                | Implement data access layer for database operations |
|                          | Frontend Page                   | 45                   | 50                | Implement frontend with HTML, CSS, and JavaScript   |
| **Testing**              | Testing                         | 30                   | 35                | Test the functionality and API connectivity         |
| **Debugging**            | Debugging                       | 20                   | 25                | Fix issues identified during testing               |
| **Deployment & Maintenance** | Deployment               | 15                   | 12                | Deploy to test or production environment           |
|                          | Documentation                   | 20                   | 18                | Write code documentation and user manual           |
|                          | Code Review & Optimization      | 20                   | 22                | Code optimization and standardization              |
| **Total**                |                                  | **315**              | **320**           |                                                    |

# Design and Implementation Process

## Project Objective
The objective of this project is to create a Contact Management System that provides CRUD (Create, Read, Update, Delete) functionality for contacts via a RESTful API. This system uses a layered architecture, with separate Controller, Service, and Mapper layers to ensure modularity, readability, and maintainability of the code.

## Architecture Design
The project uses Spring Boot and MyBatis as its technology stack. The layered structure is as follows:

- **Controller Layer**: Handles HTTP requests and responses, and calls the Service layer to implement business logic.
- **Service Layer**: Encapsulates business logic and calls the Mapper layer for data persistence.
- **Mapper Layer**: Interacts with the database using MyBatis, executing database operations.

The project structure, as shown in the provided directory, includes the following folders and classes:

- **controller**: Contains `ContactsController`, which handles requests related to contacts.
- **service** and **service.impl**: Contains the `ContactsService` interface and `ContactsServiceImpl` implementation class, which define and implement the business logic for contacts.
- **mapper**: Contains the `ContactsMapper` interface and its `ContactsMapper.xml` configuration file, where SQL is mapped using MyBatis.
- **pojo**: Contains two entity classes, `Contacts` and `Result`, which represent the structure of contact data and response data, respectively.
- **resources**: Contains MyBatis XML configuration files and the `application.yml` configuration file for database connection settings.

## Functional Structure Diagram

<img height="400" src="D:\code\ContactsGroup\Functional Structure Diagram.png" width="800"/>

```
# Installation Guide

## Prerequisites
- **Java**: Ensure Java JDK 8 or above is installed.
- **Maven**: This project uses Maven for dependency management and building the project.
- **MySQL**: The project requires a MySQL database. Make sure MySQL is installed and running.

## Installation Steps
```

1. **Clone the Repository**
   Open the ContactsGroup project in Idea

2. **Database Setup**

   - Create a new MySQL database named `contacts_group`.

   - Import the initial SQL file:

   ```
     source contacts_group.sql;
    ```
     
   - Update the database configurations in the `application.yml` file under `src/main/resources` (see Configuration section below).

3. **Install Dependencies** Use Maven to install project dependencies:

   ```
   mvn clean install
   ```

4. **Run the Application** Start the Spring Boot application:

   ```
   mvn spring-boot:run
   ```

   Alternatively, you can build a JAR file and run it:

   ```
   bashCopy codemvn package
   java -jar target/ContactsGroup-0.0.1-SNAPSHOT.jar
   ```

------

# Usage Instructions

Once the application is running, you can access the API endpoints to manage contacts. Below are some sample commands and usage instructions.

### API Endpoints

- **Get All Contacts**

  ```
  curl -X GET http://localhost:8080/contacts/search
  ```
  
- **Add a Contact**

  ```
  curl -X POST -d "name=John&phone=123456789&age=30" http://localhost:8080/contacts/add
  ```
  
- **Update a Contact**

  ```
  curl -X PUT -d "id=1&name=John Doe&phone=987654321&age=31" http://localhost:8080/contacts/edit
  ```
  
- **Delete a Contact**

  ```
  curl -X DELETE http://localhost:8080/contacts/delete/1
  ```

------

# Configuration

To configure the project for different environments, modify the `application.yml` or use separate configuration files such as `application-dev.yml`, `application-prod.yml`, etc., and specify the active profile.

### Configuration File (application.yml)

The `application.yml` file is located in `src/main/resources` and includes the following configurations:

```
yamlCopy codespring:
  datasource:
    url: jdbc:mysql://localhost:3306/contacts_group?useSSL=false&characterEncoding=UTF-8
    username: root
    password: yourpassword
  mybatis:
    mapper-locations: classpath:mapper/*.xml
server:
  port: 8080
```

Update the `username`, `password`, and `url` as per your MySQL setup.

#### Development Environment

To set up for development, configure the active profile:

```
yamlCopy codespring:
  profiles:
    active: dev
```

#### Production Environment

For production configuration, set the active profile as:

```
yamlCopy codespring:
  profiles:
    active: prod
```

------

# Dependencies

The project relies on the following libraries and frameworks:

- **Spring Boot**: The main framework for application development.
- **MyBatis**: For database interactions and mapping SQL queries.
- **MySQL Connector**: JDBC driver to connect with MySQL.
- **Lombok**: To reduce boilerplate code (e.g., getters and setters).

You can find all dependencies in the `pom.xml` file:

```
xmlCopy code<dependencies>
    <!-- Spring Boot Starter Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- MyBatis Starter -->
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.1.4</version>
    </dependency>

    <!-- MySQL Connector -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>

    <!-- Lombok -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

For a complete list of dependencies, refer to the `pom.xml` file.
