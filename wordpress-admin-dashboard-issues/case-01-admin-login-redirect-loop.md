# Case 01 — WordPress Admin Login Redirect Loop (wp-admin Keeps Redirecting to Login Page)

**Category:** WordPress Admin Dashboard Issues  
**Platform:** WordPress  
**Difficulty:** Intermediate — Advanced  
**Status:** ✅ Resolved

---

## ❗ The Symptom

User enters correct credentials on the WordPress login page.

WordPress accepts the login successfully, but instead of opening the dashboard, it redirects back to the login page again.

This creates an infinite loop:

- Login page → Accepts credentials → Redirects back to login page
- wp-admin inaccessible
- No error message displayed
- Session never persists

---

## 🎯 Objective

Identify why WordPress authentication succeeds but fails to maintain admin session, and break the redirect loop safely.

---

# 🔍 Diagnosis Process

---

## Step 1 — Browser Cache & Cookies Check

Tested:
- normal browser session
- incognito/private mode

Result:
- issue persisted in both environments

✔ Eliminated browser-side cookie corruption

---

## Step 2 — Verify WordPress URL Configuration

Checked in `wp-config.php` and database:

```php
define('WP_HOME', 'https://example.com');
define('WP_SITEURL', 'https://example.com');
```

Also verified in:

```bash
wp_options table:
- siteurl
- home
```

---

## 🎯 Found Issue

Mismatch between:
- HTTP vs HTTPS
- www vs non-www version

This causes authentication cookies to be invalid after login.

---

## Step 3 — Check COOKIE_DOMAIN Configuration

Found in `wp-config.php`:

```php
define('COOKIE_DOMAIN', 'www.example.com');
```

But actual site used:

```bash
example.com
```

Without www.

This caused WordPress to set cookies for a different domain scope.

---

## ✅ Fix Applied

Replaced with:

```php
define('COOKIE_DOMAIN', '');
```

✔ Allows WordPress to auto-detect correct domain  
✔ Fixes cookie mismatch issue  

---

## Step 4 — Clear Cache Layers

Cleared:

- WordPress cache plugin
- server-side cache
- browser cache

Also temporarily renamed:

```bash
/wp-content/cache/
```

---

## Step 5 — Plugin Conflict Check

Renamed plugins folder:

```bash
/wp-content/plugins/
```

to:

```bash
/wp-content/plugins-disabled/
```

Result:
✔ Login worked correctly

---

## 🎯 Root Cause Identified

A security plugin was causing:

- forced redirect rules
- SSL enforcement conflicts
- login session interference

---

## Step 6 — Check .htaccess Redirect Rules

Found conflicting rule:

```apache
RewriteRule ^wp-admin/$ /login/ [R=301,L]
```

This created a redirect loop with WordPress authentication system.

---

## Step 7 — SSL / HTTPS Configuration Check

Verified:

```php
define('FORCE_SSL_ADMIN', true);
```

Also ensured correct handling for proxy environments:

```php
if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) 
    && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
    $_SERVER['HTTPS'] = 'on';
}
```

---

# 🎯 Final Root Cause

The issue was caused by a combination of:

- COOKIE_DOMAIN mismatch
- Security plugin redirect conflict
- .htaccess redirect rule interference
- Cache layer storing incorrect login state

---

# ✅ Final Fix Summary

- Set `COOKIE_DOMAIN` to empty string
- Removed conflicting .htaccess redirect rule
- Disabled conflicting security plugin temporarily
- Cleared all cache layers
- Verified HTTPS configuration consistency

---

# 📌 Key Insight

The WordPress admin login redirect loop is NOT a login failure.

It is a **session persistence failure**, usually caused by:

- cookies not being stored correctly
- redirects interfering with authentication flow
- conflicting security/caching rules

WordPress successfully authenticates the user, but cannot maintain session state.

---

# 🧠 Prevention Checklist

To avoid this issue in future:

- Keep site URL consistent (HTTP/HTTPS, www/non-www)
- Avoid multiple redirect plugins
- Exclude wp-login.php and wp-admin from caching
- Test security plugins carefully
- Avoid custom login redirect logic without fallback
- Always verify COOKIE_DOMAIN behavior

---

# 💡 Final Thought

Most WordPress login loops are not complex bugs — they are configuration conflicts.

A structured debugging approach always resolves the issue faster than random plugin disabling.

---

*By [Mirza Hadi](https://hadi-mirza.com) —  
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
