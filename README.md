# 🚂 Railway Department Management System

A backend enterprise application built with **Spring Boot** and **MongoDB** for managing railway departments and employees. The system provides full CRUD functionality for departments and employees, with entity relationships handled via MongoDB DBRef mapping.

---

## 📋 Table of Contents

- [Tech Stack](#tech-stack)
- [Project Architecture](#project-architecture)
- [Project Structure](#project-structure)
- [Entity Design](#entity-design)
- [API Endpoints](#api-endpoints)
- [Advanced Features](#advanced-features)
- [Database Collections](#database-collections)
- [Testing](#testing)
- [Future Enhancements](#future-enhancements)

---

## 🛠️ Tech Stack

| Category     | Technology              |
|--------------|-------------------------|
| Language     | Java 17                 |
| Framework    | Spring Boot             |
| Database     | MongoDB + MongoDB Compass |
| Build Tool   | Maven                   |
| API Testing  | Postman                 |
| IDE          | IntelliJ IDEA           |

**Spring Boot Dependencies:** Spring Web · Spring Data MongoDB

---

## 🏗️ Project Architecture

The application follows a layered architecture pattern:

```
Controller Layer
      ↓
Service Layer
      ↓
Repository Layer
      ↓
MongoDB Database
```

| Layer      | Responsibility                                              |
|------------|-------------------------------------------------------------|
| Controller | Handles incoming HTTP requests and returns API responses    |
| Service    | Contains business logic and application processing          |
| Repository | Communicates with MongoDB using Spring Data MongoDB         |
| Database   | Stores employee and department records in collections       |

---

## 📁 Project Structure

```
com.swapnil.railwaydepartmentmanagement
│
├── controller
│   ├── DepartmentController
│   └── EmployeeController
│
├── service
│   ├── DepartmentService
│   └── EmployeeService
│
├── repository
│   ├── DepartmentRepository
│   └── EmployeeRepository
│
├── model
│   ├── Department
│   └── Employee
│
└── RailwayDepartmentManagementApplication
```

---

## 🗂️ Entity Design

### Department

| Field            | Type   |
|-----------------|--------|
| id              | String |
| departmentName  | String |
| location        | String |

**Sample Departments:**
- Information Technology
- Human Resources
- Operations
- Finance & Accounts
- Signal & Telecommunication

---

### Employee

| Field          | Type       |
|---------------|------------|
| id            | String     |
| employeeName  | String     |
| designation   | String     |
| salary        | Double     |
| department    | @DBRef     |

---

### Entity Relationship

```
One Department  ──────►  Many Employees
Many Employees  ◄──────  One Department
```

MongoDB relationship is implemented using `@DBRef`, allowing each employee to maintain a reference to their assigned department.

---

## 🌐 API Endpoints

### Department APIs

| Method   | Endpoint              | Description                  |
|----------|-----------------------|------------------------------|
| `POST`   | `/department`         | Add a new railway department |
| `GET`    | `/department`         | Retrieve all departments     |
| `GET`    | `/department/{id}`    | Retrieve department by ID    |
| `PUT`    | `/department/{id}`    | Update department details    |
| `DELETE` | `/department/{id}`    | Delete a department          |

---

### Employee APIs

| Method   | Endpoint              | Description               |
|----------|-----------------------|---------------------------|
| `POST`   | `/employee`           | Add a new employee        |
| `GET`    | `/employee`           | Retrieve all employees    |
| `GET`    | `/employee/{id}`      | Retrieve employee by ID   |
| `PUT`    | `/employee/{id}`      | Update employee details   |
| `DELETE` | `/employee/{id}`      | Delete an employee        |

---

## ⚡ Advanced Features

### Department-wise Employee Retrieval

Retrieve all employees belonging to a specific department.

```
GET /employee/department/{departmentId}
```

---

### Designation-wise Employee Retrieval

Retrieve employees filtered by their designation.

```
GET /employee/designation/{designation}
```

Example designations: `Software Engineer`, `HR Manager`, `Database Administrator`, `Finance Officer`

---

### Employee Transfer Between Departments

Transfer an employee from one railway department to another. The department reference is updated automatically in MongoDB.

```
PUT /employee/transfer/{employeeId}/{departmentId}
```

**Example:**
```
Information Technology  ──►  Human Resources
```

---

## 🗄️ Database Collections

### `departments` Collection

```json
{
  "departmentName": "Information Technology",
  "location": "Mumbai"
}
```

### `employees` Collection

```json
{
  "employeeName": "Swapnil Soni",
  "designation": "Software Engineer",
  "salary": 70000,
  "department": { "$ref": "departments", "$id": "<ObjectId>" }
}
```

---

## 🔍 Repository Methods

### DepartmentRepository
Extends `MongoRepository` to provide built-in CRUD operations.

### EmployeeRepository
Custom query methods implemented using Spring Data MongoDB conventions:

```java
findByDesignation(String designation)
findByDepartmentId(String departmentId)
```

These are automatically translated into MongoDB queries at runtime.

---

## ✅ Testing

APIs were tested using **Postman**, with responses verified via **MongoDB Compass** and **MongoDB Shell**.

Test coverage includes:

- Department Creation & Deletion
- Employee Creation, Update & Deletion
- Department Update
- Employee Transfer Between Departments
- Department-wise Employee Search
- Designation-wise Employee Search

---

## 🚀 Business Workflow

```
Department Creation
       ↓
Employee Assignment
       ↓
Employee Record Management
       ↓
Department-Based Employee Retrieval
       ↓
Designation-Based Employee Retrieval
       ↓
Employee Transfer Between Departments
       ↓
Database Update
```

---

## 🔮 Future Enhancements

- [ ] User Authentication & Authorization
- [ ] Role-Based Access Control (RBAC)
- [ ] Railway Zone Management
- [ ] Attendance Management System
- [ ] Employee Promotion Tracking
- [ ] Payroll Management
- [ ] Performance Monitoring Dashboard
- [ ] Reporting & Analytics

---

## 🧠 Key Concepts Demonstrated

- REST API Development with Spring Boot
- Spring Boot Auto Configuration
- Dependency Injection (`@Autowired`)
- MongoDB Integration with Spring Data MongoDB
- DBRef Mapping for Entity Relationships
- Layered Architecture & Repository Pattern
- Custom Query Methods
- CRUD Operations
- OOP Principles

---

## 👨‍💻 Author

**Swapnil Soni**

*Railway Department Management System — Spring Boot + MongoDB*
