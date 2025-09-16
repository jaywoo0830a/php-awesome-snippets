# Loop Snippets (PHP 8.x)

This document summarizes loop-related snippets for **foreach, for, while, generators, and functional looping patterns**.

---

## Foreach Loops

### Foreach loop

* **Prefix**: `fore`

```php
foreach ($iterable as $item) {
    // code...
}
```

### Foreach with key => value

* **Prefix**: `forek`

```php
foreach ($iterable as $key => $item) {
    // code...
}
```

### Foreach by reference

* **Prefix**: `forer`

```php
foreach ($items as &$item) {
    // mutate in-place
}
```

### Foreach destructuring (numeric list)

* **Prefix**: `forelist`

```php
foreach ($pairs as [$a, $b]) {
    // code...
}
```

### Foreach destructuring (assoc keys)

* **Prefix**: `foreassoc`

```php
foreach ($rows as ['id' => $id, 'name' => $name]) {
    // code...
}
```

### Foreach enumerated (with index)

* **Prefix**: `forenum`

```php
foreach (array_values($items) as $i => $item) {
    // $i is 0..N index
}
```

---

## For Loops

### Classic for loop

* **Prefix**: `forl`

```php
for ($i = 0; $i < $limit; $i++) {
    // code...
}
```

### For with guard continue

* **Prefix**: `forg`

```php
for ($i = 0; $i < $n; $i++) {
    if (!$condition) {
        continue; // guard to reduce nesting
    }
    // code...
}
```

### Sliding window loop

* **Prefix**: `window`

```php
for ($i = 0, $n = count($items); $i + $k <= $n; $i++) {
    $window = array_slice($items, $i, $k);
    // process $window
}
```

---

## While Loops

### While loop

* **Prefix**: `wl`

```php
while ($condition) {
    // code...
}
```

### Do … while

* **Prefix**: `dowl`

```php
do {
    // code...
} while ($condition);
```

### While read line (fgets)

* **Prefix**: `wlfile`

```php
while (($line = fgets($fp)) !== false) {
    // process $line
}
```

### Loop with timeout (monotonic clock)

* **Prefix**: `looptimeout`

```php
$start = hrtime(true); // nanoseconds
while (true) {
    if ((hrtime(true) - $start) > 1_000_000_000) { // 1s
        break; // timeout
    }
    // work...
}
```

---

## Generators

### Generator (yield values)

* **Prefix**: `gen`

```php
function rangeInclusive(int $start, int $end): Generator {
    for ($i = $start; $i <= $end; $i++) {
        yield $i; // lazy sequence
    }
}
```

### Generator (yield from)

* **Prefix**: `genfrom`

```php
function flatten(iterable $it): Generator {
    foreach ($it as $chunk) {
        yield from $chunk;
    }
}
```

---

## Batch & Functional Loops

### Chunked loop (array\_chunk)

* **Prefix**: `chunk`

```php
foreach (array_chunk($items, 1000) as $chunk) {
    // process chunk
}
```

### Parallel loop (array\_map + callable)

* **Prefix**: `maploop`

```php
$fn = strtoupper(...); // first-class callable (PHP 8.1+)
$out = array_map($fn, $items);
```

---

## Summary

* Includes **foreach, for, while, do-while** loops.
* Supports **advanced destructuring, by-reference, enumerated loops**.
* Provides **generators** (`yield`, `yield from`) for lazy evaluation.
* Adds **functional batch processing** (`chunk`, `maploop`) and **sliding windows**.
* Demonstrates **timeout-safe loops** using `hrtime()`.