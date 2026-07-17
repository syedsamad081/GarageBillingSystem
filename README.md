# 🔧 Garage Billing System

A **console-based Garage Billing System** built with **Core Java** and **JDBC** that allows garage owners to manage customers, vehicles, and generate invoices for services rendered.

---

## 📌 Features

- **Customer Management** – Add and retrieve customer details (name, phone)
- **Vehicle Management** – Register vehicles associated with customers
- **Invoice Generation** – Create invoices by linking customers, vehicles, and services
- **Invoice Viewing** – Display all generated invoices
- **MySQL Database Integration** – Persistent data storage using JDBC

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| **Java** | Core application logic |
| **JDBC** | Database connectivity |
| **MySQL** | Relational database |
| **MySQL Connector/J 8.0.30** | JDBC driver |

---

## 📁 Project Structure

```
GarageBillingSystem/
├── src/
│   ├── App.java                      # Main entry point (CLI menu)
│   ├── config/
│   │   └── DbConfig.java             # Database connection configuration
│   ├── entity/
│   │   ├── Customer.java             # Customer entity (id, name, phone)
│   │   └── Invoice.java              # Invoice entity (id, customerId, vehicleId, serviceId)
│   └── service/
│       ├── BillingService.java        # Core billing logic & invoice creation
│       ├── CustomerService.java       # CRUD operations for customers
│       ├── InvoiceService.java        # CRUD operations for invoices
│       └── VehicleService.java        # Vehicle-related operations
└── README.md
```

---

## ⚙️ Database Setup

### 1. Create the MySQL Database

```sql
CREATE DATABASE grage;
USE grage;
```

### 2. Create Tables

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) NOT NULL
);

CREATE TABLE invoices (
    id INT PRIMARY KEY AUTO_INCREMENT,
    customer_id INT,
    vehicle_id INT,
    service_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

### 3. Update Database Credentials

Edit `src/config/DbConfig.java` with your MySQL credentials:

```java
private static final String URL = "jdbc:mysql://localhost:3306/grage";
private static final String USER = "root";
private static final String PASS = "root";
```

---

## 🚀 How to Run

### Prerequisites
- **Java JDK 8+** installed
- **MySQL Server** running on `localhost:3306`
- **MySQL Connector/J 8.0.30** JAR in classpath

### Steps

```bash
# Clone the repository
git clone https://github.com/syedsamad081/GarageBillingSystem.git
cd GarageBillingSystem

# Compile
javac -cp "lib/mysql-connector-java-8.0.30.jar" -d out src/**/*.java src/App.java

# Run
java -cp "out;lib/mysql-connector-java-8.0.30.jar" App
```

> **Note:** On Linux/Mac, replace `;` with `:` in the classpath.

---

## 📖 Usage

When you run the application, you'll see a menu:

```
1. Add Customer with Vehicle
2. Generate Invoice
3. Show Invoice
4. Exit
```

| Option | Description |
|--------|-------------|
| **1** | Register a new customer with their name, phone, and vehicle details |
| **2** | Generate an invoice by providing customer ID, vehicle ID, and service IDs |
| **3** | Display all generated invoices |
| **4** | Exit the application |

---

## 🏗️ Architecture

```
┌──────────┐     ┌─────────────────┐     ┌──────────────────┐     ┌─────────┐
│  App.java│────▶│ BillingService  │────▶│ CustomerService  │────▶│  MySQL  │
│  (CLI)   │     │                 │────▶│ InvoiceService   │────▶│   DB    │
│          │     │                 │     │ VehicleService   │────▶│         │
└──────────┘     └─────────────────┘     └──────────────────┘     └─────────┘
    UI Layer         Business Layer          Data Access Layer       Database
```

---

## 👤 Author

**Syed Samad**
- GitHub: [@syedsamad081](https://github.com/syedsamad081)

---

## 📄 License

This project is open source and available for learning and personal use.
