# SupplierForm.js Documentation

## Overview

The `SupplierForm` component is a React-based form designed to create supplier records. It includes input fields for supplier details, validation logic for the Brazilian CNPJ (Cadastro Nacional da Pessoa Jurídica), and error handling for form submission. The form interacts with a backend service to persist supplier data.

---

## Features

### Functionalities
- **Form Fields**:
  - `nome`: Supplier's name.
  - `cnpj`: Supplier's CNPJ (validated for correctness).
  - `nomeContato`: Contact person's name.
  - `emailContato`: Contact person's email.
  - `telefoneContato`: Contact person's phone number.

- **Validation**:
  - Ensures all fields are filled.
  - Validates the CNPJ format and checksum.

- **Error Handling**:
  - Displays error messages for invalid input or failed submission.

- **Integration**:
  - Sends supplier data to the backend using the `createSupplier` service.

---

## Code Structure

### Data Structures
The component uses two state objects:
1. **`supplier`**: Stores the form data.
   ```javascript
   {
       nome: '',
       cnpj: '',
       nomeContato: '',
       emailContato: '',
       telefoneContato: ''
   }
   ```
2. **`error`**: Stores error messages for validation or submission failures.

### Logic
#### 1. **Event Handlers**
- **`handleChange`**:
  Updates the `supplier` state when an input field changes.

- **`handleSubmit`**:
  Validates the form data and submits it to the backend. Handles errors for missing fields, invalid CNPJ, or failed API calls.

#### 2. **Validation**
- **`validateCNPJ`**:
  Validates the CNPJ format and checksum using the following steps:
  - Removes non-numeric characters.
  - Checks if the CNPJ has 14 digits.
  - Performs checksum validation for the two verification digits.

#### 3. **Integration**
- **`createSupplier`**:
  Sends the supplier data to the backend service. Resets the form on successful submission.

---

## Insights

### Validation Logic for CNPJ
The CNPJ validation is implemented using checksum calculations:
- The first verification digit is calculated using a weighted sum of the first 12 digits.
- The second verification digit is calculated using a weighted sum of the first 13 digits.
- Both digits are compared against the last two digits of the CNPJ.

### Error Handling
The component provides user feedback for:
- Missing required fields.
- Invalid CNPJ format.
- Backend service errors during supplier creation.

### Input Masking
The `InputMask` library is used to enforce the CNPJ format (`99.999.999/9999-99`) during user input.

### Reusability
The form is modular and can be extended to include additional fields or validation rules.

---

## Dependencies

| Dependency       | Purpose                                      |
|-------------------|----------------------------------------------|
| `react`          | Core library for building the component.     |
| `react-input-mask`| Provides input masking for the CNPJ field.   |
| `supplierService` | Contains the `createSupplier` API function. |

---

## Error Messages

| Error Condition                  | Message                  |
|----------------------------------|--------------------------|
| Missing required fields          | "All fields are required"|
| Invalid CNPJ                     | "Invalid CNPJ"           |
| Backend service failure          | "Failed to create supplier"|

---

## Component Usage

### Import
```javascript
import SupplierForm from './SupplierForm';
```

### Render
```javascript
<SupplierForm />
```

This will render the supplier creation form with validation and error handling.
