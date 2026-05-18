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
