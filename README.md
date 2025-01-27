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
- **Spring Data JPA**: For database access and ORM in the `catalogue-service`.
- **PostgreSQL**: Relational database for storing product information.
- **Flyway**: For managing database schema migrations.
- **Docker**: To run a container with a PostgreSQL database.
- **Hibernate Validator**: For input validation.
- **Thymeleaf**: Templating engine for rendering dynamic HTML pages in the `manager-app`.

---

## Installation and Setup

### Prerequisites

1. **PostgreSQL**.
2. **Java 21**.
3. **Maven** for building the project.
4. **Docker**.

---

## Steps

1. **Clone the Repository**:
   ```bash  
   git clone https://github.com/your-repo/multi-module-product-manager  
   cd multi-module-product-manager  
   ```
   
2. **Set up the database using Docker**:
   - Ensure that Docker is installed and running on your machine.
   - Run the following command to start a PostgreSQL container:
   ```bash  
   docker run --name catalogue-db -p 5555:5432 -e POSTGRES_DB=catalogue -e POSTGRES_USER=catalogue
    -e POSTGRES_PASSWORD=catalogue postgres:17 
   ```

3. **Set up the Databases**:
    - Open a PostgreSQL client and execute the following:
   ```sql  
    CREATE DATABASE catalogue;  
    CREATE USER catalogue WITH PASSWORD 'catalogue';  
    GRANT ALL PRIVILEGES ON DATABASE catalogue TO catalogue;
   ```
    - Ensure the `catalogue-service` is configured to connect to this database.

4. **Run Database Migrations**:  
   Flyway will automatically create the necessary tables when the `catalogue-service` starts.

5. **Configure Application Properties**:
    - For `catalogue-service`, update the `application-standalone.yaml` file if needed:
   ```yaml  
    spring:  
     datasource:  
      url: jdbc:postgresql://localhost:5555/catalogue  
      username: catalogue  
      password: catalogue
   ```

6. **Build the Project**:  
Run the following command in the root directory:
   ```bash  
   mvn clean install
   ```

7. **Run the Services**:  
   - Start the `catalogue-service` on port `8081`:
   ```bash  
   java -jar catalogue-service/target/catalogue-service-0.0.1-SNAPSHOT.jar 
   ```
    - Start the `manager-app` on port `8080`:
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
   
---

# Многомодульный менеджер продуктов

## О проекте

**Многомодульный менеджер продуктов** — это веб-приложение, разработанное для управления информацией о продуктах с использованием модульной архитектуры.   
Приложение состоит из двух модулей:
1. **Manager-App**: Модуль пользовательского интерфейса, который позволяет просматривать, создавать, редактировать и удалять продукты.
2. **Catalogue-Service**: Бэкенд-сервис, отвечающий за хранение данных, их валидацию и бизнес-логику.

Приложение предоставляет возможность выполнения операций CRUD (создание, чтение, обновление, удаление) для данных о продуктах, включая их название и описание.

---

## Основные функции

- **Просмотр продуктов**: Отображение списка продуктов с возможностью фильтрации.
- **Добавление нового продукта**: Форма для создания новых продуктов.
- **Редактирование продукта**: Изменение информации о продукте через удобный интерфейс.
- **Удаление продукта**: Удаление записей о продуктах.
- **REST API**: Бэкенд-модуль предоставляет RESTful API для управления продуктами.

---

## Технологии

- **Spring Boot**: Для быстрой разработки и модульной архитектуры.
- **Spring MVC**: Для обработки HTTP-запросов в модуле `manager-app`.
- **Spring Data JPA**: Для доступа к базе данных и ORM в модуле `catalogue-service`.
- **PostgreSQL**: Реляционная база данных для хранения информации о продуктах.
- **Flyway**: Для управления миграциями базы данных.
- **Docker**: Для запуска контейнера с базой данных PostgreSQL.
- **Hibernate Validator**: Для валидации входных данных.
- **Thymeleaf**: Шаблонизатор для динамического формирования HTML-страниц в модуле `manager-app`.

---

## Установка и настройка

### Необходимые компоненты

1. **PostgreSQL**.
2. **Java 21**.
3. **Maven** для сборки проекта.
4. **Docker**.

---

### Шаги

1. **Клонируйте репозиторий**:
   ```bash  
   git clone https://github.com/your-repo/multi-module-product-manager  
   cd multi-module-product-manager  
   ```

2. **Настройте базу данных с помощью Docker**:
   - Убедитесь, что Docker установлен и работает на вашем компьютере.
   - Выполните следующую команду для запуска контейнера PostgreSQL:
   ```bash  
   docker run --name catalogue-db -p 5555:5432 -e POSTGRES_DB=catalogue -e POSTGRES_USER=catalogue
    -e POSTGRES_PASSWORD=catalogue postgres:17 
   ```

3. **Настройте базы данных**:
   - Откройте клиент PostgreSQL и выполните следующие команды:
   ```sql  
    CREATE DATABASE catalogue;  
    CREATE USER catalogue WITH PASSWORD 'catalogue';  
    GRANT ALL PRIVILEGES ON DATABASE catalogue TO catalogue;
   ```
   - Убедитесь, что `catalogue-service` настроен для подключения к этой базе данных.

4. **Запустите миграции базы данных**:  
   Flyway автоматически создаст необходимые таблицы при запуске `catalogue-service`.

5. **Настройте свойства приложения**:
   - Для `catalogue-service` обновите файл `application-standalone.yaml`, если это необходимо:
   ```yaml  
    spring:  
     datasource:  
      url: jdbc:postgresql://localhost:5555/catalogue  
      username: catalogue  
      password: catalogue
   ```

6. **Соберите проект**:  
   Выполните следующую команду в корневом каталоге:
   ```bash  
   mvn clean install
   ```

7. **Запустите сервисы**:
   - Запустите `catalogue-service` на порту `8081`:
   ```bash  
   java -jar catalogue-service/target/catalogue-service-0.0.1-SNAPSHOT.jar 
   ```
   - Запустите `manager-app` на порту `8080`:
    ```bash  
   java -jar manager-app/target/manager-app-0.0.1-SNAPSHOT.jar 
   ```

---

## Использование

1. Откройте браузер и перейдите по следующим адресам:
- **Manager App**: `http://localhost:8080/catalogue/products/list`
- **Catalogue Service API**: `http://localhost:8081/catalogue-api/products`
2. Используйте следующие функции в Manager App:
- **Просмотр списка продуктов**: Отображает все продукты, хранящиеся в базе данных.
- **Фильтрация продуктов**: Используйте опцию фильтрации для поиска по названиям продуктов.
- **Добавление нового продукта**: Перейдите по адресу `http://localhost:8080/catalogue/products/create`.
- **Редактирование продукта**: Нажмите на продукт из списка, чтобы изменить его детали.
- **Удаление продукта**: Используйте опцию удаления, чтобы удалить продукт.

---

## API Эндпоинты

Модуль **Catalogue-Service** предоставляет RESTful эндпоинты:

| Method | Endpoint                         | Description                        |  
|--------|----------------------------------|------------------------------------|  
| GET    | `/catalogue-api/products`        |Получить список всех продуктов (с фильтром)|  
| POST   | `/catalogue-api/products`        | Создать новый продукт               |  
| GET    | `/catalogue-api/products/{id}`   | Получить информацию о продукте по ID  |  
| PATCH  | `/catalogue-api/products/{id}`   | Обновить данные продукта             |  
| DELETE | `/catalogue-api/products/{id}`   | Удалить продукт                   | 
    