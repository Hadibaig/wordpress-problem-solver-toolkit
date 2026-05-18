# Case 01 — White Screen of Death: PHP Memory Limit

**Category:** White Screen of Death (WSOD)  
**Platform:** WordPress  
**Difficulty:** Beginner — Intermediate  
**Time to Diagnose:** 15 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Client reported their WordPress website was showing
a completely blank white screen — no error message,
no text, nothing at all.

The issue appeared suddenly without any obvious cause.
The WordPress admin dashboard was also inaccessible
showing the same blank white screen.

---

## 🔍 Diagnosis Steps

**Step 1 — Check if it is a frontend or full site issue**

Tried accessing:
- The homepage → white screen
- /wp-admin → white screen
- /wp-login.php → white screen ✅ loaded fine

Since wp-login.php loaded, the server was running.
The problem was inside WordPress itself, not the server.

**Step 2 — Enable WordPress debug mode**

Added these lines to wp-config.php via FTP/cPanel
file manager:

```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_LOG', true );
define( 'WP_DEBUG_DISPLAY', false );
```

This writes errors to /wp-content/debug.log
without showing them publicly on the site.

**Step 3 — Read the debug log**

Opened /wp-content/debug.log and found:

Fatal error: Allowed memory size of 67108864 bytes
exhausted (tried to allocate 20480 bytes) in
/wp-includes/class-wp.php on line 812

Memory limit was set to **64MB** — too low for
the plugins this site was running.

**Step 4 — Confirm the current memory limit**

Added this temporary file to the root directory
to confirm PHP memory settings:

```php
<?php echo ini_get('memory_limit'); ?>
```

Confirmed: **64M** — the default on this shared host.

---

## 🎯 Root Cause

The hosting server had a default PHP memory limit
of 64MB. The combination of plugins installed on
this site — particularly WooCommerce, a slider plugin,
and a heavy theme — required more memory than
was available.

When WordPress tried to load all of them together
it ran out of memory and produced a blank white
screen instead of an error message.

---

## ✅ The Fix

**Method 1 — via wp-config.php** *(recommended)*

Added this line to wp-config.php above the line
that says "That's all, stop editing!":

```php
define( 'WP_MEMORY_LIMIT', '256M' );
```

**Method 2 — via .htaccess** *(if Method 1 fails)*

```apache
php_value memory_limit 256M
```

**Method 3 — via php.ini** *(if hosting allows it)*

```ini
memory_limit = 256M
```

After applying Method 1 the white screen
disappeared immediately and the site loaded normally.

**Cleanup:**
- Removed the temporary PHP test file from root
- Disabled WP_DEBUG after confirming fix
- Recommended client upgrade to a better hosting
  plan to prevent recurrence

---

## 💡 Lesson

A white screen with no error message almost always
means one of three things:

1. PHP memory limit exhausted ← this case
2. Fatal PHP error in a plugin or theme
3. Corrupted .htaccess file

Always enable WP_DEBUG as your very first step
when diagnosing WSOD — it turns an invisible problem
into a readable error message and cuts diagnosis
time from hours to minutes.

**Never leave WP_DEBUG enabled on a live site
after fixing the issue.**

---

*By [Mirza Hadi](https://hadi-mirza.com) — 
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
