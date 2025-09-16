# Method Snippets (PHP 8.x)

This document summarizes method-related snippets, including **constructors, visibility modifiers, static/final/abstract methods, advanced type features, and magic methods**.

---

## Constructors

### Public constructor

* **Prefix**: `pubc`

```php
public function __construct(Type $arg)
{
    // init...
}
```

### Private constructor (factory pattern)

* **Prefix**: `pric`

```php
private function __construct(Type $arg)
{
    // for static factories
}
```

### Protected constructor (inheritance)

* **Prefix**: `proc`

```php
protected function __construct(Type $arg)
{
    // for inheritance
}
```

---

## Public Methods

### Public method

* **Prefix**: `pubf`

```php
public function methodName(Type $arg): void
{
    // code...
}
```

### Public static method

* **Prefix**: `pubsf`

```php
public static function methodName(Type $arg): void
{
    // static code...
}
```

### Final public method

* **Prefix**: `fpubf`

```php
final public function methodName(Type $arg): void
{
    // code...
}
```

### Final public static method

* **Prefix**: `fpubsf`

```php
final public static function methodName(Type $arg): void
{
    // code...
}
```

### Abstract public method

* **Prefix**: `apubf`

```php
abstract public function methodName(Type $arg): void;
```

### Abstract public static method

* **Prefix**: `apubsf`

```php
abstract public static function methodName(Type $arg): void;
```

---

## Private Methods

### Private method

* **Prefix**: `prif`

```php
private function methodName(Type $arg): void
{
    // code...
}
```

### Private static method

* **Prefix**: `prisf`

```php
private static function methodName(Type $arg): void
{
    // code...
}
```

### Final private method

* **Prefix**: `fprif`

```php
final private function methodName(Type $arg): void
{
    // code...
}
```

### Final private static method

* **Prefix**: `fprisf`

```php
final private static function methodName(Type $arg): void
{
    // code...
}
```

---

## Protected Methods

### Protected method

* **Prefix**: `prof`

```php
protected function methodName(Type $arg): void
{
    // code...
}
```

### Protected static method

* **Prefix**: `prosf`

```php
protected static function methodName(Type $arg): void
{
    // code...
}
```

### Final protected method

* **Prefix**: `fprof`

```php
final protected function methodName(Type $arg): void
{
    // code...
}
```

### Final protected static method

* **Prefix**: `fprosf`

```php
final protected static function methodName(Type $arg): void
{
    // code...
}
```

### Abstract protected method

* **Prefix**: `aprof`

```php
abstract protected function methodName(Type $arg): void;
```

### Abstract protected static method

* **Prefix**: `aprosf`

```php
abstract protected static function methodName(Type $arg): void;
```

---

## Advanced Typed Methods

### Union types (PHP 8.0+)

* **Prefix**: `m.union`

```php
public function setValue(int|string|array $value): void
{
    // handle union types...
}
```

### Nullable param & return

* **Prefix**: `m.nullable`

```php
public function maybeFind(?string $id): ?Item
{
    // return null when not found
}
```

### Intersection types (PHP 8.1+)

* **Prefix**: `m.intersection`

```php
public function consume(Traversable&Countable $collection): int
{
    return count(iterator_to_array($collection));
}
```

### Never return type (PHP 8.1+)

* **Prefix**: `m.never`

```php
public function panic(string $message): never
{
    throw new RuntimeException($message);
}
```

---

## Fluent / Self / Parent Returns

### Static return (fluent API)

* **Prefix**: `m.staticret`

```php
public function with(string $key, mixed $value): static
{
    $this->$key = $value;
    return $this;
}
```

### Self return

* **Prefix**: `m.selfret`

```php
public function reset(): self
{
    // re-init and return $this
    return $this;
}
```

### Parent return

* **Prefix**: `m.parentret`

```php
public function factory(): parent
{
    // return parent instance
}
```

---

## Attributes & Expressions

### Method with attribute (PHP 8.0+)

* **Prefix**: `m.attr`

```php
#[Route('GET', '/ping')]
public function ping(): array
{
    return ['status' => 'ok'];
}
```

### Throw expression in method (PHP 8.0+)

* **Prefix**: `m.throwexpr`

```php
public function requireId(array $data): int
{
    $id = $data['id'] ?? throw new InvalidArgumentException('Missing id');
    return (int) $id;
}
```

---

## Magic Methods

### \_\_invoke

* **Prefix**: `m.invoke`

```php
public function __invoke(Type $arg): mixed
{
    // callable object entrypoint
}
```

### \_\_toString

* **Prefix**: `m.tostr`

```php
public function __toString(): string
{
    // return string representation
}
```

### \_\_get / \_\_set

* **Prefix**: `m.getset`

```php
public function __get(string $name): mixed
{
    // dynamic getter
    return null;
}

public function __set(string $name, mixed $value): void
{
    // dynamic setter
}
```

---

## Summary

* Full coverage for **public, private, protected, abstract, static, final** methods.
* Advanced typing: **union, nullable, intersection, never, static return, self/parent return**.
* Support for **attributes** and **throw expressions** (PHP 8.0+).
* Magic methods included: `__invoke`, `__toString`, `__get`, `__set`.