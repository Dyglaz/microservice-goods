# Multi-Module Product Manager

## About the Project

**Multi-Module Product Manager** is a web application designed to manage product information, utilizing a modular architecture. The application consists of two modules:
1. **Manager-App**: A user-facing module for viewing, creating, editing, and deleting products.
2. **Catalogue-Service**: A backend service responsible for product storage, data validation, and business logic.

The application provides seamless CRUD (Create, Read, Update, Delete) operations on product data, including title and details.

---

## Key Features

- **View Products**: Display a list of products with optional filtering.
- **Add New Product**: A form for creating new products.
- **Edit Product**: Update product information through a user-friendly interface.
- **Delete Product**: Remove product records.
- **REST API**: A backend module offering RESTful endpoints for product management.

---

## Technologies

- **Spring Boot**: For rapid application development and modular architecture.
- **Spring MVC**: For handling HTTP requests in the `manager-app`.
- **Thymeleaf**: Templating engine for rendering dynamic HTML pages in the `manager-app`.
- **Spring Data JPA**: For database access and ORM in the `catalogue-service`.
- **Hibernate Validator**: For input validation.
- **Flyway**: For managing database schema migrations.
- **PostgreSQL**: Relational database for storing product information.

---

## Installation and Setup

### Prerequisites

1. **Install PostgreSQL** (Ensure it's running on port `5555` or configure another port).
2. **Install Java 21**.
3. **Install Maven** for building the project.

---

## Steps

1. **Clone the Repository**:
   ```bash  
   git clone https://github.com/your-repo/multi-module-product-manager  
   cd multi-module-product-manager  
   ```

2. **Set up the Databases**:
    - Open a PostgreSQL client and execute the following:
   ```sql  
    CREATE DATABASE catalogue;  
    CREATE USER catalogue WITH PASSWORD 'catalogue';  
    GRANT ALL PRIVILEGES ON DATABASE catalogue TO catalogue;
   ```
    - Ensure the `catalogue-service` is configured to connect to this database.

3. **Run Database Migrations**:  
   Flyway will automatically create the necessary tables when the `catalogue-service` starts.

4. **Configure Application Properties**:
    - For `catalogue-service`, update the `application-standalone.yaml` file if needed:
   ```yaml  
    spring:  
     datasource:  
      url: jdbc:postgresql://localhost:5555/catalogue  
      username: catalogue  
      password: catalogue
   ```

5. **Build the Project**:  
Run the following command in the root directory:
   ```bash  
   mvn clean install
   ```

6. **Run the Services**:  
   - Start the `catalogue-service` on port `8081`
   ```bash  
   java -jar catalogue-service/target/catalogue-service-0.0.1-SNAPSHOT.jar 
   ```
    - Start the `manager-app` on port `8080`
    ```bash  
   java -jar manager-app/target/manager-app-0.0.1-SNAPSHOT.jar 
   ```

---

## Usage

1. Open your browser and navigate to:
- **Manager App**: `http://localhost:8080/catalogue/products/list`
- **Catalogue Service API**: `http://localhost:8081/catalogue-api/products`
2. Use the following features in the Manager App:
- **View Product List**: Displays all products stored in the database.
- **Filter Products**: Use the filter option to search by product titles.
- **Add New Product**: Navigate to `http://localhost:8080/catalogue/products/create`.
- **Edit Product**: Click on a product from the list to modify its details.
- **Delete Product**: Use the delete option to remove a product.

---

## API Endpoints

The **Catalogue-Service** module provides RESTful endpoints:

| Method | Endpoint                         | Description                        |  
|--------|----------------------------------|------------------------------------|  
| GET    | `/catalogue-api/products`        | Retrieve all products (with filter)|  
| POST   | `/catalogue-api/products`        | Create a new product               |  
| GET    | `/catalogue-api/products/{id}`   | Retrieve a specific product by ID  |  
| PATCH  | `/catalogue-api/products/{id}`   | Update product details             |  
| DELETE | `/catalogue-api/products/{id}`   | Delete a product                   | 
   
