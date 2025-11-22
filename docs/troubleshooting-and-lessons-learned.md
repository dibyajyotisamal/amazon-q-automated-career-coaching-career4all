# Troubleshooting and Lessons Learned

This document summarizes issues encountered during the project and what was learned from resolving them.

---

## 1. Data Source Sync Issues

**Problem:**  
ACL changes and new S3 files were not appearing in the application.

**Root Cause:**  
Amazon Q Business requires a **manual sync** after changes.

**Lesson:**  
Always re-sync the S3 data source after:
- Updating ACLs
- Uploading new catalogs
- Modifying bucket structure

---

## 2. Guardrail Configuration Errors

**Problem:**  
"ValidationException: systemMessageOverride failed regex \P{C}\*"  

**Cause:**  
Non-ASCII characters or newlines in the blocked-message text.

**Fix:**  
Use plain ASCII text, no emojis, no curly quotes.

---

## 3. ACL Not Applied Correctly

**Common Causes:**
- Wrong group name
- Missing trailing slash in prefix
- Using IAM users instead of IAM Identity Center users

**Lesson:**  
Always test using `career.coach.one` or `career.coach.two`.

---

## 6. General Lessons

- Maintain a clean folder structure in S3 for predictable ACL rules  
- Document your prefix rules to avoid future confusion  
- Keep prompts clear and structured for consistent LLM behavior   

---

## 7. Recommendation for Future Teams

Provide:
- A validation script to test ACL rules  
- A coach-facing dashboard for catalog updates  
- Automation for daily, hourly, or event-based S3 -> Q syncing
