# Case 03 — llms.txt File Not Generating or Not Detected for SEO

**Category:** Technical SEO  
**Platform:** WordPress (SEO Plugins / Custom Implementation)  
**Difficulty:** Intermediate — Advanced  
**Time to Diagnose:** 40 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Client implemented `llms.txt` file for AI/SEO optimization, but:

- File not accessible at `/llms.txt`
- SEO plugin not generating file
- Google and AI tools not detecting content

---

## 🔍 Diagnosis Steps

### Step 1 — Checked URL directly

Tested:

```bash
https://example.com/llms.txt
```

Result:
- 404 Not Found

---

### Step 2 — Checked plugin settings

Verified SEO plugin configuration:
- llms.txt feature enabled (but not active output)
- No rewrite rule created

---

### Step 3 — Checked server rewrite rules

Inspected `.htaccess`:

Found missing rule for custom text endpoint handling.

---

### Step 4 — Tested file existence

Checked root directory:

- llms.txt file NOT present physically
- No dynamic generator hook active

---

## 🎯 Root Cause

Missing implementation layer:

- SEO plugin only enabled setting (UI feature)
- No actual file generation or rewrite rule
- Server not configured to serve `/llms.txt`

---

## ✅ The Fix

### Fix 1 — Manually created file

Created file in root:

```bash
/llms.txt
```

---

### Fix 2 — Added structured SEO content

Example:

```txt
This website provides WordPress development, SEO optimization,
technical troubleshooting, and full-stack web solutions.

Key areas:
- WordPress Development
- Technical SEO
- WooCommerce Fixes
- Performance Optimization
```

---

### Fix 3 — Verified accessibility

Tested:

```bash
https://example.com/llms.txt
```

Result:
✔ File now accessible and indexable

---

## 💡 Lesson

Many SEO plugins "claim" support for emerging standards like:

- llms.txt
- AI crawling optimization files

But in reality:

- They often do NOT generate physical files
- Or require manual server configuration

Always verify:
✔ file exists physically  
✔ URL is accessible  
✔ not just enabled in plugin UI  

---

## 📌 Final Insight

SEO is not just configuration — it is implementation verification.

If a file is not physically accessible, it does not exist for crawlers or AI systems.

---

*By [Mirza Hadi](https://hadi-mirza.com) —  
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
