# Documentation: SupplierController.java

## Overview
The `SupplierController` class is a REST controller in a Spring Boot application that manages CRUD operations for `Supplier` entities. It provides endpoints for creating, reading, updating, and deleting suppliers. The controller interacts with the `SupplierService` to perform business logic and return appropriate HTTP responses.

## Class Details

### Package
```java
package com.example.supplier.controller;
```
The class resides in the `com.example.supplier.controller` package.

### Annotations
- `@RestController`: Indicates that this class is a REST controller.
- `@RequestMapping("/api/suppliers")`: Maps all endpoints in this controller to the base URL `/api/suppliers`.

### Dependencies
- **SupplierService**: The service layer responsible for business logic related to `Supplier` entities. It is injected using `@Autowired`.

## Endpoints

| HTTP Method | Endpoint           | Description                                      | Request Body         | Response Type         |
|-------------|--------------------|--------------------------------------------------|----------------------|-----------------------|
| `GET`       | `/api/suppliers`   | Retrieves a list of all suppliers.              | None                 | `List<Supplier>`      |
| `GET`       | `/api/suppliers/{id}` | Retrieves a specific supplier by its ID.        | None                 | `ResponseEntity<Supplier>` |
| `POST`      | `/api/suppliers`   | Creates a new supplier.                         | `Supplier`           | `Supplier`            |
| `PUT`       | `/api/suppliers/{id}` | Updates an existing supplier by its ID.         | `Supplier`           | `ResponseEntity<Supplier>` |
| `DELETE`    | `/api/suppliers/{id}` | Deletes a supplier by its ID.                   | None                 | `ResponseEntity<Void>` |

### Endpoint Details

#### `GET /api/suppliers`
- **Description**: Fetches all suppliers.
- **Return Type**: `List<Supplier>`
- **Logic**: Calls `supplierService.getAllSuppliers()` to retrieve all suppliers.

#### `GET /api/suppliers/{id}`
- **Description**: Fetches a supplier by its ID.
- **Path Variable**: `id` (Long) - The ID of the supplier.
- **Return Type**: `ResponseEntity<Supplier>`
- **Logic**: Calls `supplierService.getSupplierById(id)` and returns:
  - `200 OK` with the supplier if found.
  - `404 Not Found` if the supplier does not exist.

#### `POST /api/suppliers`
- **Description**: Creates a new supplier.
- **Request Body**: `Supplier` - The supplier details.
- **Return Type**: `Supplier`
- **Logic**: Calls `supplierService.createSupplier(supplier)` to save the new supplier.

#### `PUT /api/suppliers/{id}`
- **Description**: Updates an existing supplier.
- **Path Variable**: `id` (Long) - The ID of the supplier to update.
- **Request Body**: `Supplier` - The updated supplier details.
- **Return Type**: `ResponseEntity<Supplier>`
- **Logic**: Calls `supplierService.updateSupplier(id, supplierDetails)` and returns:
  - `200 OK` with the updated supplier if successful.
  - `404 Not Found` if the supplier does not exist.

#### `DELETE /api/suppliers/{id}`
- **Description**: Deletes a supplier by its ID.
- **Path Variable**: `id` (Long) - The ID of the supplier to delete.
- **Return Type**: `ResponseEntity<Void>`
- **Logic**: Calls `supplierService.deleteSupplier(id)` and returns:
  - `204 No Content` if the deletion is successful.
  - `404 Not Found` if the supplier does not exist.

## Insights

- **Error Handling**: The controller uses `ResponseEntity` to handle cases where a supplier is not found (`404 Not Found`) or when a deletion is successful (`204 No Content`).
- **Dependency Injection**: The `SupplierService` is injected using `@Autowired`, promoting loose coupling and testability.
- **RESTful Design**: The endpoints follow RESTful principles, using appropriate HTTP methods (`GET`, `POST`, `PUT`, `DELETE`) and status codes.
- **Scalability**: The controller delegates business logic to the service layer, making it easier to scale and maintain the application.
- **Data Validation**: While the controller accepts `Supplier` objects in the request body, additional validation mechanisms (e.g., `@Valid`) could be implemented to ensure data integrity.
