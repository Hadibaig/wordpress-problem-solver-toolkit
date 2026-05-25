# Case 02 — WordPress Parse Error in functions.php (Fast Recovery Method)

**Category:** PHP Errors  
**Platform:** WordPress  
**File Affected:** functions.php  
**Difficulty:** Beginner — Intermediate  
**Status:** ✅ Resolved  

---

## ❗ Problem Summary

The WordPress site completely crashed after a code change in `functions.php`.

Symptoms:

- White screen / critical error
- wp-admin inaccessible
- No frontend output
- Error appeared immediately after editing theme file

---

## 🎯 Objective

Restore website access and fix PHP syntax error in `functions.php` without losing data or affecting database.

---

## 🔍 Diagnosis Steps

### Step 1 — Identify recent change

Checked last modification:

```
/wp-content/themes/active-theme/functions.php
```

Issue started immediately after adding custom PHP snippet.

---

### Step 2 — Enable debugging

In `wp-config.php`:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', true);
```

---

### Step 3 — Error output

Browser / debug log showed:

```
Parse error: syntax error, unexpected ';'
in functions.php on line 214
```

---

### Step 4 — Access via FTP / File Manager

Opened:

```
/wp-content/themes/active-theme/functions.php
```

Navigated to line mentioned in error.

---

### Step 5 — Root cause found

Broken PHP code:

```php
function custom_message() {
    echo "Hello World"
}
```

---

## ❌ Issue

Missing semicolon (`;`) after echo statement.

---

## ✅ Fix Applied

Corrected code:

```php
function custom_message() {
    echo "Hello World";
}
```

---

## 🚀 Result

- Site restored immediately
- wp-admin accessible again
- No further PHP errors
- Frontend working normally

---

## 🧠 Root Cause

PHP parse error due to syntax mistake in `functions.php`:

- Missing semicolon
- File executed before WordPress load completion
- Entire site blocked due to fatal compile-time error

---

## 🛠️ Fast Recovery Methods

### Method 1 — Fix via File Manager / FTP
Edit `functions.php` and remove/fix broken code.

---

### Method 2 — Rename theme folder

```
/wp-content/themes/active-theme/
→ active-theme-disabled
```

WordPress switches to default theme.

---

### Method 3 — Restore backup
Use hosting backup or version control rollback.

---

## ⚠️ Prevention Checklist

- Never edit production `functions.php` directly
- Always use staging environment
- Use child theme for custom code
- Validate PHP syntax before saving
- Keep regular backups
- Use code editor with linting (VS Code / PhpStorm)

---

## 📌 Key Insight

A single missing character in `functions.php` can bring down the entire WordPress site because:

- It loads on every request
- PHP stops execution on parse error
- WordPress cannot initialize

---

## 👨‍💻 Author

**Mirza Hadi**  
Full-Stack WordPress Developer & Technical Problem Solver  

🌐 https://hadi-mirza.com  
🔗 https://linkedin.com/in/hadibaig
