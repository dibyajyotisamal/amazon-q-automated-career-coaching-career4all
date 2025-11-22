# Security and Access Control (ACL) Configuration

This document explains how course catalog access restrictions were implemented using IAM Identity Center and an S3 ACL configuration.

---

## 1. Identity Model

The project uses the provided IAM Identity Center setup:

**Group:**  
- `CareerCoaches`

**Users:**  
- `career.coach.one`  
- `career.coach.two`

These identities are used to test access permissions.

---

## 2. ACL Enforcement

The ACL file:
- Located at `access-control-list/course_access_acl.json`
- Attached to the S3 data source in Amazon Q Business

The ACL applies allow/deny rules to specific S3 prefixes.

Example behavior:
- `Security/` catalog -> **Allowed**
- `Medicine/` catalog -> **Denied**

---

## 3. Verification

### Testing Procedure:
1. Log in as each coach user.
2. Query courses expected to be allowed.
3. Query courses expected to be restricted.

### Expected Results:
  Allowed user: `career.coach.two`  
  Restricted user: `career.coach.one`

- Allowed courses appear normally.
- Restricted courses are completely invisible or omitted.
  

Screenshots:
- `acl_access_allowed.png`
- `acl_access_denied.png`

---

## 4. Common Issues and Solutions

| Issue | Cause | Fix |
|-------|-------|------|
| ACL not applied | Data source not synced | Re-sync S3 data source |
| User still sees restricted files | Incorrect group name | Ensure exact match to IAM Identity Center |
| Prefix not respected | Missing trailing slash | Example: `Security/` not `Security` |

---

## 5. Security Notes

- Use dedicated S3 prefixes for restricted catalogs.

