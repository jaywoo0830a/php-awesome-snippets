# Error Handling Snippets (PHP 8.x)

This document covers snippets for **try/catch/finally, throw expressions, custom exceptions, and PHP 8.x improvements**.

---

## Try / Catch Blocks

### Try … catch

* **Prefix**: `tryc`
* **Description**: Basic try-catch block

```php
try {
    // code...
} catch (Throwable $e) {
    // handle error
}
```

### Try … catch … finally

* **Prefix**: `tryf`
* **Description**: Try-catch-finally with cleanup

```php
try {
    // code...
} catch (Throwable $e) {
    // handle error
} finally {
    // cleanup
}
```

### Catch

* **Prefix**: `cat`
* **Description**: Standalone catch block

```php
catch (Throwable $e) {
    // code...
}
```

### Finally

* **Prefix**: `fy`
* **Description**: Finally block only

```php
finally {
    // code...
}
```

---

## Throw Statements

### Throw new Exception

* **Prefix**: `thr`
* **Description**: Standard exception throw

```php
throw new SomeException("Error statement");
```

### Rethrow exception

* **Prefix**: `rethr`
* **Description**: Rethrow without losing original trace

```php
catch (Throwable $e) {
    throw; // rethrow
}
```

---

## Advanced Catch (PHP 8.0+)

### Multi-catch with union

* **Prefix**: `trymc`
* **Description**: Multi-catch with union types

```php
try {
    // code...
} catch (InvalidArgumentException|RuntimeException $e) {
    // handle expected errors
}
```

---

## Throw Expressions (PHP 8.0+)

### Throw expression with null coalesce

* **Prefix**: `thrnco`
* **Description**: Throw inline with `??`

```php
$value = $data['key'] ?? throw new InvalidArgumentException("Missing key");
```

### Throw expression (ternary)

* **Prefix**: `thrtern`
* **Description**: Throw in ternary false branch

```php
$result = $condition ? $okExpr : throw new RuntimeException("Error");
```

---

## Custom Exceptions

### Custom exception class

* **Prefix**: `exclass`
* **Description**: Define a reusable exception type

```php
class CustomException extends Exception {
    public function __construct(
        string $message = "Default message",
        int $code = 0,
        ?Throwable $previous = null
    ) {
        parent::__construct($message, $code, $previous);
    }
}
```

### DomainException with readonly property (PHP 8.1+)

* **Prefix**: `exreadonly`
* **Description**: Exception carrying extra readonly context

```php
final class DomainException extends RuntimeException {
    public function __construct(
        public readonly string $context,
        string $message = "Domain error"
    ) {
        parent::__construct($message);
    }
}
```

---

## Summary

* Covers **basic try/catch/finally usage**.
* Adds **modern PHP 8.x features**: union-type multi-catch, throw expressions, and readonly exception context.
* Encourages **custom domain exceptions** for expressive, domain-driven error handling.