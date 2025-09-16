# Array Snippets (PHP 8.x)

This document describes the array-related snippets available in `array.json`.
All examples assume **PHP 8.0+**, including features like arrow functions, spread operator, `array_is_list`, and trailing commas.

---

## Basic Arrays

### Array

* **Prefix**: `arr`
* **Description**: Simple array block

```php
[$value1, $value2, $value3];
```

### Array key … value

* **Prefix**: `ark`
* **Description**: Key–value array block

```php
[
    'key1' => $value1,
    'key2' => $value2,
];
```

### Key … value

* **Prefix**: `kv`
* **Description**: Single key–value line

```php
'key' => $value,
```

### Array … value

* **Prefix**: `va`
* **Description**: Single array value line

```php
$value,
```

---

## PHP 8.x Array Extensions

### Multiline array (with trailing comma)

* **Prefix**: `arrm`
* **Description**: Multiline array, trailing comma for diff-friendly edits

```php
[
    $value1,
    $value2,
    $value3,
]
```

### Multiline assoc array (with trailing comma)

* **Prefix**: `arkm`
* **Description**: Multiline associative array

```php
[
    'id'   => $id,
    'name' => $name,
    'age'  => $age,
]
```

### Merge arrays via spread

* **Prefix**: `arrmerge`
* **Description**: Merge arrays (PHP 8.1+ also supports string keys)

```php
$merged = [...$base, ...$override];
```

### Unpack into function call

* **Prefix**: `arrpack`
* **Description**: Variadic unpack in function/method calls

```php
$result = fnName(...$args);
```

---

## Array Destructuring

### Numeric destructuring

* **Prefix**: `arrdestr`

```php
[$first, $second] = $array;
```

### Assoc destructuring

* **Prefix**: `arrdestra`

```php
['id' => $id, 'name' => $name] = $row;
```

---

## Array Functions and Manipulation

### array\_map + arrow function

* **Prefix**: `arrmap`

```php
$out = array_map(fn($x) => $x * 2, $items);
```

### array\_filter + reindex

* **Prefix**: `arrfilter`

```php
$out = array_values(array_filter($items, fn($x) => $x > 0));
```

### Sort by key with spaceship

* **Prefix**: `arrsort`

```php
usort($items, fn($a, $b) => ($a['score'] ?? null) <=> ($b['score'] ?? null));
```

### Group by key with reduce

* **Prefix**: `arrgroup`

```php
$grouped = array_reduce($items, function(array $carry, $item): array {
    $k = $item['category'];
    $carry[$k] ??= [];
    $carry[$k][] = $item;
    return $carry;
}, []);
```

### array\_is\_list (PHP 8.1+)

* **Prefix**: `arrisl`

```php
if (array_is_list($arr)) {
    // handle list
} else {
    // handle assoc array
}
```

### array\_column with default & reindex

* **Prefix**: `arrcol`

```php
$ids = array_values(array_filter(array_column($rows, 'id')));
```

---

## Pipeline Example

### Map → Filter → Reduce (concise)

* **Prefix**: `amfr`

```php
$result = array_reduce(
    array_filter(
        array_map(fn($x) => $x * 2, $items),
        fn($x) => $x > 10
    ),
    fn($carry, $x) => $carry + $x,
    0
);
```

---

## Summary

* Leverages **modern PHP 8.0+ features**: spread operator, arrow functions, `array_is_list`, and trailing commas.
* Covers **array creation, merging, destructuring, higher-order operations** (map/filter/reduce), and **pipeline patterns**.
* Designed for **clean, concise, and diff-friendly code**.