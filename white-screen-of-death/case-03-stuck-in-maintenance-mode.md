# Case 03 — WordPress Stuck in Maintenance Mode After Update

**Category:** White Screen of Death (WSOD / Maintenance Mode Issue)  
**Platform:** WordPress  
**Difficulty:** Beginner  
**Time to Diagnose:** 5–10 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

After updating plugins or WordPress core, the site shows:

> “Briefly unavailable for scheduled maintenance. Check back in a minute.”

But the message never disappears.

- Frontend inaccessible
- wp-admin not loading properly
- Site stuck indefinitely in maintenance mode

---

## 🔍 Diagnosis Steps

### Step 1 — Understand what happened

WordPress creates a temporary file during updates:

```bash
.maintenance
```

If the update process is interrupted, this file is not removed.

---

### Step 2 — Check root directory

Connected via FTP / File Manager and found:

```bash
/.maintenance
```

File still exists in root directory.

---

### Step 3 — Verify cause

This happens when:
- Plugin update crashes mid-process
- Server timeout occurs during update
- Browser closed during core update
- Multiple updates triggered simultaneously

---

## 🎯 Root Cause

WordPress update process was interrupted, leaving behind:

```bash
.maintenance
```

This file forces maintenance mode until removed.

---

## ✅ The Fix

### Fix 1 — Remove maintenance file

Deleted file from root directory:

```bash
/.maintenance
```

---

### Fix 2 — Reload site

After deletion:
- Frontend restored immediately
- wp-admin accessible again

---

## ⚠️ Important Warning

Never manually interrupt updates in WordPress.

If update is running:
- wait until completion
- avoid refreshing or closing browser

---

## 💡 Prevention Tips

- Always update plugins one by one
- Avoid bulk updates on slow servers
- Use staging environment for major updates
- Ensure stable server timeout settings
- Keep backup before updates

---

## 💡 Lesson

Maintenance mode is not an error — it is a safety lock.

But when update process breaks midway:
- lock never releases automatically
- manual removal is required

A simple hidden file can block an entire website.

---

*By [Mirza Hadi](https://hadi-mirza.com) —  
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
