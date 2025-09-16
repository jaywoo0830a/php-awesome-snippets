# Control Structures Snippets (PHP 8.x)

This document covers snippets for **conditionals, loops, match expressions, error handling, and nullsafe operators**.

---

## Conditional Blocks

### If … endif

* **Prefix**: `ifen`

```php
if ($condition):
    // code...
endif;
```

### If … else … endif

* **Prefix**: `ifelen`

```php
if ($condition):
    // code...
else:
    // code...
endif;
```

### If … elseif … else … endif

* **Prefix**: `ifelifen`

```php
if ($condition):
    // code...
elseif ($other):
    // code...
else:
    // code...
endif;
```

### If block

* **Prefix**: `ifb`

```php
if ($condition) {
    // code...
}
```

### If … else

* **Prefix**: `ifel`

```php
if ($condition) {
    // code...
} else {
    // code...
}
```

### If … elseif … else

* **Prefix**: `ifelif`

```php
if ($condition) {
    // code...
} elseif ($other) {
    // code...
} else {
    // code...
}
```

---

## Switch / Case

### Switch block

* **Prefix**: `sw`

```php
switch ($var) {
    case 'one':
        // code...
        break;
    case 'two':
        // code...
        break;
    default:
        // code...
        break;
}
```

### Case statement

* **Prefix**: `cs`

```php
case 'label':
    // code...
    break;
```

---

## Ternary and Guard Clauses

### Ternary operator

* **Prefix**: `tern`

```php
$result = $condition ? $ifTrue : $ifFalse;
```

### Guard clause (early return)

* **Prefix**: `guard`

```php
if (!$condition) {
    return;
}
```

---

## Null Coalesce and Throw Expressions

### Null coalesce operator

* **Prefix**: `nco`

```php
$value = $expr ?? $default;
```

### Null coalesce assignment (PHP 7.4+)

* **Prefix**: `nca`

```php
$var ??= $default;
```

### Throw expression with ??

* **Prefix**: `throwcoalesce`

```php
$id = $data['id'] ?? throw new InvalidArgumentException('Missing id');
```

### Throw expression in ternary

* **Prefix**: `throwtern`

```php
$result = $condition ? $ok : throw new RuntimeException('Error');
```

---

## Match Expressions (PHP 8.0+)

### Simple match

* **Prefix**: `match`

```php
$result = match ($expr) {
    CaseA => ValueA,
    CaseB => ValueB,
    default => DefaultValue,
};
```

### Match with boolean guards

* **Prefix**: `matchtrue`

```php
$result = match (true) {
    $a > 10 => 'big',
    $a < 5 => 'small',
    default => 'medium',
};
```

### Match with function call result

* **Prefix**: `matchfn`

```php
$message = match (httpStatus()) {
    200, 201, 204 => 'Success',
    400, 404 => 'Client Error',
    500, 502, 503 => 'Server Error',
    default => 'Unknown',
};
```

---

## Nullsafe Operator

### Nullsafe chain

* **Prefix**: `nullsafe`

```php
$value = $obj?->getter()?->field ?? 'n/a';
```

---

## Loops

### Foreach (key => value)

* **Prefix**: `fe`

```php
foreach ($items as $key => $value) {
    // code...
}
```

### Foreach (by reference)

* **Prefix**: `fer`

```php
foreach ($items as &$value) {
    // mutate value...
}
```

### Foreach destructuring (numeric list)

* **Prefix**: `fedestruct`

```php
foreach ($items as [$first, $second]) {
    // code...
}
```

### Foreach destructuring (assoc keys)

* **Prefix**: `fedestructa`

```php
foreach ($rows as ['id' => $id, 'name' => $name]) {
    // code...
}
```

### For loop

* **Prefix**: `for`

```php
for ($i = 0; $i < $n; $i++) {
    // code...
}
```

### While loop

* **Prefix**: `while`

```php
while ($condition) {
    // code...
}
```

### Do … while loop

* **Prefix**: `dowhile`

```php
do {
    // code...
} while ($condition);
```

---

## Error Handling

### Try / catch (Throwable)

* **Prefix**: `tryc`

```php
try {
    // code...
} catch (Throwable $e) {
    // handle error
}
```

### Try / multi-catch (union types)

* **Prefix**: `trymc`

```php
try {
    // code...
} catch (InvalidArgumentException|RuntimeException $e) {
    // handle expected failures
}
```

### Try / catch / finally

* **Prefix**: `trycf`

```php
try {
    // code...
} catch (Exception $e) {
    // handle error
} finally {
    // cleanup
}
```

---

## Summary

* Covers **if/else, switch, ternary, match**, and **guard clauses**.
* Includes **loops**: foreach, for, while, do-while.
* Adds **modern PHP 8.x features**: nullsafe operator, throw expressions, null coalesce assignment, match expressions, union-type catch.
* Ensures code is **clean, safe, and expressive**.