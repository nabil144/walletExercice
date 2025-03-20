# Two-Service Microservice Exercise Using RestTemplate

## Overview
This exercise involves building two independent Spring Boot microservices that communicate with each other using `RestTemplate`. Each microservice will have its own SQL Server database, ensuring proper separation of concerns.

### **Project 1: User Service**
#### **Description**
- The `UserService` is responsible for managing users and their accounts.
- Each user has a wallet balance.
- Users can request to transfer money to another user, but the actual transaction is processed by the `TransactionService`.

#### **Requirements**
- **Database**: SQL Server
- **Entities**:
  - `User`: Represents a system user with an ID, name, email, and wallet balance.
- **Endpoints**:
  - `POST /users`: Create a new user.
  - `GET /users/{id}`: Get user details.
  - `POST /users/{id}/transfer`: Request a transfer to another user.
- **Logic**:
  - When a user requests a transfer, the `UserService` calls the `TransactionService` using `RestTemplate` to process the transaction.

### **Project 2: Transaction Service**
#### **Description**
- The `TransactionService` handles processing of money transfers between users.
- It receives requests from `UserService` and updates the transactions accordingly.

#### **Requirements**
- **Database**: SQL Server
- **Entities**:
  - `Transaction`: Represents a transaction with sender ID, receiver ID, amount, timestamp, and status.
- **Endpoints**:
  - `POST /transactions`: Create a transaction (called by `UserService`).
  - `GET /transactions/{id}`: Get transaction details.
- **Logic**:
  - When a transaction is requested, `TransactionService` verifies the sender’s balance, updates the status, and notifies `UserService`.

### **Communication Between Services**
1. `UserService` calls `TransactionService` via `RestTemplate` to create a transaction.
2. `TransactionService` verifies the sender's balance and processes the transaction.
3. If successful, `TransactionService` updates the database and notifies `UserService`.
4. `UserService` updates the wallet balances of both sender and receiver.

### **Bonus Enhancements**
- Implement proper error handling and response management.
- Add logging using `Slf4j`.
- Implement unit tests for both services.
- Add security with `Spring Security` (optional).

## **Your To Do List**
1. Set up SQL Server databases for both services.
2. Create Spring Boot applications with required dependencies (`Spring Web`, `Spring Data JPA`, `RestTemplate`).
3. Implement database entities and repositories.
4. Develop service layers and controllers.
5. Implement `RestTemplate` calls between services.
6. Test the functionality using Postman.
