# Function Snippets (PHP 8.x)

This document summarizes snippets for **functions, closures, arrow functions, attributes, and advanced PHP 8.x features**.

---

## Basic Functions

### Function

* **Prefix**: `fn`
* **Description**: Standard function with typed param and return

```php
function func_name(Type $arg): void {
    // code...
}
```

### Anonymous function

* **Prefix**: `fna`
* **Description**: Simple anonymous function

```php
function (Type $arg): void {
    // code...
}
```

### Anonymous function with `use`

* **Prefix**: `fnu`
* **Description**: Closure capturing external variables

```php
function (Type $arg) use ($vars): void {
    // code...
}
```

---

## Modern PHP 8.x Function Features

### Function with union types

* **Prefix**: `fnunion`

```php
function normalize(int|string|array $value): array {
    return is_array($value) ? $value : [$value];
}
```

### Function with nullable param & return

* **Prefix**: `fnnullable`

```php
function maybeFormat(?string $text): ?string {
    return $text !== null ? trim($text) : null;
}
```

### Function with `mixed` param

* **Prefix**: `fnmixed`

```php
function debugDump(mixed $value): void {
    var_dump($value);
}
```

### Variadic function

* **Prefix**: `fnvar`

```php
function sum(int ...$xs): int {
    return array_sum($xs);
}
```

### Arrow function (short closure)

* **Prefix**: `afn`

```php
$fn = fn(Type $x) => $expr;
```

### First-class callable (PHP 8.1+)

* **Prefix**: `fcc`

```php
$call = strtoupper(...);
$result = array_map($call, $items);
```

### Function with attributes

* **Prefix**: `fnattr`

```php
#[Route('GET', '/health')]
function healthCheck(): array {
    return ['status' => 'ok'];
}
```

### Function using throw expression

* **Prefix**: `fnthrexpr`

```php
function requireId(array $data): int {
    $id = $data['id'] ?? throw new InvalidArgumentException('Missing id');
    return (int) $id;
}
```

---

## Generators and Higher-Order Functions

### Generator function

* **Prefix**: `fngen`

```php
function rangeInclusive(int $start, int $end): Generator {
    for ($i = $start; $i <= $end; $i++) {
        yield $i;
    }
}
```

### Higher-order function (returns Closure)

* **Prefix**: `fnhof`

```php
function multiplier(int $k): Closure {
    return function (int $x): int {
        return $k * $x;
    };
}
```

---

## Named Arguments and Advanced Types

### Named arguments example

* **Prefix**: `fnnamed`

```php
function connect(string $host, int $port = 3306, bool $ssl = false): void {
    // ...
}

connect(host: 'localhost', port: 3306, ssl: true);
```

### Intersection types (PHP 8.1+)

* **Prefix**: `fninter`

```php
function consume(Traversable&Countable $collection): int {
    return count(iterator_to_array($collection));
}
```

### Never return type (PHP 8.1+)

* **Prefix**: `fnnever`

```php
function panic(string $message): never {
    throw new RuntimeException($message);
}
```

---

## Error-Handled Functions

### Function with try/catch

* **Prefix**: `fntry`

```php
function runSafe(int $x): int {
    try {
        return abs($x);
    } catch (Throwable $e) {
        // handle or rethrow
        throw $e;
    }
}
```

---

## File-Level Boilerplate

### Function with strict\_types + namespace

* **Prefix**: `fnfile`

```php
<?php
declare(strict_types=1);

namespace App\Support;

function helper(string $name): string {
    return "Hello, $name";
}
```

---

## Summary

* Provides **basic functions, anonymous functions, closures**.
* Supports **PHP 8.0+ features**: union types, nullable, mixed, attributes, throw expressions, named arguments.
* Adds **PHP 8.1+ features**: first-class callables, intersection types, never return type.
* Includes **generators, higher-order functions, and namespace boilerplate**.