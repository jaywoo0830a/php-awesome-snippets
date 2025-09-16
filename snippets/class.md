# Class & OOP Snippets (PHP 8.x)

This document summarizes the `class.json` snippet collection.
It covers **classes, interfaces, traits, enums, attributes, and modern PHP 8.x features**.

---

## Basic Classes

### Class

* **Prefix**: `cl`
* **Description**: Basic class block

```php
class ClassName
{
    // code...
}
```

### Class extends

* **Prefix**: `clx`
* **Description**: Class with inheritance

```php
class ChildClass extends BaseClass
{
    // code...
}
```

### Class implements

* **Prefix**: `cli`
* **Description**: Class implementing interfaces

```php
class Service implements SomeInterface
{
    // code...
}
```

### Class extends implements

* **Prefix**: `clxi`
* **Description**: Class with inheritance and interfaces

```php
class Repo extends Base implements Logger, ArrayAccess
{
    // code...
}
```

---

## Abstract / Final Classes

### Abstract class

* **Prefix**: `acl`
* **Description**: Abstract class definition

```php
abstract class AbstractService
{
    // code...
}
```

### Final class

* **Prefix**: `fcl`
* **Description**: Final class that cannot be extended

```php
final class ImmutableService
{
    // code...
}
```

---

## Interfaces & Traits

### Interface

* **Prefix**: `in`
* **Description**: Basic interface

```php
interface ServiceInterface
{
    // method signatures...
}
```

### Interface extends

* **Prefix**: `inx`
* **Description**: Interface extension

```php
interface AdvancedService extends ServiceInterface
{
    // extra signatures...
}
```

### Trait

* **Prefix**: `trt`
* **Description**: Reusable trait

```php
trait Loggable
{
    // shared code...
}
```

### Trait with requirement

* **Prefix**: `trtreq`
* **Description**: Trait requiring abstract method (dependency injection)

```php
trait Loggable
{
    abstract protected function logger(): Psr\Log\LoggerInterface;

    protected function info(string $message): void
    {
        $this->logger()->info($message);
    }
}
```

---

## Modern PHP 8.x Class Features

### Strict + namespace header

* **Prefix**: `cln`
* **Description**: File boilerplate with strict types and namespace

```php
<?php
declare(strict_types=1);

namespace App\Domain;

class User
{
    // code...
}
```

### Constructor Property Promotion (PHP 8.0+)

* **Prefix**: `clcpp`
* **Description**: DTO-like class with promoted constructor properties

```php
class User
{
    public function __construct(
        public string $id,
        public string $name,
        public ?string $email = null,
    ) {}
}
```

### Readonly class (PHP 8.2+)

* **Prefix**: `clro`
* **Description**: Immutable readonly class

```php
readonly class Point
{
    public function __construct(
        public int $x,
        public int $y
    ) {}
}
```

### Value Object

* **Prefix**: `vo`
* **Description**: Final readonly value object with equality

```php
final readonly class UserId
{
    public function __construct(
        public string $value
    ) {}

    public function equals(self $other): bool
    {
        return $this->value === $other->value;
    }
}
```

### Static Factory

* **Prefix**: `clfactory`
* **Description**: Private constructor with named static factories

```php
final class Token
{
    private function __construct(private string $value) {}

    public static function fromString(string $value): self
    {
        return new self($value);
    }

    public static function fromInt(int $n): self
    {
        return new self((string)$n);
    }

    public function value(): string
    {
        return $this->value;
    }
}
```

### Fluent Builder

* **Prefix**: `builder`
* **Description**: Builder pattern with static return type

```php
class Builder
{
    private array $parts = [];

    public function with(string $key, mixed $value): static
    {
        $this->parts[$key] = $value;
        return $this;
    }

    public function build(): array
    {
        return $this->parts;
    }
}
```

---

## Attributes

### Attribute class (PHP 8.0+)

* **Prefix**: `attr`
* **Description**: Define a custom attribute

```php
use Attribute;

#[Attribute(Attribute::TARGET_CLASS | Attribute::TARGET_METHOD)]
class Marker
{
    public function __construct(public int $level = 1) {}
}
```

### Attribute usage

* **Prefix**: `clattr`
* **Description**: Apply attribute to a class

```php
#[Marker(level: 2)]
class Service
{
    // code...
}
```

---

## Enums (PHP 8.1+)

### String-backed enum

* **Prefix**: `enum`
* **Description**: String-backed enum with helper method

```php
enum Status: string {
    case Draft = 'draft';
    case Published = 'published';
    case Archived = 'archived';

    public function isPublic(): bool
    {
        return $this === self::Published;
    }
}
```

### Pure enum

* **Prefix**: `enums`
* **Description**: Pure enum without backing type

```php
enum Direction {
    case North;
    case South;
    case East;
    case West;
}
```

---

## Properties

### Readonly property (PHP 8.1+)

* **Prefix**: `propreadonly`
* **Description**: Readonly property in a mutable class

```php
class Config
{
    public readonly string $dsn;

    public function __construct(string $dsn) {
        $this->dsn = $dsn;
    }
}
```

---

## Callables

### First-class callable usage (PHP 8.1+)

* **Prefix**: `callablefc`
* **Description**: First-class callable syntax

```php
$upper = strtoupper(...);
$result = array_map($upper, $items);
```

---

## Summary

* Includes **classic OOP structures**: class, interface, trait.
* Adds **modern PHP 8.x features**: property promotion, readonly classes, value objects, enums, attributes.
* Encourages **immutability, factories, builders, and first-class callables**.