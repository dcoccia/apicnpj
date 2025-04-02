# Documentation: `supplierService.js`

## Overview
This module provides utility functions to interact with a supplier management API. It includes methods for fetching all suppliers and creating a new supplier. The API is hosted on a server defined by the `serverUrl` constant.

---

## Functions

### `getAllSuppliers()`
Fetches all suppliers from the API.

#### **Usage**
```javascript
import { getAllSuppliers } from './supplierService';

getAllSuppliers()
    .then(suppliers => console.log(suppliers))
    .catch(error => console.error(error));
```

#### **Details**
- **Endpoint**: `GET /api/suppliers`
- **Returns**: A promise that resolves to the list of suppliers in JSON format.
- **Error Handling**: Throws an error if the response status is not OK (`response.ok` is `false`).

---

### `createSupplier(supplier)`
Creates a new supplier by sending a POST request to the API.

#### **Usage**
```javascript
import { createSupplier } from './supplierService';

const newSupplier = {
    name: 'Supplier Name',
    cnpj: '12.345.678/0001-99',
    address: '123 Supplier Street'
};

createSupplier(newSupplier)
    .then(createdSupplier => console.log(createdSupplier))
    .catch(error => console.error(error));
```

#### **Details**
- **Endpoint**: `POST /api/suppliers`
- **Parameters**:
  - `supplier` (Object): The supplier data to be sent. Example structure:
    ```javascript
    {
        name: 'Supplier Name',
        cnpj: '12.345.678/0001-99',
        address: '123 Supplier Street'
    }
    ```
- **Preprocessing**:
  - The `cnpj` field is sanitized to remove all non-numeric characters using a regular expression (`/\D/g`).
- **Headers**:
  - `Content-Type`: `application/json`
- **Body**: The sanitized supplier object is serialized into JSON format.
- **Returns**: A promise that resolves to the created supplier object in JSON format.
- **Error Handling**: Throws an error if the response status is not OK (`response.ok` is `false`).

---

## Constants

### `serverUrl`
- **Value**: `'http://localhost:8081'`
- **Purpose**: Defines the base URL for the API server.

---

## Insights

1. **Error Handling**:
   - Both functions implement basic error handling by checking the `response.ok` property. This ensures that failed HTTP requests are caught and reported.

2. **Data Sanitization**:
   - The `createSupplier` function sanitizes the `cnpj` field to remove non-numeric characters. This preprocessing step ensures that the data sent to the API is clean and consistent.

3. **Asynchronous Operations**:
   - Both functions use `async/await` for handling asynchronous operations, making the code more readable and easier to maintain.

4. **API Design**:
   - The module assumes a RESTful API design with endpoints for fetching (`GET`) and creating (`POST`) suppliers.

5. **Scalability**:
   - The `serverUrl` constant allows easy reconfiguration of the API base URL, making the module adaptable to different environments (e.g., development, staging, production).
