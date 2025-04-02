# Documentation: GlobalExceptionHandler.java

## Overview
The `GlobalExceptionHandler` class is a centralized exception handling mechanism for a Spring Boot application. It uses the `@ControllerAdvice` annotation to intercept exceptions thrown by controllers and provide custom responses. This approach ensures consistent error handling across the application.

## Features
- Handles specific exceptions such as `ConstraintViolationException` and `IllegalArgumentException`.
- Provides a fallback mechanism for handling generic exceptions.
- Returns meaningful HTTP responses with appropriate status codes and error messages.

## Class Details

### Annotations
| Annotation         | Purpose                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `@ControllerAdvice`| Indicates that this class provides global exception handling for controllers. |
| `@ExceptionHandler`| Specifies the type of exception to be handled by the annotated method. |

### Methods

#### 1. `handleConstraintViolationException`
Handles exceptions of type `ConstraintViolationException`.

| Aspect                | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| Input Parameter       | `ConstraintViolationException ex`                                      |
| HTTP Status Code      | `400 BAD_REQUEST`                                                     |
| Response Body         | An instance of `ErrorResponse` containing the status and validation error message. |
| Purpose               | Used to handle validation errors, typically arising from constraints on input data. |

#### 2. `handleIllegalArgumentException`
Handles exceptions of type `IllegalArgumentException`.

| Aspect                | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| Input Parameter       | `IllegalArgumentException ex`                                          |
| HTTP Status Code      | `400 BAD_REQUEST`                                                     |
| Response Body         | An instance of `ErrorResponse` containing the status and exception message. |
| Purpose               | Used to handle cases where invalid arguments are passed to methods.    |

#### 3. `handleException`
Handles generic exceptions of type `Exception`.

| Aspect                | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| Input Parameter       | `Exception e`                                                          |
| HTTP Status Code      | `500 INTERNAL_SERVER_ERROR`                                           |
| Response Body         | An instance of `ErrorResponse` containing the status and a generic error message. |
| Purpose               | Acts as a fallback for unhandled exceptions, ensuring the application does not crash. |

## Insights
- **Centralized Error Handling**: The use of `@ControllerAdvice` ensures that all exceptions are handled in a single location, promoting cleaner and more maintainable code.
- **Custom Error Responses**: The class uses a custom `ErrorResponse` object to provide structured error information, which can be easily consumed by clients.
- **Scalability**: Additional exception handling methods can be added to cater to specific application needs.
- **Debugging**: The `handleException` method includes a call to `e.printStackTrace()`, which outputs the stack trace to the console. This is useful for debugging but may need to be replaced with proper logging in production environments.

## Dependencies
- **Spring Framework**: The class relies on Spring annotations (`@ControllerAdvice`, `@ExceptionHandler`) and `ResponseEntity` for exception handling.
- **Jakarta Validation**: The `ConstraintViolationException` is part of the Jakarta Validation API, used for validating input data.

## ErrorResponse Class
The `ErrorResponse` class is assumed to be a custom data structure used to encapsulate error details. It likely contains fields such as:
- `status`: HTTP status code as a string.
- `message`: A descriptive error message.

This class is essential for providing consistent error responses across the application.
