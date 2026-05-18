# Case 01 — WordPress Database Connection Failed

**Category:** Database Errors  
**Platform:** WordPress (MySQL)  
**Difficulty:** Intermediate  
**Time to Diagnose:** 30 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Website suddenly showed:

> Error establishing a database connection

- Frontend completely down
- wp-admin inaccessible
- No recent code changes reported by client

---

## 🔍 Diagnosis Steps

**Step 1 — Checked wp-config.php**

Verified database credentials:

```php
DB_NAME
DB_USER
DB_PASSWORD
DB_HOST
```

All values were correct.

---

**Step 2 — Tested database server response**

Used hosting panel phpMyAdmin → login worked fine.

So database server was running.

---

**Step 3 — Checked DB host configuration**

Found issue:

```php
DB_HOST = localhost
```

But hosting provider required:

```php
DB_HOST = 127.0.0.1
```

---

**Step 4 — Verified connection manually**

Created test PHP file:

```php
<?php
$connection = mysqli_connect("127.0.0.1", "user", "pass", "dbname");

if (!$connection) {
    die("Connection failed");
}
echo "Connected successfully";
?>
```

Connection succeeded.

---

## 🎯 Root Cause

Incorrect database host configuration after hosting migration.

The server no longer accepted `localhost` as valid DB host.

---

## ✅ The Fix

Updated:

```php
define('DB_HOST', '127.0.0.1');
```

Reloaded site → database connection restored immediately.

---

## 💡 Lesson

After migration or hosting changes:

- Always verify DB_HOST
- Never assume localhost works on all servers
- Test DB connection before debugging plugins/themes

- *By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
