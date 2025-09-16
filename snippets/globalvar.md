# Global Variable & Input Handling Snippets (PHP 8.x)

This document provides safe alternatives to legacy superglobals (`$_GET`, `$_POST`, etc.), using `filter_input`, secure cookie/session handling, validation helpers, and PHP 8.x+ features.

---

## Input Handling

### GET parameter (string sanitize)

* **Prefix**: `in.get`

```php
$value = filter_input(INPUT_GET, 'key', FILTER_UNSAFE_RAW, [
    'flags' => FILTER_FLAG_NO_ENCODE_QUOTES,
]); // sanitize/escape later at output
```

### GET parameter (validate int)

* **Prefix**: `in.geti`

```php
$id = filter_input(INPUT_GET, 'id', FILTER_VALIDATE_INT);
if ($id === false || $id === null) {
    throw new InvalidArgumentException('Invalid id');
}
```

### POST parameter (string sanitize)

* **Prefix**: `in.post`

```php
$value = filter_input(INPUT_POST, 'key', FILTER_UNSAFE_RAW, [
    'flags' => FILTER_FLAG_NO_ENCODE_QUOTES,
]);
```

### Batch input array

* **Prefix**: `in.array`

```php
$data = filter_input_array(INPUT_POST, [
    'id'    => FILTER_VALIDATE_INT,
    'email' => FILTER_VALIDATE_EMAIL,
    'name'  => FILTER_UNSAFE_RAW,
]);
if ($data === null) {
    throw new RuntimeException('No input');
}
```

### JSON input (PHP 8.3+)

* **Prefix**: `in.json`

```php
$raw = file_get_contents('php://input') ?: '';
if (!function_exists('json_validate') || !json_validate($raw)) {
    throw new InvalidArgumentException('Invalid JSON payload');
}
$payload = json_decode($raw, true, 512, JSON_THROW_ON_ERROR);
```

### Require param or throw (PHP 8.0+)

* **Prefix**: `in.require`

```php
$id = filter_input(INPUT_GET, 'id', FILTER_VALIDATE_INT)
    ?? throw new InvalidArgumentException('Missing or invalid id');
```

---

## Cookie Handling

### Cookie read

* **Prefix**: `cookie.get`

```php
$val = filter_input(INPUT_COOKIE, 'name', FILTER_UNSAFE_RAW) ?? null;
```

### Cookie set (with options)

* **Prefix**: `cookie.set`

```php
setcookie('name', $value, [
    'expires'  => time() + 86400,
    'path'     => '/',
    'domain'   => null,
    'secure'   => true,
    'httponly' => true,
    'samesite' => 'Lax',
]);
```

---

## Session Handling

### Start session (secure options)

* **Prefix**: `session.start`

```php
session_start([
    'cookie_secure'   => true,
    'cookie_httponly' => true,
    'cookie_samesite' => 'Lax',
]);
```

### Session get/set helper

* **Prefix**: `session.getset`

```php
// get
$value = $_SESSION['key'] ?? null;
// set
$_SESSION['key'] = $value;
```

---

## Environment & Server

### Env read with default

* **Prefix**: `env.get`

```php
$val = getenv('KEY') !== false ? getenv('KEY') : null;
```

### Server param via filter\_input

* **Prefix**: `server.get`

```php
$ua = filter_input(INPUT_SERVER, 'HTTP_USER_AGENT', FILTER_UNSAFE_RAW) ?? '';
```

---

## Validation Helpers

### Validate email

* **Prefix**: `val.email`

```php
$email = filter_var($input, FILTER_VALIDATE_EMAIL);
if ($email === false) {
    throw new InvalidArgumentException('Invalid email');
}
```

### Validate URL

* **Prefix**: `val.url`

```php
$url = filter_var(
    $input,
    FILTER_VALIDATE_URL,
    FILTER_FLAG_SCHEME_REQUIRED | FILTER_FLAG_HOST_REQUIRED
);
if ($url === false) {
    throw new InvalidArgumentException('Invalid URL');
}
```

---

## File Uploads

### Safe file upload with finfo

* **Prefix**: `upload.safe`

```php
if (!isset($_FILES['file']) || $_FILES['file']['error'] !== UPLOAD_ERR_OK) {
    throw new RuntimeException('Upload failed');
}
$tmp  = $_FILES['file']['tmp_name'];
$name = basename($_FILES['file']['name']);
$dst  = __DIR__ . '/uploads/' . $name;

$finfo = new finfo(FILEINFO_MIME_TYPE);
$mime = $finfo->file($tmp) ?: 'application/octet-stream';
// TODO: allowlist check for $mime

if (!move_uploaded_file($tmp, $dst)) {
    throw new RuntimeException('Failed to move uploaded file');
}
```

---

## Security Utilities

### CSRF token (Randomizer + session)

* **Prefix**: `csrf.make`

```php
use Random\Randomizer;
if (session_status() !== PHP_SESSION_ACTIVE) {
    session_start();
}
$rnd = new Randomizer();
$token = bin2hex($rnd->getBytes(32));
$_SESSION['csrf_token'] = $token;
```

---

## Summary

* Provides **safe input handling** with `filter_input` instead of raw superglobals.
* Includes **secure cookie/session options**.
* Adds **modern PHP 8.x+ features**: throw expressions, `json_validate`, `Random\Randomizer`.
* Encourages **defensive coding** for validation, uploads, and CSRF protection.