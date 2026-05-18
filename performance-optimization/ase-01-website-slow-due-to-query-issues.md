# Case 01 — Website Slow Due to Database Query Overload

**Category:** Performance Optimization  
**Platform:** WordPress + WooCommerce  
**Difficulty:** Intermediate — Advanced  
**Time to Diagnose:** 45 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Website loading time increased significantly:

- Admin dashboard very slow
- Product pages taking 6–8 seconds
- High CPU usage on hosting

---

## 🔍 Diagnosis Steps

Installed Query Monitor plugin and found:

- Heavy queries on `wp_postmeta`
- Multiple uncached WooCommerce queries
- Repeated meta queries on every page load

---

## 🎯 Root Cause

Theme was using inefficient query:

```php
get_posts(array(
    'meta_query' => array(...)
));
```

Without caching or optimization.

---

## ✅ The Fix

### Fix 1 — Added Transient Cache

```php
$products = get_transient('cached_products');

if (!$products) {
    $products = get_posts([...]);

    set_transient('cached_products', $products, 12 * HOUR_IN_SECONDS);
}
```

---

### Fix 2 — Reduced Meta Queries

Optimized query structure to avoid repeated `meta_query` calls.

---

## 💡 Result

- Page load reduced from 7s → 2.1s
- CPU usage dropped significantly

---

## 💡 Lesson

Most WordPress slowdowns come from:
- unoptimized queries
- missing caching layer

- 
- *By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
