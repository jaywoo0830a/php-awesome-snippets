# Tag & String Block Snippets (PHP 8.x)

This file contains snippets for **PHP opening tags, strict type headers, echo shorthand, heredoc, and nowdoc**.

---

## PHP Tags

### PHP open tag

* **Prefix**: `po`

```php
<?php
```

Standard PHP open tag (always preferred).

### PHP strict types header

* **Prefix**: `pstr`

```php
<?php
declare(strict_types=1);

$0
```

Open tag with `strict_types` declaration.
Best practice for modern PHP files.

### PHP echo short tag

* **Prefix**: `peco`

```php
<?= $variable ?>
```

Short echo syntax. Always enabled since PHP 5.4.

---

## Multi-line String Blocks

### PHP heredoc block

* **Prefix**: `pher`

```php
<?php
$text = <<<TXT
multi-line content with $var interpolation
TXT;
```

Interpolated multi-line string (supports variables).

### PHP nowdoc block

* **Prefix**: `pnow`

```php
<?php
$text = <<<'TXT'
multi-line raw content
TXT;
```

Raw multi-line string (no interpolation).

---

✅ This `tag.md` covers **file starts, strict typing, shorthand echo, and modern multi-line string syntax**.