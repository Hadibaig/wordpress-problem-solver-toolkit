# Case 01 — DNS Not Updating After Domain Change

**Category:** Server Hosting  
**Platform:** Bluehost / GoDaddy / Hostinger  
**Difficulty:** Beginner — Intermediate  
**Time to Diagnose:** 60 minutes  
**Status:** ✅ Resolved

---

## ❗ The Symptom

Client changed hosting from GoDaddy to Bluehost:

- Website still showing old server
- New site not loading
- DNS changes not reflecting

---

## 🔍 Diagnosis Steps

Checked:
- DNS propagation status
- A record pointing to old IP
- TTL cache still active

---

## 🎯 Root Cause

DNS propagation delay + incorrect A record update.

---

## ✅ The Fix

- Updated A record to new server IP
- Reduced TTL value to 300 seconds
- Flushed DNS cache locally

---

## 💡 Lesson

DNS changes can take:
- 5 minutes to 48 hours globally

Always verify with DNS checker tools.


- *By [Mirza Hadi](https://hadi-mirza.com) —
Full-Stack Developer & Technical Problem Solver*  
*📰 [DCXherald Newsletter](https://linkedin.com/in/hadibaig)*
