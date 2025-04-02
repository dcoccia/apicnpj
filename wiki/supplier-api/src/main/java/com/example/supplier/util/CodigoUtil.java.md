# Documentation: `CodigoUtil.java`

## Overview
The `CodigoUtil` class provides utility methods for validating Brazilian CNPJ numbers. A CNPJ (Cadastro Nacional da Pessoa Jurídica) is a unique identifier for companies registered in Brazil. This class includes logic to verify the validity of a CNPJ based on its checksum calculation.

---

## Class: `CodigoUtil`

### Package
The class is part of the package:
```
com.example.supplier.util
```

---

## Method Details

### `isValidCNPJ(long cnpj)`
#### Description
This method validates a Brazilian CNPJ number by performing checksum calculations. It ensures the CNPJ adheres to the required format and validates its two verification digits.

#### Parameters
| Parameter | Type   | Description                                      |
|-----------|--------|--------------------------------------------------|
| `cnpj`    | `long` | The CNPJ number to be validated.                 |

#### Return Value
| Type      | Description                                      |
|-----------|--------------------------------------------------|
| `boolean` | Returns `true` if the CNPJ is valid, otherwise `false`. |

#### Logic
1. **Formatting**: Converts the `long` CNPJ into a 14-character string, padding with leading zeros if necessary.
2. **Length Check**: Ensures the formatted CNPJ has exactly 14 characters.
3. **Checksum Calculation**:
   - Uses two predefined weight arrays (`weight1` and `weight2`) for the calculation.
   - Computes the first verification digit using the first 12 digits of the CNPJ and `weight1`.
   - Computes the second verification digit using the first 13 digits of the CNPJ and `weight2`.
4. **Validation**: Compares the calculated verification digits with the last two digits of the CNPJ.
5. **Error Handling**: Returns `false` if any exception occurs during processing.

#### Algorithm Details
| Step | Description                                                                 |
|------|-----------------------------------------------------------------------------|
| 1    | Convert the `long` CNPJ to a zero-padded 14-character string.               |
| 2    | Validate the length of the string (must be 14 characters).                  |
| 3    | Calculate the first verification digit using weights `weight1`.             |
| 4    | Calculate the second verification digit using weights `weight2`.            |
| 5    | Compare the calculated digits with the actual digits in the CNPJ.           |
| 6    | Return `true` if both digits match; otherwise, return `false`.              |

---

### `main(String[] args)`
#### Description
A simple test method to demonstrate the usage of the `isValidCNPJ` method. It validates a hardcoded example CNPJ and prints the result to the console.

#### Parameters
| Parameter | Type         | Description                                      |
|-----------|--------------|--------------------------------------------------|
| `args`    | `String[]`   | Command-line arguments (not used in this method).|

#### Example Output
For the hardcoded CNPJ `12345678000195L`, the output will be:
```
CNPJ is valid: false
```

---

## Insights

### Validation Logic
- The validation relies on the checksum algorithm defined by Brazilian regulations for CNPJ numbers.
- The weights (`weight1` and `weight2`) are specific to the CNPJ format and are used to calculate the verification digits.

### Error Handling
- The method uses a `try-catch` block to handle any unexpected errors during processing, ensuring the method returns `false` in case of invalid input or calculation issues.

### Limitations
- The method assumes the input CNPJ is numeric and does not handle non-numeric inputs.
- It does not validate the format of the CNPJ beyond its checksum (e.g., it does not check for valid prefixes or registration rules).

### Practical Use
- This utility can be integrated into systems that require validation of CNPJ numbers, such as supplier registration or company verification processes.

---

## File Metadata
| Key         | Value                  |
|-------------|------------------------|
| File Name   | `CodigoUtil.java`      |
| Package     | `com.example.supplier.util` |
