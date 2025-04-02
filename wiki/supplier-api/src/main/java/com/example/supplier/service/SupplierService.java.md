# SupplierService Documentation

## Overview

The `SupplierService` class is a service layer in a Spring-based application that manages operations related to suppliers. It interacts with the `SupplierRepository` to perform CRUD (Create, Read, Update, Delete) operations on supplier entities. Additionally, it validates supplier data, such as the CNPJ (Brazilian company registration number), using utility methods.

---

## Class Details

### **Class Name**: `SupplierService`

### **Package**: `com.example.supplier.service`

### **Annotations**:
- `@Service`: Indicates that this class is a Spring service component.

---

## Dependencies

### **Injected Dependencies**:
| Dependency Name       | Type                     | Description                                                                 |
|-----------------------|--------------------------|-----------------------------------------------------------------------------|
| `supplierRepository`  | `SupplierRepository`     | Repository interface for database operations on `Supplier` entities.       |

### **Utility Class**:
| Utility Name          | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `CodigoUtil`          | Provides utility methods, such as `isValidCNPJ`, for validating CNPJ values.|

---

## Methods

### **1. createSupplier(Supplier supplier)**

#### **Description**:
Creates a new supplier entity after validating its CNPJ.

#### **Parameters**:
| Name       | Type       | Description                          |
|------------|------------|--------------------------------------|
| `supplier` | `Supplier` | The supplier entity to be created.  |

#### **Returns**:
| Type       | Description                          |
|------------|--------------------------------------|
| `Supplier` | The saved supplier entity.          |

#### **Exceptions**:
| Exception Type               | Condition                                      |
|------------------------------|------------------------------------------------|
| `IllegalArgumentException`   | Thrown if the CNPJ is invalid.                 |

---

### **2. getAllSuppliers()**

#### **Description**:
Retrieves all supplier entities from the database.

#### **Parameters**:
None.

#### **Returns**:
| Type            | Description                          |
|-----------------|--------------------------------------|
| `List<Supplier>`| A list of all supplier entities.    |

---

### **3. getSupplierById(Long id)**

#### **Description**:
Fetches a supplier entity by its ID.

#### **Parameters**:
| Name | Type   | Description                          |
|------|--------|--------------------------------------|
| `id` | `Long` | The ID of the supplier to retrieve. |

#### **Returns**:
| Type                  | Description                          |
|-----------------------|--------------------------------------|
| `Optional<Supplier>`  | The supplier entity wrapped in an `Optional`. |

---

### **4. updateSupplier(Long id, Supplier supplierDetails)**

#### **Description**:
Updates an existing supplier entity with new details after validating the CNPJ.

#### **Parameters**:
| Name              | Type       | Description                          |
|-------------------|------------|--------------------------------------|
| `id`              | `Long`     | The ID of the supplier to update.   |
| `supplierDetails` | `Supplier` | The updated supplier details.       |

#### **Returns**:
| Type       | Description                          |
|------------|--------------------------------------|
| `Supplier` | The updated supplier entity.        |

#### **Exceptions**:
| Exception Type               | Condition                                      |
|------------------------------|------------------------------------------------|
| `IllegalArgumentException`   | Thrown if the CNPJ is invalid.                 |
| `RuntimeException`           | Thrown if no supplier is found with the given ID.|

---

### **5. deleteSupplier(Long id)**

#### **Description**:
Deletes a supplier entity by its ID.

#### **Parameters**:
| Name | Type   | Description                          |
|------|--------|--------------------------------------|
| `id` | `Long` | The ID of the supplier to delete.   |

#### **Returns**:
| Type      | Description                          |
|-----------|--------------------------------------|
| `boolean` | Returns `true` if the deletion is successful. |

#### **Exceptions**:
| Exception Type     | Condition                                      |
|--------------------|------------------------------------------------|
| `RuntimeException` | Thrown if no supplier is found with the given ID.|

---

## Insights

- **Validation**: The `createSupplier` and `updateSupplier` methods ensure data integrity by validating the CNPJ using the `CodigoUtil.isValidCNPJ` method. This prevents invalid supplier data from being persisted in the database.

- **Error Handling**: The service uses exceptions (`IllegalArgumentException` and `RuntimeException`) to handle invalid input and missing entities, ensuring robust error management.

- **CRUD Operations**: The class provides complete CRUD functionality for supplier entities, making it a central component for supplier management.

- **Spring Integration**: The use of `@Service` and `@Autowired` annotations demonstrates seamless integration with the Spring framework for dependency injection and service management.

- **Optional Usage**: The `getSupplierById` method returns an `Optional<Supplier>`, promoting safe handling of potentially null values.

- **Reusability**: The class is designed to be reusable and extendable, with clear separation of concerns between validation, repository interaction, and business logic.
