# Case 01 — PHP Parse Error Breaking WordPress Site

**Category:** PHP Errors  
**Platform:** WordPress  
**Difficulty:** Beginner — Intermediate  
**Time to Diagnose:** 10 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Website showing:

> Parse error: syntax error, unexpected ‘}’ in functions.php

- Entire site down
- Admin panel not accessible

---

## 🔍 Diagnosis Steps

Accessed server via FTP:
- Checked `functions.php`
- Found missing semicolon before closing bracket

---

## 🎯 Root Cause

Simple syntax mistake:

```php
echo "Hello World"
}
```

Missing semicolon caused PHP to break parsing.

---

## ✅ The Fix

Corrected code:

```php
echo "Hello World";
}
```

---

## 💡 Lesson

Most PHP errors in WordPress come from:
- missing semicolons
- unmatched brackets
- copy-paste code issues

- 
- *By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
