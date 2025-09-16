# Statement Snippets (PHP 8.x)

This file contains snippets for **constants, requires, output, JSON handling, debugging, termination, file headers, and multi-line strings**.

---

## Constants

### Constant (prefer `const` over `define`)

* **Prefix**: `const`

```php
const NAME = 123;
```

Declare a constant inside class/namespace scope (preferred over `define`).

---

## Require & Autoload

### Require Composer autoload

* **Prefix**: `rqa`

```php
require_once __DIR__ . '/../vendor/autoload.php';
```

Require Composer autoloader (best practice).

### Require file

* **Prefix**: `rqr`

```php
require __DIR__ . '/path_to_filename.php';
```

Require a PHP file. Halts on failure (use instead of `include`).

### Require once file

* **Prefix**: `rqro`

```php
require_once __DIR__ . '/path_to_filename.php';
```

Require once, ensuring idempotency.

---

## Echo & Print

### Echo text

* **Prefix**: `eco`

```php
echo "text";
```

### Printf

* **Prefix**: `printf`

```php
printf("Hello %s\n", $name);
```

Formatted output.

### Sprintf assign

* **Prefix**: `sprintf`

```php
$out = sprintf("%s (%d)", $name, $count);
```

Format into a variable.

---

## JSON Handling

### Echo JSON response

* **Prefix**: `echo.json`

```php
header('Content-Type: application/json; charset=utf-8');
echo json_encode($data, JSON_THROW_ON_ERROR | JSON_UNESCAPED_UNICODE | JSON_UNESCAPED_SLASHES);
```

Safe JSON response with strict flags (PHP 8+).

### Decode JSON (strict)

* **Prefix**: `json.decode`

```php
$payload = json_decode($json, true, 512, JSON_THROW_ON_ERROR);
```

Throws exceptions instead of failing silently.

---

## Debugging

### var\_dump (quick debug)

* **Prefix**: `vd`

```php
var_dump($variable);
```

### var\_export (string)

* **Prefix**: `vx`

```php
echo var_export($variable, true);
```

### print\_r (string)

* **Prefix**: `pr`

```php
echo print_r($variable, true);
```

---

## Exit

### Exit with code

* **Prefix**: `exit`

```php
exit(0); // 0=success, non-zero=error
```

---

## File Headers

### Strict types header

* **Prefix**: `strict`

```php
<?php
declare(strict_types=1);
```

Enable strict typing at the top of the file (recommended).

---

## Multi-line Strings

### Nowdoc (raw multi-line)

* **Prefix**: `nowdoc`

```php
$text = <<<'TXT'
multi-line content
TXT;
```

Raw, no variable interpolation.

### Heredoc (interpolated multi-line)

* **Prefix**: `heredoc`

```php
$text = <<<TXT
Hello, $name
TXT;
```

Supports interpolation.

---

✅ This `statement.md` now fully covers modern **statements, includes, JSON, debugging, strict headers, and string blocks** in PHP 8+.