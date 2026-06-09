# 🛒 E-Commerce Backend System

> A RESTful backend API for an e-commerce platform built with Spring Boot 3, Spring Data JPA, and MySQL — covering user management, product catalogue, shopping cart, and order checkout.

![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.5.6-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Java](https://img.shields.io/badge/Java_21-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white)

---

## 📖 About

This is a **Spring Boot REST API** for an e-commerce application. It provides backend endpoints for managing users, products, shopping carts, and orders. Built using a layered architecture (Controller → Service → Repository → Model) with Spring Data JPA for database interaction and Lombok for reducing boilerplate code.

---

## ✨ Features

- 👤 **User Management** — Create, retrieve, and delete user accounts with email validation
- 📦 **Product Management** — Add, update, retrieve, and delete products with stock tracking
- 🛒 **Shopping Cart** — Add items to cart, view cart by user, and remove items
- 📋 **Order Management** — Checkout from cart (creates order with items + total), view order history
- ✅ **Bean Validation** — `@NotBlank`, `@Email` annotations for request body validation
- ⚠️ **Exception Handling** — Custom `ResourceNotFoundException` for missing entities
- 🔄 **Auto DDL** — Hibernate auto-creates/updates database tables on startup

---

## 🛠️ Tech Stack

| Technology | Version | Usage |
|------------|---------|-------|
| Java | 21 | Programming language |
| Spring Boot | 3.5.6 | Application framework |
| Spring Web | — | REST API (MVC) |
| Spring Data JPA | — | ORM & database layer |
| Spring Validation | — | Request body validation |
| Hibernate | — | JPA implementation + DDL auto |
| MySQL | — | Relational database |
| Lombok | — | `@Getter`, `@Setter` boilerplate reduction |
| Maven | — | Build and dependency management |

---

## 🗄️ Data Models

### User
| Field | Type | Notes |
|-------|------|-------|
| `id` | Long | Auto-generated PK |
| `name` | String | Required (`@NotBlank`) |
| `email` | String | Unique, validated (`@Email`) |
| `password` | String | Required |
| `orders` | List\<Order\> | One-to-many relationship |

### Product
| Field | Type | Notes |
|-------|------|-------|
| `id` | Long | Auto-generated PK |
| `name` | String | Required (`@NotBlank`) |
| `description` | String | Optional |
| `price` | Double | Product price |
| `stockQuantity` | Integer | Available stock |

### Cart
| Field | Type | Notes |
|-------|------|-------|
| `id` | Long | Auto-generated PK |
| `user` | User | Many-to-one |
| `product` | Product | Many-to-one |
| `quantity` | Integer | Cart item quantity |

### Order
| Field | Type | Notes |
|-------|------|-------|
| `id` | Long | Auto-generated PK |
| `user` | User | Many-to-one |
| `totalAmount` | Double | Total order value |
| `status` | String | Order status |
| `orderDate` | LocalDateTime | Timestamp |
| `orderItems` | List\<OrderItem\> | One-to-many |

### OrderItem
| Field | Type | Notes |
|-------|------|-------|
| `id` | Long | Auto-generated PK |
| `order` | Order | Many-to-one |
| `product` | Product | Many-to-one |
| `quantity` | Integer | Item quantity |
| `price` | Double | Item price at order time |

---

## 🌐 API Endpoints

### 👤 Users — `/api/users`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/users` | Create a new user |
| `GET` | `/api/users` | Get all users |
| `GET` | `/api/users/{id}` | Get user by ID |
| `DELETE` | `/api/users/{id}` | Delete user by ID |

**Create User — Request Body:**
```json
{
  "name": "Umindu Dinal",
  "email": "umindudinal@gmail.com",
  "password": "password123"
}
```

---

### 📦 Products — `/api/products`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/products` | Add a new product |
| `GET` | `/api/products` | Get all products |
| `GET` | `/api/products/{id}` | Get product by ID |
| `PUT` | `/api/products/{id}` | Update product |
| `DELETE` | `/api/products/{id}` | Delete product |

**Add Product — Request Body:**
```json
{
  "name": "Wireless Headphones",
  "description": "Noise cancelling headphones",
  "price": 49.99,
  "stockQuantity": 100
}
```

---

### 🛒 Cart — `/api/cart`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/cart/add?userId={id}&productId={id}&quantity={n}` | Add item to cart |
| `GET` | `/api/cart/{userId}` | Get cart items by user |
| `DELETE` | `/api/cart/remove?userId={id}&productId={id}` | Remove item from cart |

---

### 📋 Orders — `/api/orders`

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/orders/checkout/{userId}` | Checkout — creates order from cart |
| `GET` | `/api/orders/{userId}` | Get all orders for a user |

---

## 📁 Project Structure

```
ecommerce/
│
├── pom.xml                             # Maven dependencies
│
└── src/main/java/com/example/ecommerce/
    │
    ├── EcommerceApplication.java       # Spring Boot entry point
    │
    ├── controller/                     # REST controllers (HTTP layer)
    │   ├── UserController.java
    │   ├── ProductController.java
    │   ├── CartController.java
    │   └── OrderController.java
    │
    ├── service/                        # Business logic layer
    │   ├── UserService.java
    │   ├── ProductService.java
    │   ├── CartService.java
    │   └── OrderService.java
    │
    ├── repository/                     # Spring Data JPA repositories
    │   ├── UserRepository.java
    │   ├── ProductRepository.java
    │   ├── CartRepository.java
    │   └── OrderRepository.java
    │
    ├── model/                          # JPA entity classes
    │   ├── User.java
    │   ├── Product.java
    │   ├── Cart.java
    │   ├── Order.java
    │   └── OrderItem.java
    │
    └── exception/
        └── ResourceNotFoundException.java
```

---

## 🚀 Getting Started

### Prerequisites

- Java 21
- Maven 3.6+
- MySQL 8+
- IntelliJ IDEA / VS Code (recommended)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/umindudinal/E-Commerce-Backend-System-using-Spring-Boot.git
   cd E-Commerce-Backend-System-using-Spring-Boot
   ```

2. **Create the MySQL database**
   ```sql
   CREATE DATABASE ecommerce;
   ```

3. **Configure `application.properties`**

   Open `src/main/resources/application.properties` and update:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce
   spring.datasource.username=root
   spring.datasource.password=your_password
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   server.port=8080
   ```

4. **Build and run the application**
   ```bash
   ./mvnw spring-boot:run
   ```
   Or on Windows:
   ```bash
   mvnw.cmd spring-boot:run
   ```

5. **API is running at:**
   ```
   http://localhost:8080
   ```

> ✅ Hibernate will automatically create all database tables on first run (`ddl-auto=update`).

---

## 🧪 Testing the API

You can test the endpoints using [Postman](https://www.postman.com/) or [cURL](https://curl.se/).

**Example — Create a user:**
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Umindu","email":"umindu@gmail.com","password":"pass123"}'
```

**Example — Add to cart:**
```bash
curl -X POST "http://localhost:8080/api/cart/add?userId=1&productId=1&quantity=2"
```

**Example — Checkout:**
```bash
curl -X POST http://localhost:8080/api/orders/checkout/1
```

---

## 👨‍💻 Author

**Umindu Dinal**
- GitHub: [@umindudinal](https://github.com/umindudinal)
- Email: umindudinal@gmail.com

---

## 📄 License

Copyright © 2025 Umindu Dinal. All Rights Reserved.

---

<p align="center">Built with ❤️ using Spring Boot</p>
