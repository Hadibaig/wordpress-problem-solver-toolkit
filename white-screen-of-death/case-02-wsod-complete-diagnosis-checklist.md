# Case 02 — WordPress White Screen of Death Complete Diagnosis Checklist

**Category:** White Screen of Death (WSOD)  
**Platform:** WordPress  
**Difficulty:** Intermediate — Advanced  
**Time to Diagnose:** Varies by root cause  
**Status:** ✅ Troubleshooting Framework Established

---

## ❗ The Symptom

No error message.  
No warning.  
Just a completely blank white screen.

The WordPress White Screen of Death (WSOD) is one of the most alarming issues a developer or client can face because it often appears without explanation and can lock access to both the frontend and wp-admin dashboard.

---

## 🎯 Objective

The goal was not just fixing one isolated issue, but creating a systematic diagnosis process that works across:

- Plugin conflicts
- Theme errors
- PHP fatal errors
- Memory exhaustion
- Database issues
- Hosting/server problems
- Corrupted WordPress core files

---

# 🔍 Complete Diagnosis Checklist

---

## Step 1 — Establish Scope Before Touching Anything

First determine:

- Is frontend affected or admin too?
- Is it sitewide or page-specific?
- Did it happen after:
  - plugin update?
  - theme edit?
  - migration?
  - PHP version change?
- Is it live, staging, or localhost?

This immediately narrows diagnosis direction.

---

## Step 2 — Enable WordPress Debug Mode

Added to `wp-config.php`:

```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', true);
@ini_set('display_errors', 1);
```

This exposes hidden fatal errors and writes logs to:

```bash
/wp-content/debug.log
```

---

## Step 3 — Check PHP Memory Limit

Most common WSOD cause.

Increased memory via:

```php
define('WP_MEMORY_LIMIT', '256M');
```

Alternative methods:

### php.ini

```ini
memory_limit = 256M
```

### .htaccess

```apache
php_value memory_limit 256M
```

---

## Step 4 — Deactivate All Plugins

If admin accessible:
- Bulk deactivate plugins

If admin inaccessible:
- Rename plugins folder:

```bash
/wp-content/plugins/
```

to:

```bash
/wp-content/plugins-disabled/
```

Then reactivate one-by-one until issue returns.

---

## Step 5 — Switch to Default Theme

Renamed active theme folder:

```bash
/wp-content/themes/active-theme/
```

to:

```bash
/wp-content/themes/active-theme-disabled/
```

WordPress automatically loaded default fallback theme.

---

## Step 6 — Check PHP Syntax Errors

Common issues found in real projects:

### Missing semicolon

```php
echo "Hello"
```

### Mismatched quotes

```php
$var = "test';
```

### Missing closing bracket

```php
function test() {
```

### Broken PHP opening tag

```php
< ?php
```

---

## Step 7 — Verify PHP Version Compatibility

Checked:
- cPanel PHP Manager
- Site Health
- phpinfo()

Common issues:
- Older plugins incompatible with PHP 8.x
- Deprecated functions
- Strict type handling issues

---

## Step 8 — Replace Corrupted WordPress Core Files

Downloaded fresh WordPress copy from:

```bash
wordpress.org
```

Replaced:
- `/wp-admin/`
- `/wp-includes/`

Without touching:
- `/wp-content/`
- `wp-config.php`

---

## Step 9 — Check .htaccess File

Renamed:

```bash
.htaccess
```

to:

```bash
.htaccess-old
```

Generated fresh file from:
- Settings → Permalinks → Save Changes

---

## Step 10 — Check Database Integrity

Verified credentials in `wp-config.php`:

```php
DB_NAME
DB_USER
DB_PASSWORD
DB_HOST
```

Enabled temporary repair:

```php
define('WP_ALLOW_REPAIR', true);
```

Then visited:

```bash
/wp-admin/maint/repair.php
```

---

## Step 11 — Review Server Error Logs

Checked:
- Apache logs
- Nginx logs
- cPanel error logs

Found additional:
- timeout errors
- resource limits
- server-level PHP crashes

---

# ⚠️ Common Real-World WSOD Causes

Most real client cases usually traced back to:

- Plugin conflict after update
- Theme syntax error
- PHP memory exhaustion
- Incompatible PHP version
- Corrupted WordPress update
- Broken custom code snippet
- Database connection issue
- Misconfigured .htaccess

---

# 📌 Important File Permission Reference

Recommended permissions:

| Type | Permission |
|---|---|
| Files | 644 |
| Folders | 755 |
| wp-config.php | 600 or 640 |

Never use:
```bash
777
```

This creates major security risks.

---

# ✅ Prevention Checklist

To reduce future WSOD incidents:

- Use staging before updates
- Keep daily backups
- Maintain fallback default theme
- Monitor PHP compatibility
- Avoid direct live edits
- Use uptime monitoring

---

# 💡 Final Lesson

The White Screen of Death looks catastrophic but is usually recoverable.

The difference between:
- a 5-minute fix
and
- a 5-hour nightmare

is almost always systematic diagnosis.

Random guessing wastes time. Structured troubleshooting solves problems faster.

A developer's real skill is not avoiding problems completely — it is knowing exactly where to look when things break.

---

*By [Mirza Hadi](https://hadi-mirza.com) —  
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
