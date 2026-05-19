# Case 02 — FAQ Schema Not Detected in Google Search Results

**Category:** Technical SEO  
**Platform:** WordPress (RankMath / Yoast / Custom Schema)  
**Difficulty:** Intermediate  
**Time to Diagnose:** 30–45 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Client implemented FAQ sections on multiple pages, but:

- FAQ schema was not showing in Google Rich Results Test
- No rich snippets in search results
- Schema markup appeared in page source but not detected

---

## 🔍 Diagnosis Steps

### Step 1 — Checked page source

Found FAQ schema present:

```json
{
  "@type": "FAQPage",
  "mainEntity": [...]
}
```

So schema was actually being generated.

---

### Step 2 — Tested in Google Rich Results Tool

Google reported:

- “Page is not eligible for rich results”
- FAQ content ignored

---

### Step 3 — Identified conflict

Found multiple schema sources:

- RankMath FAQ schema
- Custom theme JSON-LD schema
- Elementor FAQ widget schema

👉 Result: Duplicate schema blocks on same page

---

### Step 4 — Verified HTML output

Page contained:
- 2 FAQ schema blocks
- Conflicting structured data types

Google ignores conflicting schema signals.

---

## 🎯 Root Cause

Multiple FAQ schema outputs from different sources:

- SEO plugin (RankMath / Yoast)
- Theme injected schema
- Elementor FAQ widget

This caused schema conflict and invalid structured data interpretation.

---

## ✅ The Fix

### Fix 1 — Keep only one schema source

Disabled duplicate schema from theme:

```php
remove_action('wp_head', 'theme_faq_schema');
```

---

### Fix 2 — Use single SEO plugin for schema

Kept only RankMath FAQ schema enabled.

---

### Fix 3 — Validated output again

Used:
- Google Rich Results Test
- Schema.org validator

Result:
✔ FAQ schema now detected correctly

---

## 💡 Lesson

Google does NOT penalize schema presence — it penalizes:

- duplicate schema
- conflicting structured data
- inconsistent markup sources

Always ensure **single source of truth for schema generation**.

---

*By [Mirza Hadi](https://hadi-mirza.com) —  
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
